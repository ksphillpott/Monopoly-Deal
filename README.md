# Monopoly Deal - Synology NAS Deployment

## Prerequisites

1. **Synology NAS** with Container Manager (Docker) installed
2. **Tailscale** installed on NAS and connected
3. **GitHub Secrets** configured (same as Thirty-One):
   - `NAS_HOST` - Your NAS Tailscale IP (100.x.x.x)
   - `NAS_USER` - SSH username
   - `NAS_SSH_KEY` - SSH private key
   - `TAILSCALE_AUTHKEY` - Tailscale auth key

## First-Time Setup on Synology

1. Open **Container Manager** on your Synology
2. Create folder: `/volume1/docker/monopoly-deal/`
3. Enable SSH access (if not already)

## How It Works

When you push to `main`:
1. GitHub Action connects via Tailscale
2. Copies files to `/volume1/docker/monopoly-deal/`
3. Rebuilds and restarts the Docker container

## Access the Game

After deployment:
- **Local**: `http://192.168.1.37:3001`
- **Tailscale**: `http://100.x.x.x:3001` (your NAS Tailscale IP)

## Manual Docker Commands (on NAS via SSH)

```bash
cd /volume1/docker/monopoly-deal

# Start
docker-compose up -d

# Stop
docker-compose down

# View logs
docker-compose logs -f

# Rebuild after changes
docker-compose build --no-cache && docker-compose up -d
```

## Assets

Place all card images in `public/assets/` folder:
- Property cards: `MediterraneanAvenue.PNG`, etc.
- Money: `Assets_1MILLION.PNG`, `Assets_2MILLION.PNG`, etc.
- Actions: `passgo.PNG`, `birthday.PNG`, etc.
- Rent cards: `rent_rentwild.PNG`, etc.
- Wildcards: `wildcard_wild.PNG`, etc.

## Port

Default port is 3001 (to avoid conflict with other services).
Change in `docker-compose.yml` if needed.
