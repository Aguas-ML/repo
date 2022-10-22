---
layout: default
title: Stack para Wordpress
parent: Notas Docker-compose
has_children: true
nav_order: 12
---

# Compose para Wordpress
{: .no_toc }

## Tabela de conteúdo
{: .no_toc .text-delta }

1. TOC
{:toc}

---

# Info básica
**WordPress** é um sistema livre e aberto de gestão de conteúdo para internet, baseado em PHP com banco de dados MySQL.

**Link** do [site do WP](https://wordpress.org)


---

# Docker-compose para Wordpress
Aqui segue um `< docker-compose.yml >` para que você possa levantar uma stack de Wordpress e MySQL. Você pode perceber que criamos dois volumes persistentes, verifique se é isto que você deseja também.

<div class="code-example" markdown="1">

```
version: "3"

networks:
  default:
    external:
      name: aguas-proxy

volumes:
  aguas_wpdb:
  aguas_wpdados:
  
services:
  mysql:
    image: mysql:5.7
    volumes:
      - aguas_wpdb:/var/lib/mysql
    ports:
      - 10000:3306
    restart: always
    environment:
      MYSQL_ROOT_PASSWORD: senhamysqlroot
      MYSQL_DATABASE: aguas_db
      MYSQL_USER: aguas_wp
      MYSQL_PASSWORD: senhamysql

  wordpress:
    image: wordpress:latest
    #ports:
    #  - 8000:80
    expose:
      - 80
    depends_on:
      - mysql
    restart: always
    environment:
      VIRTUAL_HOST: ${VIRTUAL_HOST}
      LETSENCRYPT_HOST: ${LETSENCRYPT_HOST}
      LETSENCRYPT_EMAIL: ${LETSENCRYPT_EMAIL}
      WORDPRESS_DB_HOST: ${WORDPRESS_DB_HOST}
      WORDPRESS_DB_NAME: ${WORDPRESS_DB_NAME}
      WORDPRESS_DB_USER: ${WORDPRESS_DB_USER}
      WORDPRESS_DB_PASSWORD: ${WORDPRESS_DB_PASSWORD}
    volumes:
      - aguas_wpdados:/var/www/html
```

</div>

---

## Variáveis de ambiente
Aqui estão as variáveis de ambiente que nós utilizamos, para um uso saudável com arquivo `.env`

<div class="code-example" markdown="1">

```
MYSQL_ROOT_PASSWORD=senhaforte
MYSQL_DATABASE=db
MYSQL_USER=dbuser
MYSQL_PASSWORD=senhaDB

WORDPRESS_DB_HOST=mysql
WORDPRESS_DB_NAME=db
WORDPRESS_DB_USER=dbuser
WORDPRESS_DB_PASSWORD=senhaDB

VIRTUAL_HOST=seudominio.org
LETSENCRYPT_HOST=seudominio.org
LETSENCRYPT_EMAIL=contato@seudominio.org
```
</div>
