
# VirtualBox Installation and Verification

## Installation

- Hypervisor: Oracle VM VirtualBox
- Version: 7.2.22r175245
- Package source: Oracle official APT repository
- Host OS: Zorin OS 18.1
- Host kernel: 7.0.0-42-generic

## Kernel Driver Verification

The following modules were loaded:

- vboxdrv
- vboxnetflt
- vboxnetadp

The device `/dev/vboxdrv` was present.

## Host Hardware

- CPU: Intel Core i5-9300H
- Physical cores: 4
- Logical processors: 8
- Hardware virtualization: Supported
- Host RAM: Approximately 15 GiB

## Virtual Machine Configuration

| Parameter | Value |
|---|---|
| Name | devops-assessment-vm |
| Guest OS | Ubuntu Server 24.04.5 LTS |
| CPU | 2 vCPU |
| RAM | 3072 MB |
| Virtual disk | 35 GiB |
| Disk format | VDI |
| Allocation | Dynamically allocated |
| Firmware | BIOS |

## Networking

- Adapter 1: NAT
- Adapter 2: Host-only
- Host-only network: 192.168.56.0/24
- Host address: 192.168.56.1
- Guest static address: 192.168.56.10

## Automatic Startup

VirtualBox autostart is configured through:

- `vboxautostart-service.service`
- `/etc/vbox/autostart.cfg`
- `/etc/default/virtualbox`

The VM was verified running after a host reboot.

## Verification

- VirtualBox installation: PASS
- Kernel modules: PASS
- VM startup: PASS
- Host-only network: PASS
- NAT connectivity: PASS
- VM automatic startup: PASS

## Notes

No existing host Nginx, Docker or Kubernetes services were modified
for this VirtualBox configuration.
