---
layout: post
title: Mysql Docker Container
date: 2019-04-10 13:49 +0300
tags: devops,mysql,docker
category: devops
---

Sometimes I use Mysql Container for simple tasks or sample queries. Sometimes I need quick laravel application to handle some API request or to do a job for me. 

Anyway, let's look at the Mysql Container Docker Compose file below,

<pre><code class="yaml">
version: '3.1'

services:

  db:
    image: mysql
    command: --default-authentication-plugin=mysql_native_password
    restart: always
    ports:  
      - 3306:3306
    environment:
      MYSQL_ROOT_PASSWORD: kazdal
</code>
</pre>


*--default-authentication-plugin=mysql_native_password* this is the command for laravel application if you want to use Mysql 8.

So I hear that you do not want to use mysql shell to check databases, so you can use adminer, so updated docker compose file for mysql is this ;

<pre><code class="yaml">
version: '3.1'
services:

  db:
    image: mysql
    command: --default-authentication-plugin=mysql_native_password
    restart: always
    ports:  
      - 3306:3306
    environment:
      MYSQL_ROOT_PASSWORD: kazdal

   adminer:
     image: adminer
     restart: always
     ports:
       - 8080:8080
</code>
</pre>

Any Comments to this [gist](https://gist.github.com/uurtech/327edbfb29058035a1c7f0daa8b60a57) is more than welcome.