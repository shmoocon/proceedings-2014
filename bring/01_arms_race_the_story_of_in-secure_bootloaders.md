# Arms Race: The Story of (In)-Secure Bootloaders

Secure Boot is the process that ensures the critical parts of software (e.g. kernel) running on a device are authorized and have not been tampered with.  Many mobile service providers prefer to have a locked down version of their smartphones that can only boot the official kernel, and do not allow the loading of customized systems developed by others.  Even the users are supposed to be owners of smartphones, they are often not granted permission to load customized kernel by default. This results in an arms race between the smartphone vendors and the users that want to load customized kernels.

This talk presents multiple rounds of arms race between device owners (that want to load customized kernel) and the vendors (that want to lock down the device to specific kernel).
Each round will consist of us showing how to bypass the security mechanisms of the bootloader in order to reach a certain goal and then show how this hole was patched. Some rounds will focus on the same device, showing how we found new bugs even after the initial bug was patched.

#### Round 1: Samsung Galaxy S3  (Goal: Load a custom kernel)  
We found that the kernel was loaded into memory twice. One was to the proper location and the other was loaded to a spare bit of memory where it could run the signature check on the code. A parser case-sensitivity discrepancy when iterating over the partition list led us to be able to load up a custom kernel for execution but still let the bootloader run the signature check on a stock, signed kernel. This was later patched by only loading the kernel once.

#### Round 2: Samsung Galaxy Note II (Goal: Load a custom kernel)
When inspecting the kernel loading process we discovered it was possible to load and run unsigned code if the code did not start with the typical Android kernel header. We surmised that this was a leftover debugging feature to allow rapid testing of new kernel builds without the need to sign each one. Using this hole we were able to write a custom kernel loader. This debug code path was removed in the next firmware update.

#### Round 2.1: Samsung Galaxy Note II (Goal: Load a custom bootloader)
When checking how the ROM verifies the bootloader from the internal flash memory we discovered several key management mistakes. All bootloaders for this CPU were signed with the same key, even if the devices were different. A bootloader was found for a hobby board that did not enforce the signature checks for later stages, allowing us to break the chain of trust. We then created a custom bootloader that did not enforce kernel checks. Due to the key management mistakes this custom bootloader was non-revocable.

#### Round 2.2: Samsung Galaxy Note II (Goal: Load a custom bootloader)
The device was updated to block our installation mechanism for putting the custom bootloader on the device. A new vulnerability was discovered in the firmware update mechanism, and by editing the partition information table we were able to make the updater skip the otherwise mandatory signature checks for files to important partitions. This allowed us to load the custom bootloader onto devices that had updated to the new firmware. This method was patched by having the device run a signature check on the partition table at boot-time to detect any modifications.

#### Round 2.3: Samsung Galaxy Note II  (Goal: Load a custom bootloader)
The firmware update mechanism had an internal blacklist of firmware versions it was not supposed to flash, functioning primarily as downgrade prevention. We found that when the firmware was updated the developers neglected to update this blacklist, and the previous exploitable firmware was able to be put back on the device. A future update properly updated the blacklist to include all previous versions.

#### Round 3: Samsung Galaxy S4 (Goal: Load a custom kernel)
The kernel load mechanism worked by first reading a header from the disk and then loading the kernel and ramdisk to the locations specified by the header. The problem is that the parameters from the header were never validated, and the attacker is able to edit the header because it’s on the internal flash. By changing the load address in the header an attacker could load code directly on top of the running bootloader, invalidating any further security mechanisms. This was addressed in an update that ensured the load addresses from the header did not overlap the bootloader. This exploit was first published by Dan Rosenberg.

All of the bugs presented differ from the typical memory corruption vulnerabilities (e.g. buffer overflow, use-after-free). One relied on the difference in parsing the same list of data two different ways, another was able to take advantage of improper key management, and a third was an example of why input validation is critical in a high-security environment.

The mobile device ecosystem offers a somewhat unique security challenge. In many cases the attackers are the owners themselves. This also implies that the attacker will have physical access to the device, which allows for a greater range of attacks.


## References

#### Metadata


Authors: Lee Harrison, Kang Li
Emails: <lee2704,kangli>@uga.edu

