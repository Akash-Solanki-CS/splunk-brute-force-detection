# Splunk Brute Force Detection Lab

## Overview
This project demonstrates SSH brute-force attack detection using Splunk SIEM.

## Tools Used
- Kali Linux
- Hydra
- AWS EC2 Ubuntu
- Splunk Enterprise

## Attack Flow
1. Kali Linux used as attacker machine
2. AWS Ubuntu server configured with SSH
3. Hydra used for brute-force simulation
4. Ubuntu auth.log collected
5. Logs ingested into Splunk
6. Failed SSH attempts detected in dashboard


## hydra attack From kali 
```bash
hydra -l ubuntu -P rockyou.txt ssh://192.168.56.102
```
## logs detect on ubuntu 
```bash
sudo tail -f /var/log/auth.log
```

## SPL Queries

### Failed Password Attempts
```spl
source="auth.log" "Failed password"
```
## accepted password
```bash
source="auth.log" "accepted password"
```
## for check time wise logs
```bash
source="auth.log" | timechart span=1h count
