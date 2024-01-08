# Azure Honeynet & SOC Project: Cyber Attacks in Real Time
<p align="center">
<img src="https://i.imgur.com/yMxqsuG.png" height="70%" width="70%" alt="9"/><br />

## Introduction

In this project, I create a mini honeynet, emulating real-world traffic by luring global attackers via Microsoft Azure. The primary objective of this undertaking is to illustrate optimal security measures, effective incident response strategies, and the impact of fortifying your system. This will be achieved by deliberately deploying virtual machines lacking safeguards against the public internet, enticing attackers into our environment. Subsequently, by incorporating log sources into the Log Analytics Workspace, Microsoft Sentinel will be utilized to generate attack maps, alerts, and incidents. The intention is to present metrics reflecting the state of the environment before and after fortification, derived from incidents recorded during the 24-hour monitoring period.

## Architecture Before Hardening / Security Controls
IMAGE MISSING

## Architecture After Hardening / Security Controls
IMAGE MISSING

## Azure Components and Architecture Technologies Used
- Azure Virtual Network (VNet)
- Azure Network Security Group (NSG)
- Virtual Machines (2x Windows, 1x Linux)
- Log Analytics Workspace with Kusto Query Language (KQL) Queries
- Azure Key Vault for Secure Secrets Management
- Azure Storage Account for Data Storage
- Microsoft Sentinel for Security Information and Event Management (SIEM)
- Microsoft Defender for Cloud to Protect Cloud Resources
- Windows Remote Desktop for Remote Access
- Command Line Interface (CLI) for System Management
- PowerShell for Automation and Configuration Management
- NIST SP 800-53 Security Controls (Rev 5)
- NIST SP 800-61 Incident Handling Guidance (Ref 2)

## Attack Maps Before Hardening / Security Controls
In the initial "BEFORE" metrics assessment, all resources were deployed with open exposure to the internet. The Virtual Machines had both their Network Security Groups and built-in firewalls configured with unrestricted access. Additionally, all other resources were deployed with public endpoints visible to the internet, without utilizing Private Endpoints.
<br>

 <b>This attack map showcases the number of incidents generated by leaving the Network Security Group (NSG) open. </b>
<p align="center">
<img src="https://i.imgur.com/9BzyZjq.png" height="70%" width="70%" alt="9"/><br />
 <br />
 <br />
 
 <b>This attack map highlights the incidents for syslog authentication failures experienced by the Linux server. </b>
<p align="center">
<img src="https://i.imgur.com/zBiRfzG.png" height="70%" width="70%" alt="9"/><br />
 <br />
 <br />
 
 <b>This attack map showcases RDP and SMB failures against the Window machine.</b>
<p align="center">
<img src="https://i.imgur.com/p3igr1I.png" height="70%" width="70%" alt="9"/><br />
 <br />
 <br />
 
 <b>This attack map showcases failures against the MSSQL server.</b>
<p align="center">
<img src="https://imgur.com/MESGY5F.png" height="70%" width="70%" alt="9"/><br />
 <br />
 <br />
 
 ## After Hardening Measures and Security Controls

In the "AFTER" phase, I implemented security enhancements and controls based on incidents identified during the initial 24-hour capture in the "BEFORE" stage. The goal was to strengthen the environment and bolster security against potential attackers. These enhancements comprised:

- Network Security Groups (NSGs): I enhanced NSGs by permitting only my own public IP address, while blocking all other traffic through newly established parameters.
- Built-in Firewalls: I configured built-in firewalls on virtual machines to deny access from unauthorized users.
- Private Endpoints: For other Azure resources, I replaced public endpoints with Private Endpoints, ensuring restricted access to sensitive resources like storage accounts and databases solely within the virtual network.
 
## Metrics Before Hardening / Security Controls

The following table shows the metrics we measured in our insecure environment for 24 hours:<br/>
Start Time 2024-01-06 05:03 PM<br/>
Stop Time 2024-01-07 05:03 PM

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 26,835
| Syslog                   | 7,716
| SecurityAlert            | 3
| SecurityIncident         | 345
| AzureNetworkAnalytics_CL | 3,050

## Attack Maps After Hardening / Security Controls

<br />

```All map queries actually returned no results due to no instances of malicious activity for the 24 hour period after hardening.```

 <br />

## Metrics After Hardening / Security Controls

The following table shows the metrics we measured in our environment for another 24 hours, but after we have applied security controls:<br/>
Start Time 2023-05-15 18:23:10<br/>
Stop Time	 2023-06-15 20:34:21

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 8778
| Syslog                   | 25
| SecurityAlert            | 0
| SecurityIncident         | 0
| AzureNetworkAnalytics_CL | 0

SecurityEvent: Witnessed an reduction of approximately 74.48%, minimizing potential threats.

Syslog: Achieved an decrease of around 97.33%, ensuring enhanced monitoring and threat detection capabilities.

SecurityAlert: Achieved an 100% decrease, indicating the elimination of alerts through rigorous hardening measures.

SecurityIncident: Successfully attained a 100% decrease, signifying complete prevention of security incidents.

AzureNetworkAnalytics_CL: Accomplished a 100% decrease, eliminating any potential entries and fortifying the network's resilience.

## Approach to Handling High-Priority Incidents with NIST Guidelines and Security Controls
For effective management of high-priority incidents, I adhered to NIST 800-61 (Revision 2) guidelines and implemented security controls specified in NIST SP 800-53 (Revision 5). The approach involved:

- Initiating preparations by establishing a log analytics workspace, configuring Azure Sentinel, and setting up alerts for incident detection. The implementation of NIST SP 800-53 security controls ensured a robust and secure environment.
- When incidents occurred, I categorized and assessed their severity, conducting thorough investigations into logs to distinguish false from true positives. The incident response procedures outlined in NIST 800-61 (Revision 2) guided this process, evaluating the scope of impact.
- To streamline incident response, I employed an incident response playbook aligned with NIST 800-61 (Revision 2), documenting incident details comprehensively. Relevant security controls from NIST SP 800-53 (Revision 5) guided the execution of incident response activities.
- Post-resolution, meticulous documentation of findings, steps taken, and analyses performed was undertaken for each incident. Closure involved indicating the resolution and any necessary follow-up actions while ensuring compliance with NIST SP 800-53 (Revision 5) security controls.

## Conclusion

In this project, a small-scale honeynet was set up in Microsoft Azure, and log sources were integrated into a Log Analytics workspace. Microsoft Sentinel was utilized to generate alerts and incidents based on the processed logs. Furthermore, metrics were assessed in the initially insecure environment, both before and after the implementation of security controls. The substantial decrease in security events and incidents post the application of security measures underscores their efficacy in fortifying the environment.

It's important to note that if the network's resources were heavily utilized by regular users, there could have been a likelihood of generating more security events and alerts in the 24-hour period following the implementation of security controls.
