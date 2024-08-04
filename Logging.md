Collection
- Account lockout - Account modifications - Event collection - Account logon - Process tracking
- Microsoft AppLocker - Services - Microsoft Defender - Windows Error Reporting

Logger (How collection carried out)

- Networking Devices (Router/Switches/Firewalls)
  - A
```
R1# configure terminal
R1(config)# logging <Host IP Address>
R1(config)# logging trap error (Severity levels 0-7)
R1(config)# logging origin-id hostname
R1(config)# logging facility localx (Type of device identifier)
R1(config)# logging trap x.x.x.x transport tcp port x
R1(config)# logging on
```

- Endpoint
  - Sysmon
  - Windows Event Logging
  - Nessus

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

Syslog
- RFC 3164
- RFC 5424
- RFC 6587
- RFC 5425

Business:
Consider (Workload Pricing, Entity Pricing, Ingest Pricing)

Open-sourced focused

curl -X POST 
