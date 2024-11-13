# Azure VM Login Monitoring with Log Analytics

## Project Overview
This project demonstrates how to deploy a Virtual Machine (VM) in Microsoft Azure and utilize Microsoft Sentinel to monitor login attempts using Log Analytics. The primary objective is to track suspicious or unauthorized logins by setting up alerts based on login activity, specifically focusing on detecting successful logins that are not system-related.

## Objectives
- Deploy a Virtual Machine (VM) in Microsoft Azure.
- Set up Microsoft Sentinel and configure Log Analytics for security event monitoring.
- Create a scheduled query rule to identify and report suspicious logins in real-time.

## Tools & Technologies Used
- **Microsoft Azure**: Cloud platform for deploying and managing resources.
- **Microsoft Sentinel**: Cloud-native SIEM and SOAR solution to enable intelligent security analytics.
- **Log Analytics Workspace**: Used for monitoring and analyzing login data.
- **Windows Security Events via AMA**: Data connector for capturing security events.

## Project Setup
1. **Create a Virtual Machine**:  
   Deployed a new VM using the Microsoft Azure portal to serve as the monitored resource.

2. **Set Up Microsoft Sentinel**:
   - Created a new Sentinel workspace called `jakobird-loganalytics` to manage security events.
   - Configured a Log Analytics workspace to capture security logs and events from the VM.

3. **Configure Data Connectors**:
   - Added the data connector **"Windows Security Events via AMA"** to ingest security event data from the VM.

4. **Create Custom Log Analytics Query**:
   - Used a custom query to monitor successful login attempts that are not from the system account:
     ```kql
     SecurityEvent
     | where Account contains "success" and Account !contains "system"
     ```
   - This query is designed to filter out system-related logins and only focus on actual user logins.

5. **Scheduled Query Rule**:
   - Created a **Scheduled Query Rule** that runs every 5 minutes to check for successful user logins that match the criteria.
   - Configured the rule to trigger an alert in Azure's Threat Management system if a login event is detected.

## Key Features
- **Real-Time Login Monitoring**: Tracks and reports any successful user login attempts that are not system-related, providing a layer of security to identify unauthorized access.
- **Automated Alerting**: Utilizes Azure's Threat Management to send alerts whenever a suspicious login attempt is detected, enabling proactive response.

## Screenshots
- **Scheduled Query Rule**:
![analytics Severity](https://github.com/user-attachments/assets/c398af40-7a25-4b14-bfa7-8ad053944c12)
![full scope](https://github.com/user-attachments/assets/7a21c62e-928d-48b5-9b4f-6a6e8f5c1338)



- **Custom Query Example**:
![KQL](https://github.com/user-attachments/assets/3971cb8d-6ce5-4bb8-af01-0c567512a3fb)


- **Threat Management Alert**:
![incidents](https://github.com/user-attachments/assets/6d0a82b2-dc33-455b-8226-c73002dbf0de)


## Challenges & Learning Outcomes
- **Challenges**: Initially faced some issues with configuring the correct query to exclude system accounts, but overcame this by understanding how to use Azure Monitor Query Language (KQL).
- **Learning Outcomes**: Gained hands-on experience with Microsoft Azure, Sentinel, Log Analytics, and automated threat detection processes, enhancing my understanding of cloud security monitoring.

## Future Improvements
- **Expanded Alerting**: Plan to add integration with email or SMS alerts for critical login events.
- **Automated Response**: Consider implementing automated remediation steps (e.g., disabling accounts) in response to suspicious login attempts.

## Getting Started
To replicate this setup, you'll need access to a Microsoft Azure subscription. Follow the steps outlined in this README to deploy your VM, set up Microsoft Sentinel, and create custom alerts for login monitoring.

### Prerequisites
- Microsoft Azure account
- Basic understanding of cloud-based security monitoring

### Instructions
1. **Create a Virtual Machine** using the Azure portal.
2. **Set Up Microsoft Sentinel** by creating a new Log Analytics workspace.
3. **Add Data Connectors** to capture security events.
4. **Create Custom Queries and Alerts** in Microsoft Sentinel.

Feel free to fork this repository and experiment with your own implementations.

## License
This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
