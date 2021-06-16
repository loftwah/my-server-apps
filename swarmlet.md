https://github.com/swarmlet/swarmlet

Installation
Make sure you have a (sub) domain available which is pointed to your server, this is necessary to access the Traefik or Portainer/Matomo dashboards located at e.g. portainer.your-domain.com.

To install the latest version of Swarmlet, log in to your server as root and run:

curl -fsSL https://get.swarmlet.dev | bash
The installation should take a few minutes to complete.

Full installation instructions can be found here

Custom installation
# Headless (noninteractive) installation:
curl -fsSL https://get.swarmlet.dev | bash -s \
  INSTALLATION_TYPE=noninteractive \
  INSTALL_ZSH=true \
  INSTALL_MODULES="matomo swarmpit" \
  NEW_HOSTNAME=swarm-manager-1 \
  SWARMLET_USERNAME=admin \
  SWARMLET_PASSWORD=nicepassword \
  ROOT_DOMAIN=dev.mydomain.com

  ## Examples

Swarmlet includes various examples of services that you can deploy to your server cluster with a simple `git push`.

*   [swarmlet-website - The swarmlet.dev website](https://github.com/swarmlet/swarmlet-website)
*   [get-swarmlet - The get.swarmlet.dev install script](https://github.com/swarmlet/swarmlet/tree/master/examples)
*   [Basic example - Static site](https://github.com/swarmlet/swarmlet/tree/master/examples)
*   [Basic example - Python web server + Redis](https://github.com/swarmlet/swarmlet/tree/master/examples)
*   [Moderate example - NGINX + React app + Node.js API](https://github.com/swarmlet/swarmlet/tree/master/examples)
*   (FIX) [Advanced example - NGINX + React app + Node.js API + CMS + staging/production](https://github.com/swarmlet/swarmlet/tree/master/examples)
*   (FIX) [GitLab CE](https://github.com/swarmlet/swarmlet/tree/master/examples) (self-hosted)
*   (FIX) [GitLab Runner](https://github.com/swarmlet/swarmlet/tree/master/examples) (self-hosted)

All these examples and the [Swarmlet documentation and website](https://swarmlet.dev) are running on a €5/mo *single* server 'cluster', using Swarmlet for deployments.

https://swarmlet.dev/docs/getting-started/installation