---
layout: auto-doc
title: step oauth
menu:
  docs:
    parent: step
---

## Name
**step oauth** -- authorization and single sign-on using OAuth & OIDC

## Usage

```raw
step oauth
[--provider=<provider>] [--client-id=<client-id> --client-secret=<client-secret>]
[--scope=<scope> ...] [--bare [--oidc]] [--header [--oidc]]

step oauth 
--authorization-endpoint=<authorization-endpoint> 
--token-endpoint=<token-endpoint>
--client-id=<client-id> --client-secret=<client-secret>
[--scope=<scope> ...] [--bare [--oidc]] [--header [--oidc]]

step oauth [--account=<account>] 
[--authorization-endpoint=<authorization-endpoint>] 
[--token-endpoint=<token-endpoint>]
[--scope=<scope> ...] [--bare [--oidc]] [--header [--oidc]]

step oauth --account=<account> --jwt 
[--scope=<scope> ...] [--header] [-bare]
```

## Description

**step oauth** command implements the OAuth 2.0 authorization flow.

OAuth is an open standard for access delegation, commonly used as a way for
Internet users to grant websites or applications access to their information on
other websites but without giving them the passwords. This mechanism is used by
companies such as Amazon, Google, Facebook, Microsoft and Twitter to permit the
users to share information about their accounts with third party applications or
websites. Learn more at https://en.wikipedia.org/wiki/OAuth.

This command by default performs he authorization flow with a preconfigured
Google application, but a custom one can be set combining the flags
**--client-id**, **--client-secret**, and **--provider**. The provider value
must be set to the OIDC discovery document (.well-known/openid-configuration)
endpoint. If Google is used this flag is not necessary, but the appropriate
value would be be https://accounts.google.com or
https://accounts.google.com/.well-known/openid-configuration

## Options


**--provider**=`value`, **--idp**=`value`
OAuth provider for authentication

**--email**=`value`, **-e**=`value`
Email to authenticate

**--console**, **-c**
Complete the flow while remaining only inside the terminal

**--client-id**=`value`
OAuth Client ID

**--client-secret**=`value`
OAuth Client Secret

**--account**=`value`
JSON file containing account details

**--authorization-endpoint**=`value`
OAuth Authorization Endpoint

**--token-endpoint**=`value`
OAuth Token Endpoint

**--header**
Output HTTP Authorization Header (suitable for use with curl)

**--oidc**
Output OIDC Token instead of OAuth Access Token

**--bare**
Only output the token

**--scope**=`value`
OAuth scopes

**--jwt**
Generate a JWT Auth token instead of an OAuth Token (only works with service accounts)

**--listen**=`address`
Callback listener `address` (e.g. ":10000")

**--redirect-url**=`url`
Terminal OAuth redirect `url`.

## Examples

Do the OAuth 2.0 flow using the default client:
```shell
$ step oauth
```

Redirect to localhost instead of 127.0.0.1:
```shell
$ step oauth --listen localhost:0
```

Redirect to a fixed port instead of random one:
```shell
$ step oauth --listen :10000
```

Get just the access token:
```shell
$ step oauth --bare
```

Get just the OIDC token:
```shell
$ step oauth --oidc --bare
```

Use a custom OAuth2.0 server:
```shell
$ step oauth --client-id my-client-id --client-secret my-client-secret \
  --provider https://example.org
```

