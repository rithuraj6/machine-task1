# Local Machine Virtualization with Static IP and DNS

A practical DevOps infrastructure project demonstrating the
virtualization of a physical Linux machine and deployment of
an externally accessible Ubuntu Server environment.

## Objectives

- Configure a local hypervisor.
- Provision Ubuntu Server as a virtual machine.
- Configure persistent static private IP addressing.
- Establish LAN and external connectivity.
- Configure domain and DNS resolution.
- Deploy Nginx as a reverse proxy.
- Enable HTTPS using Let's Encrypt and Certbot.
- Implement automatic certificate renewal.
- Validate infrastructure recovery and connectivity.

## Technology Stack

- Host OS: Zorin OS 18.1
- Hypervisor: KVM/QEMU
- VM Management: libvirt / virt-manager
- Guest OS: Ubuntu Server 24.04 LTS
- Web Server: Nginx
- SSL: Let's Encrypt / Certbot
- Version Control: Git / GitHub

## Implementation Status

- [x] Physical host infrastructure audit
- [ ] Hypervisor configuration
- [ ] Ubuntu Server VM provisioning
- [ ] Static IP configuration
- [ ] LAN connectivity
- [ ] External connectivity
- [ ] Domain and DNS
- [ ] Nginx reverse proxy
- [ ] HTTPS and SSL automation
- [ ] Verification and documentation

## Documentation

See the `docs/` directory for infrastructure documentation.