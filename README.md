home media suite
================

This project allows you to spin up various services which combined can create a reasonably complete home media server. Contains two docker-compose configurations. A base configuration (`docker-compose.yaml`) and an optional extra configuration (`extras.yaml`).

It uses an openvpn/transmission images network for most of the services.

setup
-----

- Install docker compose
- Create an `.env` file (see next section)
- Read docker-compose yaml files and update configuration to suit your needs

.env file
---------

A dummy `.env` file has been provided. Review this and update it to match your needs:

```sh
# see https://haugene.github.io/docker-transmission-openvpn/
OPENVPN_PROVIDER='NORDVPN'
NORDVPN_COUNTRY='France'
VPN_USERNAME='myuser'
VPN_PASSWORD='mypassword'
TZ='Europe/Paris'

# your user id and group id. run "id -u" and "id -g" to get these
PUID=1000
PGID=1000

# plex config. see https://github.com/plexinc/pms-docker
ADVERTISE_IP='http://192.168.1.7:32400'

# the following are only needed for cleanarr - can only be created after you set up plex
# see https://support.plex.tv/articles/204059436-finding-an-authentication-token-x-plex-token/
PLEX_TOKEN='myplextoken'
LIBRARY_NAMES='Films;TV shows'
PLEX_BASE_URL='http://192.168.1.7:32400'
```

volumes
-------

UPDATE THE DOCKER COMPOSE FILES.

The configuration in this repository assumes you have "/media/downloads" and "/media/media-server" on your machine. You will almost certainly want to change these to suit your needs. "/media/downloads" for where most of your media should be housed and "/media/media-server" for persistent state for the services themselves.

base configuration
------------------

### services

- Plex Media Server - media server (http://localhost:32400)
- Transmission - downloads client (http://localhost:9091)
- Radarr - movie management (http://localhost:7878)
- Sonarr - tv show management (http://localhost:8989)
- Jackett - tracker managemenet (http://localhost:9117)

### run

```sh
docker compose pull
docker compose up -d
```

extras configuration
--------------------

### services

- <all of base configuration, and ...>
- Bazarr - subtitle management (http://localhost:6767)
- Readarr - ebooks management (http://localhost:8787)
- Cleanarr - plex duplicate cleaner (http://localhost:8787)
- Ubooquity - ebook reader (http://localhost:8787)

### run

```sh
docker compose pull
docker compose -f docker-compose.yaml -f extras.yaml up -d
```

## Disclaimer

This project is intended for educational and non-commercial purposes only. It is not intended to promote or encourage any illegal activities, including but not limited to, the downloading or streaming of copyrighted material without authorization. The project is provided as-is and you are responsible for your own actions.

The project contains references to various services, including those that may facilitate illegal activities. The project does not endorse or promote the use of any illegal services or activities. The project is solely for informational purposes, and the references to such services do not constitute an endorsement or recommendation by the project.

By using this project, you acknowledge that you have read this disclaimer and that you accept and will be bound by the terms hereof. If you do not agree to these terms, do not use the project.
