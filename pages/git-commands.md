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
lastmod: 2025-08-23T05:02:53.289Z
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
  * [git user config](#git-user-config)
  * [Git Credential Stuff](#git-credential-stuff)
    * [Git Credential Storage](#git-credential-storage)
    * [Git Credential Manager](#git-credential-manager)
      * [Github Device flow](#github-device-flow)
  * [autocrlf](#autocrlf)
* [Quick Github Auth](#quick-github-auth)
* [Misc Git Tips and Tricks](#misc-git-tips-and-tricks)
  * [Copy a single file from one branch to another](#copy-a-single-file-from-one-branch-to-another)
  * [Restore/Rehydrate/Reinflate a repo with just the .git folder](#restorerehydratereinflate-a-repo-with-just-the-git-folder)
  * [Date Branch Created](#date-branch-created)
* [Special Git Repo files \& folders](#special-git-repo-files--folders)
  * [.gitignore](#gitignore)
  * [.gitattributes](#gitattributes)
  * [.gitmodules](#gitmodules)
  * [.github](#github)
* [Git fix's (most of them dangerous)](#git-fixs-most-of-them-dangerous)
  * [Force Reset Local worktree to remote](#force-reset-local-worktree-to-remote)
  * [Undoing and redoing commits](#undoing-and-redoing-commits)
* [Internet References](#internet-references)
<!--- cSpell:enable --->

## Common Git Aliases

<https://adtc.github.io/>

## Git CLI Setup

### git user config

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

### autocrlf

`git config core.autocrlf`: set up CRLF settings. Can be set per repo or globally.

In theory it should be set to automatic during install but you may need to adjust.

More Info:

* <https://stackoverflow.com/a/20653073>: awesome StackOverflow on how it works, what it matters and how to address.
* <https://git-scm.com/docs/gitattributes#_end_of_line_conversion>
* <https://git-scm.com/docs/git-config#Documentation/git-config.txt-coreautocrlf>

> [!IMPORTANT] Git with Windows
> This matters a lot work working with git on windows and linux machines. I don't know if things need to be changed from their defaults but an understanding should be sought.

You can also look into `--renormalize` Option in git. <ins>I haven't</ins>, but here is a suggested answer: <https://stackoverflow.com/questions/7156694/git-how-to-renormalize-line-endings-in-all-files-in-all-revisions>

> [!TIP] Set your Editor
> Some settings also need to be configured in your editor. Look into how you can set it. See [`files.eol` under Settings in VSCode Settings and Extensions](vscode-settings-and-extensions.md#settings)

There *may* be some value in looking up these settings:

* `core.eol`: <https://git-scm.com/docs/git-config#Documentation/git-config.txt-coreeol>
* `core.safecrlf`: <https://git-scm.com/docs/git-config#Documentation/git-config.txt-coresafecrlf>
* <https://git-scm.com/docs/gitattributes#_eol>
* <https://git-scm.com/docs/gitattributes#_end_of_line_conversion>

## Quick Github Auth

Create secure correctly scoped github personal access token here: <https://github.com/settings/personal-access-tokens>

* [ ] Add link to guide about PATs

Then type: `git clone https://<username>:<PAT>@github.com/<owner>/<repository>.git`

## Misc Git Tips and Tricks

### Copy a single file from one branch to another

From <https://betterstack.com/community/questions/how-do-i-copy-version-of-single-file-from-one-branch-another/>

```bash
git checkout target-branch
git checkout source-branch -- path/to/file
git add path/to/file
git commit -m "Copy file from source-branch to target-branch"
git push origin target-branch
```

### Restore/Rehydrate/Reinflate a repo with just the .git folder

Useful for browsing/using etckeeper backups or when something goes wrong and you just have the .git folder.

On a machine with Git installed:

1. Create a copy folder somewhere outside of the repo, download folder, that is clean, temporary but safe
2. Copy into that new folder the .git folder. If it is named something like MyRepoName.git, rename the folder to just .git once copied
3. open up command prompt/terminal, etc to the folder created in step 1
4. Type `git init`
5. Type `git reset --hard branchname` but change branchname to master, main or whatever branch you want to get back to

### Date Branch Created

`git reflog --date=local <branchname>`

## Special Git Repo files & folders

### .gitignore

<https://git-scm.com/docs/gitignore>

### .gitattributes

* The file: <https://git-scm.com/docs/gitattributes>
* A check command: <https://git-scm.com/docs/git-check-attr>

### .gitmodules

For Git submodules.

* An overview: <https://git-scm.com/docs/gitsubmodules>
* The file: <https://git-scm.com/docs/gitmodules>
* The command: <https://git-scm.com/docs/git-submodule>
* From the git book: <https://git-scm.com/book/en/v2/Git-Tools-Submodules>

### .github

<https://stackoverflow.com/a/61301254/5435742>

copilot-instructions.md:

* [VSCode](https://docs.github.com/en/copilot/how-tos/configure-custom-instructions/add-repository-instructions?tool=vscode)
* [WebUI](https://docs.github.com/en/copilot/how-tos/configure-custom-instructions/add-repository-instructions?tool=webui)
* Other IDEs support check one of the above links for other options

TBC

## Git fix's (most of them dangerous)

### Force Reset Local worktree to remote

From: <https://stackoverflow.com/questions/2452226/master-branch-and-origin-master-have-diverged-how-to-undiverge-branches>

`git reset --hard origin/main`

### Undoing and redoing commits

> [!NOTE] Revert vs Undo
> Revert and Undo are two different things

From: <https://stackoverflow.com/questions/927358/how-do-i-undo-the-most-recent-local-commits-in-git>

```bash
$ git commit -m "Something terribly misguided" # (0: Your Accident)
$ git reset HEAD~                              # (1)
# === If you just want to undo the commit, stop here! ===
[ edit files as necessary ]                    # (2)
$ git add .                                    # (3)
$ git commit -c ORIG_HEAD                      # (4)
```

See <https://stackoverflow.com/a/927386/5435742>

You may need to `git push -f` to overwrite if you have already pushed

## Internet References

<https://www.reddit.com/r/git/comments/1htmt9k/the_top_1120_commands_you_need_to_recover_from/>\
<https://www.reddit.com/r/commandline/comments/1m95blj/hidden_git_config_gems_you_probably_arent_using/>\
[Git Gud: Setting Up a Better Git Config](https://micahkepe.com/blog/gitconfig/)\
<https://ohshitgit.com/>
