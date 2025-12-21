---
title: WSL Tips and Tricks
description: Trips and Tricks to help with Windows Subsystem for Linux (WSL)
published: false
categories:
    - Tech
type: pages
layout: pages
date: null
lastmod: 2025-12-21T06:23:47.055Z
tags:
    - Tools
    - Windows
    - Tips
isdraft: true
fmContentType: pages
mermaid: false
keywords:
    - Linux
    - Subsystem
    - WSL
    - Windows
---
<!--- cSpell:words -->
<!--- cSpell:ignore -->
<!--- cSpell:disable --->
* [Remove Distro (but not uninstall WSL)](#remove-distro-but-not-uninstall-wsl)
* [Multiples of the same distro](#multiples-of-the-same-distro)
<!--- cSpell:enable --->

## Remove Distro (but not uninstall WSL)

`wsl --unregister <distro name>`

Also consider uninstalling from the Microsoft Store

## Multiples of the same distro

From: <https://superuser.com/questions/1816644/can-we-have-multiple-wsl2-distros-of-the-same-type-installed-in-a-single-windows>\
Based off: <https://endjin.com/blog/2021/11/setting-up-multiple-wsl-distribution-instances>

Here is how to have several copies of the same distribution:

1. Install the base distribution from the Windows Store or using:
    `wsl --install -d <distribution name>`
2. Log into the environment and modify as needed, then exit it
3. Export the environment with the following command:
    `wsl --export <distribution name> <export file name>`
4. Create a new instance of the base environment by importing the .tar file:
    `wsl --import <new distribution name> <install location> <export file name>`
5. You may now open the new environment using:
    `wsl -d <new distribution name>`
6. In Windows 11, you can browse the file-system of distributions in Explorer via Desktop > Linux
7. The new distribution will have root as the default user. To login as another user, either use the `-u <username>` flag or create/modify a `wsl.conf` file in `/etc` directory inside the environment, with the following section:

    ```linux
    [user]
    default=<username>
    ```

<!-- cSpell:ignore toolname -->
<!--
## toolname

### toolname Commands

### toolname Notes

### toolname References

<>
-->
