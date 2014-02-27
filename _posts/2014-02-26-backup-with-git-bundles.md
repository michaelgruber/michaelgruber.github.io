---
layout: post
title: Backup with Git Bundles
subtitle: A quick way to make one more copy of your code.
---

Say Github gets DDoS'd out of existence and all my hard drives simultaneously ignite; I'll bet I'd wish I had that third copy of my code to carry with me into the apocalypse! You can use `git bundle --all` to package a full repo into one file.

I made a bash script and git aliased it, to take most of the hand-cramp out of the method.

### [git_bundled.sh](https://gist.github.com/michaelgruber/9232456)
{% highlight bash linenos %}
#!/bin/sh
DEST=~/Dropbox/Git\ Backups/
REPO=$(basename "`git rev-parse --show-toplevel`")

(git bundle create "${DEST}${REPO}.bundle" --all)
{% endhighlight %}

{% highlight bash %}
git config --global alias.bundled '!sh /where/script/is/git_bundled.sh'
{% endhighlight %}

This way, `git bundled` makes a new `repo_name.bundle` appear in my Dropbox folder where it's then spirited off to the cloud. I'll do this at the end of the day, with any work I've done, or even just after a push. You can compare refs for a bundle with `git bundle verify repo_name.bundle` to a regular repo's `git show-ref`.

Once a bundle's been synced to another computer, emailed, or pulled off a thumb drive, it can be cloned or pulled from as if it were a remote.
