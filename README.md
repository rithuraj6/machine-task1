# Local Machine Virtualization with Static IP and DNS Configuration

A practical DevOps infrastructure project demonstrating local machine
virtualization, persistent private networking, reverse proxy deployment,
and externally accessible HTTPS services.

## Objectives

- Virtualize a physical Linux host using Oracle VirtualBox.
- Provision Ubuntu Server 24.04 LTS.
- Configure persistent static private IP addressing.
- Establish outbound internet connectivity.
- Configure Nginx as a reverse proxy.
- Deploy a Python HTTP backend as a systemd service.
- Enable external HTTPS access using Cloudflare Quick Tunnel.
- Configure VM and service startup recovery.
- Document DNS, domain, and TLS requirements and limitations.

## Technology Stack

| Component | Technology |
|---|---|
| Host OS | Zorin OS 18.1 |
| Hypervisor | Oracle VirtualBox 7.2.22 |
| Guest OS | Ubuntu Server 24.04.5 LTS |
| VM Networking | NAT + Host-only |
| Web Server | Nginx |
| Backend | Python HTTP Server |
| Service Management | systemd |
| External HTTPS | Cloudflare Quick Tunnel |
| Version Control | Git / GitHub |

## Network Architecture

- Host-only network: `192.168.56.0/24`
- Host management address: `192.168.56.1`
- Ubuntu VM static address: `192.168.56.10`
- NAT guest address: `10.0.2.15`
- NAT gateway: `10.0.2.2`

## Implementation Status

- [x] Physical host infrastructure audit
- [x] VirtualBox installation and verification
- [x] Ubuntu Server VM provisioning
- [x] VM CPU, RAM and storage configuration
- [x] Persistent static private IP configuration
- [x] NAT internet connectivity
- [x] Host-only SSH management
- [x] VM automatic startup
- [x] Nginx reverse proxy
- [x] Python backend systemd service
- [x] External HTTPS access using Cloudflare Quick Tunnel
- [x] Tunnel systemd service and restart recovery
- [x] Local and external HTTP verification
- [ ] Custom domain and DNS A record
- [ ] Router port forwarding
- [ ] Let's Encrypt certificate on custom domain
- [ ] Certbot automatic renewal validation

## Important Implementation Notes

Cloudflare Quick Tunnel provides temporary public HTTPS access without
requiring router administration or a purchased domain.

The generated `trycloudflare.com` hostname is temporary and may change
when the tunnel restarts. Cloudflare terminates public HTTPS at its edge.

Custom domain DNS records, direct router port forwarding, and a
Let's Encrypt certificate installed on the Nginx origin are not
implemented in this environment.

## Documentation

See `docs/` for architecture, networking, installation, implementation,
troubleshooting, and verification details.

See `evidence/` for assessment screenshots.
