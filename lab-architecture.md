
# Lab Architecture

## Overview
This lab simulates a small IT support environment where incidents are reported, tracked, investigated, and resolved using a structured workflow.

The design focuses on practical help desk tasks while also demonstrating basic systems and log analysis skills.

## Architecture

### Windows Host
Acts as the technician workstation.

Used for:
- Jira ticket management
- Slack communication
- Splunk log review
- PowerShell commands
- SSH access to the Linux VM
- Copying log files from Linux to Windows

### Linux VM
Acts as the remote endpoint being supported.

Used for:
- DNS troubleshooting
- SSH authentication troubleshooting
- Nginx service troubleshooting
- Linux log generation and review
- Remote administration over SSH

## Access Model

The Linux VM is accessed remotely from the Windows host using SSH.

### Workflow
1. User issue is reported in Slack
2. Ticket is created in Jira
3. Technician connects to Linux over SSH
4. Technician investigates and resolves the issue
5. Relevant logs are reviewed in Splunk
6. Ticket is updated and closed

## Tools and Roles

### Jira
Used to track incidents through the workflow:
- To Do
- In Progress
- Waiting
- Resolved

### Slack
Used to simulate support communication:
- `#it-support`
- `#it-incidents`
- `#it-announcements`

### Splunk
Used to review logs as supporting evidence during troubleshooting.

### SSH
Used to remotely access and troubleshoot the Linux VM from the Windows host.

## Summary

The lab combines support process and technical troubleshooting in one small environment:
- Windows as the technician workstation
- Linux as the supported remote system
- Jira for ticket flow
- Slack for communication
- Splunk for log review
- SSH for remote troubleshooting