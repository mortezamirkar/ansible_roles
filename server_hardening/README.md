
```markdown
# Ansible Role: Server Hardening

This Ansible role performs server hardening by configuring iptables for enhanced security and setting a custom SSH banner. The role includes tasks to secure the server by configuring firewall rules, disabling unnecessary services, and setting up a secure SSH configuration.

## Requirements

- Ansible 2.9 or higher
- Supported distributions: Debian-based systems (e.g., Ubuntu)

## Role Variables

The following variables can be customized to suit your needs. They are located in `defaults/main.yml`:

```yaml
# Default SSH banner message
ssh_banner_message: "Authorized access only. All activity may be monitored and reported."

# List of allowed ports
iptables_allowed_ports:
  - 22  # SSH
  - 80  # HTTP
  - 443 # HTTPS

# List of packages to install for hardening
hardening_packages:
  - ufw
  - fail2ban
```

## Dependencies

None.

## Example Playbook

Below is an example of how to use this role in a playbook. This example assumes you have an inventory file named `hosts`.

### Inventory File (`hosts`)

```ini
[all:children]
hardened_servers

[hardened_servers]
server_ip ansible_host=server_ip
```

Replace `server_ip` with the actual IP address or hostname of your server.

### Playbook (`playbook.yml`)

```yaml
---
- name: Harden servers with iptables and custom SSH banner
  hosts: hardened_servers
  become: yes
  roles:
    - server_hardening
```

## Running the Playbook

To run the playbook, use the following command:

```bash
ansible-playbook -i hosts playbook.yml
```

## Role Tasks

### Update and Upgrade Packages

The role updates the package list and upgrades all installed packages to their latest version.

### Install Hardening Packages

Installs necessary packages for hardening, including UFW and Fail2Ban.

### Configure iptables

Sets up iptables rules to allow only specific ports and drop all other traffic. The default allowed ports are SSH (22), HTTP (80), and HTTPS (443), but you can customize this list using the `iptables_allowed_ports` variable.

### Configure UFW

Sets up UFW (Uncomplicated Firewall) with default deny policies and allows only the specified ports.

### Configure Fail2Ban

Installs and configures Fail2Ban to protect against brute-force attacks.

### Set Custom SSH Banner

Configures a custom SSH banner message to be displayed upon login. The default message can be customized using the `ssh_banner_message` variable.

### Disable Unnecessary Services

Disables and stops any unnecessary services to reduce the attack surface.

### Secure SSH Configuration

Configures SSH for enhanced security by:
- Disabling root login
- Allowing only specific users
- Setting a custom banner message

## License

MIT

## Author Information

This role was created by [morteza amirkar].

## Additional Information

### Testing SSH Configuration

After running the playbook, you can test the SSH configuration by attempting to log in to the server and verifying that the custom banner message is displayed.

### Firewall Rules Verification

You can verify the iptables rules by running the following command on the target server:

```bash
sudo iptables -L
```

### Fail2Ban Status

You can check the status of Fail2Ban by running:

```bash
sudo fail2ban-client status
```

```

This `README.md` file provides a clear and concise overview of the server hardening Ansible role, including installation, usage, and customization instructions. You can adjust the content to fit your specific needs and include additional information if necessary.