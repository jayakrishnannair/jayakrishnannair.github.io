---
title: Docker Windows 10 Port Mapping
author: jayakrishnan
type: post
date: 2018-12-31T02:55:03+00:00
url: /2018/12/31/docker-windows-10-port-mapping/
categories:
  - Notes to Self
  - Technology
tags:
  - Docker
  - Windows 10

---
<pre class="wp-block-code"><code>FROM node:alpine
COPY ./ ./
RUN npm install
CMD ["npm", "start"]</code></pre>

If this is your Dockerfile and your node app starts at port 8080, then logically you would think that typing

<pre class="wp-block-code"><code>http://localhost:8080</code></pre>

would give you access to the application. This works fine on OSX, but on a Windows 10 machine using Docker Toolkit, you will get an error message which says, that the browser can’t establish a connection to the server at localhost:8080.

The logical step would be to check the hosts file and uncomment the line for

<pre class="wp-block-preformatted"># localhost name resolution is handled within DNS itself.<br /> <code>127.0.0.1       localhost</code> </pre>

Still it will not connect. Few other suggestions are to try one of the following

<pre class="wp-block-code"><code>http://0.0.0.0:8080   
http://127.0.0.1:8080  .</code></pre>

If both of these don&#8217;t work, the sure shot way is the following. Type docker-machine ls and note the NAME of your instance

<pre class="wp-block-code"><code>$ docker-machine ls
NAME      ACTIVE   DRIVER       STATE     URL                         SWARM   DOCKER        ERRORS
default   *        virtualbox   Running   tcp://192.168.99.100:2376           v17.06.0-ce</code></pre>

Following this get the IP address of your instance with

<pre class="wp-block-code"><code>$ docker-machine ip default
192.168.99.100</code></pre>

Once you have the IP address of your instance, you can type http://192.168.99.100:8080 and access your instance.