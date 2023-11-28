---
layout: post
title:  "Secure Software Flashing"
summary: "Overview about Secure Software Flashing of Automotive"
author: sangtdx
date: '2023-11-28 1:35:23 +0530'
category: ['cybersecurity', 'automotive']
tags: cybersecurity
thumbnail: /assets/img/posts/car-cyber.png
keywords: cybersecurity, automotive, multi categories and tags
usemathjax: false
permalink: /blog/secure-software-flashing/
---

# INTRODUCTION

More and more devices in our modern world come with a multitude and variety of embedded systems. An obvious example of this trend is today’s vehicles, which have dozens of electronic control units (ECUs) that control everything from the air conditioning and electric windows to the engine and brake system. Several ECUs allow downloading of updated program and data code via a boot loader. Such software might be a control unit firmware update for fixing bugs, for improving features, or for downloading data such as additional multimedia files. The first case is also called a software download or simply flashing (since flash memory is updated). The download might be performed directly over a diagnostic channel or another available communication channel such as Bluetooth and GSM.

<figure style="text-align: center;">
  <img src="/assets/img/blogs/automotive/cybersecurity/digital-signatures.png" alt="Figure 1. The generation of digital signatures at the embedded systems manufacturer." style="display: block; margin: 0 auto;">
  <figcaption>Figure 1. The generation of digital signatures at the embedded systems manufacturer.</figcaption>
</figure>

Once such vehicle communication channels are opened to the outside world for downloading software, their integrity must be ensured. An example of a malicious software download is the replacement of firmware by an unauthorized party, e.g., as done for chip tuning in the automotive context. The main security objectives are as follows:

1. Only original software must be accepted by the embedded system. No manipulated or malicious software may be downloaded to the embedded system. In particular, software must not be successfully downloaded to the embedded system that alters its defined behavior.
2. Only authenticated parties may alter data, e.g., parameters, stored in the embedded system.

Furthermore, it is also desirable for an actual security design that the compromise of a single embedded system does not affect the security of other embedded systems of the same product line, (i.e., a successful attack does not scale).

The required computational performance on the embedded system side shall be minimal.

# DIGITAL SIGNATURES

The secure software flashing scheme we present is based on digital signatures. A digital signature provides the security objective of integrity and authenticity; data being digitally signed cannot be altered by a malicious third party without being detected by the receiver. Furthermore, the receiver can verify that the data was indeed signed by the claimed signer. Moreover, the signer is not able to deny that he is the legitimate creator of the signature (non-repudiation). Digital signatures are generated and verified with asymmetric cryptographic algorithms, such as the Rivest Shamir Adleman (RSA) algorithm or Elliptic Key Cryptography (ECC).

A digital signature is computed as shown in Figure 1. There is a key pair consisting of a private key, SK, and a public key, PK. Only the signer has access to SK, whereas PK can be publicly distributed. In our setting, SK is only known to the manufacturer of the embedded system, whereas PK is built into every embedded system. The program code, x, is first hashed to a short fixed length value, y. Typically, y is computed by applying a hash function of the SHA family, resulting in an output of 20 to 32 bytes. Finally, a digital signature is computed over y using the private key, SK. The signature can then be verified by using the public key PK. Please note that the private key, SK, must never leave the secure environment of the manufacturer. Therefore, signatures are typically computed in High Security Modules (HSMs), such as smart card security controllers, which are used in banking applications and which provide tamper-resistant features in accordance with the Common Criteria (CC) security standard.

<figure style="text-align: center;" style="text-align: center;">
  <img src="/assets/img/blogs/automotive/cybersecurity/CERTIFICATES.png" alt="Secure software download." style="display: block; margin: 0 auto;">
  <figcaption>Secure software download.</figcaption>
</figure>

A public key is used in each embedded system and firmware programs are signed using the corresponding private key. It is possible to use an individual public/private key pair for each embedded system, vehicle model year, each ECU type, etc., however, this increases the logistics efforts of the overall system. In the case of individual public/private key pairs, it is reasonable to use certificates. A certificate is comparable to a passport; it certifies a public key and, if required, an identity. In the automotive case, the certificate is simply a public key signed by the OEM’s private key, together with the public key and some additional information: SigSK(PKA)|PKA|data. 

The flash program is then verified by PKA and signed with the corresponding private key. When the flashing process begins, the certificate first needs to be downloaded and verified using the OEM’s root public key PK, and then the flash program is downloaded and verified using PKA.

# SECURE SOFTWARE FLASHING

 solution for this problem in general is quite simple. Based on digital signatures, the issuer of the software signs the program code and the embedded system (e.g. the control unit in the vehicle) verifies it. Hence, the issuer holds a private key for signing the program code and the control units hold the corresponding public key for verifying it. This is shown in Figure 2 in more detail. First, the software is developed. Once it is finished (step 1), the program object code is passed to a trust center (step 2) that signs the object code using its private key. The signature is then passed back and attached to the program object code (step 3). The package of code and signature is now stored in a database (step 4) that might hold versions for different embedded systems. Finally, the appropriate program code is downloaded to an embedded system (step 5) and verified by means of its public key (step 6).

 One can see that security objective #1 is clearly fulfilled; only a legitimate authority can issue an appropriate signature for program code that will be accepted by the vehicle, i.e., only authentic software will be accepted by the embedded system. Most of today’s cars already provide a mechanism for downloading software. Hence, only a mechanism for verifying the signature is additionally needed in the vehicle. RSA is an appropriate fit for signature verification, since it allows very fast signature verification and it can be implemented in software without infringing patents.

 On the server side the key management and the organizational security must be thoroughly organized. Organizational security includes the organization of who has access to sign program code and how the process of signing is performed and recorded. However, no full-sized Public Key Infrastructure (PKI) is necessary. Basically, it is sufficient to issue a single private/public key pair such that the private key is stored in the trust center and the public key in the embedded system. The trust center might simply be a PC that is disconnected from any computer network and a secure smart card that holds the secret key.

 If a finer-grained approach is desired, a key pair for each embedded system type, for each production year, or each production location might be applied. No certificates that induce overhead are required, though. The embedded system only needs to store a public key such that no secret information is stored here. However, this public key must be protected against manipulation, i.e. it must be stored in secure memory that may be read but not overwritten. For example, many modern microcontrollers provide internal Flash ROM memory and security features which prevent the modification of this memory. Otherwise, an adversary could replace this key and then activate any manipulated software.

 Security objective #2 can be fulfilled by a simple challenge-and-response mechanism as shown in Figure 3. The embedded system and an external party (e.g., a standard PC) share a secret key. The parties then run a challenge-response scheme in order to prove that the external party knows the secret key. After a successful run, the external party can access the embedded system to adjust parameters. However, it is crucial that a well-defined interface be specified. For instance, it is reasonable to record all changes in a log file and give access only to non-safety critical data. Using a symmetric-key management is reasonable — each embedded system knows an individual symmetric secret key shared with the third party. This third party might be the system manufacturer storing all keys in a protected database. The security can be further increased by using security tokens that hold the secret key for accessing the embedded system. Such an approach even allows several authorization levels to be implemented. For instance, in the automotive context there might be a basic level for workshops to adjust typical parameters of an ECU, and another level for testing that allows all parameters to be changed.

 Protecting the key built into the embedded system is crucial. If an adversary is able to read out a symmetric key or replace a public key he might be able to manipulate program or data code. Thus, virtual software protection can be achieved only by using secure memory or applying hardware-assisted approaches employing a security anchor as described in reference 4.

 <figure style="text-align: center;">
  <img src="/assets/img/blogs/automotive/cybersecurity/falash-process.png" alt="Figure 4. Flash process" style="display: block; margin: 0 auto;">
  <figcaption>Figure 4. Flash process</figcaption>
</figure>

# SECURE FLASH PROCESS

The flash program file has several parts. Each block is optionally encrypted, and the signature of the file was computed beforehand. In the first step, the external device that triggers the flashing process optionally authenticates the bootloader (e.g., by a challenge-re sponse mechanism as described above). In the next step, a certificate might be passed to the bootloader which verifies it’s using its stored public key. Then, the external device passes block by block to the bootloader of the embedded system. The bootloader first decrypts the block and then stores it in the flash memory. At the same time, the bootloader incrementally computes the hash over each block. Once all blocks are passed, the bootloader finalizes the computation of the hash value over the new flash program file and performs a digital signature verification using the determined hash value. If the signature verification is successful, the downloaded file is accepted and activated. Otherwise, a safety procedure is activated and the bootloader awaits the download of a proper flash file. This is shown in Figure 4.

# CONCLUSIONS

Virtually all modern embedded systems are equipped with internal Flash ROM memory. Usually, a bootloader is built into the firmware to update the program. However, in most cases there are no mechanisms implemented to avoid downloading a manipulated program that alters the device’s behavior in a manner not authorized by the manufacturer. In this article we presented mechanisms to protect the software update process. These mechanisms are an efficient countermeasure to manipulation attacks, in particular, if the bootloader in the internal Flash ROM can be protected with security (so-called “lock”) bits. Such mechanisms have been successfully implemented in a variety of applications, ranging from the automotive domain to gambling and the mobile phone industry. The German automotive OEMs even standardized the mechanism for a secure bootloader2. While this standard allows the use of symmetric cryptography only via a so-called message authentication code (MAC), we strongly suggest implementing the asymmetric cryptographic approach based on digital signatures; otherwise either our original security requirements cannot be fulfilled or the organizational effort is immense.

While the cryptographic mechanisms are generally straightforward to implement, security needs to be provided at all levels, ranging from organization security to appropriate mechanisms for signing the firmware up to inclusion of suppliers. In particular, the security mechanisms need to be carefully incorporated into the existing development processes.
