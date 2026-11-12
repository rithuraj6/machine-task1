# Physical Host Infrastructure Audit

**Project:** Local Machine Virtualization with Static IP and DNS Configuration  
**Audit Date:** 12 November 2026  
**Status:** Completed

## 1. Host Information

| Parameter | Value |
|---|---|
| Manufacturer | ASUSTeK COMPUTER INC. |
| Model | ASUS ROG Strix G531GT |
| Operating System | Zorin OS 18.1 |
| Base Distribution | Ubuntu 24.04 Noble |
| Architecture | x86_64 |
| Kernel | Linux 7.0.0-42-generic |

## 2. CPU and Virtualization

| Parameter | Value |
|---|---|
| Processor | Intel Core i5-9300H |
| Physical Cores | 4 |
| Logical CPUs | 8 |
| Hardware Virtualization | Intel VT-x |
| KVM Device | /dev/kvm |
| KVM Module | kvm_intel |
| QEMU | 8.2.2 |

Hardware-assisted virtualization is supported and active.

## 3. Memory

| Parameter | Value |
|---|---:|
| Total RAM | Approximately 15 GiB |
| Available RAM at audit | Approximately 7 GiB |
| Swap | 8 GiB |

VM memory allocation will be conservative to protect host performance.

## 4. Storage

| Parameter | Value |
|---|---|
| Root Filesystem | ext4 |
| Root Capacity | 232 GiB |
| Used | 112 GiB |
| Available | 109 GiB |

The available storage is sufficient for the proposed Ubuntu Server VM.

## 5. Virtualization Software

| Component | Audit Result |
|---|---|
| QEMU | Installed |
| KVM | Installed and loaded |
| libvirt | Not installed |
| virt-manager | Not installed |
| virsh | Not installed |

The next step is to install and configure libvirt and its management tools.

## 6. Network

- Primary interface: wlo1
- Adapter: Intel Wireless-AC 9560
- Driver: iwlwifi
- Connection type: Wi-Fi
- Ethernet interface: eno2
- Ethernet link: Not connected
- NetworkManager: Active

The current environment uses a private IPv4 LAN.

Direct Wi-Fi bridging capability has not yet been established.

## 7. Existing Services

| Service | Status |
|---|---|
| Docker | Installed |
| Existing containers | Present, currently stopped |
| Nginx | Active on host |
| Node Exporter | Active on host |
| UFW | Inactive |

Existing host services will be preserved.

## 8. Version Control

- Git: 2.43.0
- GitHub SSH authentication: Successful

## 9. Infrastructure Decision

Selected virtualization architecture:

- KVM
- QEMU
- libvirt
- virt-manager
- Ubuntu Server 24.04 LTS

The final network design is pending verification of Ethernet availability,
wireless bridging capabilities and router configuration.

## 10. Security Considerations

- No host firewall changes during audit.
- No existing service configurations modified.
- No credentials or private network identifiers committed.
- VM services will be isolated from existing host services.