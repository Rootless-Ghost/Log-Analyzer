<div align="center">
  
# 📁 Log Analyzer


A Python-based security log analysis tool designed for SOC analysts. Parses log files, detects suspicious activity, and generates actionable reports.

![Python](https://img.shields.io/badge/Python-3.9+-blue?logo=python)
![License](https://img.shields.io/badge/License-MIT-yellow)

</div>

> **Scope:** This tool is retained as the log-analysis and detection stage used by [IR-Chain](https://github.com/Rootless-Ghost/Nebula-Forge/tree/main/ir-chain). [LogNorm](https://github.com/Rootless-Ghost/LogNorm) supersedes it for log normalization, and [SigmaForge](https://github.com/Rootless-Ghost/SigmaForge) supersedes it for detection-rule authoring — but neither LogNorm nor SigmaForge executes detections against an event stream, so this tool remains in active use for that stage.

## Features


- **Log Parsing**: Supports Windows Security Event Log CSV exports only. Linux auth.log parsing was never implemented — `parse_linux_log()` is a stub that returns an empty list (see Roadmap).
- **Threat Detection**: Identifies suspicious patterns including:
  - Failed login attempts (brute force detection)
  - Logins at unusual hours
  - Privilege escalation events
  - Account lockouts
- **Reporting**: Generates clean, readable reports with severity ratings


## Demo

### Analysis Output
![Log Analyzer Demo](screenshots/log-analyzer.png)


  

## Installation

```bash
git clone https://github.com/YOUR_USERNAME/log-analyzer.git
cd log-analyzer
pip install -r requirements.txt
```

## Usage

Only `--type windows` is implemented — `--type linux` calls a stub (`parse_linux_log()`) that silently returns zero events.

```bash
# Analyze a Windows Security Event Log (CSV export)
python src/log_analyzer.py --input samples/security_log.csv --type windows

# Generate HTML report
python src/log_analyzer.py --input samples/security_log.csv --type windows --report html
```

## Project Structure

```
log-analyzer/
├── src/
│   ├── log_analyzer.py      # Main script
│   ├── parsers/             # Log parsing modules
│   ├── detectors/           # Detection rule modules
│   └── reporters/           # Report generation
├── samples/                 # Sample log files for testing
├── output/                  # Generated reports
├── tests/                   # Unit tests
├── config.yaml              # Configuration file
├── requirements.txt
└── README.md
```

## Detection Rules

| Rule | Description | Severity |
|------|-------------|----------|
| Brute Force | 5+ failed logins within 5 minutes from same source | High |
| Off-Hours Login | Successful login between 12am-5am | Medium |
| Privilege Escalation | User added to admin/privileged group | High |
| Account Lockout | Account lockout event detected | Medium |

## Roadmap

- [x] Project setup
- [x] Windows Event Log parser (CSV)
- [x] Basic detection rules
- [x] Terminal output
- [x] HTML report generation
- [ ] Linux auth.log parser
- [ ] IP reputation lookup (VirusTotal/AbuseIPDB)
- [ ] Custom detection rules via config

## License

This project is licensed under the MIT License — see the [LICENSE](LICENSE) file for details.


<div align="center">

Built by [Rootless-Ghost](https://github.com/Rootless-Ghost) 

</div>
