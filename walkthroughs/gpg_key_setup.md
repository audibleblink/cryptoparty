# GPG Key Setup

## Introduction

This is one of the most important steps toward having secure communications.

While other applications and hygiene are important, this one moves you from
being a "layperson avoiding the obvious traps" to be someone with some real
_understanding_ of security.

Some of the steps are onerous, but they're designed for your protection and
we'll have some reasoning behind each one. Take your time and welcome to the
club!

## Ingredients

* 1-3 USB Sticks with 4GB or more of space

## Giving GPG a Safe Workshop

### Step: Get a Tails System

_Skip this step if you already have a Tails boot stick_

The [Tails Installation Assistant][] should help you get your bootable USB stick.

### Step: Add a Persistent Volume To Your Stick

_Skip this step if your Tails boot stick already has a persistent volume **and** has enabled GnuPG_

Follow the [Tails Persistence Volume][TPV] for both "Personal Files" and "GnuPG."

You will be prompted to add a password on this volume.

# IT IS VERY IMPORTANT THAT YOU CHOOSE A STRONG PASSWORD HERE.

This password can be one of the two listed in the Ingredients section. If someone can decrypt your persistent volume, they will gain access to your master cryptographic keys. This would be **VERY BAD**. Think of it like someone getting the plans for the lock in your front door. With those plans they come into your house unnoticed. In the cryptography world they can, effectively _be_ you: spread falsehoods with your "stamp" of approval. If you have difficulty remembering strong passwords, a password manager application would be a prudent investment.

### Step: Boot Into Tails

When you see this, you'll know you're ready to go with Tails.

![Tails Greeter](keygen-walkthru-images/tails-greeter-welcome-to-tails.png)

_The "Tails Greeter"_

### Step: Log Into Tails with an Administrator Password

When reach the Tails Greeter, you have the option to configure "More Options." Say "Yes" and you will be greeted with the Tails Admin Assistant:

![Tails Admin Assistant](./keygen-walkthru-images/Tails-1-2-welcome-to-Tails.jpg)

Here set an admin password. This need not be extremely secure, we're only going to use it for this current Tails session. 

Since we set up a persistence volume in the previous step, also provide that password here.

Click the "Login" button to log into Tails.

### Step: Verify Configuration

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

Public key cryptography works by having:

* A private key
* A public key

The essential point is that you can share your public key with all the world. In fact, you want all the world to know your public key. Your public and private keys have a (mathematical) relationship. Content encoded with your _public_ key can only be decrypted by your _private_ key. Content encrypted by your _private_ key can only be _decrypted_ by your private key.

As an example: someone you meet at a conference might take your _public_ key, encrypt a message, and send it to you. You might use your _private_ key to encrypt your list of Christmas shopping to keep prying eyes from guessing their gift.

This represents the _simplest_ case. But, unfortunately, things in the real world aren't that simple. Consider:

Suppose you have your private key on a laptop:

* What if the laptop gets stolen? The jig is up.
* What if you're sent a malware attachment in email that you open and the malware forwards on your private key?

Our strategy is this:

* Create a private key
* Create a public key
* Create a _sub-key_
* Put the _sub-key_ somewhere you can use it regularly
* Put the "master" private key somewhere safe

## Put GPG to Work

### Create the Public / Private Pair

_As a supplement, see [The GnuPG Manual](https://www.gnupg.org/gph/en/manual/c14.html)_

In the terminal type:

1. `gpg --gen-key`
2. Accept the default (1) RSA and RSA
3. For keysize choose 4096. This will make your `master` key the most complex and hard to steal possible
4. Set an expiration of `1y` (one year). Keys should have a built-in death date. If your master key is stolen or lost this is the only way to tell the public that people signing as you should stop being trusted. It's much like the expiration date an a credit card. Expiration dates, also like credit cards, can be renewed (covered elsewhere)
5. Accept these changes
6. Provide your real real name (here "Tutorial")
7. Provide a valid email address (here `tutorial@example.com`)
8. Leave comment blank
9. Select **O**kay
10. **SELECT A VERY STRONG PASSWORD** A weak password is the same as leaving your key under the mat. Make this very difficult to guess and / or store it in a password manager.
11. Re-enter it to confirm

Here we see "Tutorial" has an identity of `7EC9E024`. Henceforth in this guide use your name and key ID instead of these two bits of data.

We also must prepare for the worst. Let's suppose somehow your master key becomes compromised. You need an "anti-key" that will cancel the master key. This is called a "revocation certificate." We create it right now in the most optimistic moment and we save it in a safe place, on our Persistent volume.

Since "Tutorial" is `7EC9E024` I'll issue the following command.

`gpg --output ~/.gnupg/revoke.asc --gen-revoke 7EC9E024` Then comfirm **y** to create the certificate and accept default 1. Enter an optional description. Given that you're revoking your most-precious key, I think it's hard to come up with a good thing to put here, so I'd leave it blank. Accept with **y**. You'll be prompted for your secret key password.

Congratulations! You now have your cryptographic keys.

## Create Subkeys for Daily use

This is a rather convoluted process but it comes out like this.

1. You have a private key in a keyring
2. Generate a new sub-key on that keyring
3. Move this keyring to a safe place
4. Copy the keyring, sans the master private key to a daily use place

We follow the path defined in the [Debian Subkeys Guide](https://wiki.debian.org/Subkeys).

1. Start in the terminal
1. `cd`
1. `umask 077; tar -cf $HOME/Persistent/gnupg-backup.tar -C $HOME .gnupg`
1.  Congratulations, on your Persistent drive you have a backup of the keys `gpg` created in case something bad happens
1.  `gpg --edit-key 7EC9E024`: Remember, this is "Tutorial's" identifier. This will open the `gpg` dialog
1.  `addkey`
1.  Provide your secret key
1.  Choose "RSA (sign only)"
1.  Enter 4096
1.  Set expiry for "1y"
1.  **y** for really create
1.  `list`

_Pic here_

As you can see, the new key `963ABC84` now exists and it has `usage: S` (subkey) and it has "ultimate" trust to the original key of "Tutorial." That is, `963ABC84` knows its spawned from `7EC9E024`, the master private key. `963ABC84` will go into the world as a "representative of" the master private key but is only just that: a representative, a symbol of the authority of a thing somewhere else – rather like a diplomat. 

However, we've only created a _signing_ subkey. If we want to encrypt, we also want to create an encryption subkey. Follow the same steps as above but specify "RSA (encrypt only)."

At the `gpg>` prompt type `list` and you should see 4 keys:

* Your _master_ private key
* Your public encryption key
* Your first sub-key (for signing)
* Your first sub-key (for encrypting)

With this we finish step 2.

In step 3 we need to store this full keyring somewhere. This is simple:

`cp -r ~/.gnupg ~/Persistent/gnupg-master-Tutorial-7EC9E024`

I recommend this long informative name for easy recall. Hopefully you won't see this information often! That was it!

In our final step we need to remove the master key from the keyring.

Take a look at the key database with `gpg --list-keys`

The top key is our _master_ key and it needs to get out for the daily-use keyring.

* `gpg --output ~/Persistent/secret-subkeys --export-secret-subkeys 7EC9E024`
* `gpg --delete-secret-keys 7EC9E024` with **y** to confirm and **y** again. I know, it's scary!
* `gpg --import ~/Persistent/secret-subkeys`
* `rm ~/Persistent/secret-subkeys`

Now list your secret keys with `gpg -K`. You will see that first key `7EC9E024` now says `sec#` which means this keyring no longer has the secret key on it. By way of comparison try `gpg --homedir ~/Persistent/gnupg-master-Tutorial-7EC9E024 -K` and you'll see that the "master" directory still has the full details! The first line is `sec` versus `sec#`.

Lastly, the password on this "de-mastered" keyring is still the same as your original strong password. Apply your third (and final) password to this key with: `gpg --edit-key 7EC9E024 passwd`

At this point, on your Tails installation you have your master credentials. We now need to get your daily-use credentials on your second USB stick. Insert this USB stick into the computer. For Unix people: "We need to mount the new USB disk and copy the subkey information onto the drive."

1. Run `lsblk` this means :List Block Devices, aka Disks
2. On my system `sda` has a tree that has a bunch of Tails partitions. `sda` means device `a`. Its partitions are `sda1`, `sda2`, etc.
3. `sdb` looks similar, but seems to be the right size of the USB stick I injected. I'm going to use the first partition of this device thus `/dev/` + device `sdb` + partition `1` thus my "device name" is `/dev/sdb1`.
4. I need a "mount point" a directory on the disk that will tunnel data back to /dev/sdb1.
5. I enter the command: `sudo mount /dev/sdb1 /mnt -o umask=000`
6. This means any user can write to this "directory."
7. Copy the subkey goodies over: cp -r ~/.gnupg /mnt/gnupg`
8. `cd /mnt/gnupg`
9. `gpg --homedir . -K`: The output should show the subkey with master key removed (`sec#`).
9. `gpg --export -a  7EC9E024 > public.key`: write out a copy of your public key, other tools that sign as you will need this
9. `gpg --export-secret-key -a  7EC9E024 > private.key`: write out your public key, you'll want to share this with the world so people can contact you securely!
10. `cd && sudo umount /mnt`

## Cleanup

Let's make the default GPG directory for Tails the one that has your secret key.

1. `rm ~/.gnupg/*`
2. `cp ~/Persistent/gnupg-master-Tutorial-7EC9E024/* ~/.gnupg`
3. `gpg -K` should show that your private key is the real deal (i.e. no `sec#` but rather `sec`)

You're done. Take this Tails USB key and hide it away! Take the USB key with your subkeys and start encrypting and decryting with it. Publish that key far and wide!

## Reboot into your Standard Operating System

### Linux

* Power off Tails and put that USB key in a vault
* Power on your typical operating system (in my case, Ubuntu)
* If you have no pre-existing ~/.gnupg directory
  * Copy the contents of the sub-key USB key (in the `gnupg` directory) into ~/.gnupg
  * `cd $HOME/.gnupg`
  * `gpg -K` (`gpg` performs an upgrade)
  * See the sub-key output (`sec#`)
* If you have a pre-existing ~/.gnupg directory, you can import the key files you generated:
  * Change to the USB key directory in the terminal
  * `gpg --import public_key.gpg`
  * `gpg --import private_key.gpg`
* All set!

### Windows

* Power off Tails and put that USB key in a vault
* Power on your typical operating system
* Install [Gpg4Win][]
* Open "Kleopatra" – Installed as part of the [Gpg4Win][] install
* Click "Import Certificates"
* Browse to your USB key
* Find your `gnupg` directory
* Select your private key file
* Repeat the above for your public key file
* All set!

### OSX

OSX operates as Linux.

[Gpg4Win]: https://www.gpg4win.org/
[Tails Installation Assistant]: https://tails.boum.org/install/index.en.html
[TPV]: https://tails.boum.org/doc/first_steps/persistence/configure/index.en.html
[Tails]: https://tails.boum.org
[Tails Installation]: https://tails.boum.org/doc/index.en.html
