---
layout: post
title: "Example syntax for scp"
modified:
categories: Linux
excerpt:
share: true
tags: [linux, scp, ssh]
image:
  feature:
---

The following examples were taken from [this article](http://www.hypexr.org/linux_scp_help.php), just for my future reference.

##Examples:

* Copy remote file to local folder:

  ```shell
  $ scp USERNAME@remotehost.edu:/file/path /local/directory
  ```

* Copy remote directory to local directory:

  ```shell
  $ scp -r USERNAME@remotehost.edu:/directory/path /local/directory
  ```

* Copy local file to remote host

  ```shell
  $ scp foo.txt USERNAME@remotehost.edu:/file/path
  ```
  
* Copy local file to remote host using port 2046

  ```shell
  $ scp -p 2046 foo.txt USERNAME@remotehost.edu:/file/path
  ```

* Copy local directory to remote host

  ```shell
  $ scp -r /local/directory USERNAME@remotehost.edu:/directory/path
  ```
  
* Copy mutiple files to remote host

  ```shell
  $ scp foo.txt bar.txt USERNAME@remotehost.edu:/directory/path
  ```
  
* Copy  multiple files from the remote host to local

  ```shell
  $ scp USERNAME@remotehost.edu:~/\{foo.txt,bar.txt\} .
  ```
  
##Preformance Boost
Using the Blowfish cipher may increase the speed of transsion.

  ```Shell
  $ scp -c blowfish foo.txt USERNAME@remotehost.edu:/directory/path
  ```
  
Sometimes, if the connect is extremely low, we may try the -C option for file compression to boost speed. 

  ```shell
  $ scp -c blowfish -C foo.txt USERNAME@remotehost.edu:/directory/path
  ``` 

  

