
# Infrastructure Verification Report

**Project:** Local Machine Virtualization with Static IP and DNS Configuration

**Verification Date:** 12 November 2026

## 1. VirtualBox Verification

| Test | Result |
|---|---|
| VirtualBox installation | PASS |
| VirtualBox kernel modules | PASS |
| VM provisioning | PASS |
| VM startup | PASS |
| VM automatic startup after host reboot | PASS |

## 2. Guest Network Verification

| Test | Expected / Observed |
|---|---|
| Host-only guest IP | 192.168.56.10 |
| Host-only host IP | 192.168.56.1 |
| NAT guest IP | 10.0.2.15 |
| NAT gateway | 10.0.2.2 |
| SSH management | PASS |
| Internet connectivity | PASS |
| Static IP persistence after reboot | PASS |

## 3. Application Verification

| Test | Result |
|---|---|
| Python backend service | PASS |
| Backend loopback binding | PASS |
| Nginx service | PASS |
| Nginx configuration test | PASS |
| Nginx reverse proxy | PASS |
| Host-to-VM HTTP request | PASS |

## 4. External HTTPS Verification

Cloudflare Quick Tunnel was used to publish the application.

External request:

```bash
curl -i https://<current-quick-tunnel-hostname>
```

Observed result:

- HTTP/2 200
- Content-Type: application/json
- Server: cloudflare
- Python backend JSON response returned successfully.

The response confirmed that Nginx forwarded the request to the
Python backend.

## 5. Tunnel Recovery Verification

The Cloudflare tunnel systemd service was restarted.

A new Quick Tunnel hostname was generated.

An external HTTPS request to the new hostname returned HTTP/2 200.

Result: PASS.

## 6. Remaining Requirements

| Requirement | Status |
|---|---|
| Custom domain | Not configured |
| DNS A record | Not configured |
| Router port forwarding | Not configured |
| Dedicated public IP | Not configured |
| Let's Encrypt origin certificate | Not configured |
| Certbot renewal dry-run | Not performed |
| Custom-domain HTTPS | Not verified |

## 7. Limitations

The environment does not provide router administration access
or a purchased custom domain.

Cloudflare Quick Tunnel provides temporary public HTTPS access
without direct inbound port forwarding.

Cloudflare manages the public TLS connection. This is not equivalent
to installing and renewing a Let's Encrypt certificate on Nginx.

## 8. Overall Result

The local virtualization, persistent private networking, application
deployment, reverse proxy, external HTTPS access and tunnel recovery
were successfully demonstrated.

Custom-domain DNS and origin certificate automation remain outstanding.
