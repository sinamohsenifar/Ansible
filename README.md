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

### Setting Up Inventory

The `inventory.conf` file should contain the groups and hosts that will be managed by Ansible. Customize this file according to your infrastructure.

### Running Playbooks

Navigate to the root of the repository and run the following command to execute a playbook:

```bash
ansible-playbook -i inventory.conf playbooks/<playbook_name>.yml
