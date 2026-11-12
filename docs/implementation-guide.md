
# Implementation Guide

## 1. Virtual Machine Provisioning

- Hypervisor: Oracle VirtualBox
- VM: devops-assessment-vm
- OS: Ubuntu Server 24.04.5 LTS
- CPU: 2 vCPU
- RAM: 3072 MB
- Storage: 35 GiB dynamically allocated VDI

VM automatic startup is configured using VirtualBox autostart.

## 2. Network Configuration

Two adapters are configured:

- NAT: DHCP on enp0s3
- Host-only: static address on enp0s8

Guest Netplan configuration:

`/etc/netplan/50-cloud-init.yaml`

Host-only address:

`192.168.56.10/24`

The NAT interface provides the default route.

## 3. SSH Management

SSH is enabled on the Ubuntu VM.

From the Zorin host:

```bash
ssh devopsadmin@192.168.56.10
```

## 4. Nginx Reverse Proxy

Nginx is installed and enabled.

Configuration file:

`/etc/nginx/sites-available/devops-assessment`

Enabled site:

`/etc/nginx/sites-enabled/devops-assessment`

Nginx listens on port 80 and forwards requests to:

`http://127.0.0.1:8000`

Configuration validation:

```bash
sudo nginx -t
sudo systemctl reload nginx
```

## 5. Python Backend

Application file:

`/opt/devops-assessment/backend/app.py`

The Python HTTP server listens on:

`127.0.0.1:8000`

It returns JSON responses containing application information,
request path, backend information and timestamp.

## 6. Backend systemd Service

Service file:

`/etc/systemd/system/devops-backend.service`

Management commands:

```bash
sudo systemctl status devops-backend
sudo systemctl restart devops-backend
sudo journalctl -u devops-backend -n 30 --no-pager
```

The service is enabled at boot.

## 7. Cloudflare Quick Tunnel

Cloudflared is installed inside the Ubuntu VM.

Service file:

`/etc/systemd/system/cloudflared-quick-tunnel.service`

The service publishes the Nginx origin:

`http://localhost:80`

The service uses systemd automatic restart.

Management commands:

```bash
sudo systemctl status cloudflared-quick-tunnel
sudo systemctl restart cloudflared-quick-tunnel
sudo journalctl -u cloudflared-quick-tunnel -n 40 --no-pager
```

The current public hostname can be found in the service journal.

Quick Tunnel hostnames are temporary and can change after restart.

## 8. External HTTPS

Cloudflare terminates public HTTPS and forwards traffic through
the tunnel to the HTTP origin.

This implementation does not install a Let's Encrypt certificate
on the Nginx origin.

## 9. Domain and DNS
A permanent hostname requires a named Cloudflare Tunnel and a
domain under the user's control. Neither has been configured
for this assessment.

## 10. Recovery

The VM, Nginx, Python backend and Cloudflare tunnel are configured
for automatic startup or restart.

The tunnel restart test was successful.
