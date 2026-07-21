# Wazuh File Integrity Monitoring (FIM) with VirusTotal Integration

## Project Overview

This project demonstrates how to deploy Wazuh All-in-One on Ubuntu Server 24.04, configure a Linux Wazuh Agent, enable File Integrity Monitoring (FIM), and integrate VirusTotal for malware detection.

When a monitored file is created or modified, Wazuh generates a File Integrity Monitoring alert, calculates the file hash, and submits it to VirusTotal for reputation analysis. This helps security analysts quickly determine whether a file is malicious.

---

## Objectives

- Deploy Wazuh All-in-One on Ubuntu Server 24.04
- Install and register a Linux Wazuh Agent
- Configure File Integrity Monitoring (FIM)
- Monitor a custom directory for file changes
- Integrate VirusTotal using an API key
- Detect malicious files using the EICAR test file

---

## Lab Environment

| Component | Details |
|----------|---------|
| Operating System | Ubuntu Server 24.04 |
| Wazuh Deployment | All-in-One |
| Endpoint | Ubuntu Linux Agent |
| Monitoring | File Integrity Monitoring (FIM) |
| Threat Intelligence | VirusTotal |
| Test File | EICAR |

---
## Project Workflow

1. Deploy Wazuh All-in-One.
2. Access the Wazuh Dashboard.
3. Install and register the Linux Wazuh Agent.
4. Configure File Integrity Monitoring.
5. Monitor the `/tmp/malware` directory.
6. Integrate VirusTotal using an API key.
7. Create the EICAR test file.
8. Verify malware detection in the Wazuh Dashboard.

---

## File Integrity Monitoring Configuration

Configure the Linux agent to monitor the malware testing directory.

```xml
<agent_config os="Linux">
  <syscheck>
    <directories realtime="yes" check_all="yes">/tmp/malware</directories>
  </syscheck>
</agent_config>
```

Restart the agent:

```bash
sudo systemctl restart wazuh-agent
```
---
## VirusTotal Integration

Add the following configuration to the Wazuh Manager.

```xml
<integration>
  <name>virustotal</name>
  <api_key>YOUR_VIRUSTOTAL_API_KEY</api_key>
  <group>syscheck</group>
  <alert_format>json</alert_format>
</integration>
```

Restart the manager:

```bash
sudo systemctl restart wazuh-manager
```
---
## Testing

- Download the EICAR test file into the monitored directory.
- Wazuh generates a File Integrity Monitoring alert.
- The file hash is sent to VirusTotal.
- Detection results are displayed in the Wazuh Dashboard.

---

## Technologies Used

- Wazuh
- Ubuntu Server 24.04
- File Integrity Monitoring (FIM)
- VirusTotal API
- Linux
- XML Configuration

---

## Author

Akanksha
