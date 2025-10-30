# Ansible Server Provisioning

Production-ready Ansible playbooks for automated server provisioning and configuration management.

## 🚀 Features

- **Multi-OS Support**: Ubuntu, Debian, CentOS, RHEL
- **Role-Based**: Modular roles for different server types
- **Security Hardening**: SSH security, firewall, user management
- **Web Server Setup**: Nginx with SSL support
- **Database Configuration**: MySQL/PostgreSQL setup
- **Monitoring Ready**: Log rotation, system monitoring

## 📁 Project Structure

```
├── playbooks/
│   └── site.yml           # Main playbook
├── roles/
│   ├── common/            # Base system configuration
│   ├── webserver/         # Nginx web server setup
│   └── database/          # Database server setup
├── inventory/
│   └── hosts             # Server inventory
├── group_vars/
│   └── all.yml           # Global variables
└── host_vars/            # Host-specific variables
```

## 🛠️ Quick Start

### Prerequisites
- Ansible 2.9+
- SSH access to target servers
- Python 3.6+ on target servers

### Setup
```bash
# Clone repository
git clone https://github.com/iammaksudul/ansible-server-provisioning.git
cd ansible-server-provisioning

# Update inventory with your servers
vim inventory/hosts

# Configure variables
vim group_vars/all.yml

# Test connectivity
ansible all -i inventory/hosts -m ping

# Run playbook
ansible-playbook -i inventory/hosts playbooks/site.yml
```

## 🎯 Playbook Execution

### Full Deployment
```bash
# Deploy all roles to all servers
ansible-playbook -i inventory/hosts playbooks/site.yml

# Deploy with verbose output
ansible-playbook -i inventory/hosts playbooks/site.yml -v

# Dry run (check mode)
ansible-playbook -i inventory/hosts playbooks/site.yml --check
```

### Specific Roles
```bash
# Only common role
ansible-playbook -i inventory/hosts playbooks/site.yml --tags common

# Only web servers
ansible-playbook -i inventory/hosts playbooks/site.yml --limit webservers

# Specific server
ansible-playbook -i inventory/hosts playbooks/site.yml --limit web1
```

## 🔧 Roles Description

### Common Role
- System updates and essential packages
- User management and SSH hardening
- Firewall configuration
- NTP and timezone setup
- Log rotation configuration

### Webserver Role
- Nginx installation and configuration
- SSL certificate setup (Let's Encrypt)
- Custom web content deployment
- Security headers configuration
- Log management

### Database Role
- MySQL/PostgreSQL installation
- Database and user creation
- Security configuration
- Backup setup
- Performance tuning

## ⚙️ Configuration

### Inventory Management
```ini
[webservers]
web1 ansible_host=192.168.1.10 nginx_server_name=example.com
web2 ansible_host=192.168.1.11 nginx_server_name=api.example.com

[databases]
db1 ansible_host=192.168.1.20 mysql_root_password=secure_password

[all:vars]
ansible_user=ubuntu
ansible_ssh_private_key_file=~/.ssh/id_rsa
```

### Variable Customization
```yaml
# group_vars/all.yml
server_timezone: "America/New_York"
enable_ssl: true
ssl_email: "admin@company.com"

# Security settings
ssh_port: 2222
allowed_ssh_users:
  - devops
  - admin

# Monitoring
enable_monitoring: true
log_retention_days: 30
```

## 🔒 Security Features

- **SSH Hardening**: Disable root login, key-only auth
- **Firewall Configuration**: UFW/iptables rules
- **User Management**: Sudo users with proper permissions
- **SSL/TLS**: Automated certificate management
- **Log Security**: Secure log rotation and retention

## 📊 Monitoring Integration

- System metrics collection
- Log aggregation setup
- Health check endpoints
- Alert configuration
- Performance monitoring

## 🚀 Production Deployment

### Environment-Specific Inventories
```bash
# Development
ansible-playbook -i inventory/dev playbooks/site.yml

# Staging
ansible-playbook -i inventory/staging playbooks/site.yml

# Production
ansible-playbook -i inventory/prod playbooks/site.yml
```

### CI/CD Integration
```yaml
# .github/workflows/deploy.yml
- name: Deploy with Ansible
  run: |
    ansible-playbook -i inventory/prod playbooks/site.yml \
      --vault-password-file vault_pass.txt
```

## 🧪 Testing

### Molecule Testing
```bash
# Install molecule
pip install molecule[docker]

# Test role
cd roles/common
molecule test
```

### Vagrant Testing
```bash
# Start test environment
vagrant up

# Run playbook
ansible-playbook -i .vagrant/provisioners/ansible/inventory/vagrant_ansible_inventory playbooks/site.yml
```

## 📝 Best Practices

- Use Ansible Vault for sensitive data
- Tag tasks for selective execution
- Implement idempotency in all tasks
- Use handlers for service restarts
- Document variables and defaults
- Test playbooks in staging first

## 🤝 Contributing

1. Fork the repository
2. Create feature branch
3. Add/modify roles and playbooks
4. Test with molecule
5. Submit pull request

## 📄 License

MIT License - see LICENSE file for details.

## 👨‍💻 Author

**Alam** - DevOps Engineer
- GitHub: [@iammaksudul](https://github.com/iammaksudul)
- Email: kh.maksudul.alam.cse@gmail.com

---

*Production-tested Ansible playbooks for enterprise server management.*
