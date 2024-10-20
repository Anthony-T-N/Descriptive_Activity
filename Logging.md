## Collection
- Account lockout - Account modifications - Event collection - Account logon - Process tracking
- Microsoft AppLocker - Services - Microsoft Defender - Windows Error Reporting
- https://github.com/TonyPhipps/SIEM/blob/master/Logging.md

## Logger (How collection is carried out)

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
    - Detailed logging than WEL: Hash collection, network connection details.
    - "Not hardened against an attacker with admin rights"
  ```
  Install: sysmon64 -i
  Update configuration: sysmon64 -c [<configfile>]
  Print schema: sysmon64 -s
  ```
  - Auditd (Linux)
  - Windows Event Logging
  - Nessus Scanners
  - Application Logging
  - Nagios

```
Endpoint Agent Deployment (Ansible)
- name: Install Sysmon (Windows)
  win_package:
    path: C:\agent.exe
    arguments: /install
    state: present
 - name: Install Auditd (Linux)
      apt:
        name: audit
        state: latest
```

- Security Controls
  - Intrusion detection system (IDS)
    - Suricata (NIDS)
    ```
    sudo nano /etc/suricata/suricata.yaml
    alert http any any -> any any (http_response_line; content:"403 Forbidden"; sid:1;)
    ```
    - Wazuh agent (HIDS)
    - Snort
    - Sagan
    - Cisco Firepower
    - McAfee Network Security Platform
    - Zeek
      
  - Intrusion prevention system (IPS)
    - Suricata
    - Snort
    - Check Point IPS
    - Palo Alto Networks Next-Generation Firewall (NGFW)

### Log Types

| # | Splunk | ncsc | owasp |
| - | ----------- | ----------- | ----------- |
| 1 | Application logs  | Application | Client software |
| 2 | System logs       | Host | |
| 3 | Security logs     | | NIDS, HIDS, Firewalls |
| 4 | Network log data  | Network | |
| 5 | Audit logs        | Authentication and access | |
| 6 | Database log data | | Database applications |
| 7 | Text              | Cloud  | |

- https://docs.zeek.org/en/master/logs/index.html
- https://docs.splunk.com/Documentation/ES/7.3.2/Install/Datamodels

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
  - RFC 3164 (BSD Syslog)
  - RFC 5424 (Syslog Protocol)
  - RFC 6587 (Transport of Syslog Messages over TCP)
  - RFC 5425 (Transport of Syslog Messages over TLS)

Basic Fowarding/Collection Checks
- Test connectivity with remote server.
```
$ curl -X POST
$ logger -n <IP.ADDRESS> -P <PORT_NUMBER> -d "Syslog Test Messsage"
```

```
$ nc -v <IP.ADDRESS> <PORT_NUMBER>
```

```
$ sftp -i <KEY_FILE> user@<IP_ADDRESS>
get -R .
```

```
$ nslookup <DOMAIN_NANE>
```

```
$ sudo tcpdump -i eth0 tcp
```

Wireshark

Log sorting/seperation
- Regex different standards
- Source enviroment tagging
- Parsing of format

Logging Volume
- Work out maximum value 
  - Networking (Bandwidth vs. Throughput)
    - ```
      # On server (Listening for connections
      iperf -s
      # On client (Connect to server)
      iperf -c <server_ip_address>
      ``` 
  - Storage (Log placement)
    - `df -h`
  - Memory (Processing)
    - `free -gt`
  - CPU (Processing)

## Logging Validation & Forma Ingestion (Collected Logs, Now What?)

```
Error occurred at 2023-10-10 14:32:45 message userID: 12345
```

Consistent Structure
- Detecting irregularities in attributes
```
Logging Attributes
- `<PRIORITY><VERSION_NUMBER><TIMESTAMP><HOSTNAME><APPLICATION><APPLICATION_TAG><PROCESS_ID><STRUCTURED_DATA><MESSAGE>`
```
Field Types

- Correct source environment
Timestamp Format:
```
- ISO8601 (YYYY-MM-DDTHH:MM:SS.SSSZ) OR EPOCH Milliseconds
  - Detect logs published in the future
  - Missing sections
  - UTC (Clock Synchronization - NTP)
```
- Missing fields (Adhere to schema)

Log Level Validation

Message Content

Special Characters and Encoding Validation

Length Validation


Syslog Validation
Schema Validation

## SIEM Data Ingestion
Platforms + Methods + Final Format:
- Microsoft Sentinel
  - Logs ingestion API, Data collection transformation
- Google Security Operations SIEM
  - Forwarders
  - Ingestion APIs
  - Google Cloud
  - Data feeds
- Splunk ES
  - HEC JSON

Logging Overview Validation
- Sort by enviroment/group by sourcetype
- Percentage of sourcetype/type of log from enviroment.
- Determine logs of forensic value
- Ingestion size/processing

Log encryption
SSL/TLS
Certs

Business:
Consider (Workload Pricing, Entity Pricing, Ingest Pricing)

Open-sourced focused

TCP/IP Model
3-way handhake (TCP)
