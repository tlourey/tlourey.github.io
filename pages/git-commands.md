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
lastmod: 2025-03-12T00:58:04.793Z
tags:
    - Commands
    - References
---


<!--- cSpell:disable --->
* [Common Git Aliases](#common-git-aliases)
* [Internet References](#internet-references)
* [Copy a single file from one branch to another](#copy-a-single-file-from-one-branch-to-another)
<!--- cSpell:enable --->

## Common Git Aliases

<https://adtc.github.io/>

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
