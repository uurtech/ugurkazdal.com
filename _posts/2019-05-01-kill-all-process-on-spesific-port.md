---
layout: post
title: "Kill all processes on spesific port"
date: 2019-05-01
tags: [linux,cli,lsof,port,process]
categories: linux
---

Sometimes you have multiple apps works on same port time to time. For example I use Docker for most of my app developments but sometimes when building laravel app I use *php artisan serve --port 80* and all of sudden it runs on next available port which is mostly 81. So I kill all the process on port 80 !

Let's look at how, first, we need to list all process on a spesific port in this case 80.

<pre><code>lsof -t -i :80</code></pre>

You can kill process one by one. But hey, we are on Linux so we need to have some tricks to automatize anything.

<pre><code>kill $(lsof -t -i :80)</code></pre>

OMG. All of sudden. Port 80 is all free !