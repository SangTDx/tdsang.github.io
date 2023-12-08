---
title: Crytography for Embedded System
layout: post
summary: Overview about Crytography for Embedded System
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

**3.1 HARDWARE-BASED CRYPTOGRAPHY**
- The Middle Ages (15th century): The Alberti wheel from Italy
<figure style="text-align: center;">
  <img src="/assets/img/blogs/automotive/cybersecurity/CRYPTOGRAPHY/Alberti_wheel_from_Italy.png" alt="The Alberti wheel from Italy" style="display: block; margin: 0 auto;">
  <figcaption>“The Alberti wheel from Italy”</figcaption>
</figure>
- The 19th century from the USA
<figure style="text-align: center;">
  <img src="/assets/img/blogs/automotive/cybersecurity/CRYPTOGRAPHY/From_the_USA.png" alt="From the USA" style="display: block; margin: 0 auto;">
  <figcaption>“The 19th century from the USA”</figcaption>
</figure>