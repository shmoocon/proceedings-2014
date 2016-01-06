# ADD: Complicating Memory Forensics Through Memory Disarray

## Abstract

This paper introduces ADD (Attention Deficit Disorder), a tool that litters Windows physical memory with (configurable amounts and types of) garbage to disrupt memory forensics. Memory forensics has become so mainstream that it's catching too many attackers during routine investigations (making Jake a sad panda). If memory forensics were much harder to perform, then attackers could retain the upper hand. ADD increases the cost of memory forensics by allocating new structures in memory that serve only to disrupt an investigation.

This paper explains at a very high level how ADD complicates memory forensics and raises the bar for forensic investigator. We discuss the architecture and motivations for developing and releasing this tool that clearly can be used for malicious purposes.

## Introduction

The field of memory forensics is fascinating and rapidly evolving.  All of this is for good reason:  the search space for a memory dump is orders of magnitude smaller than that of a subject’s hard drive(s) for the same information.  Some would say that analyzing a memory dump is _damn near magic_ (okay, maybe that was just us who said that).  Memory forensics is often used to generate leads for traditional forensics, where professionals pivot from memory to other artifacts (disk/registry/etc).

## Background

Memory forensics on Windows is so attractive because the memory manager only clears the contents of RAM when it is reallocated.  As long as a machine remains powered on, remnants of old processes, network connections, files, etc. may be found in RAM long after they have been deallocated.  Additionally, residual artifacts may be found from a previous system boot. By recovering these structures from memory, investigators obtain a window into the past.

A primary concern with live response has traditionally been that rootkits might hide processes, network connections, or other OS objects from examination.  Memory forensics techniques enable the investigator to scan for objects that have been hidden by a rootkit unlinking them from lists maintained by the OS.  The same scanning technique (relying mainly on sophisticated pattern matching) may also be used to find objects which were previously allocated, but have since been deallocated.  As an example of the latter, an investigator may be able to discover that a process named “malware.exe” was executed in the past, even though it is no longer executing.  The investigator may even get additional information, such as the path to the executable on disk, the start and stop time, and parent process.

## Introducing ADD

Until now, investigators have worked under the assumption that objects found via memory scans (but not present in OS maintained lists) were either unlinked by a rootkit or that they were previously allocated and freed.  In either case, they have been treated as legitimate artifacts.  Our new framework seeks to challenge that assumption.  The ADD framework operates by creating fake artifacts in memory.  A suspect would use this framework not to hide, but to complicate investigations if/when their machines are forensically analyzed.  The suspect uses ADD to plant OS objects that are completely fake, but are detected by the scans performed by popular memory forensics tools.  

Planting fake artifacts allows the suspect to send the investigator chasing artifacts that are completely falsified.  At first glance, this may seem to be only an annoyance.  However, many investigations have strict budgetary constraints.  If the investigator’s time can be wasted (and budget expended) chasing fake artifacts, she may never determine the full extent of the compromise.  This may also frustrate junior analysts who may never determine that the artifacts are counterfeit.

We believe that the bigger issue here is that of reasonable doubt.  Explaining digital forensics to a jury (particularly in cases where the “experts” disagree) is exceedingly difficult.  The framework allows the suspect to introduce specific evidence for consideration.  Because the evidence is in memory, but not on disk, investigators must somehow explain this discrepancy.  ADD does for memory forensics what timestomp did for NTFS filesystem forensics: it forces the investigator to consider that things may not be as they appear.

## Architecture

ADD operates by replicating the structure of OS structures not normally visible in user allocated memory.  These structures are often opaque and change with OS releases and service packs (SP).  This makes ADD very OS and SP dependent.  The current release of ADD only operates correctly against Windows 7 (x86) SP1.  However, it could be easily extended to operate against other OS’s, SP’s, and architectures (x64).

Early in development, it was presumed that OS structures could be faked in memory allocated to a user space process.  The process memory could then be freed, leaving the artifact intact.  This allowed us to create a proof of concept tool without the need for a device driver.    However, this caused two problems.  First, fake allocated objects found during a memory scan are clear forgeries since they are allocated to user memory rather than kernel pools.  Second, we found (anecdotally) that user memory seems more likely to be reallocated, clearing away the forged artifact.

To facilitate the forgery of items that still appear in allocated memory, a device driver was created.  The driver allows the creation of objects with the correct kernel memory pool tags (rather than simply forging these tags).  Once the pool allocations are created and correctly populated with faux OS structures, they can either be left allocated or deallocated and returned to the free memory pool (depending on the desired effect).  Memory returned to the free pool may be reallocated, hence there is no guarantee that forged artifacts will be captured in the memory dump.  However, it is possible to manually prove (though current tools do not support this) that artifacts that remain allocated are fraudulent.  Therefore, this is a trade space that the suspect must consider carefully for maximum effect.  With regards to file objects, we have found anecdotally that allocating multiple copies of the same record and then later deallocating them at random intervals increases the chance that the forged object will remain in memory.  However, this is currently a moot point.  The suspect need not worry about freeing forged objects until tools and analysis techniques are tuned to account for such mischief.

## Why did you write ADD?

We have been criticized for introducing this framework and making this technology available to attackers and other evildoers.  However, we aren’t convinced that this technology isn’t already available to criminals.  Having studied the available tools, we understand just how fragile memory forensics is.  The fact that our framework can inject fake file objects, network connections, and processes, fooling traditional techniques means that we can’t tell (using today’s tools) if an attacker is **already** doing this.  The goal of this research is to offer a framework that developers can use to test their tool’s resistance to such trickery.

Tags: Memory Forensics, Malware, APT, Anti-Forensics

**Primary Author Name**: Jacob Williams  
**Primary Author Affiliation**: CSRgroup Computer Security  
**Primary Author Email**: malwarejake@gmail.com  
**Additional Author Name**: Alissa Torres  
**Additional Author Affiliation**: Sibertor Forensics  
**Additional Author Email**: alissa.torres@gmail.com
