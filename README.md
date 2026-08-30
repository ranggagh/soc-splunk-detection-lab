# 🛡️ SOC Splunk Detection Lab

A hands-on cybersecurity laboratory project focused on **Security Operations Center (SOC)** monitoring, log analysis, attack simulation, and threat detection using **Splunk SIEM**.

This project demonstrates how security events are generated in a controlled lab environment, ingested as logs, analyzed using Splunk Search Processing Language (SPL), and transformed into actionable detection rules.

---

## 🎯 Project Objectives

- Learn the fundamentals of SIEM and continuous security monitoring.
- Generate realistic security events in a controlled environment.
- Collect and analyze system, network, and application logs.
- Write custom Splunk SPL queries for threat detection.
- Identify suspicious activities, anomalous behavior, and attack patterns.
- Document investigation workflows and detection mechanisms.
- Build a practical cybersecurity portfolio tailored for SOC Analyst roles.

---

## 🏗️ Lab Environment

The laboratory utilizes a virtualized environment hosted on a Windows machine.

### Main Components

| Component | Role | Description |
| :--- | :--- | :--- |
| **Windows Host** | Base Host & Management | Host machine running the Splunk instance |
| **Ubuntu Linux** | Target System | Endpoint generating security and system logs |
| **Splunk Enterprise** | SIEM Platform | Log indexing, search processing, and dashboarding |
| **Splunk Universal Forwarder** | Log Agent | Shipping local logs from Ubuntu to Splunk SIEM |
| **VirtualBox** | Virtualization | Hypervisor hosting the virtual machines |

### Data Flow

```mermaid
flowchart TD
    A[Attack / Suspicious Activity] --> B[Ubuntu Target System]
    B -->|Local Logs| C[Splunk Universal Forwarder]
    C -->|Forward Logs| D[Splunk SIEM]
    D -->|Search Processing| E[SPL Detection Queries]
    E --> F[Alerting & Investigation]
🔎 Detection Scenarios
01 — SSH Brute Force
Simulates repeated failed SSH authentication attempts against an Ubuntu Linux system.

Objective: Detect brute-force attempts and isolate the source IP associated with the suspicious authentication activity.

Data Source: /var/log/auth.log

Detection Stack: Splunk, SPL, Linux Auth Logs

📁 Scenario Path: scenarios/01-ssh-bruteforce

02 — Web Attack
Simulates reconnaissance and attack vectors against a web application to analyze HTTP server logs.

Objective: Identify abnormal HTTP requests, web scanners, and malicious request patterns.

Planned Analysis:

Suspicious HTTP methods & User-Agents

Abnormal request frequency and status codes (e.g., 40x spikes)

Attacker source IP identification

📁 Scenario Path: scenarios/02-web-attack

03 — SQL Injection (SQLi)
Simulates SQL injection exploitation attempts against a vulnerable web application.

Objective: Detect malicious SQL payloads delivered via URI parameters and application logs.

Planned Analysis:

SQL payload signature pattern matching

Detection of abnormal query syntax (UNION SELECT, ' OR 1=1)

Correlation of request anomalies with web response codes

📁 Scenario Path: scenarios/03-sql-injection

04 — Phishing Investigation
Analyzes a simulated phishing vector from an operational defensive perspective.

Objective: Understand key indicators of compromise (IOCs) tied to email-borne threats and document response steps.

Planned Analysis:

Suspicious header and sender analysis

Identification of malicious URLs and embedded links

Extraction of host and network IOCs

📁 Scenario Path: scenarios/04-phishing

🛠️ Tools & Technologies
SIEM & Analytics: Splunk Enterprise, Splunk Search Processing Language (SPL)

Log Collection: Splunk Universal Forwarder

Operating Systems: Ubuntu Linux, Windows 10/11

Virtualization: VirtualBox

Data Sources: Linux Authentication Logs (auth.log), Web Server Logs (Apache/Nginx)

🧪 Detection Methodology
Each scenario follows a standardized SOC investigation lifecycle:

Cuplikan kode
flowchart LR
    A[1. Attack Simulation] --> B[2. Log Generation]
    B --> C[3. Log Collection]
    C --> D[4. Ingestion to Splunk]
    D --> E[5. SPL Querying]
    E --> F[6. Detection Rule]
    F --> G[7. Investigation]
    G --> H[8. Documentation]
📊 Example Detection Query
Below is an example SPL query designed to identify potential SSH Brute-Force attacks by thresholding failed authentication events:

Splunk SPL
index=main sourcetype=linux_secure "Failed password"
| rex "Failed password for \S+ from (?<src_ip>\d+\.\d+\.\d+\.\d+)"
| stats count by src_ip
| where count >= 5
| sort - count
Query Explanation:

Filters for raw log events containing "Failed password" in the linux_secure sourcetype.

Extracts the source IP address (src_ip) using Regex.

Groups and counts total occurrences per source IP.

Triggers when an IP reaches 5 or more failed attempts.

📂 Project Structure
Plaintext
soc-splunk-detection-lab/
│
├── README.md
│
├── scenarios/
│   ├── 01-ssh-bruteforce/
│   │   ├── README.md
│   │   ├── queries.spl
│   │   └── screenshots/
│   ├── 02-web-attack/
│   ├── 03-sql-injection/
│   └── 04-phishing/
│
├── dashboards/
└── documentation/
📸 Evidence & Documentation
Detailed evidence, investigation notes, and step-by-step screenshots are documented inside each scenario folder.

Artifacts provided include:

Execution of attack commands/scripts

Ingested raw log events in Splunk

SPL search results and logic breakdown

Custom Splunk Dashboards

🎓 Skills Demonstrated
SIEM Management: Administering log ingestion, index configurations, and parsing.

Log Analysis: Deep understanding of Linux authentication and HTTP web logs.

Threat Detection: Writing target-oriented SPL logic for attack patterns.

Threat Hunting: Identifying malicious indicators (IOCs) within noisy datasets.

Documentation: Structuring clear SOC investigation procedures and detection guides.

🚀 Future Improvements
[ ] Map all scenario detections directly to the MITRE ATT&CK® Framework.

[ ] Build interactive multi-panel Splunk Dashboards for SOC visibility.

[ ] Implement automated real-time alerts with email/webhook triggers.

[ ] Add advanced correlation searches (e.g., successful login after multiple failures).

⚠️ Disclaimer
All simulations, logs, and attacks demonstrated within this repository were performed inside an isolated and authorized laboratory environment strictly for educational and defensive security research.

Unauthorized testing against targets without explicit permission is illegal.

👤 Author
SOC Splunk Detection Lab

A portfolio project built to showcase practical skills in SOC Analysis, Threat Detection, SIEM Engineering, and Security Incident Response.