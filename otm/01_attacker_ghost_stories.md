# Attacker Ghost Stories

## Mostly Free Defenses That Give Attackers Nightmares

## Abstract

This talk is about protections, mitigations, or detection mechanisms that I’ve seen across businesses big and small that were innovative and highly effective, yet free (or mostly free) and stopped me (as an attacker) dead in my tracks. We will be going over 11 (or a many as we can get to) methods, tactics, and software setups that will cut down intrusions significantly. Changes that you can deploy or start deployment of the hour after the talk is done.

## Content

RSA, Blackhat, and other large “Infosec” conferences include vendor areas. These vendor areas are filled with black box vendors and software vendors that claim everything from all-in-one solutions to negative day detection of exploits. What aren’t vended in these areas are solutions that are free, or low cost. Why? Because it’s a ton of money to rent a table at these large conferences and it doesn’t make sense to have zero return on that investment.

So what are these low cost solutions that no know will make any money on? They are written in the notes and suggestions sections of almost every penetration test report on the planet. Below are 3 of the 12 mitigations that we’ll be talking about at ShmooCon 2014.

## Enhanced Mitigation Experience Toolkit

EMET enforces protections where memory attacks become standard. Any given attack can have a different payload, and attack any given feature or function of any particular application, but they all have to talk to memory in the same way. EMET aims to detect and prevent those types of communications, and it’s free.

EMET pushes enforcement of system layer protections (ASLR/DEP/SEHOP) as well as application specific protections are “Opt-In”. It only protects what you tell it to and in only the ways that you tell it to. But you don’t have to be an exploit developer to configure it; EMET comes out of the box with a number of example configuration files that work really well.

There are however, public bypasses for some, if not all of the protections that EMET offers. Each protection enabled increases the level of cost or effort the attacker needs to employ to get successful code execution. The will most likely mean the attacker will be required to chain multiple bugs together and they won’t do so lightly. 

## Java User-Agent Blocking

Java has joined Internet Explorer as one of the most targeted technologies for phishing. With OSX becoming much more prevalent in the corporate world this will probably become more and more the truth. 

The problem with client side attacks on Java is that memory exploits are just one of many methods of exploitation. EMET will certainly detect and block the ones that mess with memory, but what about all of the other methods?

When a user surfs to a page where an applet is hosted, be it malicious or legitimate, the browser invokes a java plugin. This plugin tells Java where to pull the applet. The applet is then pulled down to the client, not by the browser, but by java itself. User-Agents such as “Mozilla 4.0/Internet Explorer 10” is used by a browser, but is easily distinguishable against the user agent that Java uses when is “Java/1.6.0.24” or whatever version the client may be using.

A corporation can install a block any requests with the “Java/” user agent. This will also block legitimate applets as well, so it’s best to run a query on your proxy for the past 30 or 60 days for any requests using that user agent and determine which domains have java that your users use on a regular basis. Exclusions from this rule can then be put in place.

Squid, the free and open source proxy can be configured to make this kind of blocking with very little configuration

One thing of note, if this block is in place there will be no visible problems that a user will plainly understand what happened and since its Java making the call a simple splash page describing what happened won’t be effective. Make sure your helpdesk knows about this change and knows if there are web site complaints to check to see if it’s a java based site and give them a way to submit for an addition to the white list of sites allowed to do Java.

# Authenticated Splash Proxies

As an attacker, proxies are relatively simple to overcome in their most basic form. Invisible proxies will just pick up the traffic, inspect it for legitimately and forward it through. Configured proxies add another layer an attacker needs to cope with, but also simple to bypass by setting to malware to use the configured proxy server. Authenticated proxies add a slightly more difficult layer but if the proxy uses authentication that is built in to the OS (Windows supports Basic, Digest, and NTLM), then the OS will automatically do the authentication. Again, this adds just a very basic hurtle for the attacker to overcome, and is usually just another OS API call to add to the malware.

Two options that will put the hurt on any attacker are: 

1. Use authentication that isn’t built into the OS (i.e. a web form). This makes it very difficult for a piece of malware to automate and usually requires special targeting to circumvent. 

2. Domain approval splash pages. Each day an organization wipes the list and blocks every single domain on the Internet. The first user that goes to a domain is prompted with a big splash page (after they authenticate) giving them the option to “unblock” the domain they are trying to go to. Again, they attacker will have a hard time automating this process and will require an extra level of targeting to automate it. This also provides added psychological barrier for people, they are less likely to “approve” random sites when they think they are in an authoritative role (being able to approve a site). The splash page can also be worded to say something like “do you approved the unblocking of this domain for the entire company?”


Other mitigations to be covered are:

* Crowdsourcing security
* Logging
* Vuln Scanning vs. Vuln Reporting
* Antivirus / HIPS
* Port Forwarding Honeypots
* WPAD
* DNS
* Password Auditing
* Evil Canaries


Tags: defense, java, 0day, emet, proxy, honeypots, canaries, dns, antivirus, hips, ids, ips, passwords, auditing, phishing, hacker economics, bug bounty, incentive programs

**Primary Author Name**: Mubix "Rob" Fuller  
**Primary Author Affiliation**: Hak5 / Metasploit  
**Primary Author Email**: mubix@metasploit.com  
**Primary Author Bio**: Mubix is a Senior Red Teamer. His professional experience starts from his time on active duty as United States Marine. He has worked with devices and software that run gambit in the security realm. He has a few certifications, but the titles that he holds above the rest is FATHER, HUSBAND and United States Marine.
