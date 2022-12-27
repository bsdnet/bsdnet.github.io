---
title: "Security Concepts Illustrated"
date: 2022-08-21T15:14:08-07:00
categories: security
draft: false
---

It will be helpful to understand modern software system like [Kubernetes](https://kubernetes.io/)with fundamental security concepts. For example, symmetric encryption, asymmetric encryption, public/private key, digital signature, certificate and signing.

# Objective

Use diagram to illustrate critical security concepts used in modern software.

# Concepts

## Encryption

Symmetric encryption uses same key for both encryption and decryption; while asymmetric encryption use different but mathematically relatedkeys for enryption and decryption.
[Symmetric Encyption](https://www.cryptomathic.com/news-events/blog/symmetric-key-encryption-why-where-and-how-its-used-in-banking) can be illustrated in the following diagram:
![Symmetric Encyption](/images/symmetric-encryption.png)

[Asymmetric Encryption](https://cheapsslsecurity.com/blog/what-is-asymmetric-encryption-understand-with-simple-examples/) can be represented as follows:
![Asymmetric Encyption](/images/asymmetric-encryption.png)

## Message Digest
A [message digest](https://www.ibm.com/docs/en/ibm-mq/7.5?topic=concepts-message-digests) is a fixed size numeric representation of the conents of a message, computed by a
hash function. While an encypted message digest forms a [digital signature](https://www.cisa.gov/uscert/ncas/tips/ST04-018).

![Message Digest](/images/message-digest-digital-signature.png)

## Signing 

Signing is widely used in today's software system from Secure Boot to
TLS/SSL communication via HTTPS. Not mention to software package signing
or electronic document signing like DocuSign.

How senser signs a document digitally?
![Signing](/images/signing.png)

How receiver verify the digital signature?
![Verify](/images/verify-signing.png)

## Certificate
[Digital certificate](https://en.wikipedia.org/wiki/Public_key_certificate) is issued by a certificate authority(CA).
Here is the digram to illustrate the process. To get a digital certificate, you need a pair of keys - public and private key.
public key, its signature encrypted by private key, and organization information are packaged into Certificate Signing Request(CSR).
The CSR will be approve and signed by a Certificate Authority(CA), and come back as a digital certificate. This certificate needs to be installed onto your server so that every browser client can talk with your server securely.

![Certificating](/images/certificating.png)

Once you got the certicate, you can understand [how TLS/SSL cetificates work](https://www.digicert.com/how-tls-ssl-certificates-work)

# References
1. [How PGP works](http://users.ece.cmu.edu/~adrian/630-f04/PGP-intro.html)
1. [Overview of Symmetric Encryption](https://www.cryptomathic.com/news-events/blog/an-overview-of-symmetric-encryption-and-the-key-lifecycle)
1. [OpenSSL 3.0 Doc](https://www.openssl.org/docs/man3.0/)
1. [SSL certificate explained](http://www.steves-internet-guide.com/ssl-certificates-explained/)
1. [Overview of SSL/TLS handshake](https://www.ibm.com/docs/en/ibm-mq/7.5?topic=ssl-overview-tls-handshake)
1. [PKI tutorial](https://pki-tutorial.readthedocs.io/en/latest/)
1. [The illustrated TLS 1.3 Connection](https://tls13.xargs.org/)
