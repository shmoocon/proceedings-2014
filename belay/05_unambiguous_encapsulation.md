# Unambiguous Encapsulation
### Separating Data and Signaling

## Abstract

Inspired by LANGSEC and Packet in Packet, we have been investigating methods of encapsulating data such that the encapsulated data cannot be mistaken for associated metadata. Our primary goal is to find new classes of error correcting codes that support unambiguous encapsulation.

We have begun to identify new ways to encapsulate data using encodings that unambiguously differentiate inner (encapsulated) data from outer data. We present an introduction to unambiguous encapsulation and share our initial findings.

## Introduction

Existing methods of channel coding encapsulate data ambiguously. For example, a packet's payload in a wireless communication protocol is encoded and modulated in the same manner as the packet's header. This ambiguity enables a class of attacks exemplified by Packet in Packet[^1]. Similarly, data at rest are typically encapsulated in a manner that can be confused with surrounding data or executable code. This ambiguity enables many types of attack in which user supplied data are interpreted as executable code.

Below we demonstrate an example of unambiguous encapsulation using a delimited base64 file format. We then proceed to show how the technique may be applied to error correcting codes for communication and data storage.


##An example of unambiguous encapsulation: Delimited Base64 Files

The csv file format is simpler and safer to parse if each data element in the file is encoded with characters that are never used as (outer) delimiters. A traditional csv file might look as follows:

	shmoocon,january,"washington, dc"
	defcon,july,las vegas
	toorcon,october,san diego

A comma is used as a field delimiter, and a newline is used as a record delimiter. As a comma is a valid character within a field, we need to quote or escape the comma when it is used as data rather than metadata. In this respect, a commas in a csv file is ambiguous; without additional information we cannot determine the meaning for the comma.

If each field is base64 encoded, the same file looks like this:

	c2htb29jb24=,amFudWFyeQ==,d2FzaGluZ3RvbiwgZGM=
	ZGVmY29u,anVseQ==,bGFzIHZlZ2Fz
	dG9vcmNvbg==,b2N0b2Jlcg==,c2FuIGRpZWdv

Because the comma and newline do not appear in base64 encoded data, the encapsulation of inner data elements is unambiguous. Outer data consist only of commas and newlines. Inner data are represented only by characters that appear in base64 encoding. This encapsulation avoids the problems associated with escaping and quotation. Any commas or newlines present within a field are unambiguously differentiated from outer commas and newlines because they are base64 encoded.

An unambiguous format similar to this is formally defined in the delimited base64 file format specification[2]. We believe that, even with the addition of base64 decoding, a parser for this file format will require fewer lines of code than existing csv parsers. Decoding base64 data is shorter and better defined than the code required to handle quoting, escaping, and the associated corner cases of the csv format.

Delimited base64 files can encode any 8-bit data while csv files typically may include only plain text. They are nestable because the inner encoding can encode all characters found in both the delimiters and the encoded data. Nestability is an interesting property of this scheme that is not found in every scheme for unambiguous encapsulation.

An example of a similar solution is Dan Kaminsky's Interpolique[^3]. However, the outer character set (the delimiters) for a delimited base64 file format may be chosen so that it does not overlap at all with the character set of the inner encoding. This makes it easier to prove that malicious inner data can't be interpreted as outer data.


## Error Control Codes


While our delimited base64 file format is a helpful introduction to the concept of unambiguous encapsulation, our main area of interest is applying the techniques of unambiguous encapsulation to error correcting codes used for transmitting and storing data.

When data are stored or transmitted using a noisy or lossy medium, they are typically encoded with an error control code providing some degree of error detection or correction. These codes use codewords of several bits to represent a smaller number of data bits. The additional bits of transmitted information may be used by the receiver of the data to detect or correct bit errors introduced by the medium.

It may be beneficial to select these codes such that distinct codewords are used to represent metadata (outer) and encapsulated (inner) data. We have begun to discover codes that have interesting encapsulation properties.

To date, we have sought codes that consists of linear block codes providing more bits of isolation than detection. As far as we are aware, the property of isolation is a novel way to judge the effectiveness of error control codes.

Existing codes are selected primarily by the probability of uncorrectable or undetectable bit errors, the complexity of the decoder, and the efficiency of the code. We propose that future selection of error control codes should also consider the probability of bit errors breaking encapsulation.

Error control codes are traditionally generated by analytic methods, but they can also be found by brute force search. By implementing brute force methods[^4], we have produced error control codes with certain properties even if we have not produced analytic methods for the generation of codes with isolation properties.

Using a Python program to enumerate all possible codes of a given codeword length that have specified properties, we produced a list of all binary linear block codes with five bit codewords, two data bits (i.e. four codewords in the code), and a minimum Hamming distance of two.

We were then able to analyze pairs of codes, such as the following:

	00000, 00011, 00101, 01001
	01110, 10110, 11010, 11100

Each of these is a (5,2,2) linear block code in the traditional notation of coding theory. This pair is complementary in that there is no codeword present in both codes, and the pair is also isolated by a minimum Hamming distance of three from the one code to the other. We call such a pair of codes an Isolated Complementary Binary Linear Block Code (ICBLBC). One of the pair could be used to encode inner (encapsulated) data and the other to encode outer data.

A single bit error can be detected by the receiver of a message so encoded. For example, if 00001 is received, the receiver would find that the received codeword is not valid (in either code). A pair of bit errors could result in an invalid codeword (e.g. a transmitted 00000 could be received as 11000) but could also result in a valid codeword from the same code (e.g. a transmitted 00000 could be received as 00011). However, it is impossible for a pair of bit errors to result in a codeword that belongs to the other code. A minimum of three bit errors would be required for the receiver to interpret a codeword as belonging to the wrong code, thus breaking encapsulation. In many systems, the likelihood of three out of five bits being flipped is considerably less than the likelihood of one or two flipped bits.

We have built upon these initial successful findings, using a C implementation of a more efficient algorithm[4], to produce pairs of codes with 6 bit codewords that have isolation properties. We are currently working on a Verilog implementation to exploit the parallel nature of FPGA devices to brute force the discovery of even longer codes. These codes will possess greater error correction and detection capabilities, and we also expect them to have more interesting isolation properties.

In the future we hope to identify additional classes of error correcting codes that provide encapsulation. For each class of codes, we will either prove by construction that they exist or by exhaustive search that they do not exist up to a certain codeword length.

Conclusion
----------
Unambiguous encapsulation is a useful design pattern that can be applied in any
case where data are encapsulated.

We hope that the codes produced by this project will be useful in practical
applications and that we have been able to promote discussion around the
concept of unambiguous encapsulation.

Acknowledgments
---------------

We would like to thank members of the LANGSEC community for their advice,
encouragement, and feedback. We also thank Mike Kershaw and David Hulton for
assistance with the project.

Our work is supported by the DARPA Cyber Fast Track program.


## References

* [^1] Packets in packets, Goodspeed et al., USENIX Workshop on Offensive Technologies 2011,
https://www.usenix.org/legacy/events/woot11/tech/final_files/Goodspeed.pdf

* [^2] Delimited base64 file format specification, Ossmann,
https://github.com/mossmann/unambiguous-encapsulation/blob/master/doc/delimitedbase64spec.txt

* [^3] Interpolique, Kaminsky, http://dankaminsky.com/interpolique

* [^4] https://github.com/mossmann/unambiguous-encapsulation

#### Metadata

Tags: packets in packets, forward error correction, encoding

**Primary Author Name**: Michael Ossmann  
**Primary Author Affiliation**: Great Scott Gadgets  
**Primary Author Email**: mike@ossmann.com  

**Additional Author Name**: Dominic Spill  
**Additional Author Affiliation**: Great Scott Gadgets  
**Additional Author Email**: dominicgs@gmail.com