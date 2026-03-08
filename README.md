# SSH Brute Force Detection using Splunk

This project demonstrates detection of SSH brute-force attacks using Splunk SIEM.

## Project Overview
A simulated attacker performs SSH brute-force attacks against a Linux server. Authentication logs are ingested into Splunk where detection queries, dashboards, and alerts identify suspicious activity.

## Lab Architecture

Kali Linux (Attacker)
        │
        │ SSH brute force (Hydra)
        ▼
Ubuntu Server
        │
        │ /var/log/auth.log
        ▼
Splunk SIEM
        │
        ├ Dashboard
        └ Alert Detection

## Tools Used

- Kali Linux
- Ubuntu Server
- Hydra
- Splunk Enterprise
- OpenSSH

## Detection Query
index=main "Failed password"
| rex "from (?<src_ip>\d+.\d+.\d+.\d+)"
| bin _time span=1m
| stats count by src_ip _time
| where count > 10


## Dashboard Features

- Top Attacker IPs
- Failed Login Attempts Timeline
- Targeted SSH Users
- Geographic Attack Origin

## Alert

Alert triggers when more than 10 SSH failed login attempts occur within 1 minute.

## Example Attack
hydra -l sshuser -P /usr/share/wordlists/rockyou.txt ssh://192.168.1.21

## Result
Splunk detects brute-force attempts and sends alerts to the security analyst.
