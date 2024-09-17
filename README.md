# Wireguard-UI-Ansible

Ansible role for automated deployment of WireGuard Easy with SSL Nginx termination.

## Table of Contents

- [Overview](#overview)
- [Features](#features)
- [Prerequisites](#prerequisites)
- [Installation](#installation)
- [Usage](#usage)
- [Configuration](#configuration)
  - [Default Variables](#default-variables)
  - [Password Hash](#password-hash)
  - [SSL Management](#ssl-management)
- [Contributing](#contributing)

## Overview

This Ansible role automates the deployment process of [WireGuard Easy](https://github.com/wg-easy/wg-easy), providing a seamless setup with SSL Nginx termination.

## Features

| Feature | Description |
|---------|-------------|
| Deployment | Fully automated using Ansible |
| SSL | Nginx termination with self-signed certificate |
| UI Password | Secured with bcrypt hash |
| Base Project | WireGuard Easy |

## Prerequisites

- Ansible installed on your local machine
- Target server with SSH access
- Basic knowledge of Ansible and WireGuard

## Installation

1. Clone this repository:
```bash
git clone https://github.com/your-username/wireguard-ui-ansible.git
```
2. Change into the project directory:
```bash
cd wireguard-ui-ansible
```

## Usage

1. Update the `inventory.yml` file with your target server details.
2. Run the Ansible playbook:
```bash
ansible-playbook -i inventory.yml playbook.yml
```

## Configuration

### Default Variables

The following table describes the default variables used in this Ansible role:

| Variable Name | Default Value | Description |
|---------------|---------------|-------------|
| `base_deploy_path` | '/data' | Server path for deployment compose and ssl files | 
| `wireguard_deploy_path` | '{{ base_deploy_path }}/wireguard' | Path to deploy WireGuard |
| `wireguard_deploy_config` | '{{ wireguard_deploy_path }}/config' | Path to deploy WireGuard configurations |
| `wireguard_image_tag` | '14' | WireGuard Easy container tag |
| `wireguard_image` | 'ghcr.io/wg-easy/wg-easy:{{ wireguard_image_tag }}' | WireGuard Docker Image |
| `wireguard_port` | '443' | The port WireGuard will listen on |
| `wireguard_default_dns` | '8.8.8.8,8.8.4.4' | DNS server for WireGuard clients |
| `wireguard_mtu` | '1420' | MTU size | 
| `wireguard_persistent_keepalive` | '25' | Keep Alive Period for connection | 
| `wireguard_internal_subnet` | '10.13.13.0' | Subnet for VPN IPs |
| `wireguard_ui_stats` | 'true' | Enable UI user statistic | 
| `wireguard_ui_password_hash` | '$$2a$$12$$18Vzv5wrneprdOj4RhTaTOi0TXuWj30YwPMrwrvPAkjqav4BTt3nG' | Hashed Admin UI password | 
| `wg_nginx_path` | '{{ base_deploy_path }}/nginx' | Local path for Nginx deploy |
| `wg_nginx_conf_path` | '{{ wg_nginx_path}}/conf.d' | Local path for Nginx configuration |
| `wg_nginx_logs_path` | '{{ wg_nginx_path}}/logs' | Local path for Nginx logs |
| `wg_nginx_cert_path` | '{{ wg_nginx_path}}/ssl' |  Local path for Nginx certificates |

To override these defaults, you can set these variables in your playbook or inventory file.

### Password Hash

To secure your admin access, generate a bcrypt hash for your UI password:

1. Refer to the [official WireGuard Easy guide](https://github.com/wg-easy/wg-easy/blob/master/How_to_generate_an_bcrypt_hash.md) for hash generation.
2. Apply the new hash in the Ansible variables to secure your admin access.

**Important:** Do not use default values in public/production installations.

### SSL Management

The role includes a self-signed certificate by default. For production use, replace it with a valid trusted certificate.

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

