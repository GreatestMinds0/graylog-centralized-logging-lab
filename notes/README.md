# Graylog Lab — Troubleshooting Notes

## 1. Issue: Logs not appearing in Graylog
- rsyslog on Kali Linux reported:

 - Graylog input initially not created or running

## 2. Root Cause
- Syslog UDP input on Graylog not started
- Firewall blocking UDP port 1514

## 3. Steps Taken
1. Created Syslog UDP input on Graylog (port 1514)
2. Enabled “Allow overriding source” in input settings
3. Verified firewall on Ubuntu server allowed incoming 1514 UDP/TCP
4. Restarted rsyslog on Kali:
5. Sent test log from Kali:
6. Verified log appeared in Graylog streams

## 4. Outcome
- Logs successfully ingested in Graylog
- Verified with multiple test messages and `tcpdump`
- Confirmed metadata (source, facility, level) was correct
