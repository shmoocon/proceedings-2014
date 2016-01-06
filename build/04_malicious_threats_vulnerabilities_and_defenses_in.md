# Malicious Threats, Vulnerabilities and Defenses in WhatsApp and Mobile Instant Messaging Platforms

## Abstract

Global surveillance emerged as a phenomenon since the late 1940s and Internet and mobile technology are being developed with such pace that it is impossible to guarantee electronic privacy and nobody should expect it. How strong are the actual Instant Messaging Platforms? Do they take care of our security and privacy? We'll look inside the security of several clients (like BBM or Line) and will put our focus on Snapchat and WhatsApp.

We'll disclosure some vulnerabilities that can affect users and Snapchat service, increasing scores,  impersonating other accounts or launching Dos attacks.  

WhatsApp might not be as widely known as Twitter, but the company announced that it has passed 400 million active monthly users. WhatsApp has been plagued by several security issues in the past, so we decided to start the research. We've discovered several vulnerabilities, including encryption flaws, remote DOS (making the client crash by sending a custom message), or how to spoof messages manipulating sender address information.

We'll also release a new version of our tool with different protection layers: encryption, anonymity, and using a custom XMPP server. It's necessary to implement additional measures until WhatsApp decides to take security seriously.  


## INSTANT MESSAGING: HOW SECURE IS IT?

The proliferation of cell phones with full keyboards has made it easier to send mobile instant messages. All of the major instant messaging services also let users have their instant messages forwarded directly to their cell phones when they’re on-the-go. In addition, IM users are instant messaging from within their social networking profiles.

Instant messaging is not only popular at home and on-the-go, but workplace use is becoming commonplace. More than one in four users say they use instant messaging at work. Further, half of at-work IM users say that instant messaging makes them more productive at work.

We'll look inside the security of several clients, like [BBM](http://global.blackberry.com/bbm.html "BBM Homepage") or [Line](http://line.me/en/ "Line Homepage"), but we'll put our focus on [Snapchat](http://www.snapchat.com/ "Snapchat Homepage") and [WhatsApp](http://www.whatsapp.com "WhatsApp Homepage").


## SNAPCHAT

[Snapchat](http://www.snapchat.com/ "Snapchat Homepage") is a photo messaging application that let can take photos, record videos, add text and drawings, and send them to a controlled list of recipients. These sent photographs and videos are known as Snaps. Users set a time limit for how long recipients can view their Snaps after which they will be hidden from the recipient's device and deleted from Snapchat's servers.

Thanks to a gap in the service's security, the phone numbers and usernames for as many as 4.6 million accounts have been downloaded by a Web site calling itself [SnapchatDB.info](http://SnapchatDB.info "Snpachat Database Dump").

SnapchatDB reportedly gained access to the Snapchat data through a vulnerability disclosed by a group of security researchers. In a [report](http://gibsonsec.org/snapchat/fulldisclosure/ "Snapchat - GibSec Full Disclosure") posted on Christmas Day, Australia-based [Gibson Security](http://gibsonsec.org/ "Gibson Security Homepage") explained how the app's Android and iOS API could be hacked to expose user information.

We'll disclosure some other vulnerabilities in that can affect users and Snapchat service, increasing scores,  impersonating other accounts or launching [DoS](http://en.wikipedia.org/wiki/Denial-of-service_attack "Denial-of-service attack") attacks.  

**Do you think we can attack the 4.6 million accounts exposed in the last days?**

## WHATSAPP

[WhatsApp](http://www.whatsapp.com "WhatsApp Homepage") is a cross-platform (available for iPhone, Android, Blackberry, Nokia and Windows Phone, but no official desktop clients) instant messaging subscription service for smartphones, that let users send messages and multimedia files to each other. 

WhatsApp might not be as widely known as Twitter, but it is definitely just as popular in terms of users. The company announced that it has passed 400 million active monthly users ([Forbes](http://www.forbes.com/sites/parmyolson/2013/12/19/watch-out-facebook-whatsapp-climbs-past-400-million-active-users/ "WhatsApp Climbs Past 400 Million Active Users")). It’s interesting to compare that stat to Twitter, which has 230 million active monthly users, and to Instagram, which has 150 million on its platform.

According to the company, its users sent over 10 billion messages and received 20 billion messages per day during last August (counted separately because same messages are sent to multiple recipients). Just how much is 10 billion messages? That is 416,666,670 messages an hour, 6,944,440 messages a minute, and 115,704 messages a second... WhatsApp has done to SMS on mobile phones what Skype did to international calling on landlines!


## THE RESEARCH ##
With the [PRISM](http://en.wikipedia.org/wiki/PRISM_(surveillance_program) "PRISM (surveillance program)") scandal, we began to question whether Microsoft, Google, Apple and Facebook were the only companies working with governments to spy on the behavior of its citizens. Could [WhatsApp](http://www.whatsapp.com "WhatsApp Homepage") be one of these companies? Does WhatsApp store its user conversations? News of the threat by Saudi Arabia to declare applications illegal if the server was not established in that country ([Reuters](http://www.reuters.com/article/2013/06/16/us-saudi-internet-idUSBRE95F04R20130616)) did not make us feel calm. These sort of things make us think that users are defenseless and no current measures to ensure the privacy of content shared on these platforms exists.
  
WhatsApp has been plagued by numerous issues in their security. Until September 2011([WhatsApp leaks usernames, telephone numbers and messages)](http://www.yourdailymac.net/2011/05/whatsapp-leaks-usernames-telephone-numbers-and-messages/ "WhatsApp leaks usernames, telephone numbers and messages"), messages were sent in unencrypted plain-text format, making the system vulnerable to session hijacking and packet analysis. In May 2012, security researchers noticed that new updates of WhatsApp no longer sent messages as plaintext, the cryptographic method implemented was subsequently described as [broken, really broken](http://fileperms.org/whatsapp-is-broken-really-broken/ "WhatsApp is broken, really broken"). As of August 15, 2012, the WhatsApp support staff claim messages are encrypted in the latest version of the WhatsApp software, but without specifying the implemented cryptographic method, so we decided to start the research on this application.

## ENCRYPTION ##
The client authentication uses a custom Simple Authentication and Security Layer ([SASL](http://en.wikipedia.org/wiki/Simple_Authentication_and_Security_Layer "Simple Authentication and Security Layer")) mechanism, called **WAUTH-1**. The client has to generate a key using [PBKDF2](http://en.wikipedia.org/wiki/PBKDF2 "PBKDF2") (16 iterations) with his password, challenge data received from the login session as salt and SHA1 as hash function. The resulting SessionKey can be quite long, however we require only the first 20 bytes for the key for [RC4](http://en.wikipedia.org/wiki/RC4 "RC4") (an stream cipher), which is used to encrypt and [MAC](http://en.wikipedia.org/wiki/Message_authentication_code "Message authentication code"). The problem is WhatsApp uses same encryption key in both directions, so an attacker could recover the original plaintext.

Stream ciphers, where plaintext bits are combined with a cipher bit stream by an exclusive-or operation **XOR**, are vulnerable to attack if key is used more than once. Let me explain myself better: 
> Suppose Alice wants to send encryptions of **m1** and **m2** to Bob over a public channel. Alice and Bob have a shared key k; however, both messages are the same length as the key **k**. Since Alice is extraordinary lazy (and doesn't know about stream ciphers), she decides to just reuse the key. Alice sends ciphertexts **c1 = m1 ⊕ k** and **c2 = m2 ⊕ k** to Bob through a public channel. Unfortunately, Eve intercepts both of these ciphertexts and calculates **c1 ⊕ c2 = m1 ⊕ m2** . What can Eve do with **m1 ⊕ m2** ?
![](rc4.png)
  
From here, the task becomes separating the two plaintexts from one another. To do this, we have to do a little guessing about the plaintexts themselves. This sort of guessing is called a [Known-plaintext attack](http://en.wikipedia.org/wiki/Known-plaintext_attack "Known-plaintext attack")(or Crib-Dragging). The idea is to use a [Frecuency Analysis](http://en.wikipedia.org/wiki/Frequency_analysis "Frequency analysis") based on the original language used in the plaintext, following the steps bellow:    

1. [Guess a word](http://en.wikipedia.org/wiki/Most_common_words_in_English "Most common words in English") that might appear in one of the messages  
3. Encode the word from step 1 to a hex string  
3. **XOR** the two cipher-text messages  
4. **XOR** the hex string from step 2 at each position of the **XOR** of the two cipher-texts (from step 3)
5. When the result from step 4 is readable text, we guess the English word and expand our crib search.  
6. If the result is not readable text, we try an **XOR** of the crib word at the next position.  

Because of this, if two messages are encrypted with the same key and an attacker can intercept them, like on an open wireless network, he can analyze them to cancel out the key and eventually recover the original plaintext information.


**Game over for our privacy...**


## WHATSAPP PRIVACY GUARD ##
The main objective of the research was to add a new layer of security and privacy to ensure that in the exchange of messages between members of a conversation both the integrity and confidentiality could not be affected by an external attacker. 

![WhatsApp Privacy Guard](WAPG.png)

We created [WhatsApp Privacy Guard](http://www.seguridadofensiva.com/ "WhatsApp Privacy Guard Homepage") (**WAPG**) defined different layers inside a new hierarchy of security:  

- The **first layer** of security involves adding secure encryption to the client. If an attacker intercepts the messages, or any governments try to intercept our messages at WhatsApp's server , they won't find any legible information. Only recipients that know the password and algorithm chosen will be able to decrypt the original message.  
- In the **second layer**, we give a certain level of anonymity to the conversation by using fake/anonymous accounts and intermediate communication nodes. We ensure that there is no direct communication between the mobile phone and the server.  
- Finally, a **third layer** would be set to modify the inner workings of the application, routing all traffic and conversation messages to our own server ([XMPP](http://xmpp.org/ "XMPP Standards Foundation")) to ensure the privacy of communication and only using the original WhatsApp's servers to send fake and no-sense data.   

We've also discovered several vulnerabilities more that we'll disclosure (with proof of concept code), including :

- Encryption flaws (recover the original plaintext information)  
- Remote [DoS](http://en.wikipedia.org/wiki/Denial-of-service_attack "Denial-of-service attack"), which can be exploited by malicious people to cause the client crash by sending a custom message
- How to spoof messages manipulating sender address information.

## MAIN GOAL ##
We wanted to protect all of our rights and liberties so we developed this technique to be used in a manner completely transparent for the users and completely customizable. The main impact on society is providing a way to prevent prying eyes of governments and private corporations from analyzing our data and exchange of information for their own benefit.

It can be adapted to add new layers of security/privacy. The process will involve anonymizing and encrypting the data (text, pictures, videos, etc.) exchanged between users so that when they reach application's servers they won't be in "plain text" and will only be legible for the people inside the conversation.

**It's necessary to implement additional measures until Instant Messaging Platforms decide to take security seriously.**

Title: Malicious Threats, Vulnerabilities and Defenses in WhatsApp and Mobile Instant Messaging Platforms  
Primary Author Name: Jaime Sanchez  
Primary Author Affiliation: http://www.seguridadofensiva.com / @segofensiva  
Primary Author Email: jsanchez@seguridadofensiva.com  
Additional Author Name: Pablo San Emeterio  
Additional Author Affiliation: I+D Optenet / @psaneme  
Additional Author Email: psaneme@gmail.com  
Keywords:  Instant Messaging, Line, BBM, Snapchat, WhatsApp, encryption, privacy, anonymity, security, mobile, IM, Vulnerability, Defenses, Denial of Service, surveillance, RC4, XOR, WAUTH-1  