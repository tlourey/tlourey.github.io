---
title: Git Commands
description: Commands to remember for Git
type: pages
layout: pages
categories:
    - Tech
published: true
isdraft: true
date: 2025-01-05T14:25:00
lastmod: 2025-03-23T21:13:10.557Z
tags:
    - Commands
    - References
keywords:
    - cli
    - git
    - config
---


<!--- cSpell:disable --->
* [Common Git Aliases](#common-git-aliases)
* [Git CLI Setup](#git-cli-setup)
  * [git config](#git-config)
  * [Git Credential Stuff](#git-credential-stuff)
    * [Git Credential Storage](#git-credential-storage)
    * [Git Credential Manager](#git-credential-manager)
      * [Github Device flow](#github-device-flow)
* [Internet References](#internet-references)
* [Copy a single file from one branch to another](#copy-a-single-file-from-one-branch-to-another)
<!--- cSpell:enable --->

## Common Git Aliases

<https://adtc.github.io/>

## Git CLI Setup

### git config

```bash
git config --global user.name # get current value of user.name config
git config --global user.email # get current value of user.email config
git config --global user.name "Mona Lisa" # set value of user.name config
git config --global user.email "YOUR_EMAIL" # set current value of user.email config
git config --global --list # list config
```

* `-global` applies to ~/.gitconfig
* `-system` applies to /etc/gitconfig
* `-local` applies to the current repo

Note about Github emails: <https://docs.github.com/en/account-and-profile/setting-up-and-managing-your-personal-account-on-github/managing-email-preferences/setting-your-commit-email-address>

### Git Credential Stuff

<https://git-scm.com/doc/credential-helpers> - list known helpers. In general try to use [Git Credential Manager](#git-credential-manager) for any https access to repos.

#### Git Credential Storage

<https://git-scm.com/book/en/v2/Git-Tools-Credential-Storage>

#### Git Credential Manager

Replacement (Better?) than built in [Git Credential Storage](#git-credential-storage)

Install: <https://github.com/git-ecosystem/git-credential-manager/blob/release/docs/install.md>

> [!TIP] Git for Windows
> If using windows, its usually easier to just install Git for Windows which installs GCM

CLI:

```bash
git credential-manager github # review commands for github
git credential-manager github list
git credential-manager github login # has suboptions
git credential-manager github logout <account>
git credential-manager configure # make sure GCM is set as cred manager
git credential-manager unconfigure
git credential-manager get
```

More CLI Options: <https://github.com/git-ecosystem/git-credential-manager/blob/release/docs/usage.md>\
Configuration: <https://github.com/git-ecosystem/git-credential-manager/blob/release/docs/configuration.md>\
Multiple Users: <https://github.com/git-ecosystem/git-credential-manager/blob/release/docs/multiple-users.md>

You can tell GCM to remember which user to for a specific repo:

```bash
git config --global credential.<URL>.username <USERNAME>
```

Docs Index: <https://github.com/git-ecosystem/git-credential-manager/blob/release/docs/README.md>

##### Github Device flow

Useful for when login isn't associated with default browser

1. git credential-manager github login --device --username desired username
2. Get code
3. Go to <http://github.com/login/device>
4. Enter code

## Internet References

<https://www.reddit.com/r/git/comments/1htmt9k/the_top_1120_commands_you_need_to_recover_from/>\
<https://ohshitgit.com/>

## Copy a single file from one branch to another

From <https://betterstack.com/community/questions/how-do-i-copy-version-of-single-file-from-one-branch-another/>

```bash
git checkout target-branch
git checkout source-branch -- path/to/file
git add path/to/file
git commit -m "Copy file from source-branch to target-branch"
git push origin target-branch
```
