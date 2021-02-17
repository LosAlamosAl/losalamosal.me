# losalamosal.me
Static blog and JAMstack site

To clone and build this site:

```sh
# clone as follows with SSH for multiple GitHub accounts
> git clone --recursive git@losalamosal.github.com/losalamosal/losalamosal.me.git
> cd losalamosal.me
> git config user.email ...
> git config user.name ...
> git submodule update --remote
# commit this update to repo
# add a post--contraty to Hugo docs, must be post directory for this theme
> hugo new post/starting-to-blog.md
# Check the site at localhost:1313
> hugo server -D
> ^C
# push it up to GitHub
```
