# SCBD Omeka

## Prerequisite  

### Networks
- `websites` (from load-balancer)

```
docker network create --driver=DRIVER_NAME websites
```
OR
```
docker network create  websites
```

### Volumes
- omeka-html
- omeka-db

```
docker volume create omeka-html
docker volume create omeka-db
```
OR
For a local persistant solution install `local-persist` volume driver https://github.com/CWSpear/local-persist

```
curl -fsSL https://raw.githubusercontent.com/CWSpear/local-persist/master/scripts/install.sh | sudo bash
```

```
docker volume create --driver local-persist --opt mountpoint=/omeka/html --name=omeka-html
docker volume create --driver local-persist --opt mountpoint=/omeka/db   --name=omeka-db
```
OR 

## build

```
docker build https://github.com/scbd/omeka-docker.git -t scbd/omeka
```

## Start Omeka

The stack need to run behind a `Traefik` loadbalancer

```
curl -s https://raw.githubusercontent.com/scbd/omeka-docker/master/docker-compose.yml | docker-compose -f - -p omeka up -d
```
