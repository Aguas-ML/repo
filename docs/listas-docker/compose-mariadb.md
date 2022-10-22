---
layout: default
title: Stack para MariaDB
parent: Notas Docker-compose
has_children: true
nav_order: 7
---

# Compose para MariaDB
{: .no_toc }

## Tabela de conteúdo
{: .no_toc .text-delta }

1. TOC
{:toc}

---

# Info básica
**MariaDB** é um sistema de gerenciamento de banco de dados que surgiu como fork do MySQL.

**Link** do [site do MariaDB](https://mariadb.org)


---

# Docker-compose para MariaDB
Aqui segue um `< docker-compose.yml >` para que você possa levantar uma stack de MariaDB. Você pode perceber que criamos um volume persistente e explicitamos um `healthcheck`, verifique se é isto que você deseja também.

<div class="code-example" markdown="1">

```
version: '3.1'

networks:
  default:
    external:
      name: proxy

volumes:
  datos:

services:
  mariadb:
    container_name: mariadb
    hostname: mariadb
    image: mariadb
    command: >
      --character-set-server=utf8mb4
      --collation-server=utf8mb4_general_ci
      --max-allowed-packet=196M
    restart: always
    expose:
        - "3444"
    ports:
        - "3444:3306"
    environment:
      MYSQL_ROOT_PASSWORD: ${MYSQL_ROOT_PASSWORD}
      MYSQL_USER:  ${MYSQL_USER} 
      MYSQL_PASSWORD: ${MYSQL_PASSWORD}
      TZ: America/Sao_Paulo
    volumes:
      - datos:/var/lib/mysql
    healthcheck:
      test: ["CMD", "mysqladmin", "ping", "--silent"]
      interval: 30s
      timeout: 10s
      retries: 3
    networks:
      - proxy
```

