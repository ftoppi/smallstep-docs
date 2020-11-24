---
layout: auto-doc
title: step ca bootstrap
menu:
  docs:
    parent: step ca
---

## Name
**step ca bootstrap** -- initialize the environment to use the CA commands

## Usage

```raw
step ca bootstrap 
[--ca-url=<uri>] [--fingerprint=<fingerprint>] [--install]
[--team=name] [--team-url=url] [--redirect-url=<url>]
```

## Description

**step ca bootstrap** downloads the root certificate from the certificate
authority and sets up the current environment to use it.

Bootstrap will store the root certificate in `$STEPPATH/certs/root_ca.crt` and
create a configuration file in `$STEPPATH/configs/defaults.json` with the CA
url, the root certificate location and its fingerprint.

After the bootstrap, ca commands do not need to specify the flags
--ca-url, --root or --fingerprint if we want to use the same environment.

## Options


**--ca-url**=`URI`
`URI` of the targeted Step Certificate Authority.

**--fingerprint**=`fingerprint`
The `fingerprint` of the targeted root certificate.

**--install**
Install the root certificate into the system truststore.

**--team**=`ID`
The team `ID` used to bootstrap the environment.

**--team-url**=`url`
The `url` step queries to retrieve initial team configuration. Only used with
the **--team** option. If the url contains `<>` placeholders, they are replaced with the team ID.

**--redirect-url**=`url`
Terminal OAuth redirect `url`.

**-f**, **--force**
Force the overwrite of files without asking.

## Examples

Bootstrap using the CA url and a fingerprint:
```shell
$ step ca bootstrap --ca-url https://ca.example.org \
  --fingerprint d9d0978692f1c7cc791f5c343ce98771900721405e834cd27b9502cc719f5097
```

Bootstrap and install the root certificate
```shell
$ step ca bootstrap --ca-url https://ca.example.org \
  --fingerprint d9d0978692f1c7cc791f5c343ce98771900721405e834cd27b9502cc719f5097 \
  --install
```

Bootstrap with a smallstep.com CA using a team ID:
```shell
$ step ca bootstrap --team superteam
```

To use team IDs in your own environment, you'll need an HTTP(S) server
serving a JSON file:
```shell
{"url":"https://ca.example.org","fingerprint":"d9d0978692f1c7cc791f5c343ce98771900721405e834cd27b9502cc719f5097"}
```

Then, this command will look for the file at https://config.example.org/superteam:
```shell
$ step ca bootstrap --team superteam --team-url https://config.example.org/<>
```

