# chuck-norris-yang

This Ansible playbook sets a random interface description on lab routers using NETCONF and YANG. The description is fetched from the Chuck Norris Joke API.

## Requirements

- Ansible 2.9 or later.
- Access to a Cisco router (like CSR1000V) with NETCONF enabled.

## Setup

1. Install Ansible (if not already installed).
2. Configure Your Router: Ensure NETCONF is enabled on your Cisco router.

### Configure Inventory and Variables:

- Edit inventory.yml to include the IP addresses and access credentials of your routers.
- Edit group_vars/lab_routers.yml to include the appropriate credentials and settings for your lab routers.

### Playbook Details
set_random_interface_description.yml: The main playbook that fetches a random joke and sets it as the description of a randomly selected interface on each lab router.
Running the Playbook
Execute the playbook using the following command:

``` bash
ansible-playbook -i inventory.yml set_random_interface_description.yml
```

This playbook will connect to the routers specified in inventory.yml, select a random interface on each router, fetch a random Chuck Norris joke, and set it as the interface description.

### Inventory Structure
The inventory.yml file should be structured as follows:

``` yaml
---
all:
  children:
    lab_routers:
      hosts:
        router01:
          ansible_host: [Router IP]
        # Add more routers as needed
```

### Group Variables
The group_vars/lab_routers.yml file should contain the necessary variables for the lab routers:

```yaml
ansible_user: [Username]
ansible_password: [Password]      # Lab use only, store credentials responsibly!
ansible_connection: netconf
ansible_port: 830
ansible_network_os: ios
```

### Ansible Configuration
The ansible.cfg file is used to disable host key checking:

```ini
[defaults]
host_key_checking = False
```

Note: Disable host key checking only in a safe and controlled lab environment. For production use, it's recommended to manage SSH keys properly.

## Testing
Always test your changes in a controlled environment before running the playbook in production.

## Security
Store sensitive data such as passwords and secret keys using Ansible Vault. Do not store plaintext credentials in your inventory or group_vars files.

For additional security measures and best practices, consult [Ansible's official documentation](https://docs.ansible.com/ansible/latest/index.html).

Please replace all placeholder values with actual data that corresponds to your environment. This README assumes a basic familiarity with Ansible concepts such as inventory, variables, and running playbooks.