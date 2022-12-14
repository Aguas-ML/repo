---
layout: default
title: Stack para PHPMyAdmin
parent: Notas Docker-compose
nav_order: 10
---

# Compose para PHPMyAdmin
{: .no_toc }

## Tabela de conteúdo
{: .no_toc .text-delta }

1. TOC
{:toc}

---

# Info básica
{: .fs-9 }

**PHPMyAdmin** é um aplicativo web livre e de código aberto para administração do MySQL pela Internet.

**Link** do [site do PHPMyAdmin](https://www.phpmyadmin.net/)


---

# Docker-compose para PHPMyAdmin
Aqui segue um `< docker-compose.yml >` para que você possa levantar uma stack de PHPMyAdmin. Você pode perceber que criamos um volume persistente e explicitamos um `healthcheck`, verifique se é isto que você deseja também.

<div class="code-example" markdown="1">

```
version: '3.8'

networks:
  default:
    external:
      name: proxy

services:
  visordb:
    image: phpmyadmin/phpmyadmin
    container_name: visordb
    restart: always
    environment:
      PMA_ARBITRARY: ${PMA_ARBITRARY}
      PMA_PMADB: ${PMA_PMADB}
      PMA_ABSOLUTE_URI: ${PMA_ABSOLUTE_URI}
      PMA_HOST: ${PMA_HOST}
      PMA_PORT: ${PMA_PORT}
      #VIRTUAL_HOST: ${VIRTUAL_HOST}
      UPLOAD_LIMIT: ${UPLOAD_LIMIT}
    networks:
      - proxy
    ports:
      - "8000:80"
```

</div>

## Variáveis de ambiente
Aqui estão as variáveis de ambiente que nós utilizamos, para um uso saudável com arquivo `.env`


```
MYSQL_ROOT_PASSWORD=
MYSQL_DATABASE=
MYSQL_USER=
MYSQL_PASSWORD=

PMA_HOST=mysql
PMA_PORT=3306
PMA_ARBITRARY=1
PMA_ABSOLUTE_URI=
PMA_PMADB=

VIRTUAL_HOST=
UPLOAD_LIMIT=196M
```
