---
layout: auto-doc
title: step crypto jwe decrypt
menu:
  docs:
    parent: step crypto jwe
---

## Name
**step crypto jwe decrypt** -- verify a JWE and decrypt ciphertext

## Usage

```raw
step crypto jwe decrypt
[--key=<path>] [--jwks=<jwks>] [--kid=<kid>]
```

## Description

**step crypto jwe decrypt** verifies a JWE read from STDIN and decrypts the
ciphertext printing it to STDOUT. If verification fails a non-zero failure
code is returned. If verification succeeds the command returns 0.

For examples, see **step help crypto jwe**.

## Options


**--key**=`path`
The `path` to the JWE recipient's private key. The argument should be the name of a file
containing a private JWK (or a JWK encrypted as a JWE payload) or a PEM encoded
private key (or a private key encrypted using the modes described on RFC 1423 or
with PBES2+PBKDF2 described in RFC 2898).

**--jwks**=`jwks`
The JWK Set containing the recipient's private key. The `jwks` argument should
be the name of a file. The file contents should be a JWK Set or a JWE with a
JWK Set payload. The **--jwks** flag requires the use of the **--kid** flag to
specify which key to use.

**--kid**=`kid`
The ID of the recipient's private key. `kid` is a case-sensitive string. When
used with **--key** the `kid` value must match the **"kid"** member of the JWK. When
used with **--jwks** (a JWK Set) the KID value must match the **"kid"** member of
one of the JWKs in the JWK Set.

