# How to Train your Snapdragon
### Exploring Power Frameworks on Android


## Abstract

Have you ever wondered how power is routed around your phone, how it is stored and if it could be made dangerous? I have, and I somehow talked the DARPA Cyber Fast Track group into funding my research into the subject and allowing me to name it: "Project Burner: El Telefono Inteligente de Fuego." The overall goal of the project was: "Can I catch a phone on fire using nothing but the stored energy in the battery?" and / or "Can I break it beyond repair?". The answer was a resounding "yes."

This talk will center around how the Android (and Linux) kernels manage power and electricity, both from the wall and the battery. I will cover how those software based controls can be manipulated to fry internal components and brick phones in abundance. I will also walk through what protections have been put in place to prevent these types of attacks and how those mechanisms can be circumvented.

## Paper Synopsis

This project centers around the Android (and thus Linux) power regulation framework. The exploration is concerned with manipulating voltages as they route around the phone from kernel and processor controlled PMIC hardware.

The full documentation for the project is here: https://github.com/monk-dot/ProjectBurner.git

The outcome of this exploration was a fairly detailed mapping of what discrete hardware elements were protected from over-volting /
under-volting  and what hardware was not. This allows the researcher to target specific components of an Android device and physically break them beyond repair.

While there is more research to be done on the subject, this paper and talk should provide a valuable primer to the exploitation path for anyone else looking to continue the project. The original research was completed without the leaked internal Qualcomm documentation through blind trial and error. Further research will greatly benefit from these leaked files.

## References

#### Metadata

Tags: hardware, SoC, embedded, fire, android, qualcomm

**Primary Author Name**: Josh "m0nk" Thomas  
**Primary Author Affiliation**: Atredis  
**Primary Author Email**: josh@atredis.com