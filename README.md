# Jellyfin-Arr-Stack

A streamlined, portable Docker Compose stack for a complete home media server. This setup includes the full "Arr" suite for automation, qBittorrent for downloads, Tailscale for secure remote access, and Jellyfin for streaming.

## 🚀 Services Included
* **Jellyfin**: Media server for streaming to all your devices.
* **qBittorrent**: Lightweight BitTorrent client with Web UI.
* **Tailscale**: Secure VPN to access your server from anywhere without port forwarding.
* **Radarr/Sonarr**: Automated movie and TV series management.
* **Prowlarr**: Indexer management for trackers.
* **Bazarr**: Automated subtitle management.

## 🛠️ Key Features
* **Portable**: Uses relative paths (`./`)—no hardcoded usernames.
* **HW Acceleration**: Ready for Intel/AMD GPU transcoding via `/dev/dri`.
* **Zero-Config Remote Access**: Powered by Tailscale.

## 📋 Prerequisites
* Docker and Docker Compose installed.
* **Tailscale**: You will need a Tailscale account to authenticate the container.
---

## 🚀 Getting Started

Follow these steps to get your media stack up and running:

### 1. Clone the Repository
```bash
git clone [https://github.com/your-username/jellyfin-arr-stack.git](https://github.com/your-username/jellyfin-arr-stack.git)
cd jellyfin-arr-stack
```
2. Verify Hardware Acceleration (Optional)
To allow Jellyfin to use your GPU for transcoding, you need to verify your system's render group ID:

```Bash
getent group render | cut -d: -f3
```
If the output is not 105, open docker-compose.yml and update the group_add value under the Jellyfin service to match your specific output.

3. Create the Directory Structure
This stack uses a specific folder structure to ensure all apps can "see" the same files and utilize atomic moves. Run this command to create the folders:

```Bash
mkdir -p Media/{Movies,TVShows,Downloads,Anime,WebSeries}
```
4. Deploy the Stack
Run the following command to pull the images and start the containers in the background:

```Bash
docker-compose up -d
```
⚙️ Post-Install Configuration
Once the containers are running, you can access the web interfaces via your browser:

Service	Port	URL \
Jellyfin	8096	http://localhost:8096 \
Radarr	7878	http://localhost:7878 \
Sonarr	8989	http://localhost:8989 \
Prowlarr 9696	http://localhost:9696 \ 
qBittorrent	8080	http://localhost:8080 \
Bazarr	6767	http://localhost:6767 

Recommended Setup Order:
Prowlarr: Configure this first to add your indexers (trackers).

Sync: Link Prowlarr to Radarr and Sonarr under Settings > Apps to sync indexers automatically.

Jellyfin: Add your libraries. Your media will be located at /media/[Category] inside the container (e.g., /media/Movies).

Important: The default login for qBittorrent is usually admin with the password adminadmin (check logs if this fails). Change this immediately in settings.

🔒 Security
This configuration is sanitized for public sharing:

No local usernames are exposed.

No API keys or passwords are included.

Note: It is highly recommended to use a Reverse Proxy (like Nginx Proxy Manager) and a VPN if you intend to access these services outside of your home network.

