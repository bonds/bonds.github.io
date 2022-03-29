This is the source for the blog hosted at https://ggr.com/.

A Github action runs Hugo to generate the site whenever the source is deployed to Github
via git push. The generated code is checked into the ```gh-pages``` branch and then picked
up by Github Pages.

The (custom) theme may be found in the ```themes/lowtech``` folder. I was going for
something easy to use, quick to download and render, and free of unnecessary complexity
(e.g. JavaScript, trackers)...I mean I'm just throwing some words around here, no need
to get your computer's fan running, I figure.
