# AV-Evasion With the Veil Framework

##Abstract

While the effectiveness of antivirus security in today’s environments is debatable, evading antivirus has become increasingly difficult for penetration testers (without the use of proprietary tools). The fact is that antivirus can be (and is) evaded by both penetration testers and malware authors who devote enough time and effort. We as a community know antivirus generally provides a false sense of security, however valuable assessment time is often lost constantly re-engineering AV-evasion techniques.
 
Veil-Evasion was developed to address this problem by offering a simplified, modular, open-source, and UI focused framework for generating AV-evading payloads (both public and private) in a programming language and technique agnostic way. We will cover the genesis of the framework, its structure and features, and how to develop your own payload modules. Recently released modules will be discussed, and our implementation of a lesser known shellcode injection method will be released. In addition, we will discuss Veil-Catapult, which extends the capabilities of the existing Veil framework by utilizing various methods to deliver and trigger payloads across targeted machines


Finally we will cover public reaction and disclosure ethics, as well as discuss current and future mitigation strategies to combat Veil’s effectiveness.

## Genesis and Ethical Considerations


The Veil-Evasion project began due to a common problem we experience as pentesters; our payloads are getting caught more and more by antivirus. Like many pentesters, evading antivirus was never much an issue for us. However we felt the time it took to do this on assessments wasted valuable resources we could better use to provide a better service to our customers. To this end, we created an internal framework that centralized our bypass techniques, allowed us to integrate additional methods at need and significantly sped up our evasion efforts. 

Of course, many pentest firms also have their own methods of antivirus evasion, and they tend to keep these close to the chest to maximize the window of effectiveness; it should come as no surprise that Veil’s codebase was kept private for several months. However, in the end we felt that we could better help the community by assisting others in providing more efficient and effective assessments. 

Ethically, we feel that Veil aligns with the larger disclosure debate, and believe that our efforts can help bring attention to areas where the bad guys are already easily succeeding. To channel [HD Moore](https://community.rapid7.com/community/metasploit/blog/2009/02/23/the-best-defense-is-information), “In this case, like many others, the bad guys already won.” The best defense is information, and as a community it’s in our best interest to share these techniques and promote progress.


## The Veil Framework

Veil is a true framework that utilizes a common configuration and modular structure. All payload modules in **./modules/payloads/*** are loaded dynamically into the framework, allowing users to easily utilize private payloads. Many options are provided through command line switches, and the framework now keeps a running SHA1 hash list of all generated executables. By utilizing a forked version of @mubix’s [vt-notify script](https://github.com/mubix/vt-notify), the hashes of all payloads generated can be periodically polled against Virustotal.com, alerting when a sample has been submitted.

One of our main goals with Veil is to provide a framework for the community to integrate their own AV-evasion methods. A template payload file is included at **./modules/payloads/template.py**, which demonstrates various features of the framework that help facilitate writing new payload approaches, and we also have a tutorial on [payload development](https://www.veil-evasion.com/tutorial-veil-payload-development/).


## Payload Releases

As of 1/17/13, 24 payload modules have currently been published, and over twenty additional modules have been developed internally from public and private research. Starting last September, we’ve been releasing at least one new payload on the 15th of every month in a release we’ve deemed V-Day, for [“victory over antivirus”](https://www.veil-evasion.com/v-day/).

Among the more recent releases have been the HeapAlloc() injection approach for Python, a self-contained reverse_http Meterpreter .dll [without initial staging](https://www.veil-evasion.com/building-in-the-meterpreter-dll/), the integration of third party tools, and [expiring options](http://www.veil-evasion.com/self-expiring-payloads/) for Python payloads.

We’ve also begun to release various “pure” Meterpreter stagers that don’t rely on shellcode to stage the Meterpreter .dll. Reverse_tcp has been released for [C](http://www.veil-evasion.com/veil-evasion-2-2-0-release/), [Python and C#](http://www.veil-evasion.com/veil-evasion-2-3-0-stagers/), and [reverse_http and reverse_https](https://www.veil-evasion.com/veil-evasion-2-4-0-reverse-http/) have been released for Python. An excellent explanation of how these stagers work can be found here [from Raphael Mudge](http://blog.strategiccyber.com/2012/09/13/a-loader-for-metasploits-meterpreter/) and [here from Egypt](http://mail.metasploit.com/pipermail/framework/2012-September/008660.html).


## Veil-Catapult

Utilizing the Impacket library from [Core Labs](http://corelabs.coresecurity.com/index.php?module=Wiki&action=view&type=tool&name=Impacket) and the [passing-the-hash toolkit](http://passing-the-hash.blogspot.com/), as well as the functionality of Veil-Evasion, Veil-Catapult extends our framework to include the delivery of AV-evading payloads. This allows for building evasion payloads and delivering them to the target in one shot. Several methods have been developed so far; including deploying a custom .exe, powershell invoked payloads, and a slightly novel barebones python injector.

Veil-Catapult can use the passing-the-hash toolkit to upload and trigger Veil generated payloads, or custom executables. Alternatively payloads can be hosted on a temporary Impacket server and triggered with UNC paths. Additionally, Powershell can be invoked using a standard command line shellcode-injecting payload generated by Veil, and the sticky keys sethc backdoor can be triggered as well. Using Powershell also allows for cleanup functionality, with cleanup resource scripts able to kill any associated processes and/or remove uploaded binaries from target systems.

Our barebones python injector uploads a zipped 'barebones' Python environment and standalone 7zip binary to the victim machine. Wmis or winexe is then used to unzip the environment and execute a minimal Python program that injects user-specified shellcode into memory. The only files that touch disk are known Python libraries and interpreter, and the generated shellcode is invoked without a malicious executable touching disk.


## How to Stop Us

With enough time and effort, signature-based defenses are always going to be subverted. However, a lot of malware (and Veil payload) behaviors are fairly predictable. These include an immediate reverse connection made to an attacker, a memory page is allocated with RWX permissions, functions are used to copy code in, and a thread is created. In addition, a small set of APIs are usually used in a very specific and non-standard way to invoke this behavior, which gives a great behavioral detection opportunity.

Security tools that monitor for, or attempt to prevent, these types of predictable behavior are generally  going to be better than signature-based detection. One example of API call mitigation is Ambush IPS, which is an open source intrusion detection/prevention system that allows for flexible rules to be written for API calls. Another good prevention tool is the Microsoft [Enhanced Mitigation Experience Toolki](http://support.microsoft.com/kb/2458544), which is a free utility that enforces various protection mechanisms on commonly exploited binaries such as Adobe, Java, Internet Explorer, and others. Its protections do a great job in breaking various techniques for shellcode injection, but unfortunately you can’t use it to enroll all binaries on a system.