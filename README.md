# Homelab

Set of docker compose files for my personal homelab applications

## How to use

This repository contains a `.env.sample` files. Just copy (or rename it) to `.env` and add the following envs:

1. General config
    * PUID: docker user id;
    * PGID: docker group id;
    * TIMEZONE: timezone to be used on some containers. (eg: America/New_York);
    * VOLUMES_BASEDIR: folder to store the applications tmp/config files;
    * VOLUMES_ASSETS: folder to store the applications assets (pictures, audios, videos, etc);

2. For `net-docker-compose.yml`:
    * PIHOLE_PASSWD: password for pi hole service;

3. For `emu-docker-compose.yml`:
    * ROMM_ROOT_PASSWD: root password for ROOM database;
    * ROMM_DB_PASSWD: password for romm user on ROOM database;
    * ROMM_SECRET_KEY: key for authentication on ROMM server;
    * IGDB_CLIENT_ID: IGDB generated ID;
    * IGDB_CLIENT_SECRET: IGDB generated SECRET.

4. For `llm-docker-compose.yml`:
    * LANGFUSE_DB_NAME: database for LANGFUSE database;
    * LANGFUSE_DB_USER: user for LANGFUSE database;
    * LANGFUSE_DB_PASSWORD: password for LANGFUSE database;
    * LANGFUSE_NEXTAUTH_SECRET: used to validate login session cookies;
    * LANGFUSE_NEXTAUTH_URL: required for successful authentication via OAUTH;
    * LANGFUSE_SALT: used to salt hashed API keys;
    * LANGFUSE_ENCRYPTION_KEY: used to encrypt sensitive data;
    * OLLAMA_BASE_URL: ollama base url for open-webui.
