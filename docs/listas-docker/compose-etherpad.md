---
layout: default
title: Stack para Etherpad-Lite
parent: Notas Docker-compose
nav_order: 4
---

# Compose para Etherpad-Lite
{: .no_toc }

## Tabela de conteúdo
{: .no_toc .text-delta }

1. TOC
{:toc}

---

# Info básica
{: .fs-9 }

**Etherpad-Lite** é um editor online de código aberto altamente personalizável que fornece edição colaborativa de textos, em tempo real.

**Link** do [site do Etherpad-Lite](https://etherpad.org/)


---

# Docker-compose para Etherpad-Lite
Aqui segue um `< docker-compose.yml >` para que você possa levantar uma stack de Etherpad-Lite e MySQL. Você pode perceber que criamos dois volumes persistentes, verifique se é isto que você deseja também.

<div class="code-example" markdown="1">

```
version: '3'

networks:
  proxy:
    external: true

volumes:
  dados:
  plugins:
  
services:
  etherpad:
    image: etherpad/etherpad:latest
    container_name: etherpad
    volumes:
      - dados:/opt/etherpad-lite/var
      - plugins:/opt/etherpad-lite/node_modules
    environment:
      - TITLE=${TITLE}
      - FAVICON=${FAVICON}
      - IP=${IP}
      - DEFAULT_PAD_TEXT=${DEFAULT_PAD_TEXT}
      - ADMIN_PASSWORD=${ADMIN_PASSWORD}
      - ADMIN_USER=${ADMIN_USER}
      - USER_PASSWORD=${USER_PASSWORD}
      - DB_TYPE=${DB_TYPE}
      - DB_HOST=${DB_HOST}
      - DB_PORT=${DB_PORT}
      - DB_NAME=${DB_NAME}
      - DB_USER=${DB_USER}
      - DB_PASS=${DB_PASS}
      - DB_CHARSET=${DB_CHARSET}
      - APIKEY=${APIKEY}
      - SESSION_REQUIRED=false
      - ETHERPAD_PLUGINS=${ETHERPAD_PLUGINS}
      - ETHERPAD_MAXAGE=${ETHERPAD_MAXAGE}
      - TRUST_PROXY=${TRUST_PROXY}
      - NODE_ENV=${NODE_ENV}
      - COOKIE_SAME_SITE=${COOKIE_SAME_SITE}
      - SHOW_SETTINGS_IN_ADMIN_PAGE=${SHOW_SETTINGS_IN_ADMIN_PAGE}
      - SKIN_VARIANTS=${SKIN_VARIANTS}
      #- SKIN_NAME=${SKIN_NAME}
      #- VIRTUAL_HOST=${VIRTUAL_HOST}
      #- LETSENCRYPT_HOST={LETSENCRYPT_HOST}
      #- LETSENCRYPT_EMAIL={LETSENCRYPT_EMAIL}
    networks:
      - proxy
    ports:
      - "9001:9001"
```
</div>

## Variáveis de ambiente
Aqui estão as variáveis de ambiente que nós utilizamos, para um uso saudável com arquivo `.env`


```
TITLE=Pad Aguas
DEFAULT_PAD_TEXT=Que felicidade você no Pad Águas Midia Livre BR! \n\n Somos parte de um serviço global e seguro de Mídia Livre, onde a escrita colaborativa acontece para todes que souberem o link. Lembre-se que aqui você pode criar, compartilhar e editar o mesmo texto que sua equipe de modo anônimo. \n\n Não se esqueça de salvar o link deste pad \n\n Colabore e saiba mais em nossa plataforma https://brasil.aguas.ml
ADMIN_PASSWORD=senhadmin
ADMIN_USER=admin
USER_PASSWORD=senhauser
DB_TYPE=mysql
DB_HOST=db
DB_PORT=3306
DB_NAME=etherpad
DB_USER=etherpad_user
DB_PASS=senhaDB
DB_CHARSET=utf8mb4
APIKEY=crie-sua-chave-fodona-32-caracteres
ETHERPAD_PLUGINS="ep_adminpads2 ep_headings2 ep_image_upload"
ETHERPAD_MAXAGE=7200
SESSION_REQUIRED=false
SKIN_NAME=colibris
SKIN_VARIANTS="super-dark-toolbar dark-background super-light-editor"
VIRTUAL_HOST=seudominio.org
LETSENCRYPT_HOST=seudominio.org
LETSENCRYPT_EMAIL=pad@seudominio.org
TRUST_PROXY=true
NODE_ENV=production
COOKIE_SAME_SITE="Lax"
SHOW_SETTINGS_IN_ADMIN_PAGE=true
```
