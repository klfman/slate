---
title: Developermail Documentation

toc_footers:
  - <a href='https://developermail.io/signup'>Sign Up for Developermail</a>
  - <a href='https://github.com/developermail/slate'>Help improving this documentation</a>

includes: 

search: false
---


# Introduction

This is a living document. Please help us improving this documentation by forking
and opening pull requests at https://github.com/developermail/slate Thanks!

Please note that Developermail is currently in BETA. Please expect bugs and issues.
If you encounter anything, please contact us at support@developermail.io


# Getting started

## What you need?

* Invitation code (Developermail is invite-only at the moment)
* Git (``brew install git``)
* Email client

## Sign up

Open https://developermail.io/signup, enter your invitation code and
create your first mailbox. You are able to create more mailboxes/ aliases later.

We are starting by offering a 5 USD per mailbox per month plan. This plan includes
5GB of storage. Aliases under @developermail.io are limited to 3 aliases. There are no
limits on aliases for custom domains. Everything else is under our fair usage policy.


## Update DNS settings

If you registered your mailbox under @developermail.io you can skip this step.

If you registered your mailbox under a custom domain, you need to update your DNS
settings for this domain in order to retrieve emails.

Please open https://developermail.io/dns-check#/your-domain.com for more information.

## Start configuring ...

You are now ready to start configuiring. Clone your private repository and
provide the credentials that have been provided to you after your signup.

```shell
git clone https://developermail.io/git/bob@example.com
Cloning into 'bob@example.com'...
remote: Counting objects: 11, done.
remote: Compressing objects: 100% (10/10), done.
remote: Total 11 (delta 2), reused 0 (delta 0)
Unpacking objects: 100% (11/11), done.
Checking connectivity... done.

cd bob@example.com
ls
config.yaml  sieve/
```


# Configuration


## config.yaml

> Your initial ``config.yaml`` will look like this:

```yaml
developermail.io:
  fritz:
    sieve: sieve/default.sieve
    aliases: []
    forwards: []
```

> Or, if you use a custom domain:

```yaml
example.com:
  fritz:
    sieve: sieve/default.sieve
    aliases: []
    forwards: []
```

### Aliases

#### Create alias

#### Delete alias


### Forwards

#### Create forward

#### Delete forward


### Mailboxes

#### Create mailbox

#### Delete mailbox

#### Delete my account


## sieve


