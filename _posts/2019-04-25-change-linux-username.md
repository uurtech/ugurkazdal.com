---
layout: post
title: Change Linux username
tags: linux,change,username
---


Sometimes you could want to change your username in Linux like i did about 5 minutes ago. 
So let's see how to change username and directory with linux/cli.
* Logout off your current user,
* ctrl+alt+f2
* login with your current username
then
<pre>
<code>
sudo passwd root
</code>
</pre>

* logout
* now login with root
<pre>
<code>
usermod -l {newUserName} -d /home/{newUserName} -m {exUserName}
groupmod -n {newGroup} {exGroup}
</code></pre>


So thats it, now you can login with your new linux user and then run *startx* to run desktop environment.
