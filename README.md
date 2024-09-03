# Azure-SOC-Lab

# Building a SOC + Honeynet in Azure 
![image](https://github.com/user-attachments/assets/b1275282-b097-4dfc-8fca-6a4a9427f7d0)


## Introduction

In this project, I built a honeynet consisting of two virtual machines in Azure and ingested logs from various resources into Log Analytics workspace. Those logs were used by Microsoft Sentinel to build attack maps, trigger alerts, and create incidents. Security metrics were measured in the insecure environment for 24 hours. During and after the 24 hours I would respond to alerts by checking if they were true positives. The metrics shown based on the project will be: 

- SecurityEvent (Windows Event Logs)
- Syslog (Linux Event Logs)
- SecurityAlert (Log Analytics Alerts Triggered)
- SecurityIncident (Incidents created by Sentinel)
- AzureNetworkAnalytics_CL (Malicious Flows allowed into our honeynet)

## Architecture Before Hardening / Security Controls
![image](https://github.com/user-attachments/assets/f1a56169-938b-46e6-8e3a-01b03de312fe)

## Architecture After Hardening / Security Controls
![image](https://github.com/user-attachments/assets/21bb7694-0278-4dfd-909f-4f571430b507)

The architecture of the honeynet in Azure consists of the following components:

- Virtual Network (VNet)
- Network Security Group (NSG)
- Virtual Machines (1 windows, 1 linux)
- Log Analytics Workspace
- Azure Key Vault
- Azure Storage Account
- Microsoft Sentinel

All resources deployed were exposed to the internet. The Virtual Machines had both their Network Security Groups and built-in firewalls wide open, and all other resources were deployed with public endpoints visible to the Internet. 

After exposing the virtual machines for 24 hours, Network Security Groups were hardened by blocking ALL traffic with the exception of my admin workstation, and all other resources were protected by their built-in firewalls as well as Private Endpoint. 

## Attack Maps Before Hardening / Security Controls

![image](https://github.com/user-attachments/assets/d07e9db8-3e7a-4cbd-994b-e6e181764b63)
![image](https://github.com/user-attachments/assets/93ab5753-323b-4ebf-a62c-66f45dab9f7e)
![image](https://github.com/user-attachments/assets/76ef43be-a9e6-4d96-8df2-ffdef30f358e)

## Metrics Before Hardening / Security Controls

Metrics of insecure environment for 24 hours:<br>
Start Time 8/30/2024, 10:01:46.303 PM<br>
End Time 8/31/2024, 10:01:46.303 PM<br>

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 15494
| Syslog                   | 6112
| SecurityAlert            | 7
| SecurityIncident         | 221
| AzureNetworkAnalytics_CL | 1579

## Attack Maps Before Hardening / Security Controls

```All map queries returned no results due to no instances of malicious activity for the 24 hour period after hardening.```

## Metrics After Hardening / Security Controls

Metrics of secure environment after applying security contorls for 24 hours:<br>
Start Time 9/1/2024, 12:21:54.158 PM<br>
End Time	9/2/2024, 12:21:54.158 PM<br>

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 4617
| Syslog                   | 21
| SecurityAlert            | 0
| SecurityIncident         | 0
| AzureNetworkAnalytics_CL | 0

## Conclusion

In this project, a mini honeynet was made in Microsoft Azure and log sources were integrated into a Log Analytics workspace. Microsoft Sentinel was implemented to trigger alerts and create incidents based on custom rules made with KQL. Additionally, metrics were measured in the insecure environment before security controls were applied, and then again after implementing security measures. Security events and incidents were drastically reduced after the security controls were applied, demonstrating their effectiveness.

It is worth noting that if the resources within the network were heavily utilized by regular users, it is likely that more security events and alerts may have been generated within the 24-hour period following the implementation of the security controls.
