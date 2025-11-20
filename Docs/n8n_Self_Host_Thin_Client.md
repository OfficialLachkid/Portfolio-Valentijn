# Self-Hosting n8n on HP t630 Thin Client, using Docker and Cloudflare Tunnel

## Overview
This document explains how I configured an HP t630 Thin Client to run a fully functional self-hosted n8n instance on Windows. Instead of relying on the paid n8n Cloud plan (around €20 per month), I used the n8n Self-Hosted AI Starter Kit from GitHub together with Docker Compose. To make the instance accessible from anywhere in the world, I registered a custom domain through Cloudflare for **$7.50 per year** and connected everything using a Cloudflare Tunnel. This gives me secure global access to n8n without exposing any ports or making changes to my home network router.

---

## 1. Using the HP t630 as a Local Server
The HP t630 is a compact, quiet, and energy-efficient thin client that works surprisingly well as a home server. I installed Windows on it using an old USB installation stick I still had lying around from a previous PC build. Windows turned out to be the easiest environment for this project, since I avoided the difficulties I previously had with Ubuntu Linux and could immediately move on to installing Docker.

Once Windows was installed and updated, I installed Docker Desktop, enabled WSL 2 when prompted, and rebooted the system. After this, the machine was fully prepared to host containerized applications such as n8n.

---

## 2. Setting Up n8n Using the Self-Hosted AI Starter Kit
To run n8n locally, I used the official repository:

**GitHub:**  
<https://github.com/n8n-io/self-hosted-ai-starter-kit>
Helpfull tutorials: 
- https://www.youtube.com/watch?v=F1psr8uFwUU 
- https://www.youtube.com/watch?v=cZQPDLgPtNg

I cloned the repository and copied the example environment file:

```bash
git clone https://github.com/n8n-io/self-hosted-ai-starter-kit
cd self-hosted-ai-starter-kit
copy .env.example .env
```

The `.env` file contains configuration fields such as `N8N_HOST`, `N8N_PORT`, and `GEN_AI_ENABLED`. These can be adjusted depending on how you want the environment to behave. After configuring the file, I simply ran Docker Compose:

```bash
docker-compose up -d
```

Once the containers finished booting, n8n became available locally at:

```
http://localhost:5678
```

At this point the system was fully functional and ready for workflows, including AI-powered ones.

---

## 3. Registering a Domain Through Cloudflare
To give my installation a proper URL, I registered a domain directly through Cloudflare Registrar. The domain cost **$7.50 per year**, which is significantly cheaper than most traditional registrars. Since the domain is already managed inside Cloudflare’s system, it integrates seamlessly with Cloudflare Tunnel, DNS, SSL management, and security features.

With the domain added to my Cloudflare dashboard, I updated its DNS nameservers to Cloudflare’s, which activated the domain inside my account and prepared it for tunneling.

---

## 4. Making n8n Globally Accessible With Cloudflare Tunnel
One of the biggest advantages of Cloudflare Tunnel is that it allows secure remote access to local services without opening any ports. Everything is routed through Cloudflare’s infrastructure, encrypted and protected by default.

I installed cloudflared on the Windows machine and authenticated it:

```bash
cloudflared tunnel login
```

After logging in, I created a new tunnel:

```bash
cloudflared tunnel create n8n-tunnel
```

Next, I connected the tunnel to my domain by routing a DNS entry:

```bash
cloudflared tunnel route dns n8n-tunnel n8n.mydomain.com
```

The last step was creating a configuration file for the tunnel, specifying that traffic to the domain should be forwarded to the local n8n instance:

```yaml
ingress:
  - hostname: n8n.mydomain.com
    service: http://localhost:5678
  - service: http_status:404
```

Once the tunnel was started, the dashboard became reachable at:

```
https://n8n.mydomain.com
```

This worked instantly and required absolutely no router configuration. Cloudflare automatically handled SSL certificates, security, routing, and uptime.

---

## 5. Costs and Benefits
The entire setup costs only **$7.50 per year**, which is the price of the domain. Everything else—Docker, Cloudflare Tunnel, the n8n self-hosted environment, and the Windows installation—is free. Compared to the official n8n Cloud service, which costs around €20 every month, this approach saves a significant amount while providing full ownership and privacy.

Running n8n on the HP t630 gives me a quiet, low-power, always-on automation server that I can access from anywhere with WiFi. Cloudflare Tunnel keeps it secure and stable, while Docker guarantees that it stays easy to maintain. The combination makes the thin client a surprisingly powerful automation hub.

---

## Conclusion
By installing Windows on the HP t630, running n8n through Docker, and connecting everything through a Cloudflare-managed domain and tunnel, I created a flexible and cost-effective automation environment. This setup offers global access, strong security, and complete control over my automations without any recurring subscription fees. It transforms the thin client into a reliable personal server that is simple to maintain and powerful enough to handle AI-driven workflows.

---

## Images