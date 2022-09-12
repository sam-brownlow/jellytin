<img src="./jellytin.png"></img>

# Jellytin

Put your local Jellyfin server in a tin, and securely serve it up on the internet 🚀


### Intro
This project is especially helpful if you:
1) Have a local Jellyfin server that you want to access over the internet
1) Do *not* currently have any infrastructure to expose services to the internet
1) Wish to hide + secure Jellyfin behind an identity provider
   1) (and also wish to access Jellyfin via non-browser clients, e.g. Android app)


### Dependencies
* [Authentik](https://goauthentik.io/)
  * Provide authentication via LDAP, SSO, etc.
* [Nginx Proxy Manager](https://nginxproxymanager.com/)
  * Proxy between `Cloudflare Tunnel` -> `Nginx Reverse Proxy` -> `Authentik` -> `Jellyfin`
* [Cloudflare Tunnel](https://www.cloudflare.com/products/tunnel/)
  * Serve content without forwarding ports on your router


### Footnote
If you're using a Raspberry Pi, then you should run the [64-bit OS](https://www.raspberrypi.com/news/raspberry-pi-os-64-bit/).


# Instructions


### Install `docker` & `docker-compose`
```shell
# install docker
curl -sSL https://get.docker.com | sh
sudo usermod -aG docker "$USER"  # assuming current $USER will run docker
exec sudo su -l "$USER"          # https://superuser.com/a/609141
docker run hello-world           # test the install
sudo systemctl enable docker     # start docker on boot

# install docker-compose
sudo apt-get install libffi-dev libssl-dev
sudo apt install python3-dev
sudo apt-get install -y python3 python3-pip
sudo pip3 install docker-compose
```


### Deploy Authentik
* Deploy via [./authentik/](./authentik/)
* Generalize yourself with [Outposts, Providers, & Applications](https://goauthentik.io/docs/terminology)
  * tl;dr to deploy an application in Authentik, you need an Outpost to service a Provider, which services an Application


### Deploy Nginx Proxy Manager
* Deploy via [./nginx_proxy_manager/](./nginx_proxy_manager/)


### Purchase & Configure Cloudflare Domain
* Purchase your domain via [this](https://developers.cloudflare.com/registrar/get-started/register-domain)
* We'll assume that you purchase a domain of `__MY_SITE__.__COM__`
* Configure `<security stuff>`
* Disable `<caching stuff>`
* Add wildcard CNAME


### Deploy Cloudflare Tunnel
* Deploy via [./cloudflare_tunnel/](./cloudflare_tunnel/)


### Configure Nginx -> Authentik
* xx


### Deploy Authentik LDAP Service
* Deploy via [./authentik_ldap/](./authentik_ldap/)


### Configure Authentik & Nginx to Proxy Jellyfin
1) Configure Authentik
  * xx
1) Configure Nginx
  * xx


### Configure Jellyfin for LDAP Authentication
* xx




Install Nginx Proxy Manager
https://geekscircuit.com/set-up-authentik-sso-with-nginx-proxy-manager/
https://docs.ibracorp.io/authentik/authentik/authentik-proxy-solution


configure authentik ldap
  - https://github.com/jellyfin/jellyfin-plugin-ldapauth/issues/120
  - https://goauthentik.io/integrations/services/pfsense/
  - https://goauthentik.io/integrations/services/sssd/