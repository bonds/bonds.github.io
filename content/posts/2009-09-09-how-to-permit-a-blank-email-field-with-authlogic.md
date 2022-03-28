---
title: How To Permit A Blank Email Field With AuthLogic
date: 2009-09-09 12:32
tags: code
---
<img alt="image" height="133" src="/images/errors-from-blank-email-with-AuthLogic.jpg" width="512" />
<br/>

I too [ran into some trouble][1] before discovering that my beloved AuthLogic is validating my email field. The validation is a good thing overall, but I want to support blank email addresses as well as properly formatted ones.

It's all in the AuthLogic docs of course, but if I can save you a few minutes of hunting around, that's all good:

<pre>acts_as_authentic do |c|
  c.merge_validates_length_of_email_field_options({:allow_nil =&gt; true})
  c.merge_validates_format_of_email_field_options({:allow_nil =&gt; true})
end
</pre>

 [1]: http://ficial.wordpress.com/2009/03/15/ruby-on-rails-getting-error-messages-authlogic-email-validation/