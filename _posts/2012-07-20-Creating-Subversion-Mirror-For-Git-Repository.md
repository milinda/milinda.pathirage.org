---
layout: post
title: Creating SVN Mirror For Git Repository
author: Milinda Pathirage
time: 20th July 2012
---

Today I needed to mirror one of my Github repositories into a internal SVN
repository. I googled and found [several](http://stackoverflow.com/questions/661018/pushing-an-existing-git-repository-to-svn) [Stackoverflow](http://stackoverflow.com/questions/1269566/unable-to-determine-upstream-svn-information-from-head-history) threads and
[articles](http://code.google.com/p/support/wiki/ImportingFromGit) which explain different ways of doing this. But none of the
approaches in those worked for me. Finally I found [this post](http://www.codeography.com/2010/03/17/howto-mirror-git-to-subversion.html) from
Codeography which worked like a charm and which was really simple.
Following is the methodology described in that post. I am sure that this
will work for most of us when compared with the complex methods
discussed in the different places of internet.

I mirrored [CloudPipe](https://github.com/milinda/CloudPipe) repository in Github
to our internal SVN [repo](svn+ssh://bitternut.cs.indiana.edu/home/dquob/svn-repo/slosh/cloudpipe/trunk).

First step is to edit the **.git/config** file in your local Git
repository. You need to add following to *config* file.

{% highlight yaml %}
[svn-remote "svn"]                                                              
    url = svn+ssh://mpathira@bitternut.cs.indiana.edu/home/dquob/svn-repo/slosh/cloudpipe/trunk
    fetch = :refs/remotes/git-svn
{% endhighlight %}

In above **url** should point to your SVN repository. Then you need to
merge the **master** in to new branch using following commands.

{% highlight bash %}
git svn fetch svn
git checkout -b svn git-svn
git merge master
git svn dcommit
{% endhighlight %}

Then rebase the branch to the **master**, and you can **dcommit** from the
**master** to **svn**.

{% highlight bash %}
git checkout master
git rebase svn
git branch -d svn
git svn dcommit
{% endhighlight %}

After this you can commit changes to **svn**, every time you do a commit to git.
The [post](http://www.codeography.com/2010/03/17/howto-mirror-git-to-subversion.html) I mentioned above contains extra information on how to use cron
job to sync the repositories periodically. But I didn't try those, so
you may need to try and see whether they work for you.




