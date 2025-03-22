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
lastmod: 2025-03-22T13:35:14.211Z
tags:
    - Commands
    - References
---


<!--- cSpell:disable --->
* [Common Git Aliases](#common-git-aliases)
* [Git CLI Setup](#git-cli-setup)
  * [git config](#git-config)
  * [Git Credential Manager](#git-credential-manager)
* [Internet References](#internet-references)
* [Copy a single file from one branch to another](#copy-a-single-file-from-one-branch-to-another)
<!--- cSpell:enable --->

## Common Git Aliases

<https://adtc.github.io/>

## Git CLI Setup

### git config

```bash
git config --global user.name
git config --global user.email
git config --global user.name "Mona Lisa"
git config --global user.email "YOUR_EMAIL"
```

* -global applies to ~/.gitconfig
* -system applies to /etc/gitconfig
* -local applies to the current repo

Note about Github emails: <https://docs.github.com/en/account-and-profile/setting-up-and-managing-your-personal-account-on-github/managing-email-preferences/setting-your-commit-email-address>

### Git Credential Manager

Install: <https://github.com/git-ecosystem/git-credential-manager/blob/release/docs/install.md>

```bash
git credential-manager configure
git credential-manager unconfigure
git credential-manager get
```

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
