# Part 4 - Build SOC Dashboard

## Objective

The objective of this phase was to create a Security Operations Center (SOC) dashboard within Wazuh to visualise and monitor security telemetry collected from Windows and Linux endpoints.
The dashboard was designed to provide visibility into authentication activity, account management events, and failed SSH authentication attempts.

## Technologies Used

1) Wazuh Dashboard
2) Wazuh Archives Index
3) Windows Security Events
4) Linux Authentication Logs
5) OpenSearch Dashboards

## Dashboard Components

The SOC dashboard consists of three visualisations:

1) Failed Windows Logons
2) Windows Account Changes Over Time
3) Linux Failed SSH Authentication Activity

Together these visualisations provide visibility into authentication failures, account management activities, and potential unauthorised access attempts.

## Dashboard 1 - Failed Windows Logons

### Purpose

This metric visualisation tracks Windows authentication failures using Event ID 4625.

### Query

data.win.system.eventID:4625

### Findings

Three failed logon attempts were intentionally generated using incorrect passwords to validate telemetry collection.

### Security Value
Monitoring Event ID 4625 helps identify:

- Brute-force activity
- Password guessing attacks
- User authentication issues

<img width="1167" height="656" alt="image" src="https://github.com/user-attachments/assets/841a6cd0-4e4d-4f02-84f0-9d4c01f397ec" />

## Dashboard 2 - Windows Account Changes Over Time

### Purpose
This visualisation tracks account management activity within the Windows endpoint.

### Monitored Events
- 4720 - User Created
- 4722 - User Enabled
- 4723 - Password Change Attempt
- 4724 - Password Reset
- 4725 - User Disabled
- 4726 - User Deleted
- 4732 - User Added to Group
- 4733 - User Removed from Group
- 4738 - User Modified

### Findings
The dashboard successfully displayed account management activity generated during the telemetry exercises performed in Part 3.

### Security Value
This dashboard helps analysts identify:

- Privilege escalation activity
- User account creation
- Administrative changes
- Insider threat indicators

<img width="1089" height="483" alt="image" src="https://github.com/user-attachments/assets/af7bd9ad-f6d9-475d-80e1-8b84fe8c704a" />

## Dashboard 3 - Linux Failed SSH Authentication Activity

### Purpose
This data table tracks failed SSH authentication attempts targeting the Ubuntu endpoint.

- Data Monitored
- Agent Name
- Timestamp
- Username
- Destination User
- Source IP Address

### Findings
Failed SSH authentication attempts generated during the lab were successfully captured and displayed within the dashboard.

### Security Value
This dashboard assists analysts in:

- Detecting brute-force attacks
- Tracking invalid usernames
- Identifying source IP addresses
- Investigating SSH access attempts

<img width="1314" height="548" alt="image" src="https://github.com/user-attachments/assets/e396d8b3-511f-45d5-b540-c53f4737292b" />

## Challenges Encountered

### Missing Event Fields

While configuring the line chart visualisation, the field: data.win.system.eventID was unavailable for selection.

### Root Cause

The Wazuh index pattern cache had not been refreshed after ingesting new telemetry.

### Resolution

The wazuh-archives index pattern field list was refreshed from Dashboard Management. After refreshing the index pattern, the field became available and the visualisation was successfully created.

## Outcome

Successfully created a SOC dashboard consisting of three security-focused visualisations.

Achievements:

✅ Built a Failed Windows Logon dashboard
✅ Built a Windows Account Changes dashboard
✅ Built a Linux Failed SSH Authentication dashboard
✅ Identified and resolved an index pattern issue
✅ Validated telemetry visibility across Windows and Linux endpoints
✅ Established a monitoring dashboard for ongoing investigations


## Lessons Learned

- Learned how to create visualisations within Wazuh.
- Developed dashboard design skills for SOC monitoring.
- Gained experience using Wazuh index patterns.
- Learned how to troubleshoot missing fields in dashboards.
- Improved understanding of authentication monitoring.
- Built security-focused dashboards for incident investigation.


