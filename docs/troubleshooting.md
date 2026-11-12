
# Troubleshooting Notes

## 1. SSH Connection Failure

Check VM status:

```bash
VBoxManage list runningvms
```

Check guest address:

```bash
ip -br addr
```

Check SSH service inside Ubuntu:

```bash
sudo systemctl status ssh
```

## 2. Netplan Configuration

Validate Netplan:

```bash
sudo netplan generate
```

Apply configuration:

```bash
sudo netplan apply
```

Check addresses and routes:

```bash
ip -br addr
ip route
```

## 3. Nginx Failure

Test configuration:

```bash
sudo nginx -t
```

Check service:

```bash
sudo systemctl status nginx
```

Inspect logs:

```bash
sudo journalctl -u nginx -n 50 --no-pager
```

## 4. Python Backend Failure

Check service:

```bash
sudo systemctl status devops-backend
```

Inspect logs:

```bash
sudo journalctl -u devops-backend -n 50 --no-pager
```

Test backend locally:

```bash
curl http://127.0.0.1:8000
```

## 5. Cloudflare Tunnel

Check service:

```bash
sudo systemctl status cloudflared-quick-tunnel
```

Inspect logs:

```bash
sudo journalctl -u cloudflared-quick-tunnel -n 50 --no-pager
```

Find generated hostname:

```bash
sudo journalctl -u cloudflared-quick-tunnel --no-pager \
  | grep -E 'https://.*trycloudflare.com'
```

Quick Tunnel hostnames can change after restart.

## 6. Cloudflare Connectivity Pre-check Warnings

The observed environment passed connectivity checks to one Cloudflare
region but failed checks to another.

The tunnel nevertheless registered a connection and external HTTPS
requests returned HTTP/2 200.

Do not treat the pre-check warning alone as proof that the tunnel
is unavailable. Verify the actual public endpoint.

Cloudflared also reported ICMP proxy and UDP receive-buffer warnings.
These did not prevent the observed HTTP application requests.

## 7. Existing Host Services

Avoid changing host networking, firewall rules, Nginx, Docker or
Kubernetes configuration without checking dependencies.

The assessment VM uses NAT and host-only networking to avoid
modifying the host's existing application services.
