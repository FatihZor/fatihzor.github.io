---
layout: post
title:  "how to handle preflight request in asp.net web api"
date:   2015-07-28 15:22:15
categories:  [Asp.NET]
tags:  [Restful]
---

# What is preflight request? #

I would like to hightlight the points that from the [mozillar.org dev site](https://developer.mozilla.org/en-US/docs/Web/HTTP/Access_control_CORS?redirectlocale=en-US&redirectslug=HTTP_access_control "mozillar.org dev site").


## Preflighted requests ##

Unlike simple requests (discussed above), "preflighted" requests first send an HTTP request by the OPTIONS method to the resource on the other domain, in order to determine whether the actual request is safe to send.  Cross-site requests are preflighted like this since they may have implications to user data.  In particular, a request is preflighted if:



- It uses methods other than GET, HEAD or POST.  Also, if POST is used to send request data with a Content-Type other than application/x-www-form-urlencoded, multipart/form-data, or text/plain, e.g. if the POST request sends an XML payload to the server using application/xml or text/xml, then the request is preflighted.


- It sets custom headers in the request (e.g. the request uses a header such as X-PINGOTHER)
Note: Starting in Gecko 2.0, the text/plain, application/x-www-form-urlencoded, and multipart/form-data data encodings can all be sent cross-site without preflighting. Previously, only text/plain could be sent without preflighting.

An example of this kind of invocation might be:

var invocation = new XMLHttpRequest();
var url = 'http://bar.other/resources/post-here/';
var body = '<?xml version="1.0"?><person><name>Arun</name></person>';
    
    function callOtherDomain(){
	  if(invocation)
	  {
	    invocation.open('POST', url, true);
	    invocation.setRequestHeader('X-PINGOTHER', 'pingpong');
	    invocation.setRequestHeader('Content-Type', 'application/xml');
	    invocation.onreadystatechange = handler;
	    invocation.send(body); 
	  }
    }

In the example above, line 3 creates an XML body to send with the POST request in line 8.  Also, on line 9, a "customized" (non-standard) HTTP request header is set (X-PINGOTHER: pingpong).  Such headers are not part of the HTTP/1.1 protocol, but are generally useful to web applications.  Since the request (POST) uses a Content-Type of application/xml, and since a custom header is set, this request is preflighted.

Let's take a look at the full exchange between client and server:

	OPTIONS /resources/post-here/ HTTP/1.1
	Host: bar.other
	User-Agent: Mozilla/5.0 (Macintosh; U; Intel Mac OS X 10.5; en-US; rv:1.9.1b3pre) Gecko/20081130 Minefield/3.1b3pre
	Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
	Accept-Language: en-us,en;q=0.5
	Accept-Encoding: gzip,deflate
	Accept-Charset: ISO-8859-1,utf-8;q=0.7,*;q=0.7
	Connection: keep-alive
	Origin: http://foo.example
	Access-Control-Request-Method: POST
	Access-Control-Request-Headers: X-PINGOTHER
	
	
	HTTP/1.1 200 OK
	Date: Mon, 01 Dec 2008 01:15:39 GMT
	Server: Apache/2.0.61 (Unix)
	Access-Control-Allow-Origin: http://foo.example
	Access-Control-Allow-Methods: POST, GET, OPTIONS
	Access-Control-Allow-Headers: X-PINGOTHER
	Access-Control-Max-Age: 1728000
	Vary: Accept-Encoding, Origin
	Content-Encoding: gzip
	Content-Length: 0
	Keep-Alive: timeout=2, max=100
	Connection: Keep-Alive
	Content-Type: text/plain
	
	POST /resources/post-here/ HTTP/1.1
	Host: bar.other
	User-Agent: Mozilla/5.0 (Macintosh; U; Intel Mac OS X 10.5; en-US; rv:1.9.1b3pre) Gecko/20081130 Minefield/3.1b3pre
	Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
	Accept-Language: en-us,en;q=0.5
	Accept-Encoding: gzip,deflate
	Accept-Charset: ISO-8859-1,utf-8;q=0.7,*;q=0.7
	Connection: keep-alive
	X-PINGOTHER: pingpong
	Content-Type: text/xml; charset=UTF-8
	Referer: http://foo.example/examples/preflightInvocation.html
	Content-Length: 55
	Origin: http://foo.example
	Pragma: no-cache
	Cache-Control: no-cache
	
	<?xml version="1.0"?><person><name>Arun</name></person>
	
	
	HTTP/1.1 200 OK
	Date: Mon, 01 Dec 2008 01:15:40 GMT
	Server: Apache/2.0.61 (Unix)
	Access-Control-Allow-Origin: http://foo.example
	Vary: Accept-Encoding, Origin
	Content-Encoding: gzip
	Content-Length: 235
	Keep-Alive: timeout=2, max=99
	Connection: Keep-Alive
	Content-Type: text/plain
	
	[Some GZIP'd payload]

Lines 1 - 12 above represent the preflight request with the OPTIONS method.  Firefox 3.1 determines that it needs to send this based on the request parameters that the JavaScript code snippet above was using, so that the server can respond whether it is acceptable to send the request with the actual request parameters.  OPTIONS is an HTTP/1.1 method that is used to determine further information from servers, and is an idempotent method, meaning that it can't be used to change the resource.  Note that along with the OPTIONS request, two other request headers are sent (lines 11 and 12 respectively):

	Access-Control-Request-Method: POST
	Access-Control-Request-Headers: X-PINGOTHER

The Access-Control-Request-Method header notifies the server as part of a preflight request that when the actual request is sent, it will be sent with a POST request method. The Access-Control-Request-Headers header notifies the server that when the actual request is sent, it will be sent with an X-PINGOTHER custom header.  The server now has an opportunity to determine whether it wishes to accept a request under these circumstances.

Lines 15 - 27 above are the response that the server sends back indicating that the request method (POST) and request headers (X-PINGOTHER) are acceptable.  In particular, let's look at lines 18-21:

	Access-Control-Allow-Origin: http://foo.example
	Access-Control-Allow-Methods: POST, GET, OPTIONS
	Access-Control-Allow-Headers: X-PINGOTHER
	Access-Control-Max-Age: 1728000

The server responds with Access-Control-Allow-Methods and says that POST, GET, and OPTIONS are viable methods to query the resource in question.  Note that this header is similar to the HTTP/1.1 Allow: response header, but used strictly within the context of access control.  The server also sends Access-Control-Allow-Headers with X-PINGOTHER as its value, confirming that this is a permitted header to be used with the actual request.  Like Access-Control-Allow-Methods, Access-Control-Allow-Headers is a comma separated list of acceptable headers.  Finally, Access-Control-Max-Age gives the value in seconds for how long the response to the preflight request can be cached for without sending another preflight request.  In this case, 1728000 seconds is 20 days.

# A Demo in Asp.net web API #

Now, I have a requirement that I need upload a image file to the server with the Asp.net web api. in this case, it should be a post method and the content type should image/*,so refer to the preflight request's definition, if POST is used to send request data with a Content-Type other than application/x-www-form-urlencoded, multipart/form-data, or text/plain, it would be a preflight request.

1. Add a route action with post method.

	     [HttpPost]
	      public IHttpActionResult Upload()
	      {
		     bool isSavedSuccessfully = true;
		     string fName = "";
		     try
		     {
				    foreach (string fileName in HttpContext.Current.Request.Files)
				    {
				       var file = HttpContext.Current.Request.Files[fileName];
				       //Save file content goes here
				       var extension = System.IO.Path.GetExtension(file.FileName);
				       var newName = Guid.NewGuid().ToString();
				       fName = string.Format("{0}{1}", newName, extension);
				    
				       if (file != null && file.ContentLength > 0)
				       {
					      var originalDirectory = new DirectoryInfo(string.Format("{0}uploadedFiles", HttpContext.Current.Server.MapPath(@"\")));
					      string pathString = System.IO.Path.Combine(originalDirectory.ToString(), "tempFiles");
					      var fileName1 = Path.GetFileName(file.FileName);
					      bool isExists = System.IO.Directory.Exists(pathString);
					      if (!isExists)
						      System.IO.Directory.CreateDirectory(pathString);
						      var path = string.Format("{0}\\{1}", pathString, fName);
						      file.SaveAs(path);
					       }
				    }
			    }
			    catch (Exception)
			    {
			   		 isSavedSuccessfully = false;
			    }
			     if (isSavedSuccessfully)
			     {
			  		 return Json(new { Message = fName });
			     }
			     else
			     {
			   		 return Json(new { Message = "Error01" });//Error in saving file
			     }
	      }
	  


1.   Add logic in Application_BeginRequest in Global.asax.cs

 	    
			protected void Application_BeginRequest()
		    {
			    if (Request.Headers.AllKeys.Contains("Origin") && Request.HttpMethod == "OPTIONS")
			    {
			   		 Response.Flush();
			    }
		    }



1. BWT, the CROS related config in the web.config is like this.

    	
		</system.web>
    	  <system.webServer>
	    	<httpProtocol>
	    	  <customHeaders>
		    	<add name="Access-Control-Allow-Origin" value="*" />
		    	<add name="Access-Control-Allow-Headers" value="accept, cache-control, content-type, x-requested-with" />
		    	<add name="Access-Control-Allow-Methods" value="GET, POST, PUT, DELETE, OPTIONS" />
	    	  </customHeaders>
	    	</httpProtocol>
