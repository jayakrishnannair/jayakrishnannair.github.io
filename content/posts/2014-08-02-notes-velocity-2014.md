---
title: Notes from Velocity 2014
author: jayakrishnan
type: post
date: 2014-08-02T05:59:52+00:00
url: /2014/08/02/notes-velocity-2014/
categories:
  - Conferences
tags:
  - APM
  - CDN
  - New Relic
  - Velocity

---
I attended the [Velocity Conference][1] in Santa Clara this year and these are few of the takeaways. If an image could summarize the conference, it would be this image from [Scott Hanselman][2]’s Keynote address, [_Virtual Machines, JavaScript and Assembler_][3] which was the most entertaining keynote I have ever heard.<figure id="attachment_4" aria-describedby="caption-attachment-4" style="width: 500px" class="wp-caption aligncenter">



There were three main takeaways for me: APM is huge; everyone is into optimizing images and the CDNs are getting smarter.

APM is not American Public Media or Advanced Power Management or Actions Per Minute, but Application Performance Management. There was [New Relic][5], [App Dynamics][6], [SpeedCurve][7] and [Fog Light][8] showcasing their new features. Among these I have used New Relic extensively and found that extremely useful in improving MTTD and MTTR which are two new buzzwords learned at the conference. These APM tools monitor the error rate, thread counts, JVM data, response times and lets the Dev Ops configure various alerts which helps improve the Mean Time To Detect and Mean Time to Resolve.

The second important point is regarding optimizing image delivery. Most sites have a high res image as an asset and the same is delivered if you are on a high res desktop or viewing it on the small cell phone screen. This takes up bandwidth and ruins the experience for the user and the goal for all the players was to reduce bandwidth and latency on the mobile while delivering high-resolution images to tablets, desktops and laptops. Pamela Fox at Khan Academy had a very interesting talk in which she explained how they got around the problem by eliminating most of the images. (Watch [_Look, Ma, No Image Requests!_][9]). One interesting observation from her was that not many users scroll below the fold.

[Limelight Networks][10] had a smart CDN concept where they would resize the image based on the user agent without having the developer to modify the code. Handling images was a huge problem for the BBC whose stories are image heavy. Their developers talked about having to provide a useful experience for the end user who could be on any of the hundreds of possible screen resolutions using browsers of varying capacity. They solved it by going mobile first and making progressive enhancements to the site. They split the browsers into good and bad; the good ones had querySelector for the documents, localstorage in window and eventListener in the window. They also had a useful tool, [wraith][11], a screenshot comparison tool. Everyone seems to be waiting for the [new srcset attribute for the image tag][12]. Once this is available on all the browsers, the content provider will be able to specify different images for different pixel densities which might make obsolete much of the current javascript and css tricks.

Among the tools that were presented [Docker][13] and  [Gauntlt][14] looked interesting. If you want to setup your own monitoring system without relying on any of the Saas providers, then [Ganglia][15] would be a good candidate.

The slides for the conference are [now available online][16] and some of the presentations I liked were [_Achieving Rapid Response Times in Large Online Services_][17]_,  _[_Delivering Optimal Images for Phones and Tablets on the Modern Web_][18]_,_ [_Lower the barrier to programming_][19]_,_ [_Mobile Web is Not (Just) a Technical Challenge_][20]_,_ and [_Scale and Adapt &#8211; How We Built Responsive BBC News_][21]_._

 [1]: http://velocityconf.com/velocity2014
 [2]: http://www.hanselman.com/
 [3]: https://www.youtube.com/watch?v=FZYrlKbkLe8
 [4]: https://i2.wp.com/www.shooonya.org/wp-content/uploads/2014/08/hanselman.png
 [5]: http://newrelic.com/
 [6]: http://www.appdynamics.com/
 [7]: http://speedcurve.com/
 [8]: http://www.quest.com/foglight/
 [9]: https://speakerdeck.com/pamelafox/look-ma-no-image-requests
 [10]: http://www.limelight.com/
 [11]: https://github.com/BBC-News/wraith
 [12]: http://www.smashingmagazine.com/2013/08/21/webkit-implements-srcset-and-why-its-a-good-thing/
 [13]: https://www.docker.com/
 [14]: http://gauntlt.org/
 [15]: http://ganglia.sourceforge.net/
 [16]: http://velocityconf.com/velocity2014/public/schedule/proceedings
 [17]: http://velocityconf.com/velocity2014/public/schedule/detail/34266
 [18]: http://velocityconf.com/velocity2014/public/schedule/detail/35192
 [19]: http://velocityconf.com/velocity2014/public/schedule/detail/34537
 [20]: http://velocityconf.com/velocity2014/public/schedule/detail/33957
 [21]: http://velocityconf.com/velocity2014/public/schedule/detail/35177