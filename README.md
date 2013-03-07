# ssh-keyscan2sshfp

Very basic shell script to convert ssh-keyscan output to SSHFP DNS records.

## description

This is a really basic script which use ssh-keyscan output and convert them in SSHFP DNS records. The famous sshfp tool already does this but still does not support ecdsa, i.e., ecdsa-sha2-nistp256.

[draft-os-ietf-sshfp-ecdsa-sha2-00](http://tools.ietf.org/html/draft-os-ietf-sshfp-ecdsa-sha2-00)

## usage

    > ./ssh-keyscan2sshfp bombshock.mantor.org shockwave.mantor.org
    bombshock.mantor.org. IN SSHFP 2 1 D99CC6D7108DFE3E97E8AA9ED33FC9B3799E4ADB
    bombshock.mantor.org. IN SSHFP 1 1 E3784681003C2768691B458BE7084A3A70BC8E92
    bombshock.mantor.org. IN SSHFP 3 1 A924EAB29F8BBF2E6142CDCECAD1DCB616FA8EF8
    shockwave.mantor.org. IN SSHFP 2 1 4AC5A2243CEB9D7174DB456613B454D6299F30A8
    shockwave.mantor.org. IN SSHFP 1 1 D989A5820A0E4FD4D3A03A1297E0D9897BA59063

## license

Public domain
