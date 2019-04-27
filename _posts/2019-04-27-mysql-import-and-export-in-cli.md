---
layout: post
title: "Mysql Import And Export in CLI"
date: 2019-04-10 13:49 +0300
tags: [linux,mysql,mysqldump,mysql import, mysql export]
categories: linux
---


Many times I don't want to use Workbench or any other GUI supported DB Product, I mostly live in CLI, so I need to do my stuff in cli. Also Mysql Import and Export is easy on CLI, so let's give it a shot.

This is how we export current mysql database,
<pre>
<code>
mysqldump -u {USERNAME} -p {PASSWORD} database > db_backup.sql
</code>
</pre>

If you don't type password in this line you could just skip typing then cli asks you to put your password in secret mode. :) 

Let's say you want to dump all the databases you have in mysql so you can run this;
<pre>
<code>
mysqldump -u {USERNAME} -p {PASSWORD}  --all-databases > db_backup.sql
</code>
</pre>

Not enough ? You want to get geeky ? You need to export just tables ? Then we have;
<pre>
<code>
mysqldump -u {USERNAME} -p {PASSWORD}  database table1 table2 > tables.sql
</code>
</pre>


NOT ENOUGH ??? ARE YOU HANGRY !!!! you need to compress your mysql backup !!!
<pre>
<code>
mysqldump -u {USERNAME} -p {PASSWORD}  database | gzip > backups.sql.gz
</code>
</pre>

OMG. You do not want to ssh to your server and enabled remote access for mysql ? I see ... so you should run this;
<pre>
<code>
mysqldump -P 3306 -h {REMOTE_IP} -u {USERNAME} -p database > backup.sql</code>
</pre>


So all of those cli commands are for exporting mysql databases. What if you want to import a mysql database? Let's try this command,

<pre>
<code>
mysqldump -u {USERNAME} -p {PASSWORD} database < db_backup.sql
</code>
</pre>

You saw that ? we just mirrored ***>*** to ***<***.

One other tip to upload your sql to your server. 

Please use *scp* just as

*scp {WHAT} {WHERE}* 
let's give an example for *scp*

<pre>
<code>
scp my_mysql_dump_file mysshuser@REMOTE_IP:/var/www/backups
</code>
</pre>

Now you know how to upload via scp and import & export in mysql !