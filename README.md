# Part 3 - Generate and Analyse Telemetry

## Objective

The objective of this phase was to generate security-relevant activity on both Windows and Linux endpoints and analyse the resulting telemetry within Wazuh.

The goal was to understand how security events are collected, interpreted, and investigated using Wazuh dashboards, Windows Event Logs, Sysmon telemetry, and Linux audit events.

## Technologies Used

- Wazuh SIEM
- Windows Security Logs
- Sysmon
- Ubuntu Server
- OpenSSH
- VMware Workstation

## Lab Activities

### Windows Telemetry Generation

The following administrative actions were performed to generate Windows security events:

- Enumerated local users
- Enumerated local administrators
- Enabled the Guest account
- Changed the Guest account password
- Created a new local user account
- Added the user to the Administrators group
- Deleted the user account

## Key Security Events Observed

### Event ID 4726 - User Account Deleted

An event with ID 4726 was generated when the temporary user account was deleted.

#### Findings

- Account performing action: Bob
- Affected account: student1
- Event Description: A user account was deleted

#### Investigation

Using the event details and SID values, it was confirmed that the student1 account was deleted by the Bob account

<img width="1187" height="641" alt="image" src="https://github.com/user-attachments/assets/abb6d1c4-10f4-4482-b506-e48b7ca4316e" />

### Event ID 4720 - User Account Created

An event with ID 4720 was generated when the student1 account was created.

#### Findings

- New Account: student1
- Creator: Bob
- Primary Group ID: 513
- Account Type: Domain Users

#### Event Analysis

The User Account Control (UAC) value of 0x15 corresponds to:

- USER_NORMAL_ACCOUNT
- USER_PASSWORD_NOT_REQUIRED
- USER_ACCOUNT_DISABLED

<img width="1442" height="485" alt="image" src="https://github.com/user-attachments/assets/e14c2586-4eb6-4487-a24c-424efbca8457" />

### Event ID 4624 - Successful Logon

Event ID 4624 was analysed to understand successful logon activity.

#### Findings

- Logon Type: 2 (Interactive)
- User Account: Bob
- Source System: Local Computer

#### Investigation

The event provides information regarding:

- Logon type
- Account used
- Process responsible for authentication
- Correlation identifiers

<img width="1391" height="577" alt="image" src="https://github.com/user-attachments/assets/36112c4c-8c56-4d75-8a21-58c34bb983a4" />

<img width="1333" height="623" alt="image" src="https://github.com/user-attachments/assets/0aafa2f9-17cd-4f60-9776-07b472140007" />

### Event ID 4732 - Member Added to Local Group

An event was generated when the student1 account was added to the local Administrators group.

#### Findings

The event showed:

- Security Identifier (SID)
- Group information
- Subject account

Interestingly, the username was not directly available within the event record and required SID-based investigation.

<img width="1287" height="504" alt="image" src="https://github.com/user-attachments/assets/e5f632f8-cf18-4514-b253-fc4317e95b10" />

## Linux Telemetry Analysis

SSH activity was generated from the Windows endpoint to the Ubuntu server.

Activities included:

- Failed SSH authentication attempts
- Successful SSH authentication
- Command execution
- Session creation
- Session termination

### Failed SSH Login

A login attempt was made using a non-existent user account.

Findings:

- Invalid username detected
- Source IP identified
- Multiple authentication failures recorded
- The event demonstrated Wazuh's ability to detect unauthorised access attempts.

### Successful SSH Login

A successful SSH authentication was performed using a valid Ubuntu account.

Findings:

- Source IP identified
- User account identified
- Session established successfully

### Session Tracking

Wazuh captured session identifiers associated with SSH activity.

Using Session ID 10 it was possible to:

- Identify login events
- Identify command execution activity
- Identify logout events
- Build an activity timeline

This demonstrates how session identifiers can be used to correlate multiple events during an investigation.

### File Collection Activity

The contents of /etc/passwd were redirected into a file named loot.txt.

Commands executed:

- cat /etc/passwd
- cat /etc/passwd > /tmp/loot.txt

This activity was successfully captured within the collected telemetry and associated with the active SSH session.

### Challenges Encountered

Wazuh Manager Service Failure

<img width="891" height="575" alt="image" src="https://github.com/user-attachments/assets/4b4c8d47-4a0e-4e9d-ae4a-829b20a1e23d" />

During telemetry analysis the Wazuh dashboard became inaccessible.

#### Root Cause

The Wazuh Manager service had stopped unexpectedly.

<img width="1397" height="825" alt="image" src="https://github.com/user-attachments/assets/5181c638-3244-4c4b-ae74-210e51979c5b" />

#### Resolution

The Wazuh Manager service was restarted and normal functionality was restored.

<img width="838" height="88" alt="image" src="https://github.com/user-attachments/assets/3b680adf-7231-4b23-93f0-f41631e72de5" />

<img width="1388" height="782" alt="image" src="https://github.com/user-attachments/assets/300230e1-b424-458e-a1ce-2d72fb373dc6" />

















