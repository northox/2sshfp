# 2sshfp
Very basic shell scripts to create SSHFP DNS records.

## Description
I wrote those very basic script to create SSHFP DNS records when I realized 
[sshfp tool](https://github.com/xelerance/sshfp) didn't support ECDSA (i.e. 
ecdsa-sha2-nistp256) and [my patch](https://github.com/xelerance/sshfp/pull/2) 
would take years before getting in to production. See [draft-os-ietf-sshfp-ecdsa-sha2-00](http://tools.ietf.org/html/draft-os-ietf-sshfp-ecdsa-sha2-00).

Now it has evolved and also support [ed25519](http://tools.ietf.org/html/draft-moonesamy-sshfp-ed25519-01) 
as the sshfp tool seems to be dead.

## Features
Supports rsa, dsa, **ecdsa and ed25519** ciphers and sha1/sha256 hash algorithms.

## Requirements
openssl, sed and awk commands

## SSHFP records?
SSHFP are basically host ssh key fingerprints stored in DNS records. If you can trust DNS 
query (i.e. DNSSEC) you can validate SSH's host fingerprint automatically.

Here's one: 
```soundwave.mantor.org. IN SSHFP 1 1 F48459337A91E833FA259C8F95D751D22D8541C2```

The first number refers to the cipher of the key (1=rsa, 2=dsa, 3=ecdsa, 4=ed25519), the second number is the 
hash algorithm (1=sha1, 2=sha256) used and the last long string is the hash of the key itself.

## What is it used for?
Merge the resulting DNS records in your zone and use them: 

  - configure SSH client to verify SSHFP records via 'VerifyHostKeyDNS yes';
  - make sure you're using DNSSEC. ;)

### 2sshfp (using local host keys)
Recommended - Run this locally. It creates SSHFP record out of `/etc/ssh/ssh_host_*_key.pub` keys.

    > ./2sshfp vortex
    vortex IN SSHFP 1 1 BBE600FEB1200CB02D5A2912DB37648F65B4A2FE
    vortex IN SSHFP 1 2 64C62A33E3FDD2EB94A40B376C2AD4691BB215403217C5D2A92B166581880377
    vortex IN SSHFP 2 1 9DDCD0CDE23225BC7EB0051D4FB3928BB17AE4BE
    vortex IN SSHFP 2 2 2A58473A4AEC6E1943F8A0E0FDA05269B7CC77347621BBBAA813E2D00D287624
    vortex IN SSHFP 3 1 3635F4E90C969C01E5DEA94F26F8268DDC334E25
    vortex IN SSHFP 3 2 D109F93C739BC6401D74412F0A638877F1B5B7C1B94602BA20E6EB264EEB8754
    vortex IN SSHFP 4 1 C01A3E12F70139C56EACC2DE93B0E5C7CC8D6BB4
    vortex IN SSHFP 4 2 197D56859D92B89003456E30782AE449EE8A136766831C482C81344ADFCD5E4E

### ssh-keyscan2sshfp
Not recommended - This one used ssh-keyscan and connects to ssh servers to extract SSH keys remotely. 
Oviously, you need to trust your network.. which you don't right? - ARP/DNS poisoning, etc. 

    > ./ssh-keyscan2sshfp bombshock.mantor.org shockwave.mantor.org
    ####################################################
    Should not be used unless you can really trust your
    network... but who can?!?
    ####################################################
    bombshock.mantor.org. IN SSHFP 2 1 021866EBA03E5F338EE63762A70C767204490467
    bombshock.mantor.org. IN SSHFP 2 2 3955BB4170D723C2EDA27F7AD7A79CF438B940EA2D92A7929AE77ED9561F70C4
    bombshock.mantor.org. IN SSHFP 1 1 74676382DC8459218C42983A01902552529BDF9F
    bombshock.mantor.org. IN SSHFP 1 2 76C19705F568AF6E50D775FCA7BA2C029D34018D29C1502FEB06992005EC7B38
    bombshock.mantor.org. IN SSHFP 3 1 3FB05E3FC65428C8B030FB91E88EFA17C918E97D
    bombshock.mantor.org. IN SSHFP 3 2 1BCB86FA73AD341B7DFBEEA84439FA316F6916E1D912D1B71C03CA42F5B4AE89
    shockwave.mantor.org. IN SSHFP 2 1 4AC5A2243CEB9D7174DB456613B454D6299F30A8
    shockwave.mantor.org. IN SSHFP 2 2 15A706840F1FDEF2A764F42A528E8A10415219C5470DB62E924D9778B222452E
    shockwave.mantor.org. IN SSHFP 1 1 D989A5820A0E4FD4D3A03A1297E0D9897BA59063
    shockwave.mantor.org. IN SSHFP 1 2 9DDB3AF589D4063CEF5F188C1420509C118408855218865934A05F32FE2FDB31

## license
Public domain - A gift to the Internet
