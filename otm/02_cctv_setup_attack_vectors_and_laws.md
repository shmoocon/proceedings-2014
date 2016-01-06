# CCTV - Setup, Attack Vectors and Laws

## Abstract: 
Ever wonder how to set-up a CCTV Digital Video Recording security system? This article talks about just that, as well as key factors like attack vectors and recording laws.

First, we will go over basic setup on how we planned out this project. This will include things to be mindful of such as camera quality, disk space and other features. In the second part, we will cover attack vectors we considered while setting the system and how we designed a special project to help stay anonymous from CCTV systems. 

Finally, we will go over things that you should have in mind in the legal realm for this kind of project. Be forewarned; we are not a lawyers or judges, but received advice from a NC
judge regarding recording and wiretapping laws. Included is a court case that backs up some of the conclusions and decisions we made to build this system.


CCTV - Setup, Attack Vectors and Laws
=========================

Contributions
---------------
Several people made this project and presentation possible. Joshua Schroeder and Ben Van Pelt came up with the plan for Closed Circuit Television (CCTV) system and created a solution for reliable offsite backups. 

In the InfraRed LED attack: prototype, conception and design was done by Spencer Brooks with the assistance of Joshua Schroeder. Electrical design was done by Don Schroeder.

Joshua Schroeder compiled legal thoughts. 

Motivations
-------------
The motivation for the original project came when Joshua’s dad took him to the Consumer Electronics Show in 2008 where they saw hundreds of CCTV camera systems. There were exhibitors from around the world showing off how they could hide and protect company assets. 

While in college at UNC Charlotte, Joshua bought a CCTV system learn how to attack and secure this type of system. The process of selecting the correct product was done with assistance from his roommate Ben Van Pelt. They researched Amazon, Ebay, and many other sites to find a system matching their specifications:

+ Wired 10/100 Mbps hookup
+ Offsite backup
+ Minimum 4 cameras (2 for entries, 2 for living room and kitchen)
+ Large hard drive for minimum 2 weeks continuous recording (roughly 500GB+)
+ Alerting options
+ Standard Definition video and audio recording
+ Wired cameras to protect from wireless jammers
+ Under $1000

The result was the Avtech CPCAM 16 camera system with 500GB DVR from Taiwan. It included 16 camera capability (6 cameras included), claimed FTP and email uploads with alerts and live streaming via 100/10 LAN hookup. The total cost was $711 from Ebay.

Methods
----------
One the main goals was to offsite backups in order to protect the footage in the event camera data was stolen. Both Email alerting system and FTP upload were attempted. Unfortunately, neither feature worked.

First, the project used Dropbox to upload the files from a Windows VM running AVTECH’s Video Viewer (free registration required). This application logged into the AVTECH camera system, processed video for motion detection, outputted the video to AVC format and put it on to Dropbox. With normal use, Dropbox’s 2GB filled up in a week, and a switch was made to a Box.net 50GB account. 

For streaming to mobile devices, it worked out that RTSP streams and a website could be built enhance functionality.  Quicktime encoded the streams and password protection was done via some form of .htaccess files and channels were selected via GET request in the form of: rtsp://192.168.1.100/video/empty.mov?ch=1

Attack Vectors
-----------------
Joshua and Spencer looked at ways to circumvent the following types of cameras: Wireless, outdoor w/LED, indoor/outdoor oscillating, stationary indoor domes, and hidden cameras (i.e. hidden within a clock, a sprinkler, or statue). Other non-CCTV cameras surveyed included: mobile phones, laptops, and video game consoles.

For a wireless system, a wireless jammer can be used to circumvent the security. An oscillating camera might be circumvented by sneaking past the rotation cycles the same way you would get by a patrolling guard. With a wired camera, there is always the option of cutting the cables --if they are feasibly reachable. The dome and hidden cameras are obviously the most difficult to circumvent. With the dome cameras, it is hard to see which direction the camera is facing and with the hidden cameras, well, they’re hidden!
 
HackNMod.com had used IR/LED lights on hats to block nighttime recordings. However, that prototype of the IR hat just wasn’t bright enough. This led to finding more powerful IR lights of 200mW, increasing bulb count and changing to a hoodie for delivery: 10 LEDs on each side of the hood, 20 in total, providing extremely powerful outputs. Powered by four 9-v batteries (1 battery per 5 bulbs), the device is controlled by an on/off switch located in the front pocket. Please see the sources section for complete list of all materials used, links, and prices. We have also included a diagram to reference. 

“IR Stealth Hoodie” (ISH850) 
Prototype design including the placement of bulbs, wires, and batteries:
 ![CCTV Diagram - Wires, Bulbs, Switches and 9 volt batteriest](http://joshingeneral.com/images/CCTVDiagram.jpg “IR Stealth Hoodie” (ISH850)”)

Legal
------
Another aspect researched while working on this project, was consulting with a local North Carolina judge who taught at UNC Charlotte. This brought to light legal ramifications of recording without consent.

The first thing he taught us was the idea of “reasonable expectation of privacy.” Recording our front lawn or outside is “OK” because there is no reasonable expectation of privacy there. Hence, that is why Google street views can exist. Comparatively, since there is some reasonable expectation of privacy within a home or apartment, we would need to put up signs to limit that expectation of privacy. He also told us not to record audio since that would contest with current wiretapping laws. 

Further examination of laws reveals that if you have a CCTV system, it can be evidence for either party. An example of this was Aaron Hernandez, the football player, who after allegedly killing a friend of his at his residence, he had his CCTV system destroyed and house scrubbed clean. On top of the murder charges, he now also faces a destruction of evidence charge. 

Sources
---------

* Copper Wire ($11.19) http://www.amazon.com/dp/B003HGHQ56 
* ON/OFF Switches ($5.34) http://www.amazon.com/dp/B008MU4H1I/
* 9-V Batteries ($17.50) http://www.amazon.com/dp/B00009V2QZ/
* 9-V Battery Connectors ($5.48) http://www.amazon.com/dp/B00AUB8OHU
* Infrared LEDs ($7.87) http://www.amazon.com/dp/B008QUUEYS
* Black Hoodie ($11.57) http://www.walmart.com/ip/22471487
* Black Felt ($4.95/yrd) http://www.walmart.com/ip/Creative-Cuts-Anti-Pill-Fleece-by-the-Yard/19235879
* Glue ($3.47) http://www.walmart.com/ip/E6000-Jewelry-and-Bead-Glue-1-oz/32247489
* Velcro ($6.82) http://www.walmart.com/ip/Velcro-Fabric-Fusion-Tape/24626447
* AVTECH Camera
  * http://www.avtech.com.tw/index.php?Itemid=311
  * http://www.sevenseassecurity.com/p-569-cpcam-16-channel-mpeg-4-dvr.aspx
* Aaron Hernandez http://boston.cbslocal.com/2013/09/27/aaron-hernandezs-girlfriend-shayanna-jenkins-indicted-on-perjury-charge/
* Hacknmod https://hacknmod.com/hack/blind-cameras-with-an-infrared-led-hat/

Tags: CCTV, Security, Stealth, DVR, Physical Security, Law

**Primary Author Name**: Joshua Schroeder  
**Primary Author Affiliation**: Consultant  
**Primary Author Email**: JoshInGeneral@gmail.com  
**Additional Author Name**: Spencer Brooks  
**Additional Author Affiliation**: Consultant  
**Additional Author Email**: Spencer.E.Brooks@gmail.com  