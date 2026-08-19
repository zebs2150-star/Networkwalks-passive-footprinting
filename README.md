# Networkwalks-passive-footprinting
Passive footprinting and OSINT reconnaissance with theHarvester during the NETWORKWALKS Cybersecurity Internship, Batch B082.
# OSINT Reconnaissance with theHarvester

**NETWORKWALKS Cybersecurity Internship — Week 2, Project Module 4**

Passive OSINT reconnaissance against an authorised target using **theHarvester** on Kali Linux, with single-source and multi-source enumeration, evidence collection, Linux output redirection, piping, and sanitisation of sensitive reconnaissance findings.

## Project Summary

| Item | Details |
|---|---|
| Tool | theHarvester 4.10.1 |
| Platform | Kali Linux 2026.2 |
| Technique | Passive OSINT / Footprinting |
| Target | `networkwalks.com` — internship-scoped target |
| Task 1 | Baidu — no findings returned |
| Task 2 | Multiple sources — 3 ASNs, 2 URLs, 4 IP addresses, 32 hosts |
| Evidence | Terminal output, screenshots and text files |
| Disclosure | IP addresses and discovered hosts sanitised |

## Objectives

The objectives of this module were to:

- Perform passive footprinting using theHarvester
- Compare results from a single source with multi-source reconnaissance
- Preserve terminal output as technical evidence
- Observe the effect of unavailable API-backed sources
- Review and sanitise reconnaissance findings before public disclosure

## Environment & Tools

- Kali Linux 2026.2
- theHarvester 4.10.1
- Oracle VirtualBox
- Target: `networkwalks.com`

## Methodology

### 1. Tool Familiarisation

Before beginning the reconnaissance tasks, I reviewed theHarvester's available options:

```bash
theHarvester -h
```

The main parameters used during the project were:

- `-d` — target domain
- `-l` — result limit
- `-b` — data source

![theHarvester Help and Usage](screenshots/01-theharvester-help-and-usage.png)

---

### 2. Task 1 — Baidu Footprinting

The first task queried **Baidu** with a result limit of 1000:

```bash
theHarvester -d networkwalks.com -l 1000 -b baidu
```

![Task 1 Baidu Execution](screenshots/02-task1-baidu-execution.png)

**Result:** No IP addresses, email addresses, people or hosts were returned.

A search returning no findings does not necessarily indicate a failed command. OSINT results depend on what the selected external source has indexed and makes available at the time of the query.

The command output was preserved using:

```bash
theHarvester -d networkwalks.com -l 1000 -b baidu | tee task1-baidu.txt
```

`tee` allowed the output to remain visible in the terminal while simultaneously writing it to a file.

[View Task 1 evidence](evidence/task1-baidu.txt)

---

### 3. Task 2 — Multi-Source Footprinting

The second task queried all supported sources with a result limit of 50:

```bash
theHarvester -d networkwalks.com -l 50 -b all
```

![Task 2 Multi-Source Execution](screenshots/06-task2-all-sources-execution.png)

Several sources required API credentials that were not configured in the local installation. theHarvester reported those sources as unavailable while continuing to query accessible sources.

The completed run returned:

- **3 ASNs**
- **2 interesting URLs**
- **4 IP addresses**
- **32 host results**
- No email addresses
- No people
- No LinkedIn users

![Task 2 Results](screenshots/07-task2-all-sources-results.png)

**Key observation:** Multi-source enumeration produced substantially more information than the single-source Baidu query, even though several API-dependent sources were unavailable.

## Results

| Category | Task 1: Baidu | Task 2: Multiple Sources |
|---|---:|---:|
| ASNs | 0 | 3 |
| Interesting URLs | 0 | 2 |
| IP addresses | 0 | 4 |
| Hosts | 0 | 32 |
| Emails | 0 | 0 |
| People | 0 | 0 |

## Evidence Handling & Disclosure

The scan run returned infrastructure information that was redacted before publication.

For the public repository:

- Actual IP addresses were removed
- Discovered hostnames were removed
- Summary counts were retained
- Original unredacted findings were not published

[View sanitised Task 2 evidence](evidence/task2-all-redacted.txt)

Additional screenshots documenting execution, file verification and saved output are available in the [`screenshots/`](screenshots/) directory.

## Linux Output Redirection and Pipes

I used Linux output redirection and piping while preserving reconnaissance evidence:

```bash
command > file.txt      # Write or overwrite
command >> file.txt     # Append
command1 | command2     # Send output from one command into another
command | tee file.txt  # Display and save
```

The pipe operator `|` passes the standard output of the command on its left to the standard input of the command on its right.

For example:

```bash
theHarvester -d networkwalks.com -l 1000 -b baidu | tee task1-baidu.txt
```

Here, theHarvester produces the reconnaissance output, `|` passes that output to `tee`, and `tee` displays it in the terminal while also writing it to `task1-baidu.txt`.

This allowed me to view the results while saving a copy as evidence.

## Key Observations

- Baidu returned no findings, while the multi-source query returned 3 ASNs, 2 URLs, 4 IP addresses and 32 hosts.
- Several sources used by `-b all` required API credentials that were not configured, but the remaining accessible sources continued running.

## Skills Used

- Passive reconnaissance and OSINT
- theHarvester
- Single-source and multi-source enumeration
- Linux command-line usage
- Output redirection with `>` and `>>`
- Piping with `|`
- Using `tee` to display and save output
- Evidence collection and validation
- Working with API-dependent OSINT tooling
- Security-conscious evidence sanitisation
- Technical documentation

## Ethical Use & Scope

This project was completed for educational purposes as part of the **NETWORKWALKS Cybersecurity Internship Programme**.

The reconnaissance activity was performed against the internship-scoped target. Technical findings that could unnecessarily expose infrastructure details have been removed from the public repository.

## Repository Structure

```text
.
├── evidence/
│   ├── task1-baidu.txt
│   └── task2-all-redacted.txt
├── screenshots/
│   ├── 01-theharvester-help-and-usage.png
│   ├── 02-task1-baidu-execution.png
│   ├── 03-task1-baidu-output-saved.png
│   ├── 04-task1-output-file-verification.png
│   ├── 05-task1-saved-output-nano.png
│   ├── 06-task2-all-sources-execution.png
│   ├── 07-task2-all-sources-results.png
│   ├── 08-task2-output-file-verification.png
│   └── 09-task2-saved-results-mousepad.png
└── README.md
```

## Author

**Prince Manu Gyebi**  
Cybersecurity Intern — Batch B082  
NETWORKWALKS

LinkedIn: [Prince Manu Gyebi](https://www.linkedin.com/in/princemanugyebi)
