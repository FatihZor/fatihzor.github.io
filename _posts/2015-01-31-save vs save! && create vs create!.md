---
layout: post
title:  "save, save!, create, and create!"
date:   2015-01-31 23:22:15
categories:  [Rails]
tags:  [Rails]
---

It turns out that there are two versions of the save and create methods. The variants differ in the way they report errors.-  save returns true if the record was saved; it returns nil otherwise.- save! returns true if the save succeeded; it raises an exception otherwise.- create returns the Active Record object regardless of whether it was suc- cessfully saved. You’ll need to check the object for validation errors if you want to determine whether the data was written.- create! returns the Active Record object on success; it raises an exception otherwise.Let’s look at this in a bit more detail.
Plain old save() returns true if the model object is valid and can be saved.	
	if order.save 
		# all OK	else  		# validation failed	endIt’s up to us to check on each call to save() to see that it did what we expected. The reason Active Record is so lenient is that it assumes save() is called in the context of a controller’s action method and that the view code will be present- ing any errors back to the end user. And for many applications, that’s the case.
However, if we need to save a model object in a context where we want to make sure to handle all errors programmatically, we should use save!(). This method raises a RecordInvalid exception if the object could not be saved.
	begin
      order.save!
    rescue RecordInvalid => error
      #validation failed
    end