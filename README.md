# basalt-authentication-module

## Overview

## This is the runnable service for Basalt authentication

## Keycloak Setup using Docker
We run keycloak using Docker containers pointing to a DB
Create a database called *basalt_auth_db*
Start the container
Please check for the latest container build here: https://quay.io/repository/keycloak/keycloak
### Dev:
```shell
docker run --name basalt-keycloak-server --network host -d \
        -e KEYCLOAK_ADMIN=admin -e KEYCLOAK_ADMIN_PASSWORD=password \
        quay.io/keycloak/keycloak:21.0.1 \
        start-dev \
        --db=postgres \
        --features=token-exchange \
        --db-url=jdbc:postgresql://localhost/basalt_auth_db \
        --db-username=postgres \
        --db-password=postgres \
        --hostname-strict=false
```
### Dev
