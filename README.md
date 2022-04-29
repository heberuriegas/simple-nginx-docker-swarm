# Docker swarm deploy automation

This repo use Nginx + Let's encrypt + Digitalocean + Cloudflare to deploy multiple sites in a docker swarm manager.

It was inspired by the need to have small experiments without have a server for each of them.

## Setup

### 1. Setup Cloudflare

1. Creagte a cloudflare account
2. Add as many sites as needed
3. Get api token to get ssl certificates (https://dash.cloudflare.com/profile/api-tokens)

### 2. Setup Digitalocean

1. Create an account in Digital ocean
2. Create a docker droplet from digital ocean marketplace (https://marketplace.digitalocean.com/apps/docker)

   Note: I recommend you to keep the main ssd disk in 25 SSD and add a block storage so you can resize the server to any size later.

## Installation

### Setup server

- Swarm manager & private docker registry

1. SSH to docker instance
2. Run setup_manager

```
bash <(curl -s https://raw.githubusercontent.com/woohoou/simple-nginx-docker-swarm/main/setup_manager)
```

### Setup local development

1. Run setup with production and staging environment

```
./setup -p prd.my_domain.com -s stg.my_domain.com
```

2. Login into the private registry

```
docker login my_domain.com:5000
```

3. Deploy to server

```
cd nginx && docker_swarm_deploy
```

### Configure the application

4. Copy the reverse proxy sample

```
cp reverse_proxy.conf.sample my_domain.conf
```

5. Rename server name and redirect (my_domain.com) in my_domain.conf
