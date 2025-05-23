# Odoo 18 Installation Script

This script provides an automated installation of Odoo 18 on Ubuntu with Python 3.12, PostgreSQL 16, and Nginx.

## Prerequisites

- Ubuntu 22.04 LTS or higher
- Sudo privileges
- Internet connection

## Configuration

Before running the script, update the following variables at the beginning of the script:

```bash
ODOO_DIR=/home/ubuntu/odoo     # Odoo installation directory
DB_USER=odoo                   # PostgreSQL user for Odoo
DB_PASSWORD=password           # PostgreSQL password
DB_HOST=localhost             # Database host
DB_PORT=5432                  # Database port
```

## What the Script Installs

- Python 3.12 from source
- Node.js 18.20.0
- PostgreSQL 16
- Odoo 18.0 from GitHub
- Nginx as reverse proxy
- Wkhtmltopdf 0.12.6.1-3

## Directory Structure

```
$ODOO_DIR/
├── python3.12/              # Python installation
├── node-v18/               # Node.js installation
├── odoo18/                 # Odoo installation
│   ├── config/             # Odoo configuration
│   ├── logs/              # Log files
│   └── addons/            # Odoo addons
├── custom_addons/
│   ├── 3rd-addons/       # Third-party addons
│   └── customs/          # Custom addons
└── .local/                # Odoo data directory
```

## Usage

1. Make the script executable:
```bash
chmod +x odoo18-setup.sh
```

2. Run the script:
```bash
./odoo18-setup.sh
```

## Services and Ports

- Odoo: http://localhost:8069
- Nginx: http://localhost:80
- PostgreSQL: localhost:5432
- Odoo Chat/Websocket: localhost:8072

## System Services

The script creates and enables the following system service:
- `odoo18.service`: Manages the Odoo server process

## Default Configurations

- Admin Password: mysupersecretpassword
- Database Name: odoo18
- Workers: 3
- Max Cron Threads: 1
- Memory Limits:
  - Soft: 768MB
  - Hard: 835MB

## Management Commands

```bash
# Check Odoo service status
sudo systemctl status odoo18

# Restart Odoo service
sudo systemctl restart odoo18

# View Odoo logs
tail -f $ODOO_DIR/logs/odoo.log

# Check Nginx configuration
sudo nginx -t

# Reload Nginx
sudo nginx -s reload
```

## Security Notes

- The script configures basic security settings
- Database listing is disabled
- Proxy mode is enabled
- HTTPS redirection is commented out by default (uncomment in Nginx config if needed)
- Session cookies are configured with SameSite=lax and Secure flags

## Support

For issues and questions, please refer to:
- [Odoo Documentation](https://www.odoo.com/documentation/18.0/)
- [PostgreSQL Documentation](https://www.postgresql.org/docs/16/index.html)
