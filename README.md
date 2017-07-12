This is a demo password manager, once you login with your Firefox Account, it reads in your logins+passwords, and behaves like a basic standalone password manager,

It uses the Firefox Android Sync Library from here:

https://github.com/mozilla-mobile/FirefoxData-android

All of the code I added is in this directory:

[./example/src/main/java/org/mozilla/accountsexample](./example/src/main/java/org/mozilla/accountsexample)

The obvious flaw here is that instead of building cleanly on top of that library, I just mashed code on top the AccountsExample code that was already present.

There are a few reasons for this not being a 'clean' repo.
First, is that I began experimenting with a preliminary version of the FirefoxData library, modifying the sample code. 
The main repo changed significantly from the version I was experimenting with.
Second, the intent was that if it was actually being developed further, it would be refactored into a project that had a jcenter dep 
with the library.

There is no plan to use this beyond an interesting proof-of-concept.

This project has the following purposes:
- examine standalone Firefox Accounts login
- pull in logins table from Firefox Sync to a standalone app
- experiement with Android KeyStore for device secure local storage for storing a symmetric encryption key
used for encrypting/decrypting local data
- as a minor detail, experiment with app-specific passcodes, and basic copy/paste functionality for password management

Building:

Follow the build instructions from 
https://github.com/mozilla-mobile/FirefoxData-android

Essentially, open the project in Android Studio, and run the default gradle task which is to build the AccountsExample project.
I used an API level 25 simulator for most of this work, so that is the only guaranteed version.

Pattern lock view:

This uses https://github.com/aritraroy/PatternLockView, to experiment with using an in-app pattern lock without using Android's `Confirm Credential API` (that API only provides a seamless in-app flow on newer Android versions). Requiring a pattern lock or a 4-6 digit pin code to access the app seems quite common for password manager apps.

On app start you will be required to create a pattern to lock the app, the pattern is stored using the KeyStore.

There are a few pattern lock components on github, this one appears maintained and is straightforward to integrate into an app. 

