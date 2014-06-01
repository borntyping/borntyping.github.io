---
title: ZSH startup time
---

I've had issues with `zsh` starting up and running very slowly for a while. I'd assumed the problem simply lay with the number of plugins and other scripts run by `oh-my-zsh`, but a bit of research has found two solutions that have worked very well for me (your mileage may vary):

- Removing the `github` plugin. I don't think I was using it much, if at all, and removing it stoped the noticable delay each time the prompt was shown ([Source](http://superuser.com/a/269617))
- Adding `skip_global_compinit=1` to `.zshenv`. This dropped the startup time of zsh from ~0.85 seconds to ~0.15 seconds. This was benchmarked using `/usr/bin/time zsh -i -c exit` ([Source](http://blog.patshead.com/2011/04/improve-your-oh-my-zsh-startup-time-maybe.html))

