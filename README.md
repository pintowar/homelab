# Homelab

Set of docker compose files for my personal homelab applications

## How to use

This repository contains a `.env.sample` files. Just copy (or rename it) to `.env` and add the following envs:

* TIMEZONE: timezone to be used on some containers. (eg: America/New_York);
* VOLUMES_BASEDIR: folder to store the applications tmp/config files;
* VOLUMES_ASSETS: folder to store the applications assets (pictures, audios, videos, etc);
* PIHOLE_PASSWD: password for pi hole service.