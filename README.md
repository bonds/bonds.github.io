This is the source for the blog hosted at https://ggr.com/.

A Github action runs Hugo to generate the site whenever the source is deployed to Github
via git push. The generated code is checked into the ```gh-pages``` branch and then picked
up by Github Pages.

The (custom) theme may be found in the ```themes/lowtech``` folder.
