# CCTV Stack Configuration Guide

## Required Environment Variables

For deployment in Portainer (or any environment), set these variables:

### Core Configuration
- **OUT** - Output directory path (e.g., `/mnt/data/cctv`)
- **TZ** - Timezone (e.g., `America/Los_Angeles`)

### RTSP Stream Configuration  
- **RTSP_URL** - Complete RTSP URL including authentication
  - No auth: `rtsp://192.168.4.56:554/stream0`
  - With auth: `rtsp://username:password@192.168.4.56:554/stream0`

### Recording Configuration
- **FORMAT** - Video format (default: `mkv`)
- **DURATION** - Segment length in seconds (default: `600`)
- **SEGMENT_FORMAT** - Date format for filenames (default: `%d-%m-%Y_%H%M%S`)
- **TIMEOUT_BUFFER** - Recording timeout buffer (default: `30`)
- **LOG_LEVEL** - FFmpeg log level (default: `error`)

### Cleanup Configuration
- **CLEANUP_SPACE** - Minimum free space in GB before cleanup (default: `45`)
- **CLEANUP_REGEX** - File pattern for cleanup (default: `.*-[0-9]+_\(cam[0-9]\|mosaic\).*`)
- **CLEANUP_DIR** - Directory to cleanup (default: `/out/`)

### YouTube Upload (Disabled)
- **EMAIL** - Email for uploads (set to `disabled`)
- **ACCESS_TOKEN** - Upload token (set to `disabled`)

## Portainer Deployment Steps

1. **Stacks → Add stack → Git Repository**
2. **Repository URL:** `https://github.com/jijichen/cctv.git`
3. **Repository Reference:** `single-camera-pst`
4. **Compose Path:** `docker-compose.yml`
5. **Environment Variables:** Set all required variables listed above
6. **Deploy stack**

## Notes

- All sensitive data (RTSP credentials, paths) should only be set in Portainer UI
- Never commit real credentials to Git repository
- The merge container creates daily merged videos and timelapses
- Recordings are stored in `{OUT}/cam1/` as 10-minute segments