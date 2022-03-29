---
title: How To Use Facebook Open Streams With Facebooker
date: 2009-09-15T15:02:00Z
tags: code
---
![1]

I would like my Facebook Connect app to publish stories to my users' Facebook news stream. I went looking for how do this with Facebooker and figured out an answer.

The old way of doing this, and the one built into Facebooker, is to [publish a user action][2]. There are two limitations of the old way: 1: you need a valid session_key (so, the user must be logged in); 2: you may only send up to 10 messages per day (without special permissions from the user). Fortunately Facebook released their Open Stream API in April 2009 and it suffers from neither restriction: you can post without a session_key and there are no explicit limits on how many posts you can make in a day. Unfortunately Facebooker does not yet offer native support for publishing to Facebook streams, at least that I could find, but it DOES support rolling your own API calls, and in this case its not that hard to do. To post to a users' Facebook stream from your Rails app's script/console, do the following:

1.  Integrate Facebooker into your Rails app.  Verify that it works.  There are a number of ways to integrate Facebooker depending on what kind of app you are making.  e.g. I'm making a Facebook Connect app, so I used [AuthLogic][4] and the [AuthLogic Facebook Connect plugin][5] so users can login to my app using their Facebook credentials.
2.  Get a user's  permission to publish to their stream.  Make a note of their Facebook UID.  e.g. in my app, the AuthLogic Facebook Connect plugin stores the UID in my user table each time a new Facebook user logs into my site.
3.  Run script/console and execute the following commands:

> <div>
>   <p>
>     f = Facebooker::Session.create f.post 'facebook.stream.publish', :uid => '<insert_facebook_uid_here>', :message => 'test'
>   </p>
> </div>

Not so bad, huh?

*Updated on September 26th, 2013*

The links to Facebook's documentation of their old API no longer work. They have been removed.

[1]: https://ggr_com.s3.amazonaws.com/images/facebook_extended_permissions.jpg
[2]: http://facebooker.rubyforge.org/classes/Facebooker/Rails/Publisher.html
[4]: http://github.com/binarylogic/authlogic
[5]: http://github.com/kalasjocke/authlogic_facebook_connect
 
