# Authenticated vs Unauthenticated Windows Vulnerability Assessment Using Nessus

## Overview

This project compares **authenticated (credentialed)** and **unauthenticated** vulnerability scans performed with **Tenable Nessus** against Windows 7 and Windows 11 laboratory virtual machines.

The goal was to measure how access to valid Windows administrative credentials changes the visibility and number of vulnerability findings.

## Objectives

- Perform an unauthenticated Nessus assessment of Windows 7.
- Perform an authenticated Nessus assessment of Windows 7.
- Perform an unauthenticated Nessus assessment of Windows 11.
- Perform an authenticated Nessus assessment of Windows 11.
- Compare the findings from each assessment.
- Explain why credentialed scanning can reveal vulnerabilities that remote unauthenticated scanning cannot reliably identify.

## Lab Environment

| Component | Details |
|---|---|
| Vulnerability scanner | Tenable Nessus |
| Scanner OS | Ubuntu Linux |
| Windows 7 target | Virtual machine |
| Windows 11 target | Virtual machine |
| Network validation | Nmap |
| Credentialed protocol | SMB |
| Credentialed account | Dedicated `NessusScan` lab account |

> All scans in this project were performed against intentionally configured laboratory virtual machines.

## Methodology

For each Windows system, the following process was used:

1. Verify network connectivity.
2. Validate relevant Windows ports with Nmap.
3. Perform an unauthenticated Nessus scan.
4. Create/configure a dedicated administrative scanning account.
5. Configure Windows for credentialed assessment.
6. Verify SMB/administrative-share access.
7. Perform an authenticated Nessus scan.
8. Compare the results.
9. Analyze findings that became visible only after authentication.

## Results

| Operating System | Scan Type | Total Findings |
|---|---|---:|
| Windows 7 | Unauthenticated | 26 |
| Windows 7 | Authenticated | 609 |
| Windows 11 | Unauthenticated | 24 |
| Windows 11 | Authenticated | 99 |

### Key observation

The Windows 7 assessment increased from **26 findings to 609 findings** after authentication. Windows 11 increased from **24 to 99 findings**.

This demonstrates the substantially greater host-level visibility available to a credentialed vulnerability scanner.

## Severity Comparison

The severity breakdown should be added here as the individual reports are reviewed and verified. The project deliberately keeps the raw Nessus reports alongside the analysis so each conclusion can be traced back to the scan output.

## Why Authentication Matters

An unauthenticated scanner is primarily limited to information that can be obtained remotely through exposed services and network protocols.

A credentialed assessment can perform additional host-level checks, including examination of areas such as:

- Installed software
- Windows security updates and patch state
- Local users and groups
- Registry information
- Services
- Host configuration
- SMB configuration
- Other locally accessible security information

The result is not simply "a harder scan"; it is a scan with a substantially different level of visibility into the target.

## Tools Used

- Tenable Nessus
- Nmap
- SMB client (`smbclient`)
- Windows Command Prompt / PowerShell
- VirtualBox / virtualized Windows laboratory systems
- Ubuntu Linux

## Project Structure

```text
windows-nessus-auth-vs-unauth/
├── README.md
├── analysis/
├── reports/
│   ├── windows-7/
│   │   ├── authenticated/
│   │   └── unauthenticated/
│   └── windows-11/
│       ├── authenticated/
│       └── unauthenticated/
└── screenshots/
```

## Ethical Scope

This project was conducted in an isolated, authorized laboratory environment using virtual machines. The techniques and configurations documented here should only be used on systems for which the tester has explicit authorization.

## Future Work

- Add the four Nessus PDF reports.
- Add screenshots of scan configuration and results.
- Build severity-by-severity comparison charts.
- Analyze the most significant findings unique to authenticated scanning.
- Document remediation recommendations for selected vulnerabilities.
- Add a final executive summary.

