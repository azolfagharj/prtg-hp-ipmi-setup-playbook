# Add HP IPMI Ping and Fans to PRTG - Ansible Playbook

## Version: 1.0.5  
**Author**: Alireza Zolfaghar  
**GitHub**: [azolfagharj](https://github.com/azolfagharj)  
**Email**: azolfagharj@gmail.com  
**Date**: 2024-09-10  

### Overview

This Ansible playbook helps automate the process of adding HP servers with IPMI to **PRTG Network Monitor**. It clones an existing device, updates its IP address and name, and renames key sensors such as **Ping** and **Fan Monitoring**. After that, it activates the newly cloned device.

### Prerequisites

- **Ansible**: Ensure that Ansible is installed and properly configured on your control machine.
- **PRTG API Access**: You will need the following details:
  - PRTG Server URL
  - PRTG Username
  - PRTG API Password Hash (Passhash)
  - The **Device ID** of the device you wish to clone
  - The **Group ID** where the new devices will be added

### Steps to Use

1. **Prepare a Device in PRTG**  
   Create a device in PRTG manually for one of your HP servers with IPMI and ensure that **Ping** and **Fan Monitoring** sensors are active. Make note of the **Device ID** of this device.

2. **Retrieve Group ID in PRTG**  
   Identify the **Group ID** where you want to add new devices. You can find this ID in the URL when viewing the group in PRTG.

3. **Configure the Playbook**  
   You do not need to hardcode the server name and IP in the playbook. When running the playbook, you will pass them as extra variables.

   Edit the following variables in the playbook to match your PRTG setup:

   ```yaml
   vars:
     prefix: "XXXX"          # Replace with your preferred prefix for new device names
     device_id: "XXXX"     # Replace with the ID of the device you want to clone
     group_id: "XXXX"       # Replace with the ID of the target group in PRTG
     prtg_host: "https://YOUR.PRTG.ADDRESS"  # Replace with your PRTG server address
     prtg_user: "YOURPRTGUSER"  # Replace with your PRTG admin username
     prtg_pass: "YOURPRTGPASSWORD"  # Replace with your PRTG admin password hash
4. **Run the Playbook**  
    Execute the playbook using the following command, passing the server name and IP as extra variables:
```bash
   ansible-playbook prtg-hp-ipmi.yml -e "server_ip=0.0.0.0 server_name=NAME"
