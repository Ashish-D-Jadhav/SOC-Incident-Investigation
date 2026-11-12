# Part 5 - File Integration Monitor

## Objective

The objective of this phase was to configure File Integrity Monitoring on Windows and Linux endpoints and develop a custom Wazuh detection rule.

The goal was to detect unauthorised file modifications and deletions in real time, while also creating a custom alert capable of identifying when the Windows Guest account is enabled.

## Technologies Used

- Wazuh SIEM
- Wazuh File Integrity Monitoring (FIM)
- Windows 10
- Ubuntu Server 24.04
- Wazuh Agent
- OSSEC Configuration
- XML Custom Rules

## Windows File Integrity Monitoring

#### Purpose

To monitor sensitive business data stored within a custom directory and generate alerts whenever files are modified or deleted.

#### Test Environment

Directory: C:\Company Data

File: payroll.txt

Sample Contents: This is super secret please do not touch

<img width="1125" height="406" alt="image" src="https://github.com/user-attachments/assets/fc64e402-f330-40b3-aa7b-b0350fb022a0" />

#### Configuration

A custom FIM directory was added to the Windows Wazuh Agent configuration (ossec.conf).

The following directory was configured for real-time monitoring: C:\Company Data

After updating the configuration, the Wazuh Agent service was restarted.

<img width="1083" height="626" alt="image" src="https://github.com/user-attachments/assets/69686787-fea2-48fe-9d40-a0720cf545d2" />

#### Validation - File Modification

The payroll file was modified by appending additional content.

Result: Wazuh generated a File Integrity Monitoring alert indicating that the file checksum had changed.

Detection:
- Action: Modified
- File: payroll.txt
- Event Type: Integrity checksum changed

<img width="1125" height="364" alt="image" src="https://github.com/user-attachments/assets/9af41ce9-14fc-4f11-a0a2-8e0b571e1b71" />

#### Validation - File Deletion

The payroll.txt file was deleted.

Result: Wazuh successfully generated a file deletion alert.

Detection:
- Action: Deleted
- File: payroll.txt

<img width="1125" height="158" alt="image" src="https://github.com/user-attachments/assets/6b2a78a9-cbb9-4c36-9b78-f5729ced3fc9" />

## Linux File Integrity Monitoring

#### Purpose

To validate File Integrity Monitoring on Ubuntu by tracking modifications and deletions within a custom monitoring directory.

Test Directory: /opt/company-data

Test File: test.txt

<img width="698" height="340" alt="image" src="https://github.com/user-attachments/assets/315fb748-d384-4f5a-818a-b7ef79f05219" />

#### File Modification

The contents of test.txt were modified.

Result: Wazuh generated an integrity checksum changed alert.

<img width="1125" height="358" alt="image" src="https://github.com/user-attachments/assets/14b50e06-7d9d-4267-8cc2-483c0c78b78b" />

#### File Deletion

The test.txt file was deleted.

Result: Wazuh successfully generated a file deletion alert.

<img width="1125" height="363" alt="image" src="https://github.com/user-attachments/assets/7f4cca8d-6bb9-4d14-aecc-59da57e0d195" />

## Custom Detection Rule

### Objective

Create a custom Wazuh rule capable of detecting when the built-in Windows Guest account is enabled.

Unexpected activation of the Guest account may indicate:

### Threat Scenario

Unauthorised privilege changes

- Misconfiguration
- Insider activity
- Persistence mechanisms

For this reason a dedicated alert was created.

### Event Investigation

The Wazuh Discover interface was used to identify the event associated with Guest account enablement.

Key findings:
- Event ID: 4722
- Username: Guest

Query: data.win.eventdata.targetUserName: Guest AND data.win.system.eventID: 4722

<img width="1125" height="445" alt="image" src="https://github.com/user-attachments/assets/66d238dd-f163-4b16-ac12-26483123482b" />

### Rule Creation

#### Custom Rule

A custom rule was added to: local_rules.xml

Rule Purpose: Detect Guest account activation events.

Reference: https://documentation.wazuh.com/current/user-manual/ruleset/ruleset-xml-syntax/rules.html

### Rule Validation

After reloading the Wazuh Manager, the Guest account was enabled from the Windows endpoint.

Result:

✅ Custom rule triggered successfully

✅ Alert generated within Wazuh

✅ Event severity assigned according to custom configuration

<img width="1125" height="411" alt="image" src="https://github.com/user-attachments/assets/f80bb5e9-74e1-4c36-b986-1cebf13b6188" />

## Outcome

Successfully implemented File Integrity Monitoring and custom detection engineering within Wazuh.

Achievements:

✅ Configured real-time File Integrity Monitoring on Windows

✅ Configured real-time File Integrity Monitoring on Ubuntu

✅ Detected file modifications

✅ Detected file deletions

✅ Developed a custom Wazuh detection rule

✅ Detected Guest account enablement

✅ Generated custom alerts within Wazuh

## Lessons Learned

- Learned how Wazuh File Integrity Monitoring operates.
- Configured real-time file monitoring on Windows and Linux.
- Investigated file modification and deletion events.
- Developed custom Wazuh detection rules.
- Learned how Windows security events can be converted into actionable detections.
- Improved understanding of detection engineering concepts.




