# openssh-pkcs11-card-pin-patch

## Overview
This is patch to allow openssh 7.6p1 to get pkcs11 PIN from command line or configuration

## Build

You will need to install development tools/libraries for your operating system.

```
cd /path_to/openssh-7.6p1
patch <openssh-7.6p1-pin.patch
./configure --prefix=/usr/local
make
make install
```

## Added features

q.v. man pages for ssh and ssh-add (the patch includes modifications to those)

### Adds -A flag to ssh-add
This allows the pkcs11 pin to come from the command line instead of a password prompt. -A for pkcs11 PIN instead of password prompt.)

e.g.
  ```
  ssh-add -A 123456 -s /usr/local/lib/opensc-pkcs11.so
  ```
  
### Adds PKCS11PIN option to ssh config

This allows the pkcs11 pin from ssh itself to come from the command line or ssh config file.

#### command line example

e.g. 
```
  ssh -o PKCS11PIN=123456 host.domain.com 
```
  
#### ssh_config example
Similarly, you can put the PKCS11PIN option in the ssh config file

e.g.
      
```
Host host.domain.com
  PKCS11Provider /usr/local/lib/opensc-pkcs11.so
  PKCS11PIN 123456
```

