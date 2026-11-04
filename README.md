# 02-Connect-Agents-and-Deploy-Sysmon

## Objective 

The objective of this phase was to onboard the Ubuntu and Windows virtual machines to the Wazuh Server by deploying Wazuh agents on both endpoints. Additionally, Sysmon was installed and configured to provide detailed endpoint telemetry that can be collected, analysed, and monitored through the Wazuh Dashboard. 

## Technologies Used 

1) Wazuh Manager 
2) Wazuh Agent 
3) Windows 10 
4) Ubuntu Server 24.04 
5) Sysmon for Windows 
6) Sysmon for Linux 
7) VMware Workstation

## Architecture Update 

## Lab Architecture - Part 2: Agent & Sysmon Integration

     ```text
                         Part 2 - Agent & Sysmon Integration

     ┌─────────────────────────┐      ┌─────────────────────────┐
     │       Windows VM        │      │        Ubuntu VM        │
     │                         │      │                         │
     │ • Wazuh Agent           │      │ • Wazuh Agent           │
     │ • Sysmon                │      │ • Sysmon for Linux      │
     └───────────┬─────────────┘      └───────────┬─────────────┘
                 │                                │
                 │                                │
                 └──── Logs & Security Telemetry ─┘
                                │
                                ▼
     
                  ┌─────────────────────────────┐
                  │         Wazuh Server         │
                  │                             │
                  │ • Wazuh Manager             │
                  │ • Agent Authentication      │
                  │ • Log Collection            │
                  │ • Event Analysis            │
                  │ • Alert Generation          │
                  └──────────────┬──────────────┘
                                 │
                                 ▼

                  ┌─────────────────────────────┐
                  │      Wazuh Dashboard        │
                  │                             │
                  │ • Security Monitoring       │
                  │ • Threat Detection          │
                  │ • Log Analysis              │
                  │ • Incident Investigation    │
                  └─────────────────────────────┘
     ```
## Windows Agent Deployment

### Agent Installation

The Wazuh deployment wizard was used to generate the Windows agent installation command. The generated package was downloaded and installed on the Windows virtual machine.

### Validation

After installation:

<img width="1091" height="308" alt="image" src="https://github.com/user-attachments/assets/80e1a3d4-6e70-4ca7-8de2-c6a4846578cf" />

PowerShell: NET START Wazuh

The Wazuh service started successfully on the endpoint.

<img width="494" height="162" alt="image" src="https://github.com/user-attachments/assets/80023450-d422-4191-992e-d2d623a4f61f" />



