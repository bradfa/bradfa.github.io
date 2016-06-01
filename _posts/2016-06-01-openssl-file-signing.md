---
layout: post
title: Exact Steps - Use OpenSSL to Sign a File
date: 2016-06-01
comments: false
---

Sometimes you might want to deploy a file, like a tarball, with an embedded
public/private key signature so that a recipient can validate that the file came
from the source they think it came from.  This technique is often used for
deploying software updates.

Generally, a public/private key signature is distributed separate from the file
of interest.  For example, most Linux distributions will provide a signature
digest file or hash checksum value for people who download the distribution
installer to check the installer against.  This works fine but it requires 2
files, it could be more convenient to have both the file itself and the
signature concatenated together in such a way that it's easy to work with.

A way that I've found to accomplish this using OpenSSL (so as to avoid using
GnuPG) follows these exact steps:

First, create an 2048 bit RSA private key using openssl (**KEEP THIS PRIVATE KEY
SECRET!**):

```
openssl genrsa -out private.pem 2048
```

Then, create the associated public key for this private key:

```
openssl rsa -in private.pem -out public.pem -outform PEM -pubout
```

Now you have `private.pem` and `public.pem`.  Distribute `public.pem` to all
entities which need to validate that a file was signed by `private.pem` and
keep `private.pem` in a secure location (and don't lose it!).

Finally, to create a signature of a file and then append that signature to the
file:

```
openssl dgst -sha256 -sign private.pem -out digest tarball.tar.gz
cat tarball.tar.gz digest >> tarball.tar.gz.signed
```

Now you can distribute one file which has an embedded public/private key
signature! :)

If you receive a concatenated input file plus digest, you will need to first
extract the digest portion to a file on its own and then remove the digest from
the original file.  This can be done using dd:

```
SIZE=$(stat -c%s tarball.tar.gz.signed)
dd if=tarball.tar.gz.signed of=digest bs=1 skip=$((SIZE-256))
dd if=/dev/null of=tarball.tar.gz.signed bs=1 seek=$((SIZE-256))
mv tarball.tar.gz.signed tarball.tar.gz
```

And to validate a given digest file against the file it supposedly signs using
the public key, use openssl again:

```
openssl dgst -sha256 -verify public.pem -signature digest tarball.tar.gz
```
