# Jellyfin-Arr-Stack

A streamlined, portable Docker Compose stack for a complete home media server. This setup includes the full "Arr" suite for automation and Jellyfin for high-performance media streaming with hardware acceleration.

## 🚀 Services Included
* **Jellyfin**: Open-source media server for streaming to all your devices.
* **Radarr**: Automated movie collection and management.
* **Sonarr**: Automated TV series and Anime management.
* **Prowlarr**: Centralized indexer management for trackers.
* **Bazarr**: Automated subtitle management.

## 🛠️ Key Features
* **Portable Design**: Uses relative paths (`./`) so you can move your stack anywhere.
* **HW Acceleration**: Pre-configured for Intel/AMD GPU transcoding via `/dev/dri`.
* **Organized Workflow**: Shared download and media folders for seamless "Arr" integration.

## 📋 Prerequisites
Before deploying, ensure you have **Docker** and **Docker Compose** installed on your host system.

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
Bazarr	6767	http://localhost:6767 

Recommended Setup Order:
Prowlarr: Configure this first to add your indexers (trackers).

Sync: Link Prowlarr to Radarr and Sonarr under Settings > Apps to sync indexers automatically.

Jellyfin: Add your libraries. Your media will be located at /media/[Category] inside the container (e.g., /media/Movies).

🔒 Security
This configuration is sanitized for public sharing:

No local usernames are exposed.

No API keys or passwords are included.

Note: It is highly recommended to use a Reverse Proxy (like Nginx Proxy Manager) and a VPN if you intend to access these services outside of your home network.

