# 2sshfp
Very basic shell script to create SSHFP DNS records.

## Description
I wrote this very basic script to create SSHFP DNS records when I realized 
[sshfp tool](https://github.com/xelerance/sshfp) didn't support ECDSA (i.e. 
ecdsa-sha2-nistp256) and [my patch](https://github.com/xelerance/sshfp/pull/2) 
would take years before getting in to production. 

It creates SSHFP record out of `/etc/ssh/ssh_host_*_key.pub` keys.

## Features
- Supports rsa, dsa, **[ecdsa](http://tools.ietf.org/html/draft-os-ietf-sshfp-ecdsa-sha2-00) and [ed25519](http://tools.ietf.org/html/draft-moonesamy-sshfp-ed25519-01)** ciphers and sha1/sha256 hash algorithms.
- Tested on OpenBSD, FreeBSD and Linux

## Requirements
openssl, sed, tr and awk commands - basic stuff

## SSHFP records?
SSHFP are basically host ssh key fingerprints stored in DNS records. If you can trust DNS 
query (i.e. DNSSEC) you can validate SSH's host fingerprint automatically.

Here's one: 
```soundwave.mantor.org. IN SSHFP 1 1 F48459337A91E833FA259C8F95D751D22D8541C2```

The first number refers to the cipher of the key (1=rsa, 2=dsa, 3=ecdsa, 4=ed25519), the second number is the 
hash algorithm (1=sha1, 2=sha256) used and the last long string is the hash of the key itself.

## What is it used for?
Merge the resulting DNS records in your zone and use them: 

  - configure SSH client to verify SSHFP records via `VerifyHostKeyDNS yes`;
  - make sure you're using DNSSEC ;)

### Usage

    > ./2sshfp vortex
    vortex IN SSHFP 1 1 BBE600FEB1200CB02D5A2912DB37648F65B4A2FE
    vortex IN SSHFP 1 2 64C62A33E3FDD2EB94A40B376C2AD4691BB215403217C5D2A92B166581880377
    vortex IN SSHFP 2 1 9DDCD0CDE23225BC7EB0051D4FB3928BB17AE4BE
    vortex IN SSHFP 2 2 2A58473A4AEC6E1943F8A0E0FDA05269B7CC77347621BBBAA813E2D00D287624
    vortex IN SSHFP 3 1 3635F4E90C969C01E5DEA94F26F8268DDC334E25
    vortex IN SSHFP 3 2 D109F93C739BC6401D74412F0A638877F1B5B7C1B94602BA20E6EB264EEB8754
    vortex IN SSHFP 4 1 C01A3E12F70139C56EACC2DE93B0E5C7CC8D6BB4
    vortex IN SSHFP 4 2 197D56859D92B89003456E30782AE449EE8A136766831C482C81344ADFCD5E4E

## license
Public domain - A gift to the Internet
