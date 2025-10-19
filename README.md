# 🧰 Windows PowerShell Troubleshooting Scripts
*A hands-on PowerShell toolkit that automates real-world Windows troubleshooting tasks.*

![PowerShell](https://img.shields.io/badge/Language-PowerShell-blue?style=for-the-badge)
![Platform](https://img.shields.io/badge/Platform-Windows-lightgrey?style=for-the-badge)
![Automation](https://img.shields.io/badge/Automation-Task%20Scheduler-green?style=for-the-badge)

---

## 📘 Overview
This collection of PowerShell scripts automates common IT troubleshooting and diagnostic tasks across Windows environments.  
Each script is focused, efficient, and built to generate exportable logs and reports.  

The toolkit covers:
- Network connectivity testing  
- Disk health and free-space monitoring  
- Windows service verification and restart  
- Event log error scanning  
- User profile and login issue detection  
- Windows Update auditing and compliance reporting  

All scripts were created and tested in **Windows PowerShell ISE** on Windows 10/11.

---

## ⚙️ 1. Network Connectivity Troubleshooting Script
**File:** `Network Connectivity Troubleshooting Script.ps1`  
**Purpose:** Tests adapters, gateway connectivity, and DNS resolution while logging all output to a report.

**Key Features**
- Displays adapter and IP configuration details  
- Pings gateway and Google DNS (8.8.8.8)  
- Tests domain resolution using `Resolve-DnsName`  
- Generates a detailed text log  

---

## 💾 2. Disk Space and Drive Health Check
**File:** `Disk Space and Drive Health Check.ps1`  
**Purpose:** Monitors disk usage, highlights drives below a free-space threshold (default: 15%), and exports results to CSV.

**Key Features**
- Uses `Get-WmiObject Win32_LogicalDisk`  
- Calculates disk capacity and remaining percentage  
- Highlights low-space drives  
- Exports all data to CSV for analysis  

---

## 🧠 3. Windows Service Status Troubleshooter
**File:** `Windows Service Status Troubleshooter.ps1`  
**Purpose:** Checks key Windows services and restarts them if stopped or unresponsive.

**Key Features**
- Checks service state with `Get-Service`  
- Automatically restarts essential services (`Spooler`, `BITS`, `WinRM`, `W32Time`)  
- Logs actions before and after restart  
- Supports remote execution  

---

## 🪟 4. Event Log Error Scanner
**File:** `Event Log Error Scanner.ps1`  
**Purpose:** Retrieves system error events from the last 24 hours to help identify root causes for system instability.

**Key Features**
- Filters logs using `Get-WinEvent` for Level 2 (Error)  
- Displays results in `Out-GridView` for visual review  
- Exports event time, ID, provider, and message fields  
- Ideal for daily or weekly health checks  

---

## 👤 5. User Profile or Login Issue Troubleshooter
**File:** `User Profile or Login Issue Troubleshooter.ps1`  
**Purpose:** Detects corrupted user profiles and identifies problematic registry entries that can prevent login.

**Key Features**
- Reads registry data from `HKLM:\SOFTWARE\Microsoft\Windows NT\CurrentVersion\ProfileList`  
- Checks for `.bak` profile entries and missing folder paths  
- Verifies permissions on existing profile directories  
- Exports detailed results to CSV  

---

## 🔄 6. Windows Update and Compliance Check
**File:** `Windows Update and Compliance Check.ps1`  
**Purpose:** Audits installed Windows updates, identifies failed patches, and triggers an update scan.

**Key Features**
- Uses `Get-HotFix` to list installed updates  
- Identifies failed installations (Event ID 20)  
- Executes update scans via `UsoClient StartScan`  
- Creates timestamped update logs for compliance  

---

## ⚡ Automating with Task Scheduler
All scripts can be automated with **Windows Task Scheduler**.

| Setting | Example |
|----------|----------|
| **Program/script** | `powershell.exe` |
| **Arguments** | `-ExecutionPolicy Bypass -File "C:\Scripts\DiskCheck.ps1"` |
| **Trigger** | Daily at 8:00 AM |
| **Run with highest privileges** | ✅ Yes |
| **Run whether user is logged on or not** | ✅ Yes |

Example command:
```powershell
powershell.exe -ExecutionPolicy Bypass -File "C:\Scripts\DiskCheck.ps1"
