# Homelab

Set of docker compose files for my personal homelab applications.

The compose files are organized into two groups, each living in its own folder:

* `earth/` — core homelab services (network, proxy, media, photos, monitoring, home automation, security, etc.)
* `mars/` — AI / automation services (LLM UI, search, web crawler, agents, automation proxy)

## How to use

This repository contains a `.env.sample` file. Just copy (or rename it) to `.env` and fill in the values described below.

### General config

* `PUID`: docker user id (usually 1000);
* `PGID`: docker group id (usually 1000);
* `TIMEZONE`: timezone to be used on some containers (eg: `America/New_York`);
* `VOLUMES_BASEDIR`: folder to store the applications tmp/config files;
* `VOLUMES_ASSETS`: folder to store the applications assets (pictures, audios, videos, etc).

### `earth/dns.yml`

DNS and networking services (Unbound, Pi-hole, Gluetun, Wireguard).

* `PIHOLE_PASSWD`: password for Pi-hole service;
* `WIREGUARD_PK`: wireguard primary key;
* `WIREGUARD_ADDRESSES`: wireguard ip address;
* `TUN_COUNTRIES`: server countries.

### `earth/emu.yml`

Romm (game library) and its database.

* `ROMM_ROOT_PASSWD`: root password for Romm database;
* `ROMM_DB_PASSWD`: password for romm user on Romm database;
* `ROMM_SECRET_KEY`: key for authentication on Romm server;
* `IGDB_CLIENT_ID`: IGDB generated ID;
* `IGDB_CLIENT_SECRET`: IGDB generated SECRET.

### `earth/immich.yml`

Immich photo stack (server, machine learning, redis, database).

* `IMMICH_VERSION`: Immich image tag (defaults to `release`);
* `IMMICH_DB_NAME`: Immich database name;
* `IMMICH_DB_USERNAME`: Immich database user;
* `IMMICH_DB_PASSWORD`: Immich database password.

### `earth/home.yml`

Homepage dashboard and Home Assistant.

* `HOMEPAGE_ALLOWED_HOSTS`: allowed hosts for Homepage.

### `earth/security.yml`

Vaultwarden password manager.

* `VAULTWARDEN_TOKEN`: vaultwarden admin token;
* `VAULTWARDEN_DOMAIN`: vaultwarden domain.

### `earth/monitoring.yml`

System monitoring tools (Glances, Netdata). No extra env vars required beyond the general config.

### `earth/ebook.yml`

Kavita ebook server. No extra env vars required beyond the general config.

### `earth/media.yml`

Media stack (Jellyfin, Sonarr, Radarr, Bazarr, Prowlarr, Searr, etc). No extra env vars required beyond the general config.

### `earth/proxy.yml` and `mars/proxy.yml`

Reverse proxy and supporting services (Caddy on `mars/`, Nginx Proxy Manager + Dockhand on `earth/`).

* `DOMAIN`: base domain used by the Caddy service in `mars/proxy.yml`.

### `mars/hermes.yml`

Hermes agent and web UI.

* `HERMES_DASHBOARD_USERNAME`: dashboard basic auth username;
* `HERMES_DASHBOARD_PASSWORD`: dashboard basic auth password;
* `HERMES_DASHBOARD_SECRET`: session signing secret (generate with `openssl rand -hex 32`).

### `mars/chat.yml`

Open WebUI and MCPo (MCP-over-OpenAI) services. No extra env vars required beyond the general config.

### `mars/search.yml`

SearXNG meta search engine and its Valkey cache.

* `SEARXNG_SECRET`: SearXNG secret key;
* `SEARXNG_HOSTNAME`: public hostname for SearXNG (used to build the base url);
* `SEARXNG_UWSGI_WORKERS`: optional, uWSGI workers count;
* `SEARXNG_UWSGI_THREADS`: optional, uWSGI threads count.

### `mars/crawler.yml`

Firecrawl web crawler stack (API, Playwright, RabbitMQ, Postgres, Redis).

* `USE_DB_AUTHENTICATION`: optional, enable DB authentication;
* `BULL_AUTH_KEY`: optional, Bull auth key;
* `POSTGRES_USER`: optional, Firecrawl Postgres user (defaults to `postgres`);
* `POSTGRES_PASSWORD`: optional, Firecrawl Postgres password (defaults to `postgres`);
* `POSTGRES_DB`: optional, Firecrawl Postgres database (defaults to `postgres`);
* `OPENAI_API_KEY`: optional, enables AI features;
* `OPENAI_BASE_URL`: optional, custom OpenAI compatible base url;
* `OLLAMA_BASE_URL`: optional, Ollama base url for AI features;
* `MODEL_NAME`: optional, model name for AI features.

### `mars/auto.yml`

n8n automation service. No extra env vars required beyond the general config.

## Hardware acceleration

Optional snippets included in `earth/`:

* `earth/hwaccel.ml.yml` — hardware acceleration for machine learning workloads (Mali / RKNN).
* `earth/hwaccel.transcoding.yml` — hardware acceleration for media transcoding (QuickSync, VAAPI, NVENC, RK MPP, etc). Referenced by `earth/immich.yml` and `earth/media.yml` through docker compose `extends`.

## Notes

* Internal networks (`*_internal`) are declared as `internal: true` to isolate supporting services (databases, redis, etc.) from the outside. Only the front-facing services are attached to the shared `proxy_earth_network` / `proxy_mars_network` external network.