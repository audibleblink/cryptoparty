# GPG Key Setup

## Introduction

This is one of the most important steps toward having secure communications. While other applications and hygiene are important, this one moves the reader from being a "layperson with some good security sense" to be someone with some understanding of security. While some of the steps are onerous, they're designed for your protection and will have some reasoning behind each one. Take your time and welcome to the club!

## Ingredients

* [Tails] Live USB Stick: [Tails][] (to create one anew requires **2 USB sticks**). This Tails installation will be going into a "vault" (keep at home, lock in a safe, keep in a safe-deposit box, etc.). After the following process, your USB key should be taken out of daily usage.
* Daily-use USB stick: Blank. This will be used to store _*your most important data*_. After we finish this process you'll put it in a vault, safe, safety-deposit box, post an armed guard, etc. It's going to hold something very important

## Step: Get a Tails System

_Skip this step if you already have a Tails boot stick_

The [Tails Installation Assistant][] should help you get your bootable USB stick.

## Step: Add a Persistent Volume To Your Stick

_Skip this step if your Tails boot stick already has a persistent volume **and** has enabled GnuPG_

Follow the [Tails Persistence Volume][TPV] for both "Personal Files" and "GnuPG."

You will be prompted to add a password on this volume.

# IT IS VERY IMPORTANT THAT YOU CHOOSE A STRONG PASSWORD HERE

If someone can decrypt your persistent volume, they will gain access to your master cryptographic keys. This would be **VERY BAD**. Think of it like someone getting the plans for the lock in your front door. With those plans they come into your house unnoticed. In the cryptography world they can, effectively _be_ you: spread falsehoods with your "stamp" of approval. If you have difficulty remembering strong passwords, a password manager application would be a prudent investment.

## Step: Boot Into Tails

When you see this, you'll know you're ready to go with Tails.

![Tails Greeter](keygen-walkthru-images/tails-greeter-welcome-to-tails.png)

_The "Tails Greeter"_

## Step: Log Into Tails with an Administrator Password

When reach the Tails Greeter, you have the option to configure "More Options." Say "Yes" and you will be greeted with the Tails Admin Assistant:

![Tails Admin Assistant](./keygen-walkthru-images/Tails-1-2-welcome-to-Tails.jpg)

Here set an admin password. This need not be extremely secure, we're only going to use it for this current Tails session. 

Since we set up a persistence volume in the previous step, also provide that password here.

Click the "Login" button to log into Tails.

## Step: Verify Configuration

Double-click on the desktop and select "Open Terminal."

Enter the following commands:

`cd ~/.gnupg`
`df .`
`cd ~/Persistent`
`df .`
`cd`
`df .`

These steps are used to show that `~/.gnupg` and `~/Persistent` directories are on a device called `TailsData_unlocked` while the last directory (the "home directory") is on something called `aufs` which is "Mounted on" `/`. If these line up with your system, you're on the right path.

## Step: Make the Battle Plan

Public key cryptography works by 


[Tails Installation Assistant]: https://tails.boum.org/install/index.en.html
[TPV]: https://tails.boum.org/doc/first_steps/persistence/configure/index.en.html
