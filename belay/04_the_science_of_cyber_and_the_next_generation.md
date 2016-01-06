# The “Science of Cyber” and the Next Generation of Security Tools

## Abstract

Governments around the world are investing heavily in the so called "science of cyber" in order to create a rigorous scientific base for the next generation of security tools. But what's going on in the walled-off world of academia? Will this new science eventually lead to more improved security in cyber space? In this paper, we will several ongoing research projects in this new area of science including the use of game theory to defend the smart grid and the use of logical reasoning to address the attribution problem.  We firmly believe that exposing such research to the community of practitioners (i.e. the ShmooCon audience) will help initiate a dialogue with academic in order to both ground scientific endeavors in the real world as well as lead to more rapidly fielding of cutting-edge innovation.  

## Content

In recent years, there has been much investment in the so-called “Science of Cyber” in order to identify and leverage fundamental properties of cyber-security in an effort to bring about potentially game-changing technologies.  This has particularly involved academia with the desire leverage new and different ideas to the security arena.  In this paper is an effort to open a wider dialogue between academia and the practitioner community.  In fact, such an investment likely means there is a greater need for practitioners and scientists to cooperate.  The scientists lack the extensive domain knowledge practitioners gain by participating in day-to-day cyber-operations while practitioners will be interested in rapidly fielding new technology developed by scientists.  Further, scientists need practitioners to bring to help keep their theories rooted in reality, find realistic and relevant datasets, and aide in transitioning ideas to practical use.  Likewise, practitioners can leverage the efforts of scientists to obtain new methods to address problems and more rapidly use academic ideas to enhance security efforts.  In the remainder of the paper, we describe some of our ongoing efforts to provide examples of the type of academic research that may be useful to the practitioner.  


## Using Game Theory to Protect the Smart Grid  

Disruption of the power grid is a major concern for our country as we are heavily dependent upon electricity.  The increase reliance upon information technology (IT) to control the grid has caused some to speculate that an adversary may be able to cause such a disruption through cyber-attacks – particularly if he targets systems to cause a cascading failure.  Unfortunately, those defending the power grid, and the associated IT infrastructure, are faced with a handicap: they have a limited ability to patch and harden systems.  This is for two reasons: first, performing maintenance (taking systems offline) must be done in a way that minimizes customer disruption; second, many power grid systems use proprietary hardware and software – often restricting security actions.  

To address the defender’s difficulty, we modeled the scenario as a two-player game[^1].  First, the attacker wishes to target certain power substations to create a maximally-sized cascade.  Meanwhile, the defender can only harden a certain number of systems.  

We found the adversary seems to have an advantage in this game – as increase resources tend to favor attack.  We also found that a defense that tends to focus on substations connected to the more critical power lines may often be insufficient.  For instance, our simulations on a real-world power grid dataset revealed the presence of “high-payoff/low-load” nodes: critical junctures not connected to critical lines yet, if attacked, could initiate a cascade of electrical failure.  

The good news is that the creation of a probabilistic defense – where the defender randomly protects certain nodes according to a schedule – fares well against an attacker.  In our simulations this reduced the size of the cascade by 10-30 substations.  We developed algorithms for such strategies in this new line of research.  


## Using Logical Reasoning to Aide Cyber-Attribution  

Attributing which group is responsible for a cyber-attack still proves to be a daunting task.  We believe this is due to two factors:

1. The ease at which an adversary can conduct a deception operation to confuse security personnel
2. The presence of large amounts of data (evidence) to consider when conducting such analysis.

A common technique used in artificial intelligence to address this type of problem is known as logical reasoning.  However, this method presupposes that all of the analysis must be consistent – which would preclude the analyst from considering two potentially contradictory pieces of information (a case that can easily arise if the adversary is using deception).  

To address this issue, we extend a theory known as “argumentation” that allows for reasoning about competing beliefs.  In terms of cyber-attribution, this can allow for a system to consider opposing theories in an effort to determine which one is most likely.  In our work[^2], we enhanced argumentation theory with a probabilistic conditions – which represent the evidence.  Hence, an analyst would only need to specify under which evidence-based conditions a particular argument could be true.  The system would then generate all arguments for and against each different cyber-threat group and compare them using the evidence in order to assign a probability to the chances of each group having conducted the attack.  


An interesting by-product of this method is that the software will show exactly how it reached the conclusion – so an analyst can more easily trace and identify data that lead to surprising conclusions (or, alternatively, provide convincing evidence for such an explanation).  Currently, we have developed the mathematical framework and completed an initial software prototype.  

## Conclusion  
	
This paper discussed some of our ongoing efforts with regard to the “Science of Cyber” particularly how we are applying game theory and artificial intelligence to cyber-security problems.  It is our hope that this paper (and associated talk at ShmooCon) serve to spark a dialogue between academic researchers studying such problems and the practitioner community.  We close with some thoughts on collaboration.  Generally, for a scientist and a practitioner to work well together, the problem in question must be of significant to the impact to the practitioner (i.e. beyond theoretical interest) yet be interesting scientifically (i.e. cannot be solved with existing engineering methods).  Then, when modelling the problem, both sides must work to frame the correct constraints and assumptions.  While the scientist must accept certain constraints as being necessary to create a system that will eventually be useful, the practitioner must accept that certain assumptions are made in every model explored by scientists.  Finally, toward transition, the both sides must work to identify realistic and relevant datasets for testing as well as consider practical concerns for real-world use.  

We firmly believe that cooperation between the academic and practitioner community can yield significant benefits to both sides – and ultimately enhance cyber-security for users.  

## References

* [^1] P. Shakarian, H. Lei, R. Lindelauf, "Power Grid Defense Against Malicious Cascading Failure," Autonomous Agents and Multiagent Systems, to appear, 2014.  

* [^2] P. Shakarian, G. Simari, M. Falappa, "Belief Revision in Structured Probabilistic Argumentation," Foundations of Information and Knowledge Systems, to appear, 2014.  

#### Metadata

Tags: artificial intelligence, game theory, logical reasoning 

**Primary Author Name**: Paulo Shakarian  
**Primary Author Affiliation**: U.S. Military Academy (West Point)  
**Primary Author Email**: paulo@shakarian.net  