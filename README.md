\# SOC Splunk Detection Lab



A hands-on cybersecurity laboratory project focused on \*\*Security Operations Center (SOC)\*\* monitoring, log analysis, attack simulation, and detection using \*\*Splunk SIEM\*\*.



This project demonstrates how security events can be generated in a controlled lab environment, collected as logs, analyzed using Splunk Search Processing Language (SPL), and transformed into practical detection scenarios.



\---



\## 🎯 Project Objectives



The main objectives of this project are:



\* Learn the fundamentals of SIEM and security monitoring.

\* Generate realistic security events in a controlled environment.

\* Collect and analyze system and application logs.

\* Create Splunk SPL queries for threat detection.

\* Identify suspicious activities and attack patterns.

\* Document investigation and detection processes.

\* Build a practical cybersecurity portfolio focused on SOC Analyst skills.



\---



\## 🏗️ Lab Environment



The laboratory uses a virtualized environment and a Windows host.



\### Main Components



| Component                  | Role                                |

| -------------------------- | ----------------------------------- |

| Windows                    | Host machine and Splunk environment |

| Ubuntu Linux               | Target system                       |

| Splunk                     | SIEM and log analysis               |

| Splunk Universal Forwarder | Log collection and forwarding       |

| VirtualBox                 | Virtualization platform             |



\### Data Flow



```text

Attack / Suspicious Activity

\\\&#x20;         │

\\\&#x20;         ▼

\\\&#x20;    Ubuntu Target

\\\&#x20;         │

\\\&#x20;         │ Logs

\\\&#x20;         ▼

Splunk Universal Forwarder

\\\&#x20;         │

\\\&#x20;         │ Forward logs

\\\&#x20;         ▼

\\\&#x20;      Splunk SIEM

\\\&#x20;         │

\\\&#x20;         ▼

\\\&#x20;  SPL Detection Query

\\\&#x20;         │

\\\&#x20;         ▼

\\\&#x20;  Detection / Analysis

```



\---



\## 🔎 Detection Scenarios



The project is organized into several attack detection scenarios.



\### 01 — SSH Brute Force



Simulates repeated failed SSH authentication attempts against an Ubuntu system.



\*\*Objective:\*\*

Detect multiple failed login attempts and identify the source IP associated with suspicious authentication activity.



\*\*Data Source:\*\*



\* `/var/log/auth.log`



\*\*Detection Technology:\*\*



\* Splunk

\* SPL

\* Linux authentication logs



📁 \[`scenarios/01-ssh-bruteforce`](./scenarios/01-ssh-bruteforce)



\---



\### 02 — Web Attack



Simulates suspicious activity against a web application and analyzes HTTP/web server logs using Splunk.



\*\*Objective:\*\*

Identify abnormal HTTP requests and suspicious web attack patterns.



Planned analysis includes:



\* Suspicious HTTP requests

\* Abnormal request patterns

\* Attacker source IP identification

\* HTTP status code analysis

\* Detection using Splunk SPL



📁 \[`scenarios/02-web-attack`](./scenarios/02-web-attack)



\---



\### 03 — SQL Injection



Simulates SQL injection attempts against a vulnerable web application.



\*\*Objective:\*\*

Identify malicious SQL-related input and suspicious web requests through application/web server logs.



Planned analysis includes:



\* SQL injection payload detection

\* Suspicious URL parameters

\* Attacker source IP

\* Request frequency

\* HTTP response analysis

\* Splunk-based detection



📁 \[`scenarios/03-sql-injection`](./scenarios/03-sql-injection)



\---



\### 04 — Phishing



Analyzes a simulated phishing scenario from a defensive SOC perspective.



\*\*Objective:\*\*

Understand indicators commonly associated with phishing attacks and document the investigation process.



Planned analysis includes:



\* Suspicious sender information

\* Malicious URLs

\* Social engineering indicators

\* Email artifacts

\* IOC identification

\* Investigation workflow



📁 \[`scenarios/04-phishing`](./scenarios/04-phishing)



\---



\## 🛠️ Tools \& Technologies



\* \*\*Splunk SIEM\*\*

\* \*\*Splunk Search Processing Language (SPL)\*\*

\* \*\*Splunk Universal Forwarder\*\*

\* \*\*Ubuntu Linux\*\*

\* \*\*Windows\*\*

\* \*\*VirtualBox\*\*

\* \*\*SSH\*\*

\* \*\*Web Server Logs\*\*

\* \*\*Linux Authentication Logs\*\*



\---



\## 🧪 Detection Methodology



Each scenario follows a similar SOC investigation workflow:



```text

1\\\\. Attack Simulation

\\\&#x20;       ↓

2\\\\. Log Generation

\\\&#x20;       ↓

3\\\\. Log Collection

\\\&#x20;       ↓

4\\\\. Log Ingestion into Splunk

\\\&#x20;       ↓

5\\\\. SPL Query

\\\&#x20;       ↓

6\\\\. Detection

\\\&#x20;       ↓

7\\\\. Investigation

\\\&#x20;       ↓

8\\\\. Documentation

```



The goal is not only to generate an attack, but to demonstrate the complete process from \*\*security event → log → detection → investigation\*\*.



\---



\## 📊 Example Detection



Example SPL query for detecting repeated SSH authentication failures:



```spl

index=main sourcetype=linux\\\\\\\_secure "Failed password"

| rex "Failed password for \\\\\\\\S+ from (?<src\\\\\\\_ip>\\\\\\\\d+\\\\\\\\.\\\\\\\\d+\\\\\\\\.\\\\\\\\d+\\\\\\\\.\\\\\\\\d+)"

| stats count by src\\\\\\\_ip

| where count >= 5

| sort - count

```



This query extracts the source IP from failed SSH authentication events, counts the number of attempts, and highlights IP addresses with five or more failed attempts.



\---



\## 📂 Project Structure



```text

soc-splunk-detection-lab/

│

├── README.md

│

├── scenarios/

│   │

│   ├── 01-ssh-bruteforce/

│   │   ├── README.md

│   │   ├── queries.spl

│   │   └── screenshots/

│   │

│   ├── 02-web-attack/

│   │

│   ├── 03-sql-injection/

│   │

│   └── 04-phishing/

│

├── dashboards/

│

└── documentation/

```



\---



\## 📸 Evidence \& Documentation



Screenshots and supporting documentation are included to demonstrate the laboratory process and detection results.



Evidence may include:



\* Attack simulation

\* Generated logs

\* Splunk searches

\* Detection results

\* Source IP identification

\* Investigation findings

\* Relevant dashboards



\---



\## 🎓 Skills Demonstrated



This project demonstrates practical experience in:



\* SIEM monitoring

\* Log analysis

\* Security event investigation

\* SPL query development

\* Authentication monitoring

\* Attack detection

\* IOC identification

\* Linux security monitoring

\* Web security monitoring

\* SOC investigation workflow

\* Security documentation



\---



\## 🚀 Future Improvements



Planned improvements include:



\* Additional attack detection scenarios

\* Splunk dashboards

\* Alert configuration

\* Detection based on thresholds and time windows

\* More advanced correlation searches

\* Web attack detection

\* SQL injection detection

\* Phishing investigation

\* MITRE ATT\&CK technique mapping

\* Incident investigation reports



\---



\## ⚠️ Disclaimer



All attacks and security testing activities in this repository are performed in a \*\*controlled laboratory environment\*\* for educational and defensive cybersecurity purposes.



Do not use these techniques against systems without proper authorization.



\---



\## 👤 Project



\*\*SOC Splunk Detection Lab\*\*



Built as a practical cybersecurity portfolio project to demonstrate \*\*SOC Analyst, SIEM, log analysis, and threat detection skills\*\*.

