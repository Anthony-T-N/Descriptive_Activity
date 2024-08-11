Collection
- Account lockout - Account modifications - Event collection - Account logon - Process tracking
- Microsoft AppLocker - Services - Microsoft Defender - Windows Error Reporting
- https://github.com/TonyPhipps/SIEM/blob/master/Logging.md

Logger (How collection carried out)

### Network
- Networking Devices (Router/Switches/Firewalls)
```
R1# configure terminal
R1(config)# logging <Host IP Address>
R1(config)# logging trap error (Severity levels 0-7)
R1(config)# logging origin-id hostname
R1(config)# logging facility localx (Type of device identifier)
R1(config)# logging trap x.x.x.x transport tcp port x
R1(config)# logging on
```

- Intrusion detection system
  - Suricata
  - Zeek

- Intrusion prevention system
-   


- Endpoint Devices
  - Sysmon
  - Windows Event Logging
  - Nessus Scanners

### Sample

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

Business:
Consider (Workload Pricing, Entity Pricing, Ingest Pricing)

Open-sourced focused


