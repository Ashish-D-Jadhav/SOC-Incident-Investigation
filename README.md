# 01-Wazuh-Agent-Deployment

## Objective 

The objective of this phase was to build the foundational infrastructure for a Wazuh-based Security Operations Center (SOC) lab. This involved deploying VMware Workstation and creating three virtual machines: a dedicated Wazuh Server, an Ubuntu Server, and a Windows endpoint. These systems form the foundation of the lab environment that will be used for log collection, threat detection, and security monitoring throughout the project. 

## Architecture: 

The Wazuh Server serves as the central monitoring and analysis platform, while the Ubuntu Server and Windows virtual machines act as monitored endpoints. Security events, system activity, and telemetry generated on both endpoints are collected by Wazuh agents and forwarded to the Wazuh Server. The data is then processed, indexed, analysed, and visualised through the Wazuh Dashboard to support monitoring, alerting, and incident investigation. 

<img width="1092" height="729" alt="image" src="https://github.com/user-attachments/assets/024813c5-8fee-4e53-93c0-c42266f034ae" />

## Prerequisites 

To ensure stable performance of the Wazuh SOC Lab, the host machine should meet the following minimum requirements: 

| Requirement       | Specification                                                      |
|-------------------|--------------------------------------------------------------------|
| Operating System  | Windows 11                                                         |
| Processor         | Multi-core CPU with virtualisation support (Intel VT-x or AMD-V)   |
| Memory (RAM)      | 24 GB Minimum                                                      |
| Storage           | 512 GB SSD Recommended                                             |
| Hypervisor        | VMware Workstation Pro                                             |
| Network           | Internet Connectivity                                              |

Note: The lab consists of three virtual machines running simultaneously: 

1) Wazuh Server VM 
2) Ubuntu Server VM 
3) Windows VM

Additional RAM and SSD storage will significantly improve overall performance. 

## Environment Setup: 

### Hypervisor Installation: 

VMware Workstation Pro 26H1 was downloaded from Broadcom and installed on the host system.  

 <img width="670" height="324" alt="image" src="https://github.com/user-attachments/assets/6dcd2c97-451a-49be-b885-5fd730305a4b" />

The installer integrity was verified using the published MD5 hash before proceeding with the installation

<img width="1345" height="597" alt="image" src="https://github.com/user-attachments/assets/d7b052d6-1a6d-44fd-9599-52a8dd91504b" />

### Ubuntu Server Installation 

Ubuntu Server 24.04 LTS (Noble Numbat) was installed and configured as the primary operating system for the Wazuh Server. Following the installation, SSH access was configured and connectivity was successfully verified. 

<img width="1017" height="454" alt="image" src="https://github.com/user-attachments/assets/019deb52-5b60-4d3b-a6bc-473b8141feda" />

Updated all repositories and installed the latest security updates. 

<img width="806" height="53" alt="image" src="https://github.com/user-attachments/assets/9f0685e4-4271-4a4b-96ee-6ea07456e5a8" />

### Wazuh Installation 

Installed Wazuh using the Quick Start deployment method provided by Wazuh documentation 

**curl -sO https://packages.wazuh.com/4.x/wazuh-install.sh  **

**sudo bash wazuh-install.sh -a **

After the installation completed successfully, administrative credentials for the Wazuh dashboard were generated and stored securely. 

<img width="1014" height="514" alt="image" src="https://github.com/user-attachments/assets/3bff39f2-6a1c-478c-98f9-8b1747b37526" />

### Windows VM Installation 

A Windows 10 virtual machine was created and prepared as a monitored endpoint. This system will be onboarded to Wazuh and configured with Sysmon in later phases to generate and forward security telemetry. 

- Operating System: Windows 10 
- Memory: 8 GB RAM 
- Storage: 100 GB 
- CPU: 2 vCPUs 
- Network Adapter: NAT 

<img width="879" height="513" alt="image" src="https://github.com/user-attachments/assets/b9d2f832-25f7-4fc0-8418-6c8c62a23a3c" />

### Virtual Machine Configuration 

The Wazuh Server virtual machine was configured with the following resources: 

- Operating System: Ubuntu Server 24.04 LTS 
- Memory: 8 GB RAM 
- Storage: 80 GB 
- CPU: 2 vCPUs 
- Network Adapter: NAT 

<img width="581" height="542" alt="image" src="https://github.com/user-attachments/assets/89fcdc3f-a3dc-4f31-823a-5dbe0ec5e916" />

## Outcome  

The following objectives were successfully completed: 

- VMware Workstation environment deployed 
- Ubuntu Server 24.04 LTS installed and configured 
- Wazuh Server deployed and operational 
- SSH connectivity verified 
- Windows 10 endpoint prepared for onboarding 

This completed the foundational infrastructure required for the SOC lab. The next phase focuses on onboarding the Windows endpoint, deploying Sysmon, and forwarding endpoint telemetry to the Wazuh Server for analysis and monitoring 

## Lessons Learned 

- Gained experience deploying virtual infrastructure using VMware Workstation. 
- Configured Ubuntu Server and validated remote SSH connectivity. 
- Installed and deployed a Wazuh SIEM environment. 
- Learned how endpoint telemetry will be collected and analysed within a centralised monitoring platform. 
- Established the foundation for future detection engineering and incident investigation activities. 


