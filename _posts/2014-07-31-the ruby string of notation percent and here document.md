---
layout: post
title:  "The Ruby string of Notation % and Here Document"
date:   2014-07-31 23:22:15
categories:  [Ruby]
tags:  [Ruby]
---



# Notation % 


There is also a Perl-inspired way to quote strings: by using % (percent character) and specifying a delimiting character, for example:

	%{78% of statistics are "made up" on the spot}
	=> "78% of statistics are \"made up\" on the spot"
	
Any single non-alpha-numeric character can be used as the delimiter, %[including these], %?or these?, %~or even these things~. By using this notation, the usual string delimiters " and ' can appear in the string unescaped, but of course the new delimiter you've chosen does need to be escaped. However, if you use %(parentheses), %[square brackets], %{curly brackets} or %<pointy brackets> as delimiters then those same delimiters can appear unescaped in the string as long as they are in balanced pairs:

	%(string (syntax) is pretty flexible)
	=> "string (syntax) is pretty flexible"
	

A modifier character can appear after the %, as in %q[], %Q[], %x[] - these determine how the string is interpolated and what type of object is produced:

<table class="wikitable">
<tbody><tr>
<td><b>Modifier</b></td>
<td><b>Meaning</b></td>
</tr>
<tr>
<td>%q[ ]</td>
<td>Non-interpolated String (except for \\ \[ and \])</td>
</tr>
<tr>
<td>%Q[ ]</td>
<td>Interpolated String (default)</td>
</tr>
<tr>
<td>%r[ ]</td>
<td>Interpolated Regexp (flags can appear after the closing delimiter)</td>
</tr>
<tr>
<td>%i[ ]</td>
<td>Non-interpolated Array of symbols, separated by whitespace (after Ruby 2.0)</td>
</tr>
<tr>
<td>%I[ ]</td>
<td>Interpolated Array of symbols, separated by whitespace (after Ruby 2.0)</td>
</tr>
<tr>
<td>%w[ ]</td>
<td>Non-interpolated Array of words, separated by whitespace</td>
</tr>
<tr>
<td>%W[ ]</td>
<td>Interpolated Array of words, separated by whitespace</td>
</tr>
<tr>
<td>%x[ ]</td>
<td>Interpolated shell command</td>
</tr>
<tr>
<td>%s[ ]</td>
<td>Non-interpolated symbol</td>
</tr>
</tbody></table>

Here are some more examples:

	%Q{one\ntwo\n#{ 1 + 2 }}
	=> "one\ntwo\n3"

	%q{one\ntwo\n#{ 1 + 2 }}
	=> "one\\ntwo\\n#{ 1 + 2 }"

	%r/#{name}/i
	=> /nemo/i

	%w{one two three}
	=> ["one", "two", "three"]

	%i{one two three} # after Ruby 2.0
	=> [:one, :two, :three]

	%x{ruby --copyright}
	=> "ruby - Copyright (C) 1993-2009 Yukihiro Matsumoto\n"

# "Here document" notation

There is yet another way to make a string, known as a 'here document', where the delimiter itself can be any string:

	string = <<END
	on the one ton temple bell
	a moon-moth, folded into sleep,
	sits still.
	END
	
The syntax begins with << and is followed immediately by the delimiter. To end the string, the delimiter appears alone on a line.

There is a slightly nicer way to write a here document which allows the ending delimiter to be indented by whitespace:

	string = <<-FIN
           on the one-ton temple bell
           a moon-moth, folded into sleep
           sits still.

           --Taniguchi Buson, 18th century; translated by X. J. Kennedy
         FIN
         
To use non-alpha-numeric characters in the delimiter, it can be quoted:

	string = <<-"."
           Orchid - breathing
           incense into
           butterfly's wings.

           --Matsuo Basho; translated by Lucien Stryk
         .


Here documents are interpolated, unless you use single quotes around the delimiter.

The rest of the line after the opening delimiter is not interpreted as part of the string, which means you can do this:

	
	strings = [<<END, "short", "strings"]
		a long string
	END

	=> ["a long string\n", "short", "strings"]
	
You can even "stack" multiple here documents:

	string = [<<ONE, <<TWO, <<THREE]
	the first thing
	ONE
	the second thing
	TWO
	and the third thing
	THREE

	=> ["the first thing\n", "the second thing\n", "and the third thing\n"]
