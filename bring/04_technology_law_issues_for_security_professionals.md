# Technology Law Issues for Security Professionals

## Abstract

An emerging gap exists between the demands of today's technology systems, the necessity for computer security research, and the reality of the law. The potential tension between these elements poses a challenge especially for computer security researchers--some who might be misunderstood or who may unintentionally run afoul a myriad of complex laws with potentially breathtaking penalties.

In plain language, this presentation raises awareness of some of the potential traps for the unwary. The presentation raises the issues and provides a brief and general informational overview of the law. Perhaps even more importantly, the presentation provides some background on what “the law” means, how law is actually interpreted or applied, and discusses both the federal and a sampling of, the oftentimes overlooked, state laws with potentially serious, negative consequences for researchers.
Specific laws discussed include the Stored Communications Act (addressing email and other communications), the Computer Fraud and Abuse Act (increasingly applied in unintended ways such as employment contracts), Digital Millennium Copyright Act (anti-circumvention), and a sampling of potential state laws related to computer crimes.

## Content

Many people have an interest in “the law.” Most want to avoid violating the law. With the threat of prison, fines, civil lawsuit damages, and staggering legal costs, knowing “the law” seems prudent.  Furthermore, courts subscribe to an ancient maxim: ignorance of the law is no excuse.

Thus basic awareness of what “the law” means, examples of how some laws might apply, and general resources mighty help security researchers.

## What Is “the Law?”

Sources of “the law” include treaties, constitutions, statutes, regulations, rules, ordinances, and court opinions. 

![\[Illustration: U.S. Sources of Law\]](imgs/US_Sources_of_Law_Rev.png "U.S. Sources of Law")

Furthermore, these sources might be international, federal, state, or local. Some come from the judiciary; others from regulatory or administrative agencies (think IRS or FAA); others from legislators; and others from local governments. In addition, the common-law serves as a sometimes murky back-drop to the written law. Thus, “the law” exists at multiple levels and derives from multiple sources.
 
Generally, laws are criminal or civil. The government prosecutes criminal law violations and, imposes fines, prison, or some other penalty if found guilty. Private persons file civil lawsuits. A civil lawsuit results in a verdict (or settlement) with “damages” or an injunction awarded to a prevailing party. 

In the United States, court opinions (“rulings”) play a major role in shaping “the law.” While legislators “write” laws, the courts apply “the law” to specific cases. Court opinions often clarify or amplify “written” laws. In some cases, an opinion might serve as precedent for other cases. 

Precedent deserves additional description. In a nutshell, not all courts are the same. Technically, only decisions by the U.S. Supreme Court bind everyone. Otherwise, a careful analysis is required to see if an opinion is actually precedential. Appellate courts might issue precedential opinions while trial courts generally do not. Thus, precedent may be affected by: 

* state or federal case?, 
* trial or appellate court?, 
* geographic location?, and
* laws at issue? 

For example, an opinion by a California, state, appellate court does not necessarily apply to persons in Pennsylvania. An opinion by a federal, appellate court in Chicago (7th Circuit), might not apply to persons in Vermont (2nd Circuit).

![\[Illustration: Simplified U.S. Federal Court Structure\]](imgs/Simplified_Federal_Court_Structure.png "Simplified U.S. Federal Court Structure")

An opinion by a state, trial court might not bind others even in the same state. 

Thus, “the law” is complex. Not only must the sources of law be identified, but how, and if, those sources apply must be evaluated.

##Sample Federal Laws 

Starting in the 1980s, federal legislators began addressing “computer crimes.” Many of these laws include significant civil and criminal penalties. Furthermore, recent, novel applications of these laws pose potential pitfalls.

### CFAA

The Computer Fraud and Abuse Act, [18 U.S.C. §1030](http://www.law.cornell.edu/uscode/text/18/1030 "Computer Fraud and Abuse Act"), is the primary, federal, computer crimes and “anti-hacking” law. Foremost, the law imposes significant criminal and civil penalties for accessing computers “without authorization” or by “exceeding authorized access.”

Several recent cases illustrate the criminal application of the CFAA. Two persons in Las Vegas were prosecuted for exploiting a firmware bug in video poker machines. [Kevin Poulsen, *Use a Software Bug to Win Video Poker? That’s a Federal Hacking Case*, Wired (May 05, 2013)](http://www.wired.com/threatlevel/2013/05/game-king/ "Use a Software Bug to Win Video Poker? That’s a Federal Hacking Case"). An Anonymous sympathizer in Wisconsin was recently prosecuted for a one-minute, DDoS operation--resulting in two years federal probation and restitution. [Zeljka Zorz, *Wisconsin Man Sentenced for DDoS Attack Against Koch Industries*, Help Net Security (Dec. 03, 2013)](https://www.net-security.org/secworld.php?id=16039 " Wisconsin Man Sentenced for DDoS Attack Against Koch Industries"). Most people are already very familiar with the tragic Aaron Swartz case--prosecution for unauthorized access to JSTOR.

A growing trend arises from civil lawsuits under the CFAA, [18 U.S.C. §1030(g)](http://www.law.cornell.edu/uscode/text/18/1030 "Computer Fraud and Abuse Act"). Companies might bring civil lawsuits to recover data-breach costs or to force someone to stop using a service. Craigslist used a civil lawsuit to stop 3Taps from harvesting Craigslist's content. [Jon Brodkin, *Changing IP Address to Access Public Website Ruled Violation of US Law*, Ars Technica (Aug. 19, 2013)](http://arstechnica.com/tech-policy/2013/08/changing-ip-address-to-access-public-website-ruled-violation-of-us-law/ "Changing IP Address to Access Public Website Ruled Violation of US Law"). 
Employers also use the CFAA to take action against employees who take customer lists or code when leaving an employer. [*WEC Carolina Energy v. Miller*, 687 F.3d 199 (4th. Cir  2012)](http://www.ca4.uscourts.gov/Opinions/Published/111201.P.pdf "WEC Carolina Energy v. Miller, 687 F.3d 199 (4th. Cir  2012)")

Originating in 1984, the CFAA broadly punishes unauthorized access to virtually any connected computer. Due to the broad language, significant civil and criminal penalties, and novel new applications of the law, the CFAA remains a formidable force and source of liability for researchers.


### ECPA/SCA 

The Electronic Communications Privacy Act, [18 U.S.C. §§2511-2520](http://www.law.cornell.edu/uscode/text/18/part-I/chapter-119 "Electronic Communications Privacy Act"), and Stored Communications Act [18 U.S.C. §§2701-2712(http://www.law.cornell.edu/uscode/text/18/part-I/chapter-121 "Stored Communications Act") protect electronic communications from interception or access (if stored).

For security researchers, novel applications of the ECPA/SCA may result in criminal charges or civil lawsuits, [18 USC §2520](http://www.law.cornell.edu/uscode/text/18/2520 "18 USC §2520"), due to the law's broad language. For example, a recent suit allegedly involving webcam spying on students raised ECPA/SCA issues. [Gregg Keizer, *Pennsylvania Schools Spying on Students Using Laptop Webcams, Claims Lawsuit*, ComputerWorld (Feb. 18, 2010)](https://www.computerworld.com/s/article/9158818/Pennsylvania_schools_spying_on_students_using_laptop_webcams_claims_lawsuit "Pennsylvania Schools Spying on Students Using Laptop Webcams, Claims Lawsuit").  Likewise, intercepting or accessing video, VoIP calls, voicemail, or email could trigger ECPA/SCA penalties. 

### DMCA 
The Digital Millennium Copyright Act, [17 USC §§1201–1205](http://www.law.cornell.edu/uscode/text/17/chapter-12 "Digital Millennium Copyright Act"), prohibits circumvention of copyright protection technologies--unless an exception applies--and making circumvention somehow available. Those *limited* exceptions include reverse engineering *for interoperability*, cryptography  research, and security research, [§1201(j)](http://www.law.cornell.edu/uscode/text/17/1201 "§1201(j)"). However, the DMCA conditions the exceptions on compliance with the CFAA. [For example, 17 USC §§1201(j)(2)](http://www.law.cornell.edu/uscode/text/17/1201 "§1201(j)(2)") Thus, the exceptions might be narrower than they first seem.

While the anti-circumvention provisions have been largely dormant, the DMCA still poses issues for unsuspecting researchers working with copyrighted materials. 

## Sample State Laws 

States individually enact laws. Most states adopt computer crimes codes with hefty penalties just like the federal laws. State laws might even sound very similar to federal laws. But each state is free to distinctly interpret the similar language. 

For example, Pennsylvania prohibits unlawful use of computers, computer trespass, data theft, unlawful data duplication, DoS, spam, and computer viruses,  [18 Pa.C.S. §§7601-7661](http://www.legis.state.pa.us/cfdocs/legis/LI/consCheck.cfm?txtType=HTM&ttl=18&div=0&chpt=76 "18 Pa.C.S. §§7601-7661"). Other laws might also have computer-related implications. For example, the School Code permits student expulsion for violation of computer use policies. [M.T. v. Cent. York Sch. Dist., 937 A.2d 538 (Pa.Commw.Ct. 2007)](http://www.leagle.com/decision/20071475937A2d538_11321 "M.T. v. Cent. York Sch. Dist., 937 A.2d 538 (Pa.Commw.Ct. 2007)"). 

Thus, state laws can include even broader liability than federal laws. State laws vary from state to state so knowing state law can be complicated.

##Conclusion##

While only the briefest overview, the complexities of “the law” should be evident. Many organizations do an great job of raising awareness of legal issues--such as [SlashDot](http://slashdot.org/), [Ars Technica](http://arstechnica.com/), [EFF](https://www.eff.org/), and [EPIC](https://www.epic.org/). If uncertain, some organizations offer legal help or consult an attorney directly. But even general awareness and more refined assessment of online resources might be helpful.


## References

#### Metadata

Tags: law, statutes, courts, Computer Fraud and Abuse Act, CFAA, Stored Communications Act, SCA, Electronic Communications Privacy Act, ECPA, Digital Millennium Copyright Act, DMCA, computer crimes, state computer crimes, data breach reporting, emerging legal issues

**Primary Author Name**: Shannon Brown  
**Primary Author Affiliation**: Shannon Brown, Esq.—Consulting Attorney  
**Primary Author Email**: shmoocon2014@shannonbrownlaw.com  
**Primary Author Bio**: Shannon Brown has a background as a software developer; CIO; independent technology consultant; systems administrator; national, public policy researcher; language translator; college instructor; farmer; community leader; cooperative president; lawyer; and business owner. Shannon is a licensed attorney in Pennsylvania, New Jersey, and federal court with focus on legal issues in technology, cryptography,  and computer security. He also regularly writes articles and conducts training about law-and-technology for attorneys. Shannon recently developed a machine learning software application for the legal community to help provide access to justice. His research interests include computer security, cryptography, and machine learning. 