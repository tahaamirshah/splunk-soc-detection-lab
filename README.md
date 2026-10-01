# Splunk SOC Lab

## About This Project

For this project I used Splunk Cloud with a Windows VM to practice basic SOC monitoring.

I generated different types of activity on the Windows machine, checked the events in Event Viewer and Sysmon, sent the logs to Splunk, and then made searches and alerts for them.

The main detections I worked on were:

- repeated failed logins
- PowerShell using ExecutionPolicy Bypass
- scheduled task creation
- curl download activity

## Tools

- Splunk Cloud
- Windows 11 VM
- Sysmon
- PowerShell
- Event Viewer
- Splunk HEC

## Detection 1 - Repeated Failed Logins

I created multiple failed login attempts on the Windows VM.

Windows recorded the failed logins as Event ID 4625. I sent the events into Splunk and used an SPL search to count repeated failed attempts.

![Failed Login Events](Screenshots/05-failed-login-splunk.png)

![Failed Login Detection](Screenshots/06-repeated-failed-login-detection.png)

![Failed Login Alert](Screenshots/07-repeated-failed-login-alert.png)

## Detection 2 - PowerShell Execution

For this test I ran PowerShell with `-ExecutionPolicy Bypass`.

Sysmon recorded the process as Event ID 1. I searched for the command in Splunk and created an alert for it.

![PowerShell Sysmon Event](Screenshots/08-sysmon-powershell-event.png)

![PowerShell Detection](Screenshots/09-suspicious-powershell-splunk.png)

![PowerShell Alert](Screenshots/10-suspicious-powershell-alert.png)

## Detection 3 - Scheduled Task Creation

I created a scheduled task using `schtasks.exe`.

The task was set to run when a user logs in. Sysmon recorded the process and I searched for `schtasks.exe` with `/Create` in Splunk.

![Scheduled Task Created](Screenshots/11-scheduled-task-created.png)

![Scheduled Task Sysmon Event](Screenshots/12-scheduled-task-sysmon-event.png)

![Scheduled Task Detection](Screenshots/13-scheduled-task-splunk.png)

![Scheduled Task Alert](Screenshots/14-scheduled-task-alert.png)

## Detection 4 - Curl Download

For the last detection I used `curl.exe` to download a test page from example.com.

Sysmon recorded the curl process and I used Splunk to search for the command and create an alert.

![Curl Sysmon Event](Screenshots/15-curl-sysmon-event.png)

![Curl Detection](Screenshots/16-curl-splunk.png)

![Curl Alert](Screenshots/17-curl-download-alert.png)

## What I Practiced

This project gave me practice with:

- Windows Security logs
- Sysmon
- Splunk searches
- SPL
- alert creation
- process monitoring
- failed login detection
- basic persistence detection

The SPL searches I used are saved in the `Queries` folder.
