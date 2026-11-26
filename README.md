# 07-Incident-Investigation-Report

## Summary

During the investigation of security telemetry collected by the Wazuh SOC lab, multiple account management, authentication and file integrity events were identified across Windows and Ubuntu endpoints.  

The activity included creation and deletion of user accounts, changes to local administrator group membership, Guest account activation, SSH authentication attempts, command execution on Linux systems, and file modifications/deletions monitored through File Integrity Monitoring (FIM). 

## Incident 1: Windows Endpoint Activities 

### Findings: 

The investigation identified the following activities: 

- User account student1 was created by account Bob (Event ID 4720).  
- User account student1 was added to the local Administrators group (Event ID 4732).  
- User account student1 was subsequently deleted by account Bob (Event ID 4726).  
- The built-in Windows Guest account was enabled and detected by a custom Wazuh detection rule based on Event ID 4722.  
- Successful interactive logons were observed for account Bob (Event ID 4624).

### Investigation Summary 

The investigation revealed a sequence of administrative and security-related activities performed across both Windows and Ubuntu endpoints. 

A temporary Windows account (student1) was created, granted elevated privileges through membership in the Administrators group, and later deleted by account Bob.  
The built-in Guest account was also enabled and successfully detected through a custom Wazuh rule. 

### Who, What, When, Where, Why, and How 

#### Who 

| | | |
|---|---|---|
| Bob | Created student1, added student1 to Administrators group, deleted student1, successfully logged on to Windows |
| student1 | Newly created account later granted administrative privileges and subsequently deleted |
| Guest | Built-in account enabled and detected by custom rule |

#### What 

The following activities occurred: 

- User account creation. 
- User account deletion. 
- Local administrator group modification. 
- Guest account activation. 
- Interactive logon activity. 

#### When 

Windows account events occurred during telemetry generation activities 

#### Where 

The activities occurred on the following hosts: 

| | | |
|---|---|---|
| Windows Endpoint (MYDFIR-Windows) | Account creation, deletion, logon events, Guest account activation, FIM alerts |

#### Why 

The purpose was to: 

- Validate Windows security event collection 
- Generate telemetry for SOC investigations 

#### How 

- User management activities generated Event IDs 4720, 4726 and 4732.  
- Guest account activation generated Event ID 4722 which triggered a custom Wazuh rule.  

| Question          | Answer                                                      |
|-------------------|--------------------------------------------------------------------|
| What happened?  | User accounts were created, privileged, and deleted|
| When did it happen? | 21 Sept 2026 20:55 - 20:59 UTC |
| Which hosts were involved? | MYDFIR-Windows, DESKTOP-3ULMB4N  |
| Which accounts were changed? | student1 was created, added to Administrators and deleted; Guest was enabled |
| What should we recommend? | Disable Unused Accounts, Monitor Privileged Account Changes |


## Incident 2: Linux Endpoint Activities 

### Findings: 

The investigation identified the following activities: 

- Multiple failed SSH authentication attempts were recorded using an invalid username (fakeuser).  
- Successful SSH authentication was performed using a valid Ubuntu account.  
- SSH session activity was correlated using Session ID 10, allowing login, command execution, and logout events to be tracked.  
- Contents of /etc/passwd were copied into loot.txt using shell commands. 

### Investigation Summary 

On the Linux server, both failed and successful SSH login attempts were detected. Session tracking allowed the entire sequence of login, activity, and logout events to be monitored. 

### Who, What, When, Where, Why, and How 

#### Who

| | | |
|---|---|---|
| fakeuser | Invalid account used during failed SSH attempts |
| mydfir | Valid account used for successful SSH authentication |

#### What 

The following activities occurred: 

- Failed SSH authentication attempts. 
- Successful SSH authentication. 

#### When 

SSH activity occurred during Linux telemetry generation and analysis 

#### Where 

The activities occurred on the following hosts: 

| | | |
|---|---|---|
| Ubuntu Endpoint (MYDFIR-Linux)  | SSH activity, command execution, FIM alerts  |

#### Why 

The purpose was to: 

- Validate SSH monitoring. 
- Generate telemetry for SOC investigations 

#### How 

- SSH authentication attempts generated successful and failed login events.

| Question          | Answer                                                      |
|-------------------|--------------------------------------------------------------------|
| What happened?  | SSH activity occurred |
| When did it happen? | 21 Sept 2026 20:55 - 20:59 UTC |
| Which hosts were involved? | MYDFIR-Linux  |
| Was SSH abuse observed? | Failed SSH attempts using fakeuser were observed, followed by successful authentication using a valid account. |
| What should we recommend? | Strengthen SSH Monitoring, Implement Threat Hunting Dashboards  |


## Incident 3: File Integrity Monitoring Events 

### Findings: 

The investigation identified the following activities: 

#### Windows 

- File payroll.txt in C:\Company Data was modified.  
- File payroll.txt was deleted.  

#### Ubuntu 

- File test.txt in /opt/company-data was modified.  
- File test.txt was deleted.  

### Investigation Summary 

File Integrity Monitoring detected file modifications and deletions on both Windows and Ubuntu systems, proving that the monitoring controls were functioning as intended.  

### Who, What, When, Where, Why, and How 

#### Who 

No user attribution was available from the File Integrity Monitoring alerts. 

Affected files: 
- payroll.txt: modified and deleted on Windows. 
- test.txt: modified and deleted on Ubuntu 

#### What 

The following activities occurred: 
- File modification. 
- File deletion. 

#### When 

File integrity events occurred during FIM validation testing 

#### Where 

- MYDFIR-Windows: -  C:\Company Data\payroll.txt 
- MYDFIR-Linux:- /opt/company-data/test.txt 

#### Why 

The purpose was to: 
- Test File Integrity Monitoring 
- Generate telemetry for SOC investigations. 

#### How 

- Wazuh FIM monitored specified directories. 
- File modifications and deletions generated alerts. 
- Alerts were forwarded to the Wazuh Dashboard. 

| Question          | Answer                                                      |
|-------------------|--------------------------------------------------------------------|
| What happened?  | Files were modified and deleted |
| When did it happen? | 12 Oct 2026 20:58 - 21:22 UTC |
| Which hosts were involved? | MYDFIR-Windows (DESKTOP-3ULMB4N), MYDFIR-Linux |
| Was a file deleted? | Yes. payroll.txt and test.txt were deleted |
| What should we recommend? | Expand File Integrity Monitoring Coverage, Implement Threat Hunting Dashboards |

## Conclusion 

The investigation confirmed that Wazuh successfully detected and recorded account lifecycle events, administrator group modifications, Guest account activation, SSH authentication activity, command execution, and file integrity changes across both Windows and Ubuntu systems. The telemetry pipeline, monitoring controls, and custom detection rules operated as expected and provided sufficient evidence to reconstruct user activity and support incident investigations 

