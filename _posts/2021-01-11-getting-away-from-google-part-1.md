---
layout: post
title: "Getting Away from Google (Part 1: Passwords)"
tags:
    - computing
    - google
    - english
    - bitwarden
published: true
category: Computing
permalink: /:year/:month/:day/:title:output_ext
---


A few months ago, I decided to reduce my usage of Google services and to take back control of my digital life, or at least a part of it.

The first part of this adventure was to replace Chromium/Chrome by Firefox, and at the same time, replace Chrome's Saved Password and KeepassX with a more modern solution.

## My history with Google

I've been a "Google Addict" for a long time now.

I've had a Google Account for more than ten years, even before I got my fist smartphone. I've been a proud Android user since I got my first phone, and I've become more entangled with Google services year after year. My GMail address is my main email address. I store a lot of files on my Google Drive account. I enjoy having all my Photos in my Google Account, easy to reach from any web browser. I replaced my office suite with Google Docs. I ditched Firefox for Chromium...

And one day in the middle of august, all of a sudden, I decided to rethink the way I work online.

If Google's services will, inevitably, remain essential in my day to day life, I want to think about the alternatives that exist and, when they are good enough for me, switch to them.

## The need for a new password manager

About 10 years ago, when I started really using "the Internet" and was still a child, I did the very bad thing everyone does: I used the same password everywhere.

As I grew up, both IRL and in my understanding of the networks and of its threats, I changed this model and started using random passwords for all my accounts. To store these passwords, I used KeepassX and its variants.

KeepassX is a software running on my machine, separated from my browser. It keeps a password database and encrypts it with a passphrase (or a key file). It works quite well but has two major drawbacks:

- Browser integration doesn't work well. Maybe it works better now, but multiple different solutions were provided by the software to enable seamless integration in the browser, and none of them was as seamless as I wished it was. The "CTRL+MAJ+V" shortcut to quickly invoke KeepassX therefore became my best friend.
- It's entirely offline, and doesn't support any kind of synchronization among various devices. During a long time, I would simply email myself the databse everytime I changed it, but it quickly became unmanageable as the database on my phone diverged from the one on my laptop.

At the same time, Google hugely improved the way saved passwords are integrated into Android. When registering on a website, Chrome now directly suggested a new random password and saved it directly into my Google account. When opening new accounts, just letting Google pick a password and remember it was way easier than opening Keepass, creating a new entry, generating a password, copying it, going back to the app, completing registration. And so I ended up using Chrome's saved passwords more and more.

If I wanted to get away from Chrome, my first mission would therefore be to find a new password manager.

This password manager needed to have four important features:

- Good browser integration: I want it to work almost as well as the included "Remember my password" feature.
- Synchronization between devices
- Self-hosting: if I don't trust Google with my passwords, I won't trust an anonymous company I never heard of with them either.
- Open source software: for the same reason as before

## The solution: Bitwarden

After some research, I decided Bitwarden would work well for my situation. I decided to host it myself and not to use the cloud version.

BitWarden has two components: a server, that I hosted on some machine I rent somewhere, and a client, that exists both as a browser plugin and as a standalone app for Windows/Linux/Android (probably other platforms as well).

It also supports two factor authentication, including using U2F tokens.

I therefore did the following:
 
1. Started BitWarden on my server using a docker image (I use [bitwarden_rs](https://github.com/dani-garcia/bitwarden_rs), an unofficial implementation of the server)
2. Set up NGINX proxying and make it accessible from one domain I own
3. Created a new email address with a very strong random password and TFA
    + The password for this email was stored into a new empty KeePass database, with very strong encryption.
    + The TFA secret key was stored into another empty KeePass database with very strong encryption
4. Picked a new strong password I could remember for the new Bitwarden database I created
5. Imported all my Chrome and KeePass passwords into this brand new database
6. Configured the apps on all my devices
7. Cleared all the passwords out of my Google account

And voilà! I indeed changed my most important passwords (social media, email accounts...) "just-in-case" - because an old lost KeePass database could resurface at some point.

I then set-up a backup script for the BitWarden database. It saves the database and sends it to me via email. It also uploads it to a backup storage that comes with my server. This way, if my server dies, I'll have backups that I can restore.

I also sent myself an email (and made a backup of that email) containing the nginx and bitwarden configuration for my domain, to make sure I could recover in case of problem.

## The next steps

Liberated from Chrome's saved passwords, I could now install Firefox and some privacy-enhancing plugins (mainly Privacy Badger). I also switched to StartPage as my main search engine for some time.

Because of performance issues, I switched back to Chromium on my linux laptop, but turned off all synchronization features. However, Firefox remains my default browser on my desktop PC and android phone.