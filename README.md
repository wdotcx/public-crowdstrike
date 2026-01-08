# CrowdStrike Firewall Toolkit

This repository provides a small set of scripts to migrate, analyse, and manage Windows Firewall rules at scale using CrowdStrike. It focuses on converting Group Policy exports, creating rules via the CrowdStrike API, and summarising firewall activity logs.

## Contents

- `WindowsFirewall_xml2csv.py` converts Windows Firewall Group Policy export XML to CSV.
- `API_Add-Rules.ps1` adds firewall rules via the CrowdStrike API from CSV.
- `API_WatchMode.ps1` bulk enables or disables Watch Mode on firewall rules.
- `summariseLogs.py` summarises exported CrowdStrike "Firewall activity" CSV logs.
- `compareLogs.py` compares summaries to highlight rules to add, delete, or update.

## Prerequisites

- Python 3.8+ for the `.py` scripts
- PowerShell 5.1+ or PowerShell 7+ for the `.ps1` scripts
- CrowdStrike API credentials for the API scripts

## How to use

### Convert Group Policy XML to CSV

Export your Windows Firewall Group Policy to XML, then convert it to CSV for review or further processing.

```bash
python WindowsFirewall_xml2csv.py path/to/firewall.xml > firewall.csv
```

### Add firewall rules from CSV via CrowdStrike API

Prepare a CSV of rules, then run the script with your CrowdStrike API credentials.

```powershell
.\API_Add-Rules.ps1 -ClientId <client_id> -ClientSecret <client_secret> -CsvPath .\firewall.csv
```

### Toggle Watch Mode on rules

Bulk enable or disable Watch Mode for rules in your tenant.

```powershell
.\API_WatchMode.ps1 -ClientId <client_id> -ClientSecret <client_secret> -Enable
```

### Summarise firewall activity logs

Export CrowdStrike "Firewall activity" logs to CSV and summarise inbound and outbound usage.

```bash
python summariseLogs.py path/to/firewall_activity.csv
```

### Compare summaries for rule changes

Compare two summary outputs to identify rules to add, delete, or update.

```bash
python compareLogs.py summary_old.csv summary_new.csv
```

## Notes

- CSV formats are specific to the scripts in this repository; check script headers for expected columns.
- Use a non-production tenant or a limited scope when testing API changes.
