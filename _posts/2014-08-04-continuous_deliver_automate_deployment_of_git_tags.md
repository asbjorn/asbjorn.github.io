---
title: Continuous Delivery: Automate deployment of "git tags"
layout: post
---

{{ page.title }}
================

## Goal?

We want to be able to create a tag in our git repository signalling a point where 
we're confident that the code is stable and reached the point of the intended 
feature set. So. our steps would ideally be as follows:

1. Create new git tag
{% highlight bash %}
$> git tag -a v1.0 -m 'New release'
{% endhighlight %}

2. Push the tag to the remote Git repository (Gitlab)
{% highlight bash %}
$> git push --tags
{% endhighlight %}

3. Our git server (Gitlab) will then fire off a previously setup "Webhook" for any 
*git tag* push events, and trigger our build server. 

4. Then our build server (Jenkins) will recognize the new tag, and start crunching. 
More precisly checkout the tag, compile the code, cleanup development specific stuff
then create a nice smooth release.


## How did we do it?

Here is where the magic happens. It really isn't much magic though. So, we have all 
code in a Git repository on our [Gitlab](https://about.gitlab.com/) server. We also 
have a [Jenkins](http://jenkins-ci.org/) build server that deals with the compile 
checks, testing, etc.

Now we want our *Gitlab* and *Jenkins* server to play together as a team. 
