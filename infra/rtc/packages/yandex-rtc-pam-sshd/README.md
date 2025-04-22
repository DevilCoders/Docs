# PAM sshd config for RTC clusters

This package replace (divert) `/etc/pam.d/sshd` (which originally belongs to
`openssh-server`) by it's RTC version.

Initial RTC conf is based on `openssh-server=1:7.2p2-4ubuntu2.8` default
conf with following patch:

```
mixas@sas1-0003:~$ diff openssh-server/etc/pam.d/sshd GIDEON-18-pam-sshd
0a1,2
> # DO NOT EDIT MANUALLY: this file is part of a deb package
>
55a58,60
>
> # Logging SSH sessions (st/GIDEON-18 and st/GIDEON-16).
> session    optional     pam_gideon.so
mixas@sas1-0003:~$ md5sum openssh-server/etc/pam.d/sshd GIDEON-18-pam-sshd
8b4c7a12b031424b2a9946881da59812  openssh-server/etc/pam.d/sshd
16d79b0e4764330f1662162925fddf90  GIDEON-18-pam-sshd
mixas@sas1-0003:~$
```

There are several reasons to put PAM sshd config file statically:

* Security - this conf must be verifiable, reviewable and have commits hostory.
* Consistency - identical config for all hosts.
* Reproducibility - even corrupted, conf may be easily restored.
* Maintainability - conf files with such structure can't be maintained safely
  with local editions made by scripts (directives sequence is important at
  least).

Yep, all this means local patching is NOT supported. ANY changes SHOULD be done
explicitly, under supervision of hostman and security teams and deployed using
stages.

## How to build package manually

    ya package --debian --checkout --not-sign-debian pkg.json
