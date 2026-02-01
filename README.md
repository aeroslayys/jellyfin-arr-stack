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

Before deploying, ensure you have **Docker** and **Docker Compose** installed.

### 🐧 Hardware Acceleration (Optional but Recommended)
To allow Jellyfin to use your GPU for transcoding, you need to verify your `render` group ID. Run:
```bash
`getent group render | cut -d: -f3`.





