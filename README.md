# Homelab

Set of docker compose files for my personal homelab applications

## How to use

This repository contains a `.env.sample` files. Just copy (or rename it) to `.env` and add the following envs:

* TIMEZONE: timezone to be used on some containers. (eg: America/New_York);
* VOLUMES_BASEDIR: folder to store the applications tmp/config files;
* VOLUMES_ASSETS: folder to store the applications assets (pictures, audios, videos, etc);
* PIHOLE_PASSWD: password for pi hole service;
* ROMM_ROOT_PASSWD: root password for ROOM database;
* ROMM_DB_PASSWD: password for romm user on ROOM database;
* ROMM_SECRET_KEY: key for authentication on ROMM server;
* IGDB_CLIENT_ID: IGDB generated ID;
* IGDB_CLIENT_SECRET: IGDB generated SECRET.