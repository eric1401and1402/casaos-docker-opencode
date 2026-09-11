# CasaOS Docker Compose - OpenCode

CasaOS Docker Compose file for deploying [OpenCode](https://github.com/anomalyco/opencode) AI coding assistant.

## What is OpenCode?

OpenCode is an interactive AI-powered CLI tool for software engineering tasks. It runs as a web application and provides a chat interface for code generation, debugging, refactoring, and more.

## Quick Start

### Option 1: CasaOS Web UI

1. Open your CasaOS dashboard
2. Go to **App Store** > **Custom Install**
3. Select **Docker Compose**
4. Upload or paste the contents of `opencode.yaml`
5. Click **Install**

### Option 2: Command Line

```bash
# Download the compose file
curl -O https://raw.githubusercontent.com/eric1401and1402/casaos-docker-opencode/main/opencode.yaml

# Rename for docker compose (optional)
mv opencode.yaml docker-compose.yml

# Start the container
docker compose up -d
```

## Access OpenCode

After installation, access OpenCode at:

```
http://<your-host-ip>:3000
```

## Configuration

### Volumes

| Host Path | Container Path | Description |
|---|---|---|
| `/DATA/opencode/config` | `/home/opencode/.opencode` | OpenCode configuration |
| `/DATA/opencode/work` | `/workspace` | Your project workspace |

### Resources

| Resource | Value |
|---|---|
| CPU Shares | 50 |
| Memory Limit | 1024 MB |
| Port | 3000 |
| Restart Policy | `unless-stopped` |
| Healthcheck | HTTP `localhost:3000` (30s interval) |
| Log Rotation | JSON, max 10MB x 3 files |

### Environment Variables

| Variable | Default | Description |
|---|---|---|
| `TZ` | `Asia/Taipei` | Container timezone |

## Customization

Edit `opencode.yaml` before uploading to adjust:

- **Memory limit**: Change `2048M` in `deploy.resources.limits.memory`
- **Port**: Change `3000` in both `ports` and `command` sections
- **Workspace path**: Change `/DATA/opencode/work` to your preferred directory
- **Timezone**: Change `TZ` environment variable to your timezone
- **Image tag**: Change `ghcr.io/anomalyco/opencode:latest` to a specific version for stability

## Features

- Healthcheck enabled for container monitoring
- Automatic log rotation (10MB max, 3 files)
- Persistent config and workspace volumes
- CasaOS App Store ready

## License

[Apache License 2.0](LICENSE)
