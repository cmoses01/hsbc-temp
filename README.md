# vCenter Configuration Assurance

This project provides automated configuration assurance for vCenter resources using Ansible. It's designed for the Distributed Compute team to validate and maintain consistent configurations across VMware infrastructure components.

## Overview

The configuration assurance framework currently supports ESXi hosts and is designed to be extensible for all vCenter resources including:
- ESXi Hosts (currently implemented)
- Virtual Machines (planned)
- Datastores (planned)
- Networks and Port Groups (planned)
- Resource Pools (planned)
- vApps (planned)

## Features

- **Resource Discovery**: Automatically discovers vCenter resources (currently ESXi hosts)
- **Configuration Validation**: Validates host configurations against defined standards
- **Configuration Tests**: Runs comprehensive configuration assurance tests on hosts
- **Reporting**: Generates assurance reports for compliance tracking
- **Check Mode**: Validates configurations without making changes

## Prerequisites

- Ansible 2.9 or higher
- Python 3.6 or higher
- VMware community collection (`community.vmware`)
- Access to vCenter Server with appropriate permissions

## Installation

1. Install required Ansible collections:
```bash
ansible-galaxy collection install community.vmware
```

2. Clone this repository:
```bash
git clone <repository-url>
cd hsbc-temp
```

3. Set environment variables:
```bash
export VCENTER_USERNAME="administrator@vsphere.local"
export VCENTER_PASSWORD="your-password"
```

## Configuration

Update the default variables in `roles/vmware-host-config-assurance/defaults/main.yml`:

- `vcenter_hostname`: Your vCenter server hostname
- `datacenter_name`: Target datacenter name
- `ntp_servers`: List of NTP servers for validation
- `check_mode`: Set to `true` for validation only, `false` for enforcement

## Usage

Run the configuration assurance playbook:

```bash
ansible-playbook config_assurance.yml
```

The playbook performs the following steps:
1. Discovers vCenter resources from the specified datacenter (currently ESXi hosts)
2. Runs configuration assurance tests on each discovered resource
3. Generates assurance reports

## Project Structure

```
├── config_assurance.yml          # Main playbook
├── roles/
│   └── vmware-host-config-assurance/
│       ├── defaults/main.yml      # Default variables
│       ├── tasks/
│       │   ├── main.yml          # Main task orchestration
│       │   ├── discover_hosts.yml # Resource discovery logic (hosts)
│       │   ├── ntp_check.yml     # Configuration validation tests
│       │   └── report_assurance_result.yml # Reporting
│       ├── handlers/main.yml     # Event handlers
│       ├── vars/main.yml         # Role variables
│       └── meta/main.yml         # Role metadata
```

## Extending the Framework

To add new configuration checks:

1. Create a new task file in `roles/vmware-host-config-assurance/tasks/`
2. Include the task in `tasks/main.yml`
3. Add relevant variables to `defaults/main.yml`
4. Update this README with the new functionality

## Security Considerations

- Store sensitive credentials as environment variables
- Use vault encryption for production deployments
- Ensure proper vCenter permissions are configured
- Review and validate all configuration changes before enforcement

## Contributing

Branch flow: feature → develop → main

1. Create a feature branch from develop
2. Make your changes
3. Test thoroughly in a lab environment
4. Submit a pull request to develop branch
5. After review, changes will be merged to main

## Support

For issues or questions, contact the Distributed Compute team.

## License

Internal use only - HSBC Distributed Compute Team