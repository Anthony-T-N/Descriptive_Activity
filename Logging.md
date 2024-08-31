## Collection
- Account lockout - Account modifications - Event collection - Account logon - Process tracking
- Microsoft AppLocker - Services - Microsoft Defender - Windows Error Reporting
- https://github.com/TonyPhipps/SIEM/blob/master/Logging.md

## Logger (How collection carried out)

### Logging Sources

- Networking Infrastructure (Router/Switches/Firewalls)
  - Sample configuration
  ```
  R1# configure terminal
  R1(config)# logging <Host IP Address>
  R1(config)# logging trap error (Severity levels 0-7)
  R1(config)# logging origin-id hostname
  R1(config)# logging facility localx (Type of device identifier)
  R1(config)# logging trap x.x.x.x transport tcp port x
  R1(config)# logging on
  ```

- Endpoint Devices & Application Logs (Windows/Linux Endpoints)
  - Sysmon (Windows)
  - Auditd (Linux)
  - Windows Event Logging
  - Nessus Scanners
  - Application Logging

- Security Controls
  - Intrusion detection system
    - Suricata
    ```
    sudo nano /etc/suricata/suricata.yaml
    alert http any any -> any any (http_response_line; content:"403 Forbidden"; sid:1;)
    ```
    - Zeek
      
  - Intrusion prevention system
    - Suricata

### Log Types

| # | Splunk | ncsc | owasp |
| - | ----------- | ----------- | ----------- |
| 1 | Application logs       | Application | Client software |
| 2 | System logs        | | |
| 3 | Security logs        | | NIDS and HIDS |
| 4 | Network log data        | Network  | |
| 5 | Audit logs        | | |
| 6 | Database log data        | | Database applications |
| 7 | Text        | Cloud  | |

Manual fowarding
-  `curl -X POST`
-  `logger -n <IP.ADDRESS> -P <PORT_NUMBER> -d "Syslog Test Messsage"`

Log Forwarding Agents (Bandwidth requirements)
- SFTP
- Winlogbeat
- NXLog
- Fluentd 
- Rsyslog
- Splunk forwarders (Heavy/Universal forwarders)
- Windows Event Forwarding (WEF)
- Stroom Agent

Centralised event logging facility
- Rsyslog (Listening)
- /etc/rsyslog.conf
- Log Protection, Log Retention

Logging Formats
- JSON (JavaScript Object Notation)
- Windows Event log
- CEF (Common Event Format)
- CLF (Common Log Format)
- ELF (Extended Log Format)
- XML (Extensible Markup Language)
- CSV (Comma-separated values)
- Syslog
  - RFC 3164
  - RFC 5424
  - RFC 6587
  - RFC 5425

Log sorting/seperation
- 

Logging Volume
- Bandwidth
- Storage
- Memory
- CPU

 
Logging Attributes
- `<PRIORITY><VERSION_NUMBER><TIMESTAMP><HOSTNAME><APPLICATION><APPLICATION_TAG><PROCESS_ID><STRUCTURED_DATA><MESSAGE>`
- Detecting irregularities in attributes ()
- ISO8601 (YYYY-MM-DDTHH:MM:SS.SSSZ) OR EPOCH Milliseconds (Detect logs published in the future)
- UTC (Clock Synchronization - NTP)

Log encryption
SSL/TLS

Business:
Consider (Workload Pricing, Entity Pricing, Ingest Pricing)

Open-sourced focused
