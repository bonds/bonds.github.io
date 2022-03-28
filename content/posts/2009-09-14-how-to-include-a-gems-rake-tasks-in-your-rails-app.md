---
title: How To Include a Gem's Rake Tasks in Your Rails App
date: 2009-09-14 12:21
tags: code
---
Rake tasks contained in a gem are not automatically available to a rails app that requires the gem. Whether that's the right way to do things is [under debate][1], but in the mean time there are a couple workarounds.

**Option #1**: Use the gem as a plugin instead. Files that match the following pattern are automatically pulled in, so you're good to go:

> <div>
>   <p>
>     #{RAILS_ROOT}/vendor/plugins/*/**/tasks/**/*.rake
>   </p>
> </div>

**Option #2**: Create a ruby file that loads the gem's tasks, then require the ruby file you made in your rail app's Rakefile. For example, if you've installed the Facebooker gem and you want to use its rake tasks, you might create a file called 'facebooker.rb' and save it to your *<railsapproot>/tasks* directory with these contents:

> <div>
>   <p>
>     $VERBOSE = nil<br />Dir["#{Gem.searcher.find('facebooker').full_gem_path}/lib/tasks/*.rake"].each { |ext| load ext }
>   </p>
> </div>

Then add this line to your Rakefile:

> <div>
>   <p>
>     require 'tasks/facebooker'
>   </p>
> </div>

But as it turns out, Facebooker's tasks uses relative paths to get at its config file in your rails app, which won't work if its installed in the gem path as a gem rather than in your rails app as a plugin! So be careful with using option #2, it may not be what the gem you're trying to use expects.

 [1]: https://rails.lighthouseapp.com/projects/8994/tickets/59