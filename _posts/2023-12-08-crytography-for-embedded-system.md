---
title: Cryptography for Embedded System
layout: post
summary: Overview about Cryptography for Embedded System
author: sangtdx
date: '2023-11-28 1:35:23 +0530'
category:
- cybersecurity
- automotive
tags:
- cybersecurity
thumbnail: "/assets/img/posts/car-cyber.png"
keywords: cybersecurity, automotive, multi categories and tags
usemathjax: false
permalink: "/blog/crytography-for-embedded-system/"
---

Hi Everyone! This training is focused on its applications in the embedded context.

- [1. Cryptography Definition](#1-cryptography-definition)
- [2. The Ecosystem](#2-the-ecosystem)
- [3. A Little bit of History](#3-a-little-bit-of-history)
  - [3.1 HARDWARE-BASED CRYPTOGRAPHY](#31-hardware-based-cryptography)
  - [3.2 AN IMPORTANT ADDITION –THE “KEY”](#32-an-important-addition-the-key)
  - [3.3 TERMINOLOGY](#33-terminology)
  - [3.4 Kerckhoffs’ Law](#34-kerckhoffs-law)
  - [3.5 HOW CAN WE BREAK A CIPHER?](#35-how-can-we-break-a-cipher)
  - [3.6 HISTORY CAN TEACH US MANY LESSONS](#36-history-can-teach-us-many-lessons)
- [4. SYMMETRIC CIPHERS](#4-symmetric-ciphers)
  - [4.1 A SIMPLE EXAMPLE](#41-a-simple-example)
  - [4.2 THE GENERIC ALGORITHM](#42-the-generic-algorithm)
  - [4.3 A PRACTICAL ALGORITHM](#43-a-practical-algorithm)

# 1. Cryptography Definition

 - Cryptography (AKA “encryption”) is a set of techniques & computations that are applied for securing data and communication against interception and eavesdropping.
 - It is the most important tool for enhancing Cyber-security and privacy, *when it is applied in a correct way*
 - We use it daily in our phones, our web surfing, when we travel (in epassports), when we use public transportation tickets, when we pay with credit cards etc.

# 2. The Ecosystem

<figure style="text-align: center;">
  <img src="/assets/img/blogs/automotive/cybersecurity/CRYPTOGRAPHY/aliceandbob.png" alt="“Alice” & “Bob”" style="display: block; margin: 0 auto;">
  <figcaption>“Alice” & “Bob”</figcaption>
</figure>

The cryptographic ecosystem:
 - 2 parties (A & B) that want to communicate with confidentiality, often called “Alice” & “Bob”, Sometimes we may add “Charlie”, “Dave” & others
 - A passive eavesdropper, often called “Eve”
 - A more active/malicious adversary, often called “Mallory”
 - The message that needs confidentiality – the “plaintext”
 - The encrypted message – the “ciphertext”
 - The encryption/decryption process (“algorithm” or “protocol”)

<figure style="text-align: center;">
  <img src="/assets/img/blogs/automotive/cybersecurity/CRYPTOGRAPHY/ecosystem.png" alt="The Ecosystem – cont" style="display: block; margin: 0 auto;">
  <figcaption>“The Ecosystem – cont”</figcaption>
</figure>

Use cases - Cryptography is applied for other use cases, not only for confidentiality:
 - Integrity protection:
	 - Examples: data in e-passports, signed software/firmware
 - Identity management & establishing trust:
	 - Examples: TLS, proving website identities to browsers
 - Access control:
	 - Examples: automotive RKE, diagnostics access to ECUs
 - Authenticity:
	 - Example: cryptocurrencies (proving that transactions were committed)

# 3. A Little bit of History

 - Some words in the Bible are encrypted with a simple substitution cipher called ATBASH (from the names of Hebrew letters)
 - ATBASH is based on the reverse order of Hebrew letters:
<figure style="text-align: center;">
  <img src="/assets/img/blogs/automotive/cybersecurity/CRYPTOGRAPHY/ATBASH.png" alt="ATBASH is based on the reverse order of Hebrew letters" style="display: block; margin: 0 auto;">
  <figcaption>“ATBASH is based on the reverse order of Hebrew letters”</figcaption>
</figure>
 - The secret is the process and once known – it can be decrypted
by anyone

## 3.1 HARDWARE-BASED CRYPTOGRAPHY
- The Middle Ages (15th century): The Alberti wheel from Italy
<figure style="text-align: center;">
  <img src="/assets/img/blogs/automotive/cybersecurity/CRYPTOGRAPHY/Alberti_wheel_from_Italy.png" alt="The Alberti wheel from Italy" style="display: block; margin: 0 auto;">
  <figcaption>“The Alberti wheel from Italy”</figcaption>
</figure>
- The 19th century from the USA
<figure style="text-align: center;">
  <img src="/assets/img/blogs/automotive/cybersecurity/CRYPTOGRAPHY/From_the_USA.png" alt="Security by Obscurity" style="display: block; margin: 0 auto;">
  <figcaption>“Security by Obscurity”</figcaption>
</figure>

## 3.2 AN IMPORTANT ADDITION –THE “KEY”
- A secret process like ATBASH is “Security by Obscurity” and is not really secure
- The Alberti Wheel added something new:

<figure style="text-align: center;">
  <img src="/assets/img/blogs/automotive/cybersecurity/CRYPTOGRAPHY/Security-by-Obscurity.png" alt="From the USA" style="display: block; margin: 0 auto;">
  <figcaption>“Security by Obscurity”</figcaption>
</figure>

- Different relative positions of the inner wheel will produce different ciphertexts
- The relative position of the wheels is the "KEY" but the process stays the same: Substitute each letter in the inner wheel with the adjacent letter in the outer wheel

## 3.3 TERMINOLOGY
- We call the cryptographic process “Algorithm” or “Protocol”
- We differentiate between instances of the same algorithm with different keys

<figure style="text-align: center;">
  <img src="/assets/img/blogs/automotive/cybersecurity/CRYPTOGRAPHY/different-keys.png" alt="algorithm with different keys" style="display: block; margin: 0 auto;">
  <figcaption>“Algorithm with different keys”</figcaption>
</figure>

## 3.4 Kerckhoffs’ Law
- The algorithm can be public
- Only the key must be secret
- The key can be changed, transported and stored
- The algorithm may be applied to all relevant data types:
	- Text, maps…
- The process should be easy (complexity ≠ security, fewer logistics = better security)

## 3.5 HOW CAN WE BREAK A CIPHER?
- There is one attack method that will always succeed: **Brute-force attack**
- We can try every possible key until we hit something meaningful. Such exhaustive searches over the entire key space are called ***“brute force attacks”***
- Brute force attacks will ***always*** succeed, unless we make them impractical:
	- Impractical = too long = until the sun runs out of hydrogen
	- Impractical = not enough silicon on earth for building HW that will do it
	- Impractical = not enough silicon on earth for building HW that will do it
	- Impractical = too long = for the lifespan of a device
- We want brute force attacks to be expensive ***enough*** for our adversaries

## 3.6 HISTORY CAN TEACH US MANY LESSONS
- We always want robust ciphers, that cannot be cryptanalyzed 
- How do we know what can be trusted? 
- This is not easy, better left to professional specialist mathematicians 
- It is far easier to know what CANNOT be trusted, especially when the author claims that the proposed scheme is unbreakable…
- We call such bogus products “Snake Oil” and there are some telltale signs:
	- 1st and foremost à not in the common standards 
	- Unreasonable key sizes (“128 bits is weak, we use a key with ten thousand bits”) 
	- Claiming “military-grade” encryption 
	- No peer review, “trust us, we know what we do” 
	- Algorithm not disclosed (remember Kerckhoff?)
- Some Cipher machine in history:
	- THE ZIMMERMAN TELEGRAM –WW1, 1917
	- WW2 – the German army used a sophisticated cipher machine called “Enigma”:
		- Originally built for banks
		- 3 rotors with ~158,000,000,000,000,000,000 combinations, a 4th rotor was added later
		- Initial cryptanalysis started in Poland and results were shared with the UK, including a crude design of a cryptanalysis machine
		- The German generals used a different machine with twelve rotors - the Lorenz machine

<figure style="text-align: center;">
  <img src="/assets/img/blogs/automotive/cybersecurity/CRYPTOGRAPHY/Enigma_Machine.png" alt="machine called “Enigma”" style="display: block; margin: 0 auto;">
  <figcaption>“Machine called “Enigma””</figcaption>
</figure>

- Today cryptography happens behind the scene in many places, such as web browsers:

<figure style="text-align: center;">
  <img src="/assets/img/blogs/automotive/cybersecurity/CRYPTOGRAPHY/moden-time.png" alt="web browsers" style="display: block; margin: 0 auto;">
  <figcaption>“web browsers”</figcaption>
</figure>

# 4. SYMMETRIC CIPHERS
## 4.1 A SIMPLE EXAMPLE
Example 1: 
- **Simple modulo addition as the algorithm:** 
	- Encryption algorithm: Ciphertext = Plaintext + Key MOD 10 
	- Decryption algorithm: Plaintext = Ciphertext + Key MOD 10
	- Plaintext = “9” o Key = “5” o Encryption: “9” + “5” MOD 10 = “4” 
	- Decryption: “4” + “5” MOD 10 = “9” 
- The decryption process is identical to the encryption in this case 
- The key must be pre-shared or agreed between parties 
	- Because both parties must apply the same key
- In the previous example, both parties applied the same key, with an identical algorithm
- In other cases, the encryption & decryption algorithms can be different but are always related
- Regardless of the algorithms, **the same pre-shared key is used by both parties**

<figure style="text-align: center;">
  <img src="/assets/img/blogs/automotive/cybersecurity/CRYPTOGRAPHY/symmetric_encryption.png" alt="This is called “symmetric encryption”" style="display: block; margin: 0 auto;">
  <figcaption>“This is called “symmetric encryption””</figcaption>
</figure>

## 4.2 THE GENERIC ALGORITHM
- The algorithm is always a fixed process-
- The specific key allows multiple instances, which are opaque to each other

<figure style="text-align: center;">
  <img src="/assets/img/blogs/automotive/cybersecurity/CRYPTOGRAPHY/SYMMETRIC-CIPHERS-algo.png" alt="symmetric encryption ALGORITHM" style="display: block; margin: 0 auto;">
  <figcaption>“symmetric encryption ALGORITHM”</figcaption>
</figure>

## 4.3 A PRACTICAL ALGORITHM
- Simple addition is obviously not robust enough, we want much better masking of the plaintext and much higher resistance to cryptanalysis
- The most common symmetric algorithm today is AES, which is a sequence of very simple operations, that also depend on the key:
  - XOR with the key
  - Write data in a 4X4 matrix
  - Swap rows & columns in matrix
  - Permutate values (i.e., mix bits in a column from the matrix)
  - Substitute values (i.e., “C” will be mapped to “W”)
  - Add/subtract modulo
  - Multiple rounds (10, 12 & 14 for 128. 192 & 256 bits respectively)
- Most of the steps use simple lookup tables, so are very fast
- Other common algorithms: Triple-DES, Twofish, RC4, XTEA…

<figure style="text-align: center;">
  <img src="/assets/img/blogs/automotive/cybersecurity/CRYPTOGRAPHY/PRACTICAL-ALGORITHM.png" alt="common symmetric algorithm" style="display: block; margin: 0 auto;">
  <figcaption>“symmetric encryption ALGORITHM”</figcaption>
</figure>