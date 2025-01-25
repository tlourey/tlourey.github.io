---
title: Mermaid test
type: index
fmContentType: default
date: 2025-01-24T22:15:00
modifieddate: 2025-01-24T11:24:25.879Z
layout: default
---

```mermaid
graph LR;
    Device --> Rsyslog;
    API Client --> Rsyslog
    Rsyslog --> AMA --> DCE --> DCR --> LAW;
```
