## Collection (TO-DO)
- Account lockout - Account modifications - Event collection - Account logon - Process tracking
- Microsoft AppLocker - Services - Microsoft Defender - Windows Error Reporting
- https://github.com/TonyPhipps/SIEM/blob/master/Logging.md
- https://www.cyber.gov.au/about-us/view-all-content/alerts-and-advisories/enhanced-visibility-and-hardening-guidance-communications-infrastructure

## Logger (Collection Procedures) (TO-DO)

### Logging Sources

- Networking Infrastructure (Router/Switches)

  <details>
    <summary>Infrastructure List</summary>

    ```
    - Routers
    - Switches
    - Access Points
    - Load balancers
    - DHCP Server
    - DNS Server
    - VPN Server
    - Proxy Server
    - Network taps
    - NAS (Network Attached Storage)
    ```
  </details>

  <details>
    <summary>Sample Router Logging configuration</summary>
    
    ```
    R1# configure terminal
    R1(config)# logging <Host IP Address>
    R1(config)# logging trap error (Severity levels 0-7)
    R1(config)# logging origin-id hostname
    R1(config)# logging facility localx (Type of device identifier)
    R1(config)# logging trap x.x.x.x transport tcp port x
    R1(config)# logging on
    ```
  
  </details>

- Endpoint Devices & Application Log Sources (Windows/Linux Endpoints) (TO-DO)

  | # | Endpoint Logs           | Agent  |
  |---|-------------------------|--------|
  | 1 | Operating System Logs   | Windows Event Forwarding (WEF), rsyslog, Auditd |
  | 2 | Application Logs        | Fluentd |
  | 3 | Security Software Logs  | PLACEHOLDER |
  | 4 | Network Logs            | PLACEHOLDER |
  | 5 | User Activity Logs      | PLACEHOLDER |
  | 6 | System Performance Logs | Prometheus, Zabbix, Nagios |
  | 7 | Device Management Logs  | PLACEHOLDER |
  | 8 | Hardware Logs           | PLACEHOLDER |

  Collection: 
  <details open>
      <summary>Sysmon (Windows)</summary>

      - Resource: https://learn.microsoft.com/en-us/sysinternals/downloads/sysmon
        - 30 Event IDs
        - https://www.splunk.com/en_us/blog/security/threat-hunting-sysmon-event-codes.html
      - Detailed logging than WEL: Hash collection, network connection details.
      - "Not hardened against an attacker with admin rights"
  
      ```
      Install: sysmon64 -i
      Update configuration: sysmon64 -c [<configfile>]
      Print schema: sysmon64 -s
      ```  
    </details>

  <details open>
    <summary>Auditd (Linux)</summary>
    
    <br>
    
    ```
    https://www.redhat.com/en/blog/configure-linux-auditing-auditd\
    sudo aureport -x
    ```

  </details>


  <details open>
    <summary>Windows Event Logging</summary>

    ```
    TEST AGENTS
    ```

  </details>

  <details open>
    <summary>Nessus Scanners</summary>

    ```
    Application Coverage
    ```

  </details>

  <details open>
    <summary>Prometheus</summary>

    ```
    TEST
    ```

  </details>

  <details open>
    <summary>Sample Ansible configuration</summary>
    
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
   </details>

- Security Controls
  - Intrusion detection system (IDS)
    <details>
       <summary>Suricata (NIDS)</summary>
      
      ```
      sudo nano /etc/suricata/suricata.yaml
      alert http any any -> any any (http_response_line; content:"403 Forbidden"; sid:1;)
      ```
    </details>
    
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
   
  - Identity and Access Management
    - Domain Controller
    - Active Directory
    - LDAP servers
 
  - Firewall
 
  - SIEM

### Asset Coverage (Understanding your assets)
- CMDB (Configuration management database)
- Critical assets
- Networks of interest
- Systems of interest
- Accounts of interest
- Glassbreak accounts
- Mobile phones
- Logging systems/assets
- Vlans of interest
- Person of interest
- Internet-facing devices/Entry points
- Public IP ranges vs Private IP ranges

### Log Types

| # | Splunk            | ncsc                      | owasp                 |
|---|-------------------|---------------------------|-----------------------|
| 1 | Application logs  | Application               | Client software       |
| 2 | System logs       | Host                      |                       |
| 3 | Security logs     |                           | NIDS, HIDS, Firewalls |
| 4 | Network log data  | Network                   |                       |
| 5 | Audit logs        | Authentication and access |                       |
| 6 | Database log data |                           | Database applications |
| 7 | Text              | Cloud                     |                       |

- https://docs.zeek.org/en/master/logs/index.html
- https://docs.splunk.com/Documentation/ES/7.3.2/Install/Datamodels

Log Forwarding Agents
- SFTP
- Winlogbeat
- NXLog
- Fluentd 
- Rsyslog
- Splunk forwarders (Heavy/Universal forwarders)
- Windows Event Forwarding (WEF)
- Stroom Agent

Centralised event logging facility (Cental point for logs)
- Rsyslog (Listening)
- /etc/rsyslog.conf
- Log Protection, Log Retention
- Syslog forwarding

Centralised event logging facility <-> Logging Network
Logging redundancy

Logging Formats
- JSON (JavaScript Object Notation)
- CEF (Common Event Format) `Version|Device Vendor|Device Product|Device Version|Signature ID|Name|Severity|Extension`
- CLF (Common Log Format) `[Remote host address] - [Remote log name] [Username] [Timestamp] [Request and Protocol Version] [HTTP Status Code] [Bytes Sent]`
- ELF (Extended Log Format)
- XML (Extensible Markup Language) - (Windows Event log)
- CSV (Comma-separated values)
- Syslog
  - RFC 3164 (BSD Syslog)
  - RFC 5424 (Syslog Protocol)
  - RFC 6587 (Transport of Syslog Messages over TCP)
  - RFC 5425 (Transport of Syslog Messages over TLS)

Basic Fowarding/Collection Checks
- Test connectivity with remote server.
- Test transfer with remote server
```
$ curl -X POST
$ logger -n <IP.ADDRESS> -P <PORT_NUMBER> -d "Syslog Test Messsage"

$ nc -v <IP.ADDRESS> <PORT_NUMBER>

$ sftp -i <KEY_FILE> user@<IP_ADDRESS>
get -R .

$ nslookup <DOMAIN_NANE>

$ sudo tcpdump -i eth0 tcp
```
- Wireshark

Log sorting/seperation
- Regex different standards
- Source enviroment tagging
- Parsing of different formats

Logging Volume

- (Bandwidth requirements)

- Calculating baseline and possible maximum values
  - Networking (Bandwidth vs. Throughput)
    - ```
      # On server (Listening for connections)
      iperf -s
      # On client (Connect to server)
      iperf -c <server_ip_address>
      ``` 
  - Storage (Log placement)
    - `df -h`
  - Memory (Processing)
    - `free -gt`
  - CPU (Processing)

## Logging Validation & Formal Ingestion (Collected Logs, Now What?) (TO-DO)

Bad log example:
```
Error occurred at 2023-10-10 14:32:45 message userID: 12345
```

Consistent Structure
- Detecting irregularities in attributes
```
Logging Attributes
- `<PRIORITY><VERSION_NUMBER><TIMESTAMP><HOSTNAME><APPLICATION><APPLICATION_TAG><PROCESS_ID><STRUCTURED_DATA><MESSAGE>`
```

https://www.whitehouse.gov/wp-content/uploads/2021/08/M-21-31-Improving-the-Federal-Governments-Investigative-and-Remediation-Capabilities-Related-to-Cybersecurity-Incidents.pdf
```
- Properly formatted and accurate timestamp (millisecond granularity is ideal)
- Event type (status code)
- Device identifier (MAC address or other unique identifier)
- Session/transaction ID
- Autonomous system number
- Source and destination IP (includes both IPv4 and IPv6)
- Status code
- Response time
- Additional headers (e.g. HTTP headers)
- The user ID, where appropriate
- The command executed, where appropriate
- A unique event identifier to assist with event correlation, where possible.
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
RFC 5424
- Drop irrelevant logs based on level
- Emergency
- Alert
- Critical
- Error
- Warning
- Notice
- Informational
- Debug

Message Content
- Unknown encoding
- Meaningful context

Special Characters and Encoding Validation

Length Validation
- Too long = Potential Issue

Syslog Validation
- Syslog standard check

Schema Validation

Build basic parser (POC) 
- Auditd log - Extract fields using regex.

## SIEM Data Ingestion (TO-DO)
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
- Organization sorting. Business unit

Log encryption
SSL/TLS
Certs

Business:
Consider (Workload Pricing, Entity Pricing, Ingest Pricing)

Balance Act
Security Value vs Resourcing

Open-sourced focused

TCP/IP Model
3-way handhake (TCP)
