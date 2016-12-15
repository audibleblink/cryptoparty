# Password Managers

## Introduction

One of the first and most effective steps you can take toward securing your
online data is to use a password manager. Generally these act as "vaults" which
store multiple login username / password pairs which can be accessed after
providing a single "master" password.

## Why?

Creating a credential at a site is a risky operation. Since many of us act as
our own personal brand emissaries these days, it's not uncommon to find people
repeating their login name in various places. Therefore hackers targeting your
account have half the data they need to access your account. Now comes the
question of password. While it's nice to create a password that's easy to
remember, it's easy for a computer to "brute force" your password. If you use a
strong password, however, it's hard for a computer to "brute force"...but it's
also hard to remember!

Humans have, historically, opted to choose the option that's easy to remember.
This, unfortunately, happens to be the one that's easy to hack with a swarm
of computers focused on brute force guessing the password.

Since users on the internet often repeat login names _and_ login passwords,
once that initial password is cracked it provides means of access to > 1 site.
So while the hacker had to work hard for that first account the rest come
easily. It will be the first username / password combination tried over and
over again.

## Scenario

Consider an old social networking site you set up as a teen.

A hacker looks at cached oldspace.com pages and sees your username (your bad
luck!). The hacker then starts trying your username plus common words in a
dictionary file: ant, aardvard, abalone, ..., zebra. Given a huge network of
compromised hosts, the hacker could have thousands of computers working 24/7 to
crack your password.

How was your password hygiene when you created that account? How many
characters were in the password? Are they all letters or a mix of numbers,
letters, and symbols?

Your account gets cracked. The hacker then searches the web for your username
and sees you used it at another social network and on a photo sharing app. He
tries that password / login that was shared across sites and...now gets 2 more
websites for the price of having hacked one. He doesn't even have to pay the
cost of running that attack army.

With each login the greater the chance that a photo or a sent mail might
contain something that makes it easier to get a higher value login. If the
hacker could get to your college email account, they might find your social
security number for that internship you applied to; or if they could find your
photo sharing site they might find your first car make and model and find a way
to reset a password based on knowing that datum, etc.

As of the day of this wriging, Yahoo announced that _1 billion_ accounts have
been compromised [source](https://yahoo.tumblr.com/post/154479236569/important-security-information-for-yahoo-users).

This is for real.

## Protection

Because of the swift cascading of this type of failure you should **make sure
that each account has a different, strong password**. A fancy way to say that
is to "limit the failure domain." Just like how submarines have strong doors to
hold back water ("localize") in the case of a leak, you can "localize" the
consequences of a hack by having your logins use complex, unique passwords.

To get around humans' tendency to forget different, strong passwords, a
password manager is a great investment. It requires you remember *one* password
in exchange for it helping you have unique, strong passwords for multiple
sites.

1Password has created [a video which describes the dangers of having too-simple a password](https://vimeo.com/88901304).

## Using A Password Manager

Install the software on your phone or your computer. These apps usually have a
synchronization feature between them so that you can provide your password in a
browser context or by looking it up on your phone. These are consumer-oriented
applications and installation is usually a snap.

A password manager + two-factor authentication (i.e. an SMS sent to your phone
when you sign in to your webmail account) increase your protection
considerably. For each account the hacker has to pay the cost in time and money
to crack the username and the login and _even then_ has to find a way to
intercept your SMS notification or your two-factor hardware. Given these
options a hacker has to have it in for you to a great degree to pay those costs
or, more likely, the hacker will move on to a softer target.
