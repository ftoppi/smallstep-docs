---
layout: auto-doc
title: step certificate bundle
menu:
  docs:
    parent: step certificate
---

## Name
**step certificate bundle** -- bundle a certificate with intermediate certificate(s) needed for certificate path validation

## Usage

```raw
step certificate bundle <crt_file> <ca> <bundle_file>
```

## Description

**step certificate bundle** bundles a certificate
    with any intermediates necessary to validate the certificate.

## Positional arguments

`crt_file`
The path to a leaf certificate to bundle with issuing certificate(s).

`ca`
The path to the Certificate Authority issusing certificate.

`bundle_file`
The path to write the bundle.

## Options


**-f**, **--force**
Force the overwrite of files without asking.

## Exit codes

This command returns 0 on success and >0 if any error occurs.

## Examples

Bundle a certificate with the intermediate certificate authority (issuer):

```shell
$ step certificate bundle foo.crt intermediate-ca.crt foo-bundle.crt
```


