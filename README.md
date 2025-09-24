# Report Automation Pipeline — Project Summary

**Status:** Proof-of-concept / Internal automation  
**Owner:** [Caroline Wanjiru Muturi]  
**Last updated:** 2025-09-22

## Overview
This repository contains a *non-sensitive* summary and documentation for an internal automation pipeline I developed to streamline the reporting workflow.  
**Note:** The actual automation script(s) (production Python scripts, credentials, and downloaded data) are intentionally *not* included here due to data-protection and confidentiality requirements.

## What the automation does (high level)
- Logs into a secured internal dashboard (SmartCollect) and downloads the **Progress From Notes** report for a specific client and debt type.  
- Downloads the bank's Excel attachment (subject: ** REPORT**) from a configured Gmail account.  
- Performs a VLOOKUP-style merge: matches the bank `AccountID` to `ACCOUNT NO.` from the Progress report and pastes the `REPORT` field into the bank file on the **Pending** sheet.  
- Formats the merged file (wrap text for `REPORT`, apply borders to the used range).  
- Saves the processed file as `FINAL_REPO.xlsx` on the Desktop for manual review and sending.

## Why we built it
- Reduce manual copy/paste and human error when reconciling bank reports.  
- Save ~30–60 minutes per report cycle and standardize formatting.  
- Keep final send step manual during initial testing to ensure data quality.

## Tech stack (implementation notes)
- **Language:** Python 3.x  
- **Automation / Browser:** Selenium (Firefox + geckodriver)  
- **Data processing:** Pandas, OpenPyXL (Excel read/write and formatting)  
- **Email retrieval:** IMAP (Gmail via app password)  
- **Platform:** Windows (scripts run on user workstation); future plan: schedule with Task Scheduler or a safe CI runner

## Security & data protection
- No code or credentials are shared in this public repo.  
- Secrets (Gmail app password, internal system credentials) are stored only on the operator’s machine in a local, protected location — **never** committed.  
- Files downloaded from email or internal systems are not included in the repo.  
- If access to the real script is required, a formal access request is necessary (see **Access** section).

## Access (how to request the script)
If you require access to the script for review or audit, please send a request to **[wanjirumuturi007@gmail.com]** with:
- Purpose of access (audit, review, operations)  
- Your affiliation & role  
- Whether you need read-only or operational access  
Requests will be approved by the project owner and access provided through a secure channel (SFTP / shared drive / direct copy), not via GitHub.

## Testing & operation notes
- Before running: install packages `selenium`, `pandas`, `openpyxl`.  
- Ensure Firefox + geckodriver are installed and geckodriver is in PATH.  
- Use a Gmail app password (IMAP) for automated downloads — do not use an account password.  
- Keep Excel files closed while the script runs (Windows locks files).

## Limitations & next steps
- Current flow saves the final file locally; sending is manual by design during the test period.  
- Next steps: (a) add a safe draft creation via Gmail API, (b) add a scheduled runner with logging & alerts, (c) implement unit tests and sanitized demo mode for public distribution.

## Changelog / Ownership
- Developed by: [Caroline Wanjiru Muturi.]  
- Original implementation: 2025-08-09 
- Current status: being tested manually before enabling send automation
