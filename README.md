# ssh-keyscan2sshfp

Very basic shell script to convert ssh-keyscan output to SSHFP DNS records.

## description

This is a really basic script which takes ssh-keyscan output and convert them in SSHFP dns records. sshfp tool already does that but still does not support ecdsa, i.e., ecdsa-sha2-nistp256.

## usage

    ssh-keyscan -t ecdsa,dsa,rsa bombshock.mantor.org >> output

    cat output | ssh-keyscan2sshfp

## license

This script is released under the new-BSD license.
