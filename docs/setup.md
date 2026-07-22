# Setup & Deployment Guide — [PROJECT NAME]

---

## Prerequisites

- Access to Schubert Nexus (SSH as `z121532` or via self-hosted GitHub Actions runner)
- Repo cloned to `/opt/[witchesbrew]/` on Schubert
- `.env` file in place at `/opt/[witchesbrew]/.env` (see `.env.example`)

---

## Local Development

```bash
# Clone the repo
git clone https://github.com/theonlygeranium/[witchesbrew].git
cd [witchesbrew]

# Copy env template
cp .env.example .env
# Fill in values in .env

# Install dependencies
# TODO: add install command (e.g. npm install / pip install -r requirements.txt)

# Start dev server
# TODO: add dev start command
```

---

## Deploying to Schubert

### Automatic (recommended)
Push to `main` — the self-hosted GitHub Actions runner (`schubert-local`) picks up the job and runs `scripts/deploy.sh` directly on Schubert.

### Manual (on Schubert directly)
```bash
cd /opt/[witchesbrew]
sudo -u z121532 git pull origin main
sudo bash scripts/deploy.sh
```

### Remote fallback (self-hosted runner offline)
Trigger via **GitHub Actions → Deploy to Schubert → Run workflow → `force_remote: true`**.
This uses Tailscale OAuth to SSH into Schubert from a cloud runner.

---

## First-Time Schubert Setup

```bash
# 1. Clone repo
sudo mkdir -p /opt/[witchesbrew]
sudo chown z121532:z121532 /opt/[witchesbrew]
sudo -u z121532 git clone https://github.com/theonlygeranium/[witchesbrew].git /opt/[witchesbrew]

# 2. Create .env
sudo -u z121532 cp /opt/[witchesbrew]/.env.example /opt/[witchesbrew]/.env
sudo vim /opt/[witchesbrew]/.env   # fill in real values
sudo chmod 600 /opt/[witchesbrew]/.env

# 3. Run deploy script
sudo bash /opt/[witchesbrew]/scripts/deploy.sh
```

---

## Verifying the Deployment

```bash
# Check service status
systemctl is-active [SERVICE-NAME]

# Check logs
sudo journalctl -u [SERVICE-NAME] -n 50 --no-pager

# Health check
curl -s https://[your-domain]/health
```
