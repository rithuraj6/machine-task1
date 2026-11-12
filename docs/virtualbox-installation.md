# VirtualBox Installation and Verification

## Installation

- Hypervisor: Oracle VM VirtualBox
- Version: 7.2.22r175245
- Package source: Oracle official APT repository
- Host OS: Zorin OS 18.1
- Host kernel: 7.0.0-42-generic

## Installation Summary

- Five new packages installed.
- No packages removed.
- No existing packages upgraded during VirtualBox installation.
- VirtualBox installation completed successfully.

## Kernel Driver Verification

The following modules were observed loaded:

- vboxdrv
- vboxnetflt
- vboxnetadp

The device `/dev/vboxdrv` was present.

## Hardware Virtualization

- CPU: Intel Core i5-9300H
- Physical cores: 4
- Logical processors: 8
- Hardware virtualization: Supported
- Host RAM: Approximately 15.5 GiB
- Available RAM at verification: Approximately 6.9 GiB

## Planned Guest Configuration

- Guest OS: Ubuntu Server 24.04 LTS
- vCPU: 2
- RAM: 3 GiB
- Virtual disk: 35 GiB
- Disk format: VDI
- Allocation: Dynamically allocated

## Notes

- DKMS is not installed. The VirtualBox driver modules were nevertheless
  observed loaded, and `/dev/vboxdrv` was present.
- The vboxusers group was created by the VirtualBox installation.
- The current user was added to vboxusers.
- Host-only networking has not yet been configured.
- No existing host Nginx, Docker, or Kubernetes services were modified.
