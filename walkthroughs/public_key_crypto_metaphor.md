## Metaphor: Public Key Cryptography as "Public Wand Magic"

Before we get started, walkthroughs tend to follow a format where someone who
(purportedly) already knows what's going on tells the reader step-by-step to
type some impenetrable commands to produce some result. We don't think that's
nearly educational enough for something as important as this. In order to ease
understanding, we'd like to present a metaphor here so that, even if you don't
understand the _exact_ commands, you can try to see how the steps gel into a
game plan. Then, at the very least, you can talk in terms of the metaphor with
someone and frame questions more easily (we hope!).

It's a little hard to associate cryptography (hard math with 1's and 0's inside
a computer) with physical security systems (locks, bolts, keys, etc.) made of
metal, so we're not going to even try. Let's think about magical wands from the
world of fantasy.

We know of a wand-maker called `gpg`. For many years now, `gpg` has come to
visit new encryption wizards.  He creates for you two magic wands: a "public
wand" and a "private wand." He requires your help in this process.

First `gpg` crafts the "private wand." Private wands are created by means of
the advanced knowledge of `gpg` **and** a piece of *your* magic. You have to
provide `gpg` a magical phrase or "password." This should be a [strong][]
password that's hard for a Nasty Wizard to guess. You tell it to him.

In a great flurry of magic `gpg` assembles the "private wand" components. In a
puff of mathematical magic he brings it to life and makes it obey only your
secret password.

He then asks your private wand to create a "public wand." With a flick of the
wrist,  your "private wand" summons materials and assembles a single public
wand.  The private wand then shares a little bit of its own magical secret with
the public wand in order to give the public wand magical power. Forever shall
these two wands have a special relationship between them but the "private wand"
is more powerful. They exist as a pair. We could call these a "wand-pair." To
keep things clear let's call these the "original wand-pair."

The public wand can be used to do magic that can only be un-done by the private
wand. Magic done with the private wand can only be un-done by the private wand.
We might call this "public wand magic." What's the value of this kind of magic?

Well, let's imagine a time when owls bearing messages were frequently being
captured and their messages stolen by Nasty Wizards. Anyone could read that
owl's message. Let's think about how wizards could securely send a messages.

Wizard Alice wants to send a message to Wizard Bob. Alice writes her message to
Bob, pulls out her dear, protected *private* wand and then casts the spell
"confusus maximus" and suddenly the message is unreadable. She sneds the
message by owl to Bob. Bob receives it and tries to use his private wand to
read it. It doesn't work. Bob's wand says: "The 'confusus' spell was not cast
by me on this message. I give up!" Remember: only *you* can unscramble things
magicked by your private wand, so your friend will get a message that they will
never be able to read. Likewise if Nasty Wizard Eve gets this message, she will
likewise be unable to read it. The only person who can read it is you. Not very
helpful.

Recall that a "public wand" is created with a little bit of magical knowledge
by its "private wand." We can use this relationship to have secure
communications.

Bob gives you his **public** wand, you could scramble the message using his
public wand and his **private** wand, recognizing that his brother created the
message, can use their special magical relationship to un-do the scrambling!
You meet Bob at the Bar, he gives you his public wand, you go home. You write a
special message, scramble it with his wand, send it to him, and he and only he
can read it by the magic of his private wand! If Nasty Wizard Eve gets a hold
of this message, she could not read it! Public Wand message scrambling works!

But wait, that whole part where we had to meet Bob at the bar and take his
public wand. That wasn't so great. I mean, why not *tell* him the message then?

But wait, would it hurt anything for there to be *multiple* public wands? Let's
imagine you leave a big box of copies of your public wand somewhere. Further,
these wands can only do "letter scrambling magic." People could scramble
newspapers, pictures, love letters, grocery lists and leave them laying around
scrambled. Any damage there? Not really save for a waste of time for those wand
wavers. Is there any benefit? Well, if someone later learns about you and wants
to send you a secure message, they could do so. So that's a positive.

So, in the final analysis, positive things happen by a result of making copies
of your public wand and sharing it! Realizing the advantage of this, `gpg`'s
friends have made a magical delivery service that would allows you to request
and integrate someone's public key in an instant! People who only know you by
reputation can reach out to you and be sure that their message to you is safe
and secure!

By way of comparison: what if you left your "private wand" in a public place
and someone were to make a copy of it? All those wizards who assumed that you
and only you could read their message are now **wrong**. So while we should
give away copies of our public wand as much as possible, we must guard our
private wand with great diligence.

## Complications




However, there are strategies we can use to make sure our original private wand
stays safe.  Since the private wand can be used to create new wands (it created
a public wand as its first act of existence, after all!), the secret wand of
your original wand-pair can also create "sub-wands." These are wands that
recognize your original "private wand" as being the boss.  Consequently if the
original tells them to go *poof* out of existence, *they will*. This provides
us great security: if ever those sub-wands get stolen by a Nasty Wizard, the
wands can be remotely "revoked." Thus we could ask our original wand-pair to
create a "daily use" wand pair. We could leave the original private wand at
home under our pet dragon surrounded by an army of trolls and take the daily
use wand out.


This ends our metaphor of public key cryptography as wands. In case you didn't
guess, "wand," in cryptography, is the same as "key." This is the essence of
public key cryptography.

## Public Key Cryptography

We generate a "keypair" a public key and a private key. We'll call this your
"original keypair." Messages encoded with your public key can only be decoded
with your private key (maybe a new password for your email account). Messages
encoded with your private key can only be decoded with your private key (maybe
your diary).

Your original key pair can create sub-keys which can live independent lives
*but* which can be canceled by the original parent key-pair.  Just like getting
keys to an apartment: it's wise to make copies of the keys the landlord gives
you and to keep the originals locked somewhere safe. You use the _copies_ day
to day but if ever they get lost or stolen you can generate _new_ copies. Even
better than real life is that if you lose your subkeys, you can "cancel" or
"revoke" them so they can't be used! Awesome!
