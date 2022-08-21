---
title: "Security Concepts Illustrated"
date: 2022-08-21T15:14:08-07:00
draft: false
---

It will be helpful to understand modern software system like [Kubernetes](https://kubernetes.io/)with fundamental security concepts. For example, symmetric encryption, asymmetric encryption, public/private key, digital signature, certificate and signing.

# Objective

Use diagram to illustrate critical security concepts used in modern software.

# Concepts

## Encryption

Symmetric encryption uses same key for both encryption and decryption; while asymmetric encryption use different but mathematically relatedkeys for enryption and decryption.

![Symmetric Encyption](/images/symmetric-encryption.png)
![Asymmetric Encyption](/images/asymmetric-encryption.png)

## Message Digest
![Message Digest](/images/message-digest.png)

## Signing 
Sign a document and get a digital signature.

![Signing](/images/signing.png)

How receiver verify the digital signature?
![Verify](/images/verify-signing.png)

## Certificate
![Certificating](/images/certificating.png)

# References
1. [Overview of Symmetric Encryption](https://www.cryptomathic.com/news-events/blog/an-overview-of-symmetric-encryption-and-the-key-lifecycle)
1. [OpenSSL 3.0 Doc](https://www.openssl.org/docs/man3.0/)
1. [SSL certificate explained](http://www.steves-internet-guide.com/ssl-certificates-explained/)
