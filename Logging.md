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

Centralised event logging facility
- Rsyslog (Listening)

Logging Formats
- JSON
- Windows Event logs
- CEF
- CLF
- ELF
- XML
- CSV

Syslog

Business:
Consider (Workload Pricing, Entity Pricing, Ingest Pricing)


curl -X POST 
