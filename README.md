# QBittorrent-NordVPN Docker Setup

This project provides a Docker Compose setup to run **qBittorrent** through **NordVPN** using the NordLynx technology. This ensures all torrent traffic is routed securely and anonymously through NordVPN.

## Table of Contents
- [Overview](#overview)
- [Prerequisites](#prerequisites)
- [Setup Instructions](#setup-instructions)
  - [1. Clone the repository](#1-clone-the-repository)
  - [2. Configure the environment](#2-configure-the-environment)
  - [3. Run the containers](#3-run-the-containers)
- [Accessing qBittorrent](#accessing-qbittorrent)
- [Ports](#ports)
- [Managing the Services](#managing-the-services)
  - [Start the services](#start-the-services)
  - [Stop the services](#stop-the-services)
  - [Restart the services](#restart-the-services)

## Overview

This setup includes two primary services:
1. **NordVPN**: A container that runs NordVPN with the NordLynx protocol for secure, anonymous internet connections. The VPN traffic is routed through servers in Switzerland by default.
2. **qBittorrent**: A torrent client container whose traffic is routed through the NordVPN container to ensure anonymity.

This Docker Compose configuration ensures that your torrenting activity is secure by routing all traffic through NordVPN, preventing any accidental IP leaks.

## Prerequisites

Before you begin, ensure you have the following:
- Docker and Docker Compose installed on your system.
- A **NordVPN** subscription.
- Your **NordVPN private key** (needed for NordLynx authentication).

## Setup Instructions

### 1. Clone the repository

Start by cloning this repository to your local machine:

```bash
git clone https://github.com/bcalderom/QBittorrent-NordVPN-Docker.git
cd QBittorrent-NordVPN-Docker
```

### 2. Configure the environment

You will need to create an `.env` file to store your NordVPN credentials and folder paths for qBittorrent configuration and downloads.

1. Copy the provided `env.template` and rename it to `.env`:
   
   ```bash
   cp env.template .env
   ```

2. Edit the `.env` file and replace the placeholder values with your own:

   ```env
   PRIVATE_KEY="<Your_NordVPN_Private_Key_Here>"
   QBIT_CONFIG_FOLDER="/absolute/path/to/config/folder"
   QBIT_DOWNLOAD_FOLDER="/absolute/path/to/downloads/folder"
   ```

   - **PRIVATE_KEY**: Your NordVPN private key. Follow [this guide](https://github.com/bubuntux/nordlynx/pkgs/container/nordlynx#how-to-get-your-private_key) to generate your private key.
   - **QBIT_CONFIG_FOLDER**: The directory on your host system where qBittorrent configuration files will be stored.
   - **QBIT_DOWNLOAD_FOLDER**: The directory on your host system where torrent downloads will be saved.

### 3. Run the containers

Once your `.env` file is configured, start the containers:

```bash
docker-compose up -d
```

This will start both **NordVPN** and **qBittorrent** containers in the background (detached mode).

## Accessing qBittorrent

After the containers are running, you can access the **qBittorrent** web interface by navigating to:

```
http://localhost:8080
```

- **Default credentials**: 
  - **Username**: `admin`
  - **Password**: A temporary password will be displayed in the Docker logs on the first run. You can check it with the following command:
    ```bash
    docker logs qbittorrent
    ```
  - **Important**: It's highly recommended to change the default password upon the first login.

## Ports

The following ports are exposed and can be customized if needed:
- **8080**: For accessing the **qBittorrent WebUI**.
- **6881**: For **torrenting traffic** (TCP/UDP).

## Managing the Services

### Start the services

To start the services manually:

```bash
docker-compose up -d
```

### Stop the services

To stop and remove the containers:

```bash
docker-compose down
```

### Restart the services

To restart the containers and apply configuration changes:

```bash
docker-compose down && docker-compose up -d
```
