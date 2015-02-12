---
title: Developermail Documentation

toc_footers:
  - <a href='https://developermail.io/signup'>Sign up for Developermail</a>
  - <a href='https://github.com/developermail/slate'>Help improving this documentation</a>

search: false
---


# Introduction

This is a living document. Please help us improving this documentation by forking
and opening pull requests on [Github](https://github.com/developermail/slate) Thanks!

Please note that Developermail is currently in BETA. Not all features are deployed yet.
You might also expect some bugs and glitches, even though we're pretty confident to provide a stable
service nontheless, as the underlying techologies are battle-proven open-source products.

If you encounter any bugs or security issues, please [contact us](mailto:support@developermail.io).


# Getting started

## Requirements

* Invitation code (Developermail is invite-only at the moment)
* [Git](http://git-scm.com/)
* Email client (IMAP/SMTP capable)

## Sign up

Open [https://developermail.io/signup](https://developermail.io/signup), enter your invitation code and
create your first mailbox. You are able to create more mailboxes/ aliases later.

Make sure you note your password once your signup is complete! It won't be displayed again. This
password is used to authenticate yourself at the IMAP/SMTP services as well as for Git
configuration.

We are starting by offering a 5 USD per mailbox per month plan.
This plan includes 5GB of storage.
Aliases for @developermail.io mailboxes are limited to three. Custom domains include unlimited free
aliases.


## Update DNS settings

> DNS settings

```shell
MX  "smtp.developermail.io."
TXT "developermail-verification=xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"
TXT "v=spf1 ip4:88.198.18.23 -all"
TXT "spf2.0/mfrom,pra ip4:88.198.18.23 -all"
TXT "v=DKIM1; h=rsa-sha256; k=rsa; p=MIGfMA0GCSqGSIb3DQEBAQUAA4GNADCBiQKBgQCpOR9yd9SJwCX/JW0CBVaZfNESAswo1Q6xXguHkMPcrWOG4cFiw2Z/Z45HBzco8GOnqqpeNJLWxaAEbJ7kTlNPcZVn0E+/iEm8trSrqUTOwNk3OkUFs0GGCn37wxypdzG8eKpLXAVrNRmmTEgvKnuBBmxz+nXFtqWYexnT0U31cwIDAQAB"
```

If you registered your mailbox using the @developermail.io domain, you can skip this step.

When using a custom domain, you need to update your DNS settings in order to retrieve mails.

We're providing a DNS settings check page ``https://developermail.io/dns-check#/your-domain.com`` to
help you with these settings.


## Configure your email client

> IMAP Endpoint

```shell
imap.developermail.io  # Port 143/STARTTLS or 993/SSL
```

> SMTP Endpoint

```shell
smtp.developermail.io  # Port 587/STARTTLS or 465/SSL
```

Developermail provides ``IMAP`` and ``SMTP`` endpoints for receiving/ sending emails.
We only accept secure connections.

Use ``username@domain.tld`` as username and the password we generated for you upon signup!


# Configuration

## Setup your repository

> Clone your private developermail configuration repository

```shell
$ git clone https://developermail.io/git/bob@example.com
Cloning into 'bob@example.com'...
Username for 'https://developermail.io': bob@example.com
Password for 'https://bob@example.com@developermail.io': *********

remote: Counting objects: 11, done.
remote: Compressing objects: 100% (10/10), done.
remote: Total 11 (delta 2), reused 0 (delta 0)
Unpacking objects: 100% (11/11), done.
Checking connectivity... done.

$ cd bob@example.com
$ tree
.
├── config.yaml
└── sieve
    └── default.sieve

1 directory, 2 files
```

Clone your repository.

You are now ready to start configuring.


Configuring your Developermail mailboxes follows the regular git workflow.
You make your changes to a file, commit them, and push them. As soon as they're pushed (and there's
not error), the changes are live!

As your configuration is a fully-functional git repository, you can use all the awesome Git candy,
such as [revert, branch, blame and all the others](http://www.git-scm.com/docs)!

## Your first push

> Add an alias to config.yaml

```yaml
developermail.io:
  # Configuration section for bob@developermail.io
  bob:
    # Add a new alias here. bob.smith@developermail.io
    # will be aliases to bob@developermail.io.
    # You can then send and receive emails from both addresses
    # Note: Aliases are free of charge!
    aliases: [bob.smith]
```

> Commit all your changes

```shell
git commit -am 'Add additional alias'
```

> Push your changes to Developermail

```
$ git push
Counting objects: 3, done.
Delta compression using up to 8 threads.
Compressing objects: 100% (3/3), done.
Writing objects: 100% (3/3), 301 bytes | 0 bytes/s, done.
Total 3 (delta 1), reused 0 (delta 0)
remote:
remote: Processing config.yaml in master branch:
remote:     Created alias bob.smith@developermail.io -> bob@developermail.io
remote:
remote:
remote: -------------------------------------------------------------------------
remote: You'll be billed $5.00 this month.
remote: If you have any questions, feel free to contact support@developermail.io!
remote:
To https://developermail.io/git/bob@developermail.io
   d336592..b33b7d7  master -> master
```

As an example, add an additional alias to your newly created mailbox.

- Edit the ``config.yaml`` file with your favorite editor
- Commit your changes
- Push them
- Your configuration is live immediately!



## Initial config.yaml

> config.yaml (custom domain)

```yaml
# We registered at Developermail using bob@example.com
example.com:
  bob:
    sieve: sieve/default.sieve
    aliases: []
    forwards: []
```

Your initial ``config.yaml`` will look like this.


> config.yaml (developermail.io)

```yaml
# We registered bob@developermail.io
developermail.io:
  bob:
    sieve: sieve/default.sieve
    aliases: []
    forwards: []
```

Or like this, if you chose to signup for a @developermail.io mailbox.


## Aliases

> Create and delete aliases

```yaml
aliases:
  # Add alias1@domain.tld and alias2@domain.tld
  # as aliases for the mailbox
  - alias1
  - alias2
```

You are able to create and delete aliases by simply adding and removing them
to/ from the ``aliases`` array.

Please note that there is a limit of 3 aliases per mailbox if you use our developermail.io domain.
If you use a custom domain, there is no limitation of how many aliases you can use per mailbox.


## Forwards

> Create and delete forwards

```yaml
forwards:
  - bob.smith@gmail.com
  - claudia.bechermehl@posteo.de
```

You are able to create and delete forwards by simply adding and removing them
to/ from the ``forwards`` variable.

There are no limits on forwards neither for developermail.io nor for custom domains.

Note: When using a forward, the email will not be delivered to your Developermail mailbox, but only
forwarded to the addresses specified.


## Mailboxes

> Create and delete mailboxes

```yaml
developermail.io:
  fritz:
    sieve: sieve/default.sieve
    aliases: []
  hans:
    aliases:
      - hansi
```

You are able to create and delete mailboxes by simply adding and removing them
to/ from the ``domain`` section.

Please note that your credit card will be charged automatically.


> Change your mailbox password

```shell
curl -X POST -u fritz@developermail.io "https://developermail.io/api/accounts/change-password"
```

### Change your mailbox password

Passwords are automatically generated by our system. If you want to update
the mailbox password, you need to initiate a ``curl`` request.
You will be asked for your old password. On success, a new password is generated for you.


> Change password for another mailbox using the admin account

```shell
curl -X POST -u admin@my-domain.com "https://developermail.io/api/accounts/change-password" --data '{"user": "fritz", "domain": "my-domain.com"}'
```

You can also re-generate passwords for all mailboxes under your command, using the admin login (the
first mailbox you created when registering for developermail)


## Domains

> Create and delete domains

```yaml
developermail.io:
  fritz:
    sieve: sieve/default.sieve
    aliases: []

custom-domain.com:
  frith:
    sieve: sieve/default.sieve
    aliases: []
```

You are able to create and delete domains by simply adding and removing them
to/ from the global section.

There are not limits on domains. We won't charge for domains neither.

Once you push your changes, you'll receive all information required to adapt the domains DNS
settings. If you need any help, or if you want to check whether your settings are ok, visit the
DNS settings check page ``https://developermail.io/dns-check#/your-domain.com``.

The domain will not be activated until you at least set the ``developermail-verification`` TXT
record.


## Sieve

> Your initial ``default.sieve`` will look like this:

```c
require "fileinto";
require "regex";
require "imap4flags";

# Place all spam mails in "Spam" folder
if allof (header :regex "X-DSPAM-Result" "^(Spam|Virus|Bl[ao]cklisted)$",
  not header :contains "X-DSPAM-Reclassified" "Innocent") {

  # Uncomment this if you want your spam mails to be automatically marked as read
  # setflag "\\Seen";

  fileinto "Spam";
  stop;
}
```

You can use Sieve for mail filterung rules that are applied directly on our servers.


### Sieve Examples

> File messages from certian addresses into folders

```c
require ["fileinto"];

# Automatically put all emails from Facebook and Twitter in the Social folder
if anyof (address :contains "From" "twitter.com",
          address :contains "From" "@facebookmail.com") {

    fileinto "Social";
    stop;
}
```

Developermail has full sieve support. Refer to the [RFCs](http://sieve.info/documents) for detailed
information, or adapt one of our examples!

Share your sieve configurations with other Developermail users (e.g. by sending a pull-request on
this document on [Github](https://github.com/developermail/slate) for additional karma!


# Billing & Account

> Billing information displayed upon "git push"

```
$ git push
[...]
remote: You'll be billed $15.00 this month.
remote: If you have any questions, feel free to contact support@developermail.io!
remote:
To https://developermail.io/git/bob@example.com
   52ab6e0..d336592  master -> master
```

Upon every push, you'll receive a note of the amout you'll be billed in the upcoming month.
If there's any issues, please feel free to send an email to our [support](mailto:support@developermail.io).


## Delete account

Please contact our support team if you want to delete your account.
We're currently working on the automated process for deleting accounts.
