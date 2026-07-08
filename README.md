# Tdarr Home Assistant Integration (PD-Codes Edition)

[![GitHub Release](https://img.shields.io/github/v/release/PD-Codes/Tdarr_HA_PD-Codes?style=flat-square)](https://github.com/PD-Codes/Tdarr_HA_PD-Codes/releases)
[![HACS Custom](https://img.shields.io/badge/HACS-Custom-41BDF5.svg?style=flat-square)](https://github.com/hacs/integration)

An advanced, feature-rich Home Assistant custom component for monitoring and controlling your [Tdarr](https://tdarr.io/) v2 distributed transcoding cluster.

Maintained and enhanced by [**PD-Codes**](https://github.com/PD-Codes/Tdarr_HA_PD-Codes).  
*(Forked and expanded from `deosrc/tdarr_ha` and `itchannel/tdarr_ha` — thanks to all original contributors!)*

---

## ✨ Why PD-Codes Edition? (Key Enhancements)

- **🚀 Dynamic Library Breakdown (Option A):** Automatically scans and generates individual, high-precision sensors for **every single library** (`All` as well as custom libraries like `1D - Platte`).
  - **Resolutions Breakdown:** Live file count sensors for `720p`, `1080p`, `4kuhd`, `480p`, `576p`, and more.
  - **Container Breakdown:** Live file count sensors for `mkv`, `mp4`, `avi`, etc.
  - **Codec Breakdown:** Live file count sensors for `hevc`, `h264`, `vp9`, `av1`, etc.
- **📊 Expanded Core & Statistics Sensors:**
  - **Lifetime Transcodes & Health Checks:** Tracks total historical transcodes and health checks performed (`TOTAL_INCREASING` counter, ready for Home Assistant Statistics & Energy dashboard).
  - **Tdarr Score & Health Check Score:** Real-time optimization percentages (`%`) directly from your Tdarr database.
  - **Total Files & Active Nodes:** Instant metrics on total library size and currently connected transcoding nodes.
  - **Server Uptime:** Accurate duration sensor (`seconds`).
- **🇩🇪 & 🇬🇧 Native Localizations:**
  - Complete, natural **German (`de`)** and **English (`en`)** translations. No awkward robotic translations—every label perfectly mirrors standard IT terminology and Tdarr's native Web UI (`Staged`, `Tdarr-Score`, `Space Saved`, `Transcode Queue`, etc.).
- **🔐 Robust API Key Authentication:**
  - Bulletproof `x-api-key` header handling across every single HTTP GET and POST request (`cruddb`, `client/staged`, `get-nodes`, etc.), allowing seamless operation whether authentication is enabled or disabled on your Tdarr server.

---

## 📦 Installation

### Option 1: HACS (Recommended)
1. Open **HACS** in your Home Assistant instance.
2. Click the three dots `...` in the top right corner and select **Custom repositories**.
3. Enter `https://github.com/PD-Codes/Tdarr_HA_PD-Codes` and select **Integration** as the category.
4. Search for **Tdarr (PD-Codes Edition)** and click **Download**.
5. Restart Home Assistant (`Settings > System > Restart`).

### Option 2: Manual Installation
1. Download the latest release from the [Releases page](https://github.com/PD-Codes/Tdarr_HA_PD-Codes/releases).
2. Copy the `custom_components/tdarr` folder into your Home Assistant's `/config/custom_components/` directory.
3. Restart Home Assistant.

---

## ⚙️ Configuration

1. Go to **Settings > Devices & Services** (`/config/integrations`).
2. Click **+ Add Integration** and search for **Tdarr**.
3. Enter your Tdarr server details:
   - **Server IP:** e.g., `192.168.31.75`
   - **Server Port:** default is `8265`
   - **API Key:** Enter your API key if authentication is enabled in Tdarr (otherwise leave blank).
4. Click **Submit**! Your server and nodes will appear instantly as devices.

---

## 🎛️ Features & Entities Overview

### 🖥️ Server Device
- **Sensors:**
  - `Server Status` (Online / Error)
  - `Space Saved` (Formatted size savings)
  - `Staged Files`
  - `Total Files`
  - `Lifetime Transcodes` & `Lifetime Health Checks`
  - `Tdarr Score` & `Health Check Score` (`%`)
  - `Server Uptime`
  - `Active Nodes`
  - `Transcode Queue`, `Transcode Success`, `Transcode Error`
  - `Health Check Queue`, `Health Check Success`, `Health Check Error`
  - `Total Frame Rate (FPS)`, `Total Transcode FPS`, `Total Health Check FPS`
  - **Dynamic Library Breakdowns:** `{Library}: {Resolution/Container/Codec}`
- **Controls & Switches:**
  - `Pause All Nodes`
  - `Ignore Schedules`

### 💻 Node Devices
- Automatically discovered whenever nodes connect to your cluster.
- **Sensors:**
  - `Connection Status`
  - `CPU & RAM Usage` (`%` and exact memory metrics via attributes)
  - `Node Frame Rate (FPS)` (Transcode, Health Check, Combined)
- **Controls & Limits:**
  - `Pause Node` switch
  - `Worker Limit: Transcode CPU` / `Transcode GPU`
  - `Worker Limit: Health Check CPU` / `Health Check GPU`

### 🛠️ Services
- `tdarr.scan_library`: Rescan or refresh a specific library (`Fresh Scan` or `Find New`).
- `tdarr.cancel_worker_item`: Cancel a running worker task on a specific node with a custom log reason.
- `tdarr.get_workers`: Fetch real-time active worker tasks across nodes.

---

## 📸 Screenshots

### Server Stats & Dynamic Option A Breakdowns
![Server sensors](./screenshots/server_sensors.png)

### Node Controls & Worker Limits
![Node controls](./screenshots/node_controls.png)

---

## 🔄 Automated Releases & Maintenance

This repository includes custom automated GitHub Actions (`.github/workflows/auto-release.yaml`):
Whenever `manifest.json` is bumped with a new version number on the `main` branch, a fresh release and tag are automatically packaged for HACS!

## 🤝 Contributing & Issues

Found a bug or have a feature request? Please open an issue or submit a Pull Request on the [GitHub Issue Tracker](https://github.com/PD-Codes/Tdarr_HA_PD-Codes/issues).
