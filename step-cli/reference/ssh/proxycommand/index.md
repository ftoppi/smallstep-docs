---
layout: auto-doc
title: step ssh proxycommand
menu:
  docs:
    parent: step ssh
---

## Name
**step ssh proxycommand** -- proxy ssh connections according to the host registry

## Usage

```raw
step ssh proxycommand <user> <host> <port>
[--provisioner=<name>] [--set=<key=value>] [--set-file=<path>] 
[--ca-url=<uri>] [--root=<file>] [--offline] [--ca-config=<path>]
```

## Description

**step ssh proxycommand** looks into the host registry
and proxies the ssh connection according to its configuration. This command
is used in the ssh client config with `ProxyCommand` keyword.

This command will add the user to the ssh-agent if necessary.

## Positional arguments

`user`
The remote username, and the subject used to login.

`host`
The host to connect to.

`port`
The port to connect to.

## Options


**--provisioner**=`name`, **--issuer**=`name`
The provisioner `name` to use.

**--set**=`key=value`
The `key=value` pair with template data variables to send to the CA. Use the **--set** flag multiple times to add multiple variables.

**--set-file**=`path`
The `path` of a JSON file with the template data to send to the CA.

**--ca-url**=`URI`
`URI` of the targeted Step Certificate Authority.

**--root**=`file`
The path to the PEM `file` used as the root certificate authority.

**--offline**
Creates a certificate without contacting the certificate authority. Offline mode
uses the configuration, certificates, and keys created with **step ca init**,
but can accept a different configuration file using **--ca-config** flag.

**--ca-config**=`path`
The `path` to the certificate authority configuration file. Defaults to
$STEPPATH/config/ca.json

