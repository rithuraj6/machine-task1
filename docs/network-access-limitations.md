# External Network Access and Implementation Limitations

## 1. Overview

The project implements a locally virtualized Ubuntu Server environment using Oracle VirtualBox. The VM has persistent private networking, an Nginx reverse proxy, a Python backend service and externally accessible HTTPS through Cloudflare Quick Tunnel.

Some requirements involving router administration and domain ownership could not be implemented because the assessment environment does not provide access to the office router or a domain under the candidate's control.

## 2. Observed Network Configuration

The Ubuntu VM uses two network adapters.

| Component | Configuration |
|---|---|
| NAT interface | enp0s3 |
| NAT guest IP | 10.0.2.15/24 |
| NAT gateway | 10.0.2.2 |
| NAT DNS resolver | 10.0.2.3 |
| Host-only interface | enp0s8 |
| Static private IP | 192.168.56.10/24 |
| Host-only host IP | 192.168.56.1 |
| Host-only subnet | 192.168.56.0/24 |

The NAT adapter provides outbound internet connectivity. The host-only adapter provides private communication between the Zorin host and Ubuntu VM.

The public IPv4 address observed through an external IP lookup service was not independently verified against the office router's WAN address. Therefore, direct public IP assignment and CGNAT status remain unconfirmed.

## 3. Router Port Forwarding Limitation

Router administration access was unavailable in the office environment.

Consequently:
- No router port forwarding rules were created.
- No inbound public connections were configured directly to the VM.
- No office firewall settings were modified.

Direct external access through router port forwarding would require authorization from the network administrator and confirmation that the internet connection supports inbound connectivity.

## 4. Custom Domain and DNS Limitation

No domain name or DNS management account was available.

Therefore:
- No custom domain or subdomain was configured.
- No DNS A record was created.
- DNS propagation for a custom hostname was not tested.

A conventional DNS A record would point a hostname to a reachable public IPv4 address.

Dynamic DNS can be used when a public IP address changes. A client or router updates the DNS record whenever the address changes. Dynamic DNS does not bypass CGNAT or provide router port forwarding.

## 5. Cloudflare Quick Tunnel Alternative

Cloudflare Quick Tunnel was implemented to demonstrate external HTTPS access without requiring router administration or inbound port forwarding.

Traffic flow:

1. An external user accesses the temporary Cloudflare hostname.
2. Cloudflare terminates the public HTTPS connection.
3. Cloudflare forwards the request through the outbound tunnel.
4. The tunnel connects to the Nginx service inside the Ubuntu VM.
5. Nginx forwards the request to the Python backend on 127.0.0.1:8000.

The tunnel was configured as a systemd service with automatic restart.

The generated Quick Tunnel hostname is temporary and can change after restarting the tunnel.

## 6. HTTPS and Certificate Management

Public HTTPS was successfully demonstrated through Cloudflare.

However, the Nginx origin uses HTTP internally, and a Let's Encrypt certificate was not installed on the VM.

Certbot issuance and renewal tests were not performed because no custom domain or DNS management access was available.

An alternative future implementation could use Let's Encrypt DNS-01 validation with a domain under the candidate's control. This method does not require inbound router port forwarding, but it does require DNS control and appropriate validation records.

## 7. Security Considerations

- Existing host Nginx, Docker and Kubernetes services were preserved.
- The VM uses NAT and host-only networking.
- No unnecessary host firewall changes were made.
- The Python backend listens only on 127.0.0.1:8000.
- External access is provided through the Cloudflare tunnel.
- No private credentials or access tokens are included in this documentation.

## 8. Conclusion

The local virtualization, persistent private IP configuration, VM automatic startup, SSH management, Nginx reverse proxy, Python backend service and external HTTPS access were implemented and verified.

Direct router port forwarding, custom-domain DNS and origin-side Let's Encrypt certificate automation remain outstanding because the required router and domain administration access was unavailable.

Cloudflare Quick Tunnel was used as an alternative to demonstrate external HTTPS connectivity without changing the office network infrastructure.
