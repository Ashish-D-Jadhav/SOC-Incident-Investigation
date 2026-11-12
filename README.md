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

## Section 1: Windows File Integrity Monitoring

### Windows File Integrity Monitoring

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


