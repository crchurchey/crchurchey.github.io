---
layout: post
title: Use Chromecast on hotel WiFi
---

Getting a Chromecast to work on some of the major hotel chain networks is a little difficult in most cases. There are multiple problems that arise:

#####1) Wireless Isolation
Most hotels have wireless isolation turned on. This means that wireless clients like a Chromecast or your laptop/smart device cannot see each other or communicate directly with each other over the wireless network. This is a problem because the current protocols that Chromecast uses to communicate with your laptop or smart device requires both to be able to communicate directly with each other over the wireless network (See [mDNS](http://en.wikipedia.org/wiki/Multicast_DNS) and [DIAL](http://en.wikipedia.org/wiki/DIscovery_And_Launch)).

#####2) Wifi Login Page
Most hotels have a wifi login page. They have you enter a username/room # and sometimes a password before they'll let you access the internet from their wireless network. Most of these use a [whitelisting](http://en.wikipedia.org/wiki/Whitelist) approach where once you click login on the page and accept the terms, they will add your wifi device's [MAC address](http://en.wikipedia.org/wiki/MAC_address) to a list that allows you to access the internet from their wireless network. The problem with the Chromecast is that there is currently no way for it to "login" to that web page and get it's MAC address added to the whitelist. So even if you could communicate between the Chromecast and your laptop/smart device, the Chromecast could not go out and grab the content to stream.

#####3) WISP Mode Issues
Some folks (including me) knew the above two problems existed and bought WISP enabled travel routers/Access Points. These devices are able to connect to the hotel wifi and create their own wireless network at the same time and share the hotel wifi with any devices connected to it...in theory. These don't seem to work well with enterprise wifi networks that all of the same [ESSID](http://en.wikipedia.org/wiki/Service_set_(802.11_network)#Service_set_identification_.28SSID.29) but many differnt [BSSID's](http://en.wikipedia.org/wiki/Service_set_(802.11_network)#Basic_service_set_identification_.28BSSID.29).

##The Solution
---------------------------
1. Connect to the hotel wifi with a laptop (or other computer)
2. Connect a travel router/AP to the laptop's ethernet
3. Share the wifi connection with laptop's ethernet port
4. Connect Chromecast and other wireless devices to your travel router/AP
5. Profit

###Things you will need
   + Laptop
     + Linux OS that uses Network Manager
     + I've been testing with Ubuntu 15.04
     + Has a free WiFi radio and Ethernet port
   + WiFi Access Point or Travel Router
     + I've been testing with TP-LINK TL-MR3020
   + Chromecast

###Steps
1. Connect the laptop to the hotel's WiFi
 + Sign-in to hotel's login page if necessary
 + Verify that you have a connection to the Internet
2. Create a new connection in Network Manager for the Laptop
 + Open the Network Connections drop-down<br><br>
![Network Manager Icon](/images/network-manager-icon.png)
 + Select the 'Edit Connections...' option
 + Click the 'Add' button<br><br>
<img src=/images/net-connect-dialog.png width="400">
 + Choose 'Ethernet' and click 'Create...'<br><br>
<img src=/images/net-con-type.png width="300">
 + On the 'General' tab, fill in a new 'Connection name' and select your Ethernet cards MAC-address from the drop-down menu<br><br>
<img src=/images/net-con-eth-tab.png width="400">
 + On the 'IPv4 Settings' tab, select 'Shared to other computers' in the 'Method' drop-down<br><br>
<img src=/images/net-con-ipv4-tab.png width="400">
3. Connect the Wireless AP or Travel Router to the laptop's Ethernet port
 + Note that step (2) above automatically provides a DHCP server to the network that is attached to the Laptop's Ethernet port
 + For efficiency (and possibly even to work) the WiFi device you connect should have NAT/DHCP disabled (i.e. the WiFi clients should be getting IP-addresses via the Laptop's DHCP server that was set up)
4. Power on the WiFi device
5. Open the Network Connections drop-down and select the connection name that was set-up in Step 2
6. Connect the chromecast and any other wireless devices to the WiFi AP or Travel Router and enjoy!

**NOTE THAT GOOGLE HAS ENABLED AN [ULTRASONIC AUDIO-BASED GUEST MODE](https://support.google.com/chromecast/answer/6109297?hl=en) THAT MAY OFFER AN EASIER ALTERNATIVE THAN THE STEPS LISTED HERE**
