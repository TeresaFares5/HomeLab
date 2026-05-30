# Teresa's HomeLab

A self-hosted Ubuntu home server project built from scratch to host personal websites, dashboards, backup monitoring, Docker apps, and remote-access services.

This project is designed as a practical home lab for learning Linux server administration, Docker, reverse proxying, remote access, backups, monitoring, and self-hosted web services.

![Dashboard Screenshot](images/dashboard.png)

---

## Overview

This HomeLab runs on an Ubuntu server and provides a central dashboard for the services I host. It includes remote access, public subdomains, Docker-based apps, a portfolio website, service health checks, and backup status monitoring.

The goal of this setup is to create a reliable personal server environment where I can host projects, test infrastructure ideas, and build real-world IT skills.

---

## What I Set Up

### Ubuntu Server

- Installed and configured Ubuntu Server as the main operating system.
- Connected the server to Wi-Fi during setup.
- Configured remote access so the server can be managed without needing a monitor or keyboard.
- Confirmed services can automatically start again after reboot.
- Set up SSH access for command-line administration.
- Used terminal tools such as `nano`, `systemctl`, `docker compose`, and Linux service commands.

---

### Remote Access

Remote access was configured so the server can be managed from another device.

#### Tailscale

- Installed and configured Tailscale for secure private remote access.
- Used Tailscale to connect to the server over a private VPN-style network.
- Confirmed Tailscale starts automatically after reboot.
- Used Tailscale IPs for local/private access to services.

#### SSH

- Enabled SSH access to the Ubuntu server.
- Used SSH to manage files, services, Docker containers, and configuration remotely.

---

### Cloudflare Tunnel

Cloudflare Tunnel was configured to expose selected services publicly without opening router ports.

- Installed and configured `cloudflared`.
- Created a systemd service for Cloudflare Tunnel.
- Configured the tunnel to run automatically after reboot.
- Used Cloudflare DNS/subdomains to route public URLs to internal services.
- Troubleshot Cloudflare tunnel issues including local service availability and systemd service configuration.

Example service configuration checked:

```ini
[Unit]
Description=cloudflared
After=network-online.target
Wants=network-online.target

[Service]
TimeoutStartSec=15
Type=notify
ExecStart=/usr/bin/cloudflared --no-autoupdate --config /etc/cloudflared/config.yml tunnel run
Restart=on-failure
RestartSec=5s

[Install]
WantedBy=multi-user.target
```

---

### Docker and Docker Compose

Docker was used to run services in containers.

- Installed Docker and Docker Compose.
- Created dedicated folders for different apps.
- Used `docker-compose.yml` files to define services.
- Restarted and checked containers from the terminal.
- Used Docker to host dashboard and app services.
- Used Dockge as a web interface for managing Docker Compose stacks.

Useful commands used during setup:

```bash
docker ps
sudo docker compose up -d
sudo docker compose down
sudo docker compose restart
sudo docker compose logs -f
```

---

## Dashboard

A central dashboard was created to display the hosted services and server-related information.

The dashboard acts as the main landing page for the HomeLab and includes links/status cards for apps and websites.

### Dashboard Features

- App/service cards.
- Links to hosted services.
- Health/status indicators.
- Backup status card.
- Website card for the portfolio.
- Dockge health card.
- Clean visual interface for accessing everything from one place.

### Services Added to the Dashboard

- Portfolio website.
- Dockge.
- Backup status.
- Other self-hosted services as they are added.

---

## Portfolio Website Hosting

A personal portfolio website was added to the HomeLab.

- Hosted the portfolio on the server.
- Connected the website to the dashboard.
- Fixed server-side display issues where only the CSS gradient was showing.
- Confirmed the website loaded correctly after troubleshooting.
- Added the website as a dashboard card.
- Planned use of the website favicon as the dashboard icon.

---

## Dockge

Dockge was set up to manage Docker Compose stacks from a web interface.

- Installed Dockge using Docker Compose.
- Confirmed Dockge works locally.
- Connected Dockge to the dashboard.
- Configured a public Cloudflare subdomain for Dockge.
- Troubleshot local and public access issues.
- Confirmed Dockge health status appears on the dashboard.

Example public URL format:

```text
dockge.example.com
```

---

## Backup System

A backup system was configured for the HomeLab.

### GitHub Backup Repository

Backups are pushed to a GitHub repository:

```text
https://github.com/TeresaFares5/HomeLabBackups.git
```

### Backup Features

- Created a backup workflow for important HomeLab files.
- Connected the backup system to GitHub.
- Added backup status output to the dashboard.
- Created a status JSON file to display backup information.
- Added a dashboard card showing backup status.
- Tested running backups manually.

### Backup Status

The dashboard was configured to show backup status from a JSON file.

Example status file path:

```text
/status/backup-status.json
```

The backup status card can show information such as:

- Last backup date/time.
- Backup success/failure state.
- Backup destination.
- Repository status.

### Manual Backup Test

Backups can be manually tested from the server using the backup script/command created during setup.

Example workflow:

```bash
cd ~/homelab
./backup.sh
```

---

## System Services and Auto Start

Important services were configured to run automatically after reboot.

Configured services include:

- Tailscale.
- SSH.
- Cloudflare Tunnel.
- Docker.
- Docker containers managed with Docker Compose.
- Dockge.
- Hosted dashboard and website services.

Useful service commands:

```bash
sudo systemctl status cloudflared
sudo systemctl restart cloudflared
sudo systemctl enable cloudflared
sudo systemctl status tailscaled
sudo systemctl status ssh
```

---

## Reboot and Service Checks

The server can be rebooted from the terminal:

```bash
sudo reboot
```

After reboot, services can be checked with:

```bash
systemctl status ssh
systemctl status tailscaled
systemctl status cloudflared
docker ps
```

---

## Skills Practised

This HomeLab helped me practise real-world infrastructure and support skills, including:

- Linux server setup.
- Ubuntu Server administration.
- SSH remote management.
- Tailscale remote access.
- Cloudflare Tunnel configuration.
- DNS and public subdomain routing.
- Docker and Docker Compose.
- Docker stack management with Dockge.
- Web hosting.
- Dashboard setup and customisation.
- Backup automation.
- GitHub repository backups.
- JSON status monitoring.
- Troubleshooting local and public service access.
- Systemd service management.
- Server reboot testing.
- Service health checks.

---

## Technologies Used

- Ubuntu Server
- Linux CLI
- SSH
- Tailscale
- Cloudflare Tunnel
- Docker
- Docker Compose
- Dockge
- GitHub
- HTML
- CSS
- JavaScript
- JSON
- systemd

---

## Current Status

The HomeLab currently has:

- A working Ubuntu server.
- Remote access through Tailscale and SSH.
- Public access through Cloudflare Tunnel.
- A central dashboard.
- A hosted portfolio website.
- Dockge for Docker Compose management.
- GitHub-based backups.
- Dashboard backup status monitoring.
- Services configured to start after reboot.

---

## Future Improvements

Planned improvements include:

- Add more services to the dashboard.
- Add server CPU, RAM, disk, and uptime stats.
- Add last reboot time.
- Add a safe reboot button for the server.
- Add more automated health checks.
- Improve backup reporting.
- Add alerting for failed backups or offline services.
- Document each service in more detail.

---

## Purpose

This HomeLab is a personal learning project that demonstrates hands-on experience with server administration, self-hosting, networking, automation, backups, and web hosting.

It shows that I can build, troubleshoot, document, and maintain a small infrastructure environment from scratch.
