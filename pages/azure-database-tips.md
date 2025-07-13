---
title: Azure Database Tips
description: ""
published: false
categories:
    - Tech
type: pages
layout: pages
date: 2025-03-21T03:11:35.280Z
lastmod: 2025-05-22T04:21:48.463Z
tags:
    - Azure
    - Azure_Databases
    - PostgreSQL
isdraft: true
fmContentType: pages
mermaid: false
preview: ""
---

<!--- cSpell:disable --->
* [Azure PostgreSQL](#azure-postgresql)
  * [Provisioning with AzCLI](#provisioning-with-azcli)
  * [Extensions](#extensions)
  * [Azure AD / Entra ID Authentication](#azure-ad--entra-id-authentication)
* [SQL Server on Windows Server](#sql-server-on-windows-server)
<!--- cSpell:enable --->

## Azure PostgreSQL

### Provisioning with AzCLI

Per [--storage-size parameter for az postgres flexible-server create command in azure cli:](https://learn.microsoft.com/en-us/cli/azure/postgres/flexible-server?view=azure-cli-latest#az-postgres-flexible-server-create:~:text=values%3A%20Disabled%2C%20Enabled-,%2D%2Dstorage%2Dsize,-The%20storage%20capacity):
> The storage capacity of the server. Minimum is 32 GiB and max is 16 TiB.
>
> Default value: 128

The value is in GiB (not MiB)

### Extensions

Pre-Approved PostgreSQL extensions are available but are require whitelisting by default. They need to be allowed first in Azure. Steps are at: <https://learn.microsoft.com/en-us/azure/postgresql/extensions/how-to-allow-extensions>.

### Azure AD / Entra ID Authentication

You can configure PG Auth via Azure AD / Entra ID Authentication. Steps are at: <https://learn.microsoft.com/en-us/azure/postgresql/flexible-server/how-to-configure-sign-in-azure-ad-authentication>.

## SQL Server on Windows Server

* [ ] Add notes about extra provisioning components available via portal and/or rest API:
  * [ ] Licensing to affect billing
  * [ ] SQL VM configuration
  * [ ] SQL Server Patching
  * [ ] SQL Agent backups
