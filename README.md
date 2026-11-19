# chromium (NAS)

Chromium browser in a container on the NAS (Z4 Pro), for installing the
Muse Chrome extension (needs Chrome 137+).

- Image: `lscr.io/linuxserver/chromium:latest` (multi-arch; NAS is amd64.
  `kasmweb/chrome` is amd64-only and cannot run on OCI ARM, but this image
  works on both.)
- Access: Tailscale only — the container shares the NAS tailscale network
  namespace (`network_mode: container:tailscale`), so the web UI binds
  directly to the NAS Tailscale IP: `http://100.66.222.41:3000`.
  No Docker port mapping (Tailscale does not forward to mapped ports).
- Profile persists in the named volume `chromium_config` (`/config`).
- Internet via the OpenWrt proxy (`HTTP_PROXY`/`HTTPS_PROXY`, Stack env
  vars, defaults point at `10.10.10.250:7890`).

## Deploy

Portainer Git Stack on the NAS Edge environment (`z4pro-nas`, endpoint 6),
from this repo (root `docker-compose.yml`). The image must already be
present on the NAS (Portainer 3.0.1 does not auto-pull on Stack create);
pull it first via zspace-cli if needed.
