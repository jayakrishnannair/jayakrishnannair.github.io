---
title: Handling Docker Login Errors
author: jayakrishnan
type: post
date: 2018-12-23T05:20:57+00:00
url: /2018/12/23/fix-for-docker-unauthorized-incorrect-username-or-password/
categories:
  - Notes to Self
  - Technology

---
If you have installed Docker for the first time, it is better to verify the install with the command

<pre class="wp-block-code"><code>docker run hello-world</code></pre><figure class="wp-block-image">

<img src="https://i1.wp.com/d2sa5t9ngheghz.cloudfront.net/docker-1.png" alt="" data-recalc-dims="1" /> </figure> 

When you ran that command and got the error &#8220;unauthorized: incorrect username or password&#8221;, read on. **Most likely you would have entered your Docker hub e-mail and password.** Big mistake. 

The instruction says that you should <g class="gr_ gr\_7 gr-alert gr\_spell gr\_inline\_cards gr\_run\_anim ContextualSpelling multiReplace" id="7" data-gr-id="7">login</g> with your Docker ID. **This Docker ID is not your e-mail**. For <g class="gr_ gr\_6 gr-alert gr\_gramm gr\_inline\_cards gr\_run\_anim Punctuation only-ins replaceWithoutSep" id="6" data-gr-id="6">that</g> you need to login to Docker Hub with your e-mail and go to the Profile page. There you can find your Docker ID. 

Go back to your shell prompt and type

<pre class="wp-block-code"><code>docker login</code></pre>

Enter the Docker ID and password and you should get a message that the login succeeded. Now type the first command and it will work

<pre class="wp-block-code"><code>docker run hello-world</code></pre><figure class="wp-block-image">

<img src="https://i1.wp.com/d2sa5t9ngheghz.cloudfront.net/docker-2.png" alt="" data-recalc-dims="1" /> </figure>