
# Infrastructure Architecture

## Hypervisor

Oracle VM VirtualBox

## Host

- Hardware: ASUS ROG Strix G531GT
- OS: Zorin OS 18.1
- CPU: Intel Core i5-9300H
- RAM: 15 GiB

## Guest

- OS: Ubuntu Server 24.04 LTS
- vCPU: 2 (proposed)
- RAM: 3 GiB (proposed)
- Storage: 35 GiB QCOW2 is not used;
  VirtualBox native VDI format will be used.

## Virtualization Components

- Hypervisor: Oracle VM VirtualBox
- Management: VirtualBox Manager
- CLI: VBoxManage
- Guest Additions: Only if required

## Networking

Preferred:
- Bridged Adapter over Wi-Fi, subject to testing.

Fallback:
- NAT with static guest configuration
  and controlled port forwarding.

## Web Infrastructure

- Nginx
- Certbot
- Let's Encrypt
- UFW

## Version Control

Git and GitHub.

## Security

- No production credentials.
- No unnecessary exposed ports.
- Private keys excluded from Git.
- Host and guest services remain isolated.
