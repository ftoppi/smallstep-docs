---
layout: auto-doc
title: step beta ca admin remove
menu:
  docs:
    parent: step beta ca admin
---

## Name
**step beta ca admin remove** -- remove an admin from the CA configuration

## Usage

```raw
step beta ca admin remove <subject> [--provisioner=<id>] [--ca-url=<uri>]
[--root=<file>]
```

## Description

**step beta ca admin remove** removes an admin from the CA configuration.

## Positional arguments

`name`
The name of the admin to be removed.

## Options


**--provisioner**=`value`
Filter admins by provisioner name.

**--admin-cert**=`chain`
Admin certificate (`chain`) in PEM format to store in the 'x5c' header of a JWT.

**--admin-key**=`file`
Private key `file`, used to sign a JWT, corresponding to the admin certificate that will
be stored in the 'x5c' header.

**--admin-provisioner**=`name`, **--admin-issuer**=`name`
The provisioner `name` to use for generating admin credentials.

**--admin-subject**=`subject`, **--admin-name**=`subject`
The admin `subject` to use for generating admin credentials.

**--password-file**=`file`
The path to the `file` containing the password to encrypt or decrypt the private key.

**--ca-url**=`URI`
`URI` of the targeted Step Certificate Authority.

**--root**=`file`
The path to the PEM `file` used as the root certificate authority.

## Examples

Remove an admin:
```shell
$ step beta ca admin remove max@smallstep.com
```

Remove an admin with additional filtering by provisioner:
```shell
$ step beta ca admin remove max@smallstep.com --provisioner admin-jwk
```


