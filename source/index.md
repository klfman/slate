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

<aside class="notice">
Please note that Developermail is currently in BETA. Not all features are deployed yet.
You might also expect some bugs and glitches, even though we're pretty confident to provide a stable
service nontheless, as the underlying techologies are battle-proven open-source products.
</aside>

If you encounter any bugs or security issues, please contact us:
<span class="email">(sorry, you need Javascript to see this address)</span>


# Getting started

## Requirements

* Invitation code (Developermail is invite-only at the moment)
* [Git](http://git-scm.com/)
* Email client (IMAP/SMTP capable)

## Sign up

> Git username

```shell
user          # for user@developermail.io
subexamplecom # for admin@sub.example.com
```

- If you signed up using the developermail domain, your git username is the userpart of the email
- If you signed up using a custom domain, your username is the domain name without the dots (.)


> IMAP/ SMTP/ CalDAV username

```shell
user@developermail.io
admin@sub.example.com
```

Use the full email address of your mailbox.

Open [https://developermail.io/signup](https://developermail.io/signup), enter your invitation code and
create your first mailbox. You are able to create more mailboxes/ aliases later.

Make sure you note your password once your signup is complete! It won't be displayed again. This
password is used to authenticate yourself at the IMAP/ SMTP/ CalDAV services as well as for Git
configuration.

<aside class="notice">
Username for IMAP/ SMTP/ CalDAV is different than the one for cloning the git repo.
</aside>

We are starting by offering a 5 USD per mailbox per month plan.
This plan includes 5GB of storage.
Aliases for @developermail.io mailboxes are limited to three. Custom domains include unlimited free
aliases.


## Prices

Refer to our [pricing page](https://developermail.io/pricing)


## Update DNS settings

> DNS settings

```shell
MX    example.com "smtp.developermail.io."
TXT   example.com "developermail-verification=xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"
TXT   example.com "v=spf1 include:spf.developermail.io ~all"
CNAME 2015._domainkey.example.com "dkim.developermail.io"
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


## Configure your calendar and address book

### CalDAV and CardDAV Endpoint

> Endpoint

```shell
https://dav.developermail.io/username@domain.tld
```

Developermail uses the CalDAV/ CardDAV protocol to sync calendars and address books.
Use this URL for clients like

- iOS
- OS X iCal
- [Davdroid](https://play.google.com/store/apps/details?id=at.bitfire.davdroid)
- [CalDAV-Sync](https://play.google.com/store/apps/details?id=org.dmfs.caldav.lib)/
  [CardDAV-Sync](https://play.google.com/store/apps/details?id=org.dmfs.carddav.Sync)


> Endpoint for limited clients

```shell
# Default calendar
https://dav.developermail.io/username@domain.tld/calendar

# Address book
https://dav.developermail.io/username@domain.tld/addresses
```

If your client only supports a subset of the CalDAV protocol, you need
to specify the full path to your calendar in your configuration.
Use this URL for clients like

- [Thunderbird](https://mozilla.org/thunderbird)/
  [Lightning](https://addons.mozilla.org/de/thunderbird/addon/lightning/)


Use your full email address as username along your mailbox password.


# Configuration

## Setup your repository

> Clone your private developermail configuration repository

```shell
$ git clone https://developermail.io/git/bob
Cloning into 'bob'...
Username for 'https://developermail.io': bob
Password for 'https://bob': *********

remote: Counting objects: 11, done.
remote: Compressing objects: 100% (10/10), done.
remote: Total 11 (delta 2), reused 0 (delta 0)
Unpacking objects: 100% (11/11), done.
Checking connectivity... done.

$ cd bob
$ tree
.
├── config.yaml
├── settings.yaml
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
remote: If you have any questions, feel free to contact support!
remote:
To https://developermail.io/git/bob
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

<aside class="notice">
Please note that there is a limit of 3 aliases per mailbox if you use our developermail.io domain.
If you use a custom domain, there is no limitation of how many aliases you can use per mailbox.
</aside>

> Catchall aliases

```yaml
catchall.me:
  # Setup a catchall for mailbox all@catchall.me
  # All email to any address @catchall.me will be
  # delivered to to "all@catchall.me" mailbox.
  all:
     aliases: ["@"]
```

Catchalls are also supported. Using a catchall address, all email going to `*@example.com` will end
up in a certian mailbox (unless there's another mailbox/ alias configured).

<aside class="notice">
Please note that catchalls only work for custom domains.
</aside>

### Address tags

> Address tags

```
john+work@developermail.io -> john@developermail.io
```

Developermail fully supports email tags for all mailboxes.
Tags can also be used to create single-use addresses, or to filter incoming emails.
For example, if your email address is "john@developermail.io", you may use
"john+work@developermail.io" for your work emails. The emails will end up in John's inbox, and can
be filtered by sieve (see sieve section below). The tag can be chosen freely.

The address tag section on [Wikipedia](https://en.wikipedia.org/wiki/Email_address#Address_tags)
might also be informational.


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
Forwards are free of charge on custom domains.


### Forward and keep emails in mailbox

If you want to forward emails, but also keep them in your developermail mailbox, configure
forwarding using a sieve filter. See [below](/docs#sieve) for details.
This also enables IMAP and SMTP access for the forwarded mailbox, allowing you to send emails.
Please note that unlike forwards, forwards with the mailbox activated are charged as a normal
mailbox.

## Set mailbox password length

> Set password length

```yaml
company.com:
  admin:
    # Generate 35 character passwords
    # for mailbox admin@company.com
    password_length: 35
```

Developermail only uses secure, randomly generated passwords by default. It is, although, possible
to define the length of the generated passwords in case you e.g. need higher entropy.

The password length needs to be between 10 and 50 characters.

<aside class="notice">
You need to re-generate the password once you set `password_length` in your configuration (and
pushed it using `git push`). See the [change password](/docs#change-your-mailbox-password) section for details.
</aside>


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

> Confirm deletion of a mailbox

```shell
curl https://developermail.io/api/mailboxes/mailbox@domain.tld/delete/TOKEN
```

Once you removed a mailbox from your `config.yaml` and pushed the changes, you'll receive a URL
including a delete token to confirm the deletion of your mailbox.
This prevents you to accidently delete your mailbox e.g. due to a misconfiguration.
If you visit the URL in your browser or curl it, the mailbox is permanently deleted.

<aside class="notice">
Please note that your invoice will be automatically changed accordingly.
</aside>


> Change your mailbox password

```shell
curl -X POST -u fritz@developermail.io "https://developermail.io/api/mailboxes/change-password"
```

## Change your mailbox password

Passwords are automatically generated by our system. If you want to update
the mailbox password, you need to initiate a ``curl`` request.
You will be asked for your old password. On success, a new password is generated for you.


> Change password for another mailbox using the admin account

```shell
curl -X POST -u examplecom "https://developermail.io/api/mailboxes/change-password" --data '{"user": "fritz", "domain": "example.com"}'
```

You can also re-generate passwords for all mailboxes under your command, using the account login
(the login you also use to access the git repository)

If you need more entropy (longer) passwords, you can set the required length using the
`password_length` parameter in your `config.yaml`. See [this section](/docs#set-mailbox-password-length) for details.


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

    fileinto :create "Social";
    stop;
}
```

> Redirect only emails not marked as spam

```c
require "fileinto";
require "regex";

# Place all spam mails in "Spam" folder
if allof (header :regex    "X-DSPAM-Result" "^(Spam|Virus|Bl[ao]cklisted)$",
      not header :contains "X-DSPAM-Reclassified" "Innocent") {

  fileinto "Spam";
  stop;
}

# Use sieve filter to redirect messages, so spam is not forwarded
# Match all emails (unless they're spam)
if header :contains "to" "" {
  redirect "first.redirect@domain.tld";
  redirect "second.redirect@otherdomain.tld";
}
```


> Redirect mails, but also keep a copy in inbox

```c
# Match all emails
if header :contains "to" "" {
  redirect "external@domain.tld";

  # Also keep a copy in inbox, but mark as seen
  setflag "\\Seen";
  keep;
}
```

<aside class="notice">
If you want to `fileinto` another folder, make sure to create it first!
Alternatively, you can use `fileinto :create "Foldername"`.
</aside>

Developermail has full sieve support. Refer to the [RFCs](http://sieve.info/documents) for detailed
information, or adapt one of our examples!

Also find more inspiration on the [Dovecot Sieve](http://wiki.dovecot.org/LDA/Sieve) documentation
site!

Share your sieve configurations with other Developermail users (e.g. by sending a pull-request on
this document on [Github](https://github.com/developermail/slate) for additional karma!


# Account

> settings.yaml (account settings)

```yaml
# account_password_length: 10
```

All settings regarding your account are configured in the YAML file `settings.yaml`.
Analog to the mailbox configuration, you can edit the file with your favorite editor, commit and
push the changes, and they're live!


## Change your account password

Your initial password is automatically generated upon registration. If you want to generate a new
password, you can do so using a ``curl`` request. You will be asked for your old password. On
success, a new password is generated for you.

> Change account password

```shell
curl -X POST -u examplecom "https://developermail.io/api/accounts/change-password"
```

If you need more entropy (longer) passwords, you can set the required length using the
`account_password_length` parameter in your `settings.yaml`. See [this
section](/docs#set-account-password-length) for details.


## Set account password length

> Increase account password entropy

```yaml
account_password_length: 35
```

Developermail, analog to mailboxes, only uses secure, randomly generated passwords by default. It
is, although, possible to define the length of the generated passwords in case you e.g. need higher
entropy. In case you need additional security for your account, you can increase the password
entropy using the `account_password_length` field in the `settings.yaml` configuration file.

The password length needs to be between 10 and 50 characters.

<aside class="notice">
You need to re-generate the password once you set `account_password_length` in your configuration (and
pushed it using `git push`). See the [change password](/docs#change-your-account-password) section for details.
</aside>

## Billing

> Billing information displayed upon "git push"

```
$ git push
[...]
remote: You'll be billed $15.00 this month.
remote: If you have any questions, feel free to contact support
remote:
To https://developermail.io/git/bob
   52ab6e0..d336592  master -> master
```

Upon every push, you'll receive a note of the amout you'll be billed in the upcoming month.
If there's any issues, please feel free to send an email to our support:
<span class="email">(sorry, you need Javascript to see this address)</span>



## Delete account

Please contact our support
(<span class="email">sorry, you need Javascript to see this address</span>)
if you want to delete your account.
We're currently working on the automated process for deleting accounts.



<script type="text/javascript" language="javascript">
<!--
// Email obfuscator script 2.1 by Tim Williams, University of Arizona
// Random encryption key feature by Andrew Moulden, Site Engineering Ltd
// This code is freeware provided these four comment lines remain intact
// A wizard to generate this code is at http://www.jottings.com/obfuscator/
{ coded = "10RRbpd@NJeJSbRJpn9jS.jb"
  key = "1Nw3Z8uQS6MJxnBtCTUqWpIifvcF7a0GzOoHkKsdyDPLhRlj4egmX95YAEbr2V"
  shift=coded.length
  link=""
  for (i=0; i<coded.length; i++) {
    if (key.indexOf(coded.charAt(i))==-1) {
      ltr = coded.charAt(i)
      link += (ltr)
    }
    else {
      ltr = (key.indexOf(coded.charAt(i))-shift+key.length) % key.length
      link += (key.charAt(ltr))
    }
  }
$('.email').html("<a href='mailto:"+link+"'>"+link+"</a>")
}
//-->
</script>
