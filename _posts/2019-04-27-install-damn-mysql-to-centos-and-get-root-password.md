---
layout: post
title: "Install Damn Mysql To Centos And Get Root Password"
date: 2019-04-27
tags: [linux, mysql, centos, reset mysql root password,recover mysql root password]
categories: linux, mysql
---

Sometimes it can be pain on the keyboard to handle mysql on Centos if you don't follow instructions. 
So we need to focus on tutorials line by line. So Let's start with Mysql On Centos,

First thing first, Which Mysql Version you need ? I prefer 5.7 but let's continue for MySql 8.0 then we can move on for MySql 5.7

#Enable MySQL 8.0 Repository and install
<pre>
<code>
sudo yum localinstall https://dev.mysql.com/get/mysql80-community-release-el7-1.noarch.rpm
sudo yum install mysql-community-server
</code>
</pre>

#Enable for Mysql 5.7 and install
<pre>
<code>
sudo yum localinstall https://dev.mysql.com/get/mysql57-community-release-el7-11.noarch.rpm
sudo yum install mysql-community-server
</code>
</pre>

Now you can get your automatically generated Mysql root password by

<pre>
<code>
sudo grep 'temporary password' /var/log/mysqld.log
</code>
</pre>

And the output should looks like this (or uglier)
<pre>
<code>[Server] A temporary password is generated for root@localhost: %sasdS)(=)
</code></pre>

Now we should do mysql_secure_installation to set new rules and password for root,

<pre><code>
sudo mysql_secure_installation
</code></pre>

Now can access mysqll by typing 

<pre><code>mysql -u root -p </code></pre>

#Recover Mysql Root Password

Sometimes when you do not log any information for you systems, you forget your root password, 

First stop your mysql service,
<pre><code>
sudo systemctl stop mysql
</code></pre>

Start the mysql without loading grant tables,
<pre><code>sudo mysqld_safe --skip-grant-tables --skip-networking &</code></pre>

Now you should able to login mysql without root password and set new mysql root password
<pre><code>
sudo mysql -u root
ALTER USER 'root'@'localhost' IDENTIFIED BY 'new_password';
FLUSH PRIVILEGES;
</code></pre>

Now if everything should work fine you can restart mysql service,
<pre><code>sudo systemctl stop mysql
sudo systemctl start mysql</code></pre>

If you have any problem with mysql installation, setting new root password or recovering mysql root password. Just get in touch. 