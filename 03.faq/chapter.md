---
title: FAQ
taxonomy:
    category: chapter
---

##### Drupal/Wordpress got updated... how should i update my app?

Well, you should branch wp, create a new dev/test site, go into wp, update via web interface, and if everything works, then commit the changes and merge to master... OR go update the master directly.

##### My SSH Key is not uploading

Does devPanel say "Invalid ssh-key" ?

Does your key look like this?

````
-- BEGIN SSH2 PUBLIC KEY --
Comment: "rsa-key-20180208"
AAAAB3NzaC1yc2EAAAABJQAAAQEAtbirDwEVali2B85+v24nDOhF5BjzDACCQvTY
aSwk1ILzwoOm52juXSsGNIPbckueJNIWPVrkQX4PqBh9Kox8FhBnviSL8fpyYIyy
NQXF61zHDCs2n/fcQAxf23C+A8LBBDrobT0k2d3jg09PTOD08Dq0PqEjiHJb/m0f
LXxJwXUL0bl4MNiUjJnmMtXNiPAihre5jgY5gzlCk4IS29JtErTbZH9jsMM1/95N
175NWM2gBJ0mhvpGUrmcEVGjexZcpg3D1YTMTRzS/JkICPdPbHKJEouqk8ococoF
TPQS1hhvn+NxPIv0U6bLZoDhNggzlPih4edgA5kCFb2Amlr6bQ==
-- END SSH2 PUBLIC KEY --
```

Then it's because this key is not in the openssh format... you need to convert it with the command below and user the converted key that it'll generate:
```
$ ssh-keygen -i -f key-file
```
