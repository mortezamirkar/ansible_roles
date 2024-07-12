
```markdown
# Ansible Role: LAMP Setup with Nginx, PHP 8.2, MySQL, and Redis

This Ansible role sets up a LAMP stack (Linux, Nginx, MySQL, PHP) with PHP 8.2 and Redis on a server. It handles the installation and basic configuration of Nginx, MySQL, PHP, and Redis.

## Requirements

- Ansible 2.9 or higher
- Supported distributions: Debian-based systems (e.g., Ubuntu)

## Role Variables

The following variables can be customized to suit your needs. They are located in `defaults/main.yml`:

```yaml
php_version: "8.2"
mysql_root_password: "your_root_password"
php_extensions:
  - php8.2
  - php8.2-mysql
  - php8.2-redis
  - php8.2-cli
  - php8.2-dom
  - php8.2-common
  - php8.2-zip
  - php8.2-gd
  - php8.2-mbstring
  - php8.2-curl
  - php8.2-xml
  - php8.2-bcmath
  - php8.2-redis
  - php8.2-intl
  - php8.2-gmp
  - php8.2-ctype
  - php8.2-pdo
  - php8.2-tokenizer
  - php8.2-fpm
```

## Dependencies

None.

## Example Playbook

Below is an example of how to use this role in a playbook. This example assumes you have an inventory file named `hosts`.

### Inventory File (`hosts`)

```ini
[all:children]
lamp_servers

[lamp_servers]
server_ip ansible_host=server_ip
```

Replace `server_ip` with the actual IP address or hostname of your server.

### Playbook (`playbook.yml`)

```yaml
---
- name: Set up LAMP stack with Nginx, PHP 8.2, MySQL, and Redis
  hosts: lamp_servers
  become: yes
  roles:
    - lamp_setup
```

## Running the Playbook

To run the playbook, use the following command:

```bash
ansible-playbook -i hosts playbook.yml
```

## Role Tasks

### Update and Upgrade Packages

The role updates the package list and upgrades all installed packages to their latest version.

### Install Common Dependencies

Installs common dependencies required for the setup.

### Install PHP and Extensions

Adds the PHP repository and installs PHP 8.2 along with the specified extensions.

### Install and Configure MySQL

Adds the MySQL APT repository, installs the MySQL server, sets the root password, and secures the installation.

### Install and Configure Nginx

Installs Nginx, starts the service, and creates a default server block configuration for serving PHP applications.

### Install and Configure Redis

Installs Redis, starts the service, and ensures it is enabled to start on boot.

### Handlers

Handlers are included to reload Nginx and restart PHP-FPM when configuration changes are made.

## Testing PHP Installation

A test PHP file (`info.php`) is created in the web root to verify the PHP installation. You can access it via `http://your_server_ip/info.php`.

## License

MIT

## Author Information

This role was created by [Your Name].

```

This `README.md` file provides a clear and concise overview of the Ansible role, including installation, usage, and customization instructions. You can adjust the content to fit your specific needs and include additional information if necessary.