---
layout: auto-doc
title: step certificate format
menu:
  docs:
    parent: step certificate
---

## Name
**step certificate format** -- reformat certificate

## Usage

```raw
step certificate format <crt_file> [--out=<file>]
```

## Description

**step certificate format** prints the certificate in
a different format.

Only 2 formats are currently supported; PEM and ASN.1 DER. This tool will convert
a certificate in one format to the other.

## Positional arguments

`crt_file`
Path to a certificate file.

## Options


**--out**=`value`
Path to write the reformatted result.

**-f**, **--force**
Force the overwrite of files without asking.

## Exit codes

This command returns 0 on success and >0 if any error occurs.

## Examples

Convert PEM format to DER.
```shell
$ step certificate format foo.pem
```

Convert DER format to PEM.
```shell
$ step certificate format foo.der
```

Convert PEM format to DER and write to disk.
```shell
$ step certificate format foo.pem --out foo.der
```


