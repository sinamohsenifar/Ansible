# Ansible Playbooks and Roles

This repository contains various Ansible playbooks and roles for automating infrastructure and application management. Below you'll find instructions on how to use these playbooks and roles.

## Repository Structure

- **playbooks/**: Contains individual playbooks for different tasks and environments.
- **roles/**: Includes reusable Ansible roles that are used within the playbooks.
- **inventory.conf**: Inventory file defining the hosts and groups.

## Usage

### Prerequisites

- Ensure Ansible is installed on your control machine.
- Clone this repository to your local machine.
- This ansibles uses ssh key to login to servers. make sure you added your ssh-key to every machines with this command:
    
    ```bash
    ssh-copy-id root@<ip-address>
    ```
### Setting Up Inventory

The `inventory.conf` file should contain the groups and hosts that will be managed by Ansible. Customize this file according to your infrastructure.

### Running Playbooks

- Navigate to the root of the repository and run the following command to execute a playbook:

    ```bash
    ansible-playbook -i inventory.conf playbooks/<playbook_name>.yml
    ```




## 1) Manage DNS SERVER With Ansible

### notes:
- Every time you changed zone files you can run it again
- you must add your host name and their ip to zone file. 

### Main Zone Configuration
    
Playbook: playbooks/config_main_zone.yml
    
- Usage: Configures DNS settings for the main zone servers, this server is like bridge between all dns servers and zones.
    Command:

    ```bash
    ansible-playbook -i inventory.conf playbooks/config_main_zone.yml
    ```

### Zone One Configuration

Playbook: playbooks/config_zone_one.yml
- Usage: Configures DNS settings for the first set of zone servers.
    Command:

    ```bash
    ansible-playbook -i inventory.conf playbooks/config_zone_one.yml
    ```

### Zone Two Configuration

Playbook: playbooks/config_zone_two.yml
- Usage: Configures DNS settings for the second set of zone servers.
    Command:

    ```bash
    ansible-playbook -i inventory.conf playbooks/config_zone_two.yml
    ```

### Zone Three Configuration

Playbook: playbooks/config_zone_three.yml
- Usage: Configures DNS settings for the third set of zone servers.
    - **Command**:
     ```bash
     ansible-playbook -i inventory.conf playbooks/config_zone_three.yml
     ```


## 2) Install list of packages in server with ansible 

   - **Playbook**: playbooks/install-package.yml
   - **Usage**: Installs specified packages on a target host group using a dedicated role.
   - **Command**:
     ```bash
     ansible-playbook -i inventory.conf playbooks/install-packages.yml -e "host_group=kafka packages=python3,bind"
     ```

Details: This playbook runs the install-packages role to install the packages listed in the packages variable on the hosts specified in the host_group.


## 3) Change Password
   - **Playbook**: playbooks/change-password.yml
   - **Note**: this playbook will change all servers password and save them in directory of role change-password/passwords/<date-time-format>
   - **Usage**: Changes the password for a specified user on target hosts.
   - **Command**:
     ```bash
     ansible-playbook -i inventory.conf playbooks/change-password.yml
     ```

## 4) Set Hostnames
   - **Playbook**: `playbooks/set-hostnames.yml`
   - **Usage**: Sets the hostname on target hosts without requiring a reboot.
   - **Note**: this playbook will use hostname of server from inventory file.
   - **Command**: 
     ```bash
     ansible-playbook -i inventory.conf playbooks/set-hostnames.yml
     ```

## 5) Set NTP
   - **Playbook**: `playbooks/set-ntp.yml`
   - **Usage**: Configures NTP settings on target hosts to ensure time synchronization.
   - **Command**: 
     ```bash
     ansible-playbook -i inventory.conf playbooks/set-ntp.yml
     ```


## 6) Install and Config Kafka servers and kraft with Ansible
   - **Playbook**: `playbooks/install-kafka.yml`
   - **Usage**: Configures Kafka servers with Kraft.
   - **Command**: 
     ```bash
     ansible-playbook -i inventory.conf playbooks/install-kafka.yml
     ```
