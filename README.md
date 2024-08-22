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

Navigate to the root of the repository and run the following command to execute a playbook:

    ```bash 
    ansible-playbook -i inventory.conf playbooks/<playbook_name>.yml
    ```




## Manage DNS SERVER With Ansible
    ### notes:
    - Every time you changed zone files you can run it again
    - you must add your host name and their ip to zone file. 

### Main Zone Configuration
    Playbook: playbooks/config_main_zone.yml
    Usage: Configures DNS settings for the main zone servers, this server is like bridge between all dns servers and zones.
    Command:

    ```bash 
    ansible-playbook -i inventory.conf playbooks/config_main_zone.yml
    ```

### Zone One Configuration

    Playbook: playbooks/config_zone_one.yml
    Usage: Configures DNS settings for the first set of zone servers.
    Command:

    ```bash 
    ansible-playbook -i inventory.conf playbooks/config_zone_one.yml
    ```

### Zone Two Configuration

    Playbook: playbooks/config_zone_two.yml
    Usage: Configures DNS settings for the second set of zone servers.
    Command:

    ```bash 
    ansible-playbook -i inventory.conf playbooks/config_zone_two.yml
    ```

### Zone Three Configuration

    Playbook: playbooks/config_zone_three.yml
    Usage: Configures DNS settings for the third set of zone servers.
    Command:

    ```bash 
    ansible-playbook -i inventory.conf playbooks/config_zone_three.yml
    ```


## Install list of packages in server with ansible 

### Install Packages Using a Role

    Playbook: playbooks/install-package.yml
    Usage: Installs specified packages on a target host group using a dedicated role.
    Command:

    ```bash 
    ansible-playbook -i inventory.conf playbooks/installpackage.yml -e "host_group=kafka packages=python3,bind"
    ```

    Details: This playbook runs the install_packages_role to install the packages listed in the packages variable on the hosts specified in the host_group.