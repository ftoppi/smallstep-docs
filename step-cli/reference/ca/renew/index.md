---
layout: auto-doc
title: step ca renew
menu:
  docs:
    parent: step ca
---

## Name
**step ca renew** -- renew a valid certificate

## Usage

```raw
step ca renew <crt-file> <key-file>
[--ca-url=<uri>] [--root=<path>] [--password-file=<path>]
[--out=<path>] [--expires-in=<duration>] [--force]
[--expires-in=<duration>] [--pid=<int>] [--pid-file=<path>]
[--signal=<int>] [--exec=<string>] [--daemon]
[--renew-period=<duration>]
```

## Description


**step ca renew** command renews the given certificate (with a request to the
certificate authority) and writes the new certificate to disk - either overwriting
`crt-file` or using a new file when the **--out**=`file` flag is used.

With the **--daemon** flag the command will periodically update the given
certificate. By default, it will renew the certificate before 2/3 of the validity
period of the certificate has elapsed. A random jitter is used to avoid multiple
instances running at the same time. The amount of time between renewal and
certificate expiration can be configured using the **--expires-in** flag, or a
fixed period can be set with the **--renew-period** flag.

The **--daemon** flag can be combined with **--pid**, **--signal**, or **--exec**
to provide certificate reloads on your services.

## Positional arguments

`crt-file`
The certificate in PEM format that we want to renew.

`key-file`
They key file of the certificate.

## Options


**--ca-config**=`path`
The `path` to the certificate authority configuration file. Defaults to
$STEPPATH/config/ca.json

**--ca-url**=`URI`
`URI` of the targeted Step Certificate Authority.

**-f**, **--force**
Force the overwrite of files without asking.

**--offline**
Creates a certificate without contacting the certificate authority. Offline mode
uses the configuration, certificates, and keys created with **step ca init**,
but can accept a different configuration file using **--ca-config** flag.

**--password-file**=`file`
The path to the `file` containing the password to encrypt or decrypt the private key.

**--root**=`file`
The path to the PEM `file` used as the root certificate authority.

**--out**=`file`, **--output-file**=`file`
The new certificate `file` path. Defaults to overwriting the `crt-file` positional argument

**--expires-in**=`duration`
The amount of time remaining before certificate expiration,
at which point a renewal should be attempted. The certificate renewal will not
be performed if the time to expiration is greater than the **--expires-in** value.
A random jitter (duration/20) will be added to avoid multiple services hitting the
renew endpoint at the same time. The `duration` is a sequence of decimal numbers,
each with optional fraction and a unit suffix, such as "300ms", "-1.5h" or "2h45m".
Valid time units are "ns", "us" (or "µs"), "ms", "s", "m", "h".

**--pid**=`value`
The process id to signal after the certificate has been renewed. By default the
the SIGHUP (1) signal will be used, but this can be configured with the **--signal**
flag.

**--pid-file**=`path`
The `path` from which to read the process id that will be signaled after the certificate
has been renewed. By default the the SIGHUP (1) signal will be used, but this can be configured with the **--signal**
flag.

**--signal**=`number`
The signal `number` to send to the selected PID, so it can reload the
configuration and load the new certificate. Default value is SIGHUP (1)

**--exec**=`command`
The `command` to run after the certificate has been renewed.

**--daemon**
Run the renew command as a daemon, renewing and overwriting the certificate
periodically. By default the daemon will renew a certificate before 2/3 of the
time to expiration has elapsed. The period can be configured using the
**--renew-period** or **--expires-in** flags.

**--renew-period**=`duration`
The period with which to schedule renewals of the certificate in daemon mode.
Requires the **--daemon** flag. The `duration` is a sequence of decimal numbers,
each with optional fraction and a unit suffix, such as "300ms", "1.5h", or "2h45m".
Valid time units are "ns", "us" (or "µs"), "ms", "s", "m", "h".

## Examples

Renew a certificate with the configured CA:
```shell
$ step ca renew internal.crt internal.key
Would you like to overwrite internal.crt [Y/n]: y
```

Renew a certificate without overwriting the previous certificate:
```shell
$ step ca renew --out renewed.crt internal.crt internal.key
```

Renew a certificate forcing the overwrite of the previous certificate:
```shell
$ step ca renew --force internal.crt internal.key
```

Renew a certificate providing the `--ca-url` and `--root` flags:
```shell
$ step ca renew --ca-url https://ca.smallstep.com:9000 \
  --root /path/to/root_ca.crt internal.crt internal.key
Would you like to overwrite internal.crt [Y/n]: y
```

Renew skipped because it was too early:
```shell
$ step ca renew --expires-in 8h internal.crt internal.key
certificate not renewed: expires in 10h52m5s
```

Renew the certificate before 2/3 of the validity has passed:
```shell
$ step ca renew --daemon internal.crt internal.key
```

Renew the certificate before 8 hours and 30m of the expiration time:
```shell
$ step ca renew --daemon --expires-in 8h30m internal.crt internal.key
```

Renew the certificate every 16h:
```shell
$ step ca renew --daemon --renew-period 16h internal.crt internal.key
```

Renew the certificate and reload nginx:
```shell
$ step ca renew --daemon --exec "nginx -s reload" internal.crt internal.key
```

Renew the certificate and convert it to DER:
```shell
$ step ca renew --daemon --renew-period 16h \
  --exec "step certificate format --force --out internal.der internal.crt" \
  internal.crt internal.key
```

Renew a certificate using the offline mode, requires the configuration
files, certificates, and keys created with **step ca init**:
```shell
$ step ca renew --offline internal.crt internal.key
```

