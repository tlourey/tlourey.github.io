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
    APIClient --> Rsyslog;
    Rsyslog --> AMA;
    AMA --> DCE;
    DCE --> DCR;
    DCR --> LAW;
```

```mermaid
flowchart LR
  Device --> Rsyslog;
  subgraph SysLog Server
    direction LR
    APIClient --> Rsyslog --> AMA
    DCR1[DCR] --> AMA
  end
  AMA --> DCE;
  DCE --> DCR2[DCR];
  DCR2[DCR] --> LAW;
```
