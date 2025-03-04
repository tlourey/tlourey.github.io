---
title: Azure VM Tips
description: Tips for setting up Azure VM's
published: true
categories:
    - Tech
type: pages
layout: pages
draft: true
date: 2025-01-15T14:05:00
lastmod: 2025-03-04T06:18:25.025Z
tags:
    - Azure
    - Tips
---


<!--- cSpell:disable --->
* [Access Methods](#access-methods)
* [Resetting VM Passwords](#resetting-vm-passwords)
* [Updating or Adding SSH Keys](#updating-or-adding-ssh-keys)
* [DNS Settings](#dns-settings)
* [Multiple IP Addresses on Azure vms](#multiple-ip-addresses-on-azure-vms)
* [Static Mac Address on Nic in Azure](#static-mac-address-on-nic-in-azure)
  * [First Time Setup](#first-time-setup)
  * [Using on 2nd machine](#using-on-2nd-machine)
<!--- cSpell:enable --->

## Access Methods

[Azure PowerShell](https://learn.microsoft.com/en-au/powershell/azure/)\
[Azure CLI](https://learn.microsoft.com/en-au/cli/azure/)\
[Azure CloudShell](https://learn.microsoft.com/en-us/azure/cloud-shell/overview) - Direct access links:

* <https://shell.azure.com/>
* <https://portal.azure.com>

## Resetting VM Passwords

<https://learn.microsoft.com/en-us/troubleshoot/azure/virtual-machines/windows/reset-rdp#reset-the-local-administrator-account-password> - Reset Password using Azure Portal\
<https://learn.microsoft.com/en-us/troubleshoot/azure/virtual-machines/windows/reset-rdp#reset-the-local-administrator-account-password-1> - Reset Password using Azure PowerShell\
<https://learn.microsoft.com/en-us/troubleshoot/azure/virtual-machines/linux/reset-password> - Reset Linux Password using Azure CLI or Azure Cloudshell

## Updating or Adding SSH Keys

<https://learn.microsoft.com/en-us/troubleshoot/azure/virtual-machines/linux/troubleshoot-ssh-connection#use-the-azure-portal> - reset or change an existing SSH key\
<https://learn.microsoft.com/en-us/azure/virtual-machines/extensions/vmaccess-linux#update-ssh-key> - setup a ssh key

## DNS Settings

Set DNS Servers via Azure Nic interface
Refresh on system via `sudo netplan try`

Set DNS Domain via Netplan on box: (<https://learn.microsoft.com/en-us/troubleshoot/azure/virtual-machines/linux/custom-dns-configuration-for-azure-linux-vms?tabs=Ubuntu>)

Don't worry too much about reddog: (<https://learn.microsoft.com/en-us/azure/virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances?tabs=ubuntu>)

## Multiple IP Addresses on Azure vms

<https://learn.microsoft.com/en-au/azure/virtual-network/ip-services/virtual-network-multiple-ip-addresses-portal>

## Static Mac Address on Nic in Azure

Must be on 2nd non-primary Nic

[Understanding static MAC address licensing in Azure](https://techcommunity.microsoft.com/blog/itopstalkblog/understanding-static-mac-address-licensing-in-azure/1386187)

### First Time Setup

1. Add a 2nd Nic that isn't the primary nic to your VM
2. Connect it up
3. Document MAC Address
4. Disable your first nic.
5. Apply preferred IP Address to 2nd nic
6. Put an azure resource lock on 2nd nic but not end of world if it gets deleted.

### Using on 2nd machine

1. Add a 2nd Nic that isn't the primary nic to your VM
2. Connect it up
3. Document MAC Address
4. Disable your first nic.
5. Apply preferred IP Address to 2nd nic
6. Put an azure resource lock on 2nd nic but not end of world if it gets deleted.
7. Go to devicemanager and hard code the mac address you want on the 2nd nic

Or something like `Set-NetAdapterAdvancedProperty -Name 'Private Team' -DisplayName 'MAC Address' -DisplayValue '00-00-00-00-00-00'`
