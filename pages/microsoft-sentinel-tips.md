---
title: Microsoft Sentinel Tips
description: ""
published: false
categories:
  - Tech
type: pages
layout: pages
draft: true
tags:
  - Azure
  - Azure_Log_Analytics
  - Azure_Sentinel
  - Security
fmContentType: pages
lastmod: 2025-01-31T07:13:39.921Z
date: 2025-01-27T06:07:50.792Z
---

<!--- cSpell:disable --->
* [New Deployments](#new-deployments)
* [SysLog connector testing](#syslog-connector-testing)
* [Misc Sites](#misc-sites)
<!--- cSpell:enable --->

## New Deployments

<https://www.devjev.nl/posts/2024/you-had-me-at-bicep-deploying-microsoft-sentinel-made-easy/>

## SysLog connector testing

Verify that logs messages from your linux machine or security devices and appliances are ingested into Microsoft Sentinel.

1. To validate that the syslog daemon is running on the UDP port and that the AMA is listening, run this command:

    ```bash
    netstat -lnptv
    ```

    You should see the `rsyslog` or `syslog-ng` daemon listening on port 514.

1. To capture messages sent from a logger or a connected device, run this command in the background:

    ```bash
    tcpdump -i any port 514 -A -vv &
    ```

<!-- markdownlint-disable MD033-->
1. After you complete the validation, we recommend that you stop the `tcpdump`: Type `fg` and then select <kbd>Ctrl</kbd>+<kbd>C</kbd>.
<!-- markdownlint-enable MD033-->
1. To send demo messages, complete of the following steps:
    * Use the netcat utility. In this example, the utility reads data posted through the `echo` command with the newline switch turned off. The utility then writes the data to UDP port `514` on the localhost with no timeout. To execute the netcat utility, you might need to install another package.

        ```bash
        echo -n "<164>CEF:0|Mock-test|MOCK|common=event-format-test|end|TRAFFIC|1|rt=$common=event-formatted-receive_time" | nc -u -w0 localhost 514
        ```

    * Use the logger. This example writes the message to the `local 4` facility, at severity level `Warning`, to port `514`, on the local host, in the CEF RFC format. The `-t` and `--rfc3164` flags are used to comply with the expected RFC format.

        ```bash
        logger -p local4.warn -P 514 -n 127.0.0.1 --rfc3164 -t CEF "0|Mock-test|MOCK|common=event-format-test|end|TRAFFIC|1|rt=$common=event-formatted-receive_time"
        ```

1. To verify that the connector is installed correctly, run the troubleshooting script with one of these commands:

    * For CEF logs, run:

        ```python
         sudo wget -O Sentinel_AMA_troubleshoot.py https://raw.githubusercontent.com/Azure/Azure-Sentinel/master/DataConnectors/Syslog/Sentinel_AMA_troubleshoot.py&&sudo python Sentinel_AMA_troubleshoot.py --cef
        ```

    * For Cisco Adaptive Security Appliance (ASA) logs, run:

        ```python
        sudo wget -O Sentinel_AMA_troubleshoot.py https://raw.githubusercontent.com/Azure/Azure-Sentinel/master/DataConnectors/Syslog/Sentinel_AMA_troubleshoot.py&&sudo python Sentinel_AMA_troubleshoot.py --asa
        ```

    * For Cisco Firepower Threat Defense (FTD) logs, run:

        ```python
        sudo wget -O Sentinel_AMA_troubleshoot.py https://raw.githubusercontent.com/Azure/Azure-Sentinel/master/DataConnectors/Syslog/Sentinel_AMA_troubleshoot.py&&sudo python Sentinel_AMA_troubleshoot.py --ftd
        ```

## Misc Sites

<https://cyberdom.blog/category/microsoft-sentinel/> - found this while hunting for memes for this page. Looks good, may have to start reading.
