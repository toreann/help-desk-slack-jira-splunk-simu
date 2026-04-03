# help-desk-slack-jira-splunk-simu
A hands-on help desk lab simulating a small IT support workflow using **Jira**, **Slack**, **Splunk**, **Windows**, and **Linux**.

## Project Overview

This project was built to simulate a realistic support environment where incidents are reported, tracked, investigated, and resolved through a structured workflow.

### Lab stack
- **Windows host** as the technician workstation
- **Ubuntu Linux VM** as the remote endpoint
- **SSH** for remote troubleshooting
- **Jira** for ticket management
- **Slack** for simulated user communication
- **Splunk** for log review and investigation support

## Goals

- Practice incident handling in a structured workflow
- Document technical troubleshooting clearly
- Demonstrate remote support using SSH
- Show familiarity with ticketing, communication, and log analysis tools
- Build a portfolio project relevant to Help Desk and entry-level IT roles

## Simulated Workflow

User issue reported in Slack  
→ Ticket created in Jira  
→ Remote investigation over SSH  
→ Logs reviewed in Splunk  
→ Resolution documented  
→ Ticket closed

## Tickets Covered

### 1. DNS Resolution Failure
A Linux VM could reach external IP addresses but could not resolve domain names. The issue was investigated remotely over SSH, tested with `ping`, and resolved by correcting DNS settings.

### 2. SSH Authentication Failure
A user could not log in to the Linux VM over SSH. Authentication failures were reproduced, reviewed through Linux logging, and resolved by correcting credentials and validating successful access.

### 3. Nginx Service Failure
A web service running on the Linux VM became unavailable. The issue was investigated remotely, service status and logs were reviewed, and the service was restarted and validated.

## Key Skills Demonstrated

- Ticket handling and documentation
- Incident prioritization and workflow tracking
- Remote Linux support using SSH
- Basic network troubleshooting
- DNS troubleshooting
- Service troubleshooting with systemd
- Log review using Splunk
- Communication and status updates through Slack

## Tools Used

- Jira
- Slack
- Splunk Enterprise
- Windows
- Ubuntu Server
- OpenSSH
- Nginx
- PowerShell
- Linux CLI

## Screenshots
The screenshots/ folder contains evidence from each phase of the workflow:

→ Slack user reports and support updates
→ Jira ticket lifecycle
→ Windows PowerShell and SSH sessions
→ Linux troubleshooting commands
→ Splunk log searches and results

---

## `tickets/ticket-1-dns-issue.md`
# Ticket 1 - DNS Resolution Failure

## Summary
The Linux VM could reach external IP addresses but failed to resolve domain names. The issue was investigated remotely over SSH and resolved by correcting DNS configuration.

## Priority
High

## Environment

- Technician workstation: Windows host
- Remote endpoint: Ubuntu Linux VM
- Access method: SSH
- Ticketing: Jira
- Communication: Slack
- Log review: Splunk

## Issue Description
A user reported that the Linux VM could not access websites even though the network connection appeared active.

## Initial User Report

**Slack message:**
> User cannot access websites from the Linux system.

## Investigation

The Linux VM was accessed remotely from the Windows host using SSH.

### Commands used

```bash
ping -c 3 8.8.8.8
ping -c 3 google.com
ip a
ip route
cat /etc/resolv.conf
```
## Findings

- Connectivity to 8.8.8.8 was successful
- Connectivity to google.com failed

## Stesps Taken

- Connected to the Linux VM over SSH
- Tested raw IP connectivity with ping 8.8.8.8
- Tested domain resolution with ping google.com
- Reviewed DNS configuration
- Copied Linux log data to the Windows host
- Reviewed related log activity in Splunk

## Root Cause and Resolution
The Linux VM was configured with an invalid test DNS server, which prevented domain name resolution. DNS settings were corrected to valid resolvers and connectivity was retested successfully.

---

# Ticket 2 - SSH Authentication Failure

## Summary
A user was unable to log in to the Linux VM over SSH. The issue was reproduced, investigated through SSH-related logs, and resolved by correcting credentials and validating successful remote access.

## Priority
Medium

## Environment

- Technician workstation: Windows host
- Remote endpoint: Ubuntu Linux VM
- Access method: SSH
- Ticketing: Jira
- Communication: Slack
- Log review: Splunk

## Issue Description
A user reported that SSH access to the Linux VM was failing.

## Initial User Report

**Slack message:**
> I cannot log in to the Linux system over SSH.

## Investigation

The issue was reproduced by attempting SSH login with invalid credentials from the Windows host.

### Example action

- Attempted SSH login using the wrong password
- Reviewed Linux SSH authentication logs
- Confirmed authentication failures during the incident window

## Steps Taken

- Reproduced the issue with an invalid SSH login attempt
- Connected to the Linux VM with an administrative account
- Reviewed SSH-related logs using `journalctl`
- Confirmed failed authentication attempts
- Exported relevant log output for Splunk review
- Reset or corrected credentials
- Retested SSH login successfully

## Useful commands

```bash
sudo journalctl -u ssh --since "10 minutes ago" --no-pager
```

## Root Cause and Resolution
The failure was caused by invalid SSH credentials during login. Credentials were corrected and SSH access was retested successfully.


---

# Ticket 3 - Nginx Service Failure

## Summary
A web service hosted on the Linux VM became unavailable. The issue was investigated remotely over SSH, service logs were reviewed, and the nginx service was restarted and validated.

## Priority
High

## Environment

- Technician workstation: Windows host
- Remote endpoint: Ubuntu Linux VM
- Access method: SSH
- Service affected: Nginx
- Ticketing: Jira
- Communication: Slack
- Log review: Splunk

## Issue Description
A user reported that the web service running on the Linux VM was unavailable.

## Initial User Report

**Slack message:**
> The web service on the Linux server is unavailable.

## Investigation

The Linux VM was accessed remotely over SSH and the status of the nginx service was checked.

### Commands used

```bash
sudo systemctl status nginx
sudo journalctl -u nginx --since "15 minutes ago" --no-pager
```

## Findings

- The nginx service was stopped
- Service-related logs were reviewed to support the incident timeline

## Steps Taken

- Connected to the Linux VM over SSH
- Verified nginx service status with systemctl
- Reviewed service logs with journalctl
- Collected nginx-related logs for Splunk review
- Restarted the nginx service
- Confirmed the service was running normally again

## Root Cause and Resolution
The nginx service was not running on the Linux VM. The nginx service was restarted and service availability was confirmed.

```bash
sudo systemctl start nginx
sudo systemctl status nginx
```