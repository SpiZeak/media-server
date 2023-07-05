## Notes
The Transmission client is using [Mullvad](https://mullvad.net/) as a VPN provider, feel free to fork this repo and change it.

## Instructions
- Create a .env file with the following variables:
    - *OPENVPN_PROVIDER*
    - *OPENVPN_CONFIG*
    - *OPENVPN_USERNAME*
    - *OPENVPN_PASSWORD*
- `docker compose up -d`
- The following services should now be accessible from your browser:
    - *Jellyfin* - [localhost:80](http://localhost:80)
    - *transmission* - [localhost:9091](http://localhost:80)
    - *radarr* - [localhost:7878](http://localhost:7878)
    - *sonarr* - [localhost:8989](http://localhost:8989)
    - *prowlarr* - [localhost:9696](http://localhost:9696)
    - *bazarr* - [localhost:6767](http://localhost:6767)
    - *portainer* - [localhost:9000](http://localhost:9000)
    - *flaresolverr* - [localhost:8191](http://localhost:8191)
