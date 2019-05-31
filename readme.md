# Set up [nginx-proxy](https://github.com/jwilder/nginx-proxy) with [letsencrypt-nginx-proxy-companion](https://github.com/JrCs/docker-letsencrypt-nginx-proxy-companion)

## Step 1. Getting set up network

Create a unique network for nginx-proxy and other Docker containers to communicate through.

`docker network create nginx-proxy`

## Step 2. Clone repository

Clone this repository.

`git clone git@github.com:evgeny-golubev/docker-nginx-proxy-with-lets-encrypt`

## Step 3. Running nginx-proxy

Now run the docker-compose command.

`cd docker-nginx-proxy-with-lets-encrypt && docker-compose up -d`

## Step 4. Configure your containers

In your container you must configure the following:

* Three environment variables: `VIRTUAL_HOST`, `VIRTUAL_PORT` (80 by default), `LETSENCRYPT_HOST`, `LETSENCRYPT_EMAIL`

```yaml
environment:
    VIRTUAL_HOST: example.com
    VIRTUAL_PORT: 80
    LETSENCRYPT_HOST: example.com
    LETSENCRYPT_EMAIL: email@example.com
```

* Exposing port 80 or change VIRTUAL_PORT if other

```yaml
expose:
  - 80
```

* The Docker network: `nginx-proxy`

```yaml
networks:
    default:
        external:
            name: nginx-proxy
```