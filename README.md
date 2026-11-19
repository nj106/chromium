# chromium (OCI)

Chromium browser in a container on the OCI ARM server, for installing the
Muse Chrome extension (needs Chrome 137+).

- Image: `lscr.io/linuxserver/chromium:latest` (arm64 build exists;
  `kasmweb/chrome` is amd64-only and cannot run on OCI ARM).
- Web UI (KasmVNC): port 3000, fronted by Caddy over HTTPS.
- Profile persists in the named volume `chromium_config` (`/config`).

## Access (planned)

- Domain: `chrome.njcq.dpdns.org` (reusing the deleted NAS-Chrome name)
  -> Caddy `reverse_proxy 127.0.0.1:3000`, DNS grey cloud (no Cloudflare
  proxy, for stable websocket, same as firefox.njcq.dpdns.org).
- Deploy as a Portainer Git Stack (endpoint Local) from this repo.
