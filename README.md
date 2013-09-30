# ssh-keyscan2sshfp

I wrote this very basic shell script to convert ssh-keyscan output to SSHFP DNS records when I realized 
[sshfp tool](https://github.com/xelerance/sshfp) didn't support ECDSA (i.e. ecdsa-sha2-nistp256) and 
[my patch](https://github.com/xelerance/sshfp/pull/2) would take years before getting in production.

See [draft-os-ietf-sshfp-ecdsa-sha2-00](http://tools.ietf.org/html/draft-os-ietf-sshfp-ecdsa-sha2-00).

## usage

    > ./ssh-keyscan2sshfp bombshock.mantor.org shockwave.mantor.org
    bombshock.mantor.org. IN SSHFP 2 1 D99CC6D7108DFE3E97E8AA9ED33FC9B3799E4ADB
    bombshock.mantor.org. IN SSHFP 1 1 E3784681003C2768691B458BE7084A3A70BC8E92
    bombshock.mantor.org. IN SSHFP 3 1 A924EAB29F8BBF2E6142CDCECAD1DCB616FA8EF8
    shockwave.mantor.org. IN SSHFP 2 1 4AC5A2243CEB9D7174DB456613B454D6299F30A8
    shockwave.mantor.org. IN SSHFP 1 1 D989A5820A0E4FD4D3A03A1297E0D9897BA59063

## license

Public domain
