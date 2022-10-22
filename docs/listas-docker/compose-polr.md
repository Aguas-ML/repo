---
layout: default
title: Compose para Polr
parent: Notas para docker
has_children: true
nav_order: 3
---

# Compose para Polr
{: .no_toc }

## Tabela de conteúdo
{: .no_toc .text-delta }

1. TOC
{:toc}

---


---

## Docker-compose versão 3

Aqui segue um `< compose >` para que você possa levantar uma stack de Polr e MariaDB. Você pode perceber que criamos três volumes, verifique se é isto que deseja também.

<div class="code-example" markdown="1">
```docker
version: '3.3'
#####
networks:
  default:
    external:
      name: aguas-proxy
#####
volumes:
  data:
  env:
  ses:
#####
services:
  mariadb:
    image: mariadb
    container_name: mariadb
    restart: always
    expose:
      - "3306"
    environment:
      - MYSQL_ROOT_PASSWORD=${DB_ROOT_PASSWORD}
      - MYSQL_DATABASE=${DB_DATABASE}
      - MYSQL_USER=${DB_USERNAME}
      - MYSQL_PASSWORD=${DB_PASSWORD}
    volumes:
      - data:/var/lib/mysql
  polr:
    image: ajanvier/polr
    container_name: polr
    ports:
      - '8084:80'
    environment:
      DB_HOST: ${DB_HOST}
      DB_PORT: ${DB_PORT}
      DB_DATABASE: ${DB_DATABASE}
      DB_USERNAME: ${DB_USERNAME}
      DB_PASSWORD: ${DB_PASSWORD}
      APP_NAME: ${APP_NAME}
      APP_PROTOCOL: ${APP_PROTOCOL}
      APP_ADDRESS: ${APP_ADDRESS}
      SETTING_PUBLIC_INTERFACE: ${SETTING_PUBLIC_INTERFACE}
      SETTING_SHORTEN_PERMISSION: ${SETTING_SHORTEN_PERMISSION}
      SETTING_ADV_ANALYTICS: ${SETTING_ADV_ANALYTICS}
      ADMIN_USERNAME: ${ADMIN_USERNAME}
      ADMIN_PASSWORD: ${ADMIN_PASSWORD}
    volumes:
      - env:/var/www/.env
      - ses:/var/session
    networks:
      - aguasproxy
#####
```
</div>
Aqui estão as variáveis de ambiente que nós utilizamos.

<div class="code-example" markdown="1">
```env
DB_HOST=mariadb
DB_PORT=3306
DB_DATABASE=db
DB_USERNAME=db
DB_PASSWORD=senha
ADMIN_USERNAME=admin
ADMIN_PASSWORD=senhadmin
ADMIN_EMAIL=seu@amil
APP_NAME=Vai Aguas!
APP_PROTOCOL=https://
APP_ADDRESS=seu.dominio.com
POLR_ALLOW_ACCT_CREATION=false
POLR_ACCT_ACTIVATION=false
POLR_ACCT_CREATION_RECAPTCHA=true
POLR_RECAPTCHA_SITE_KEY=
POLR_RECAPTCHA_SECRET=
POLR_BASE=62
SETTING_PUBLIC_INTERFACE=true
SETTING_SHORTEN_PERMISSION=true
SETTING_AUTO_API=false
SETTING_PSEUDORANDOM_ENDING=true
SETTING_ADV_ANALYTICS=true
```
</div>
