# 🛡️ SOC Splunk Detection Lab

> A hands-on cybersecurity laboratory focused on **Security Operations Center (SOC)** monitoring, log analysis, attack simulation, and threat detection using **Splunk SIEM**.

This project demonstrates how security events can be generated in a controlled laboratory environment, collected as logs, forwarded to a SIEM platform, analyzed using **Splunk Search Processing Language (SPL)**, and transformed into practical security detection scenarios.

The goal of this project is to simulate a simplified **SOC monitoring workflow** and build practical skills relevant to a **Junior SOC Analyst / Cybersecurity Analyst** role.

---

## 🎯 Project Objectives

This laboratory was created to practice and demonstrate the following cybersecurity skills:

* Understand the fundamentals of **SIEM and security monitoring**
* Generate security events in a controlled environment
* Collect system and application logs
* Configure **Splunk Universal Forwarder**
* Forward logs from Ubuntu to Splunk
* Analyze security events using **Splunk SPL**
* Detect suspicious activities and attack patterns
* Investigate security events using log data
* Create repeatable detection queries
* Document attack simulations and investigation results
* Build a practical cybersecurity portfolio focused on **SOC Analyst skills**

---

## 🏗️ Lab Architecture

The laboratory uses a virtualized environment where **Windows acts as the host and Splunk environment**, while **Ubuntu is used as the target system**.

### 🔹 Lab Components

| Component                         | Role                                    |
| --------------------------------- | --------------------------------------- |
| 🪟 **Windows**                    | Host machine and Splunk environment     |
| 🐧 **Ubuntu Linux**               | Target system                           |
| 🔎 **Splunk SIEM**                | Log collection, analysis, and detection |
| 📡 **Splunk Universal Forwarder** | Log collection and forwarding           |
| 📦 **VirtualBox**                 | Virtualization platform                 |

---

## 🔄 Data Flow

The overall detection workflow used in this project:

```text
┌──────────────────────────┐
│  Attack / Suspicious     │
│       Activity           │
└────────────┬─────────────┘
             │
             ▼
┌──────────────────────────┐
│     Ubuntu Target        │
│      System / Web        │
└────────────┬─────────────┘
             │
             ▼
┌──────────────────────────┐
│        System /          │
│    Application Logs      │
└────────────┬─────────────┘
             │
             ▼
┌──────────────────────────┐
│ Splunk Universal         │
│       Forwarder          │
└────────────┬─────────────┘
             │
             ▼
┌──────────────────────────┐
│       Splunk SIEM        │
│   Log Search & Analysis  │
└────────────┬─────────────┘
             │
             ▼
┌──────────────────────────┐
│       SPL Detection      │
│         Queries          │
└────────────┬─────────────┘
             │
             ▼
┌──────────────────────────┐
│ Detection / Investigation │
│       & Analysis         │
└──────────────────────────┘
```

---

## 🧪 Detection Scenarios

The laboratory is organized into several attack and detection scenarios.

| #  | Scenario           | Attack / Activity                  | Log Source                   | Detection                 |
| -- | ------------------ | ---------------------------------- | ---------------------------- | ------------------------- |
| 01 | 🔐 SSH Brute Force | Repeated failed SSH authentication | `auth.log`                   | Failed login threshold    |
| 02 | 🌐 Web Attack      | Suspicious HTTP requests           | Web server logs              | Abnormal request patterns |
| 03 | 💉 SQL Injection   | Malicious SQL input                | Web server logs              | SQLi indicators           |
| 04 | 🎣 Phishing        | Suspicious email / URL activity    | Application / simulated logs | Phishing indicators       |

> ⚠️ All attack simulations are performed in a **controlled laboratory environment** for educational and defensive security purposes.

---

# 🔐 Scenario 01 — SSH Brute Force

The first detection scenario focuses on identifying repeated failed SSH authentication attempts.

### Attack Simulation

The attacker generates multiple unsuccessful SSH login attempts against the Ubuntu target.

```text
Attacker
   │
   │ Multiple failed SSH login attempts
   ▼
Ubuntu SSH Service
   │
   ▼
/var/log/auth.log
   │
   ▼
Splunk Universal Forwarder
   │
   ▼
Splunk
   │
   ▼
SPL Detection
   │
   ▼
🚨 Possible SSH Brute Force
```

### Log Source

```text
/var/log/auth.log
```

### Sourcetype

```text
linux_secure
```

### Example Detection Query

```spl
index=main sourcetype=linux_secure "Failed password"
| rex "Failed password for \S+ from (?<src_ip>\d+\.\d+\.\d+\.\d+\.\d+)"
| stats count by src_ip
| where count >= 5
```

### Detection Logic

The query:

1. Searches for failed SSH authentication events.
2. Extracts the source IP address.
3. Counts failed login attempts by source IP.
4. Flags an IP when the number of failed attempts reaches the defined threshold.

This simulates a basic SOC detection rule for identifying potential SSH brute-force activity.

---

# 🌐 Scenario 02 — Web Attack

The second scenario focuses on detecting suspicious activity against a web application.

The objective is to generate HTTP requests that represent potentially malicious behavior and analyze the resulting web server logs using Splunk.

### Detection Workflow

```text
Suspicious HTTP Request
          ↓
     Web Application
          ↓
      Web Server
          ↓
      Access Logs
          ↓
Splunk Universal Forwarder
          ↓
        Splunk
          ↓
     SPL Detection
          ↓
   🚨 Web Attack Alert
```

Detection indicators may include:

* Abnormal HTTP requests
* Suspicious URL patterns
* Repeated requests
* Unusual HTTP status codes
* Suspicious user agents
* Potential attack payloads

---

# 💉 Scenario 03 — SQL Injection

This scenario focuses on identifying potential **SQL Injection** activity through web server logs.

The laboratory simulates malicious requests containing SQL-related patterns and investigates whether these indicators can be identified using Splunk.

### Example Indicators

Potential SQL Injection indicators may include patterns such as:

```text
UNION SELECT
OR 1=1
' --
' OR '
SELECT *
```

### Detection Workflow

```text
SQL Injection Attempt
          ↓
     Web Application
          ↓
      Web Server
          ↓
      Access Logs
          ↓
        Splunk
          ↓
     SPL Detection
          ↓
   🚨 Possible SQLi
```

The objective is to demonstrate how a SOC analyst can use logs to identify potentially malicious web requests.

---

# 🎣 Scenario 04 — Phishing

The final scenario focuses on identifying indicators associated with phishing activity.

The simulation demonstrates how suspicious URLs, domains, or email-related indicators can be analyzed from available logs or simulated security events.

### Example Indicators

* Suspicious URLs
* Untrusted domains
* URL obfuscation
* Suspicious email activity
* Malicious-looking links
* Repeated access to suspicious destinations

### Detection Workflow

```text
Suspicious Email / URL
          ↓
      User Activity
          ↓
       Log Event
          ↓
        Splunk
          ↓
     SPL Detection
          ↓
   🚨 Phishing Indicator
```

---

# 🔎 Splunk Detection

Splunk is used as the central SIEM platform for this laboratory.

The detection process follows a simple SOC workflow:

```text
Collect
   ↓
Normalize
   ↓
Search
   ↓
Detect
   ↓
Investigate
   ↓
Document
```

### Example SPL Workflow

```spl
index=main
| stats count by sourcetype
```

This can be used to obtain an overview of the available log sources.

For authentication monitoring:

```spl
index=main sourcetype=linux_secure
```

For failed authentication events:

```spl
index=main sourcetype=linux_secure "Failed password"
```

For identifying repeated failed attempts:

```spl
index=main sourcetype=linux_secure "Failed password"
| rex "Failed password for \S+ from (?<src_ip>\d+\.\d+\.\d+\.\d+)"
| stats count by src_ip
| sort - count
```

---

# 📊 Investigation Process

Each scenario follows a similar investigation methodology.

### 1️⃣ Generate the Event

A controlled attack or suspicious activity is performed against the target.

### 2️⃣ Verify the Logs

The target system is checked to confirm that the activity generated the expected log entries.

### 3️⃣ Forward the Logs

The **Splunk Universal Forwarder** collects and forwards the relevant logs.

### 4️⃣ Search in Splunk

The events are searched using Splunk SPL.

### 5️⃣ Identify Indicators

Potential indicators such as:

* Source IP
* Username
* Timestamp
* Destination
* Request URI
* HTTP status code
* Authentication result

are extracted and analyzed.

### 6️⃣ Create Detection Logic

The observed behavior is converted into a repeatable SPL detection query.

### 7️⃣ Document the Investigation

Screenshots, queries, findings, and conclusions are documented for each scenario.

---

# 📁 Project Structure

```text
soc-splunk-detection-lab/
│
├── 📄 README.md
│
├── 📁 scenarios/
│   │
│   ├── 📁 01-ssh-bruteforce/
│   │   ├── 📄 README.md
│   │   ├── 📄 queries.spl
│   │   └── 📁 screenshots/
│   │
│   ├── 📁 02-web-attack/
│   │   ├── 📄 README.md
│   │   ├── 📄 queries.spl
│   │   └── 📁 screenshots/
│   │
│   ├── 📁 03-sql-injection/
│   │   ├── 📄 README.md
│   │   ├── 📄 queries.spl
│   │   └── 📁 screenshots/
│   │
│   └── 📁 04-phishing/
│       ├── 📄 README.md
│       ├── 📄 queries.spl
│       └── 📁 screenshots/
│
├── 📁 dashboards/
│
└── 📁 documentation/
```

---

# 📸 Evidence & Documentation

Each detection scenario contains screenshots documenting the investigation process.

Evidence may include:

* Attack simulation
* Ubuntu terminal
* Generated security logs
* Splunk search results
* SPL queries
* Detection results
* Investigation findings
* Splunk dashboards

The screenshots provide evidence that the detection scenarios were successfully reproduced in the laboratory.

---

# 🧰 Technologies & Tools

| Technology                    | Purpose                          |
| ----------------------------- | -------------------------------- |
| 🪟 Windows                    | Host operating system            |
| 🐧 Ubuntu                     | Target operating system          |
| 🔎 Splunk                     | SIEM and security monitoring     |
| 📡 Splunk Universal Forwarder | Log collection                   |
| 📦 VirtualBox                 | Virtual machine environment      |
| 💻 SPL                        | Security detection queries       |
| 🌐 Web Server                 | Web attack simulation            |
| 🔐 SSH                        | Authentication attack simulation |

---

# 📚 Skills Demonstrated

Through this project, the following practical cybersecurity skills are demonstrated:

### SOC & SIEM

* SIEM fundamentals
* Security monitoring
* Log analysis
* Event investigation
* Detection engineering basics
* Alert analysis

### Splunk

* SPL query development
* Log searching
* Field extraction
* Event aggregation
* Threshold-based detection
* Security event investigation

### Linux

* Linux system administration
* SSH configuration
* Authentication log analysis
* Linux log locations
* Service monitoring

### Cybersecurity

* Brute-force detection
* Web attack detection
* SQL Injection detection
* Phishing detection
* IOC identification
* Attack investigation
* Security documentation

---

# 🎓 Learning Outcome

This project provides hands-on experience with a simplified SOC workflow:

```text
        ATTACK
           │
           ▼
       LOG EVENT
           │
           ▼
     LOG COLLECTION
           │
           ▼
        SPLUNK
           │
           ▼
       DETECTION
           │
           ▼
     INVESTIGATION
           │
           ▼
      DOCUMENTATION
```

Rather than only learning cybersecurity concepts theoretically, this laboratory demonstrates how security events can be **generated, collected, detected, investigated, and documented** using a SIEM platform.

---

# ⚠️ Disclaimer

This project is intended for **educational and portfolio purposes only**.

All attack simulations are performed within a controlled laboratory environment using systems owned or authorized by the lab operator.

Do not perform these techniques against systems, applications, networks, or accounts without explicit authorization.

---

# 👤 Author

**Rangga Ganupranowo Hadad**

Computer Engineering Student
Cybersecurity & SOC Analyst Enthusiast

---

⭐ If you find this project useful, feel free to explore the individual detection scenarios and their corresponding SPL queries.
