# Infrastructure Architecture

## 1. Hypervisor

- Oracle VM VirtualBox 7.2.22
- VM management: VirtualBox Manager and VBoxManage
- Virtual disk: dynamically allocated VDI

## 2. Physical Host

| Component | Configuration |
|---|---|
| Hardware | ASUS ROG Strix G531GT |
| OS | Zorin OS 18.1 |
| CPU | Intel Core i5-9300H |
| Physical cores | 4 |
| Logical CPUs | 8 |
| RAM | Approximately 15 GiB |

Existing host services, including Nginx, Docker and Node Exporter,
are preserved.

## 3. Virtual Machine

| Component | Configuration |
|---|---|
| VM name | devops-assessment-vm |
| Guest OS | Ubuntu Server 24.04.5 LTS |
| CPU | 2 vCPU |
| RAM | 3072 MB |
| Virtual disk | 35 GiB |
| Disk format | VDI |
| Allocation | Dynamically allocated |
| Hostname | devops-vm |
| User | devopsadmin |

## 4. Network Design

Two VirtualBox adapters are configured.

### Adapter 1 — NAT

Provides outbound internet connectivity.

- Guest interface: enp0s3
- Guest address: 10.0.2.15
- Gateway: 10.0.2.2
- Address assignment: DHCP

### Adapter 2 — Host-only

Provides stable host-to-VM management connectivity.

- Guest interface: enp0s8
- Host interface: vboxnet0
- Host address: 192.168.56.1
- Guest address: 192.168.56.10
- Subnet: 192.168.56.0/24
- Guest address assignment: Static

The host-only interface is used for SSH and private management.
The NAT interface is used for outbound internet connectivity.

## 5. Application Architecture

- Nginx listens on guest port 80.
- Nginx forwards requests to 127.0.0.1:8000.
- Python HTTP Server provides JSON responses.
- The backend is managed by systemd.
- The backend listens only on loopback.

## 6. External Access

Cloudflare Quick Tunnel publishes the Nginx HTTP origin through
a temporary public HTTPS hostname.

Traffic flow:

Public HTTPS
-> Cloudflare Edge
-> Cloudflare Tunnel
-> Ubuntu Nginx
-> Python Backend

The tunnel runs as a systemd service.

## 7. Automatic Startup

- VirtualBox VM automatic startup is enabled.
- Nginx is enabled at boot.
- Python backend is enabled at boot.
- Cloudflare Quick Tunnel is enabled at boot.

## 8. Security Considerations

- The backend listens only on 127.0.0.1.
- The VM is managed through a private host-only network.
- No router ports were opened.
- No custom domain or permanent public endpoint is configured.
- Private credentials and secrets must not be committed to Git.
