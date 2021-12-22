---
title: "SOLVED: Sonos Orbi WiFi Issues"
date: 2021-12-21T21:05:30-08:00
tags:
  - sonos
  - orbi
---

When I tried to add a Sonos Beam Gen 2 to my home network, which consists of a Orbi mesh with one receiver and multiple satellites, I ran into few issues. There are others who have run into [similar issues](https://community.netgear.com/t5/Orbi/Sonos-can-t-connect-to-Orbi/td-p/1695787) trying to battle 2.4 Ghz and passwords.

1. Sonos would not connect to my default network (5.0 Ghz) and it could only connect to a 2.4 Ghz network. So I enabled a guest network with 2.4 Ghz and the Beam connected. Once the connection was done, the app mentioned that the Beam was not configured properly. It would show the Beam in the app, but you cannot do much with it. The main problem was that my phone was on the default home network (5.0 Ghz) while the Beam was on 2.4 Ghz.

2. While going through the *Wireless* screen in Orbi, I realized that the default home network supports both 2.4 Ghz and 5.0 Ghz channels. You don't need to enable Guest Wifi.

3. After disabling the guest network, it was back to sqaure one. The Beam would not connect to the network. Finally the way to solve it was to set an explicit channel for the 2.4 Ghz from the Orbi admin page. In my case it was set to "Auto". Just changing it to an explicit channel (11 in my case), solved the issue. This is how the page looks like on the Orbi admin page ![Sonos-Orbi](https://d2sa5t9ngheghz.cloudfront.net/orbi-sonos.png)

