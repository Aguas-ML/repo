---
layout: default
title: Stack para Ghost
parent: Notas Docker-compose
nav_order: 4
---

# Compose para Ghost
{: .no_toc }

## Tabela de conteúdo
{: .no_toc .text-delta }

1. TOC
{:toc}

---

# Info básica
{: .fs-9 }

**Ghost** é uma plataforma de blogs gratuita e de código aberto para publicações online.

**Link** do [site do Ghost](https://ghost.org)


---

# Docker-compose para Ghost
Aqui segue um `< docker-compose.yml >` para que você possa levantar uma stack de Ghost utilizando um Banco de Dados MySQL previamente criado. Você pode perceber que criamos um volume persistente, verifique se é isto que você deseja também.

<div class="code-example" markdown="1">

```
version: '3.1'

networks:
  default:
    external:
      name: proxy

volumes:
  conteudo:

services:
  ghost:
    image: ghost:5-alpine
    container_name: ghost
    restart: always
    environment:
      database__client: ${database__client}
      database__connection__host: ${database__connection__host}
      database__connection__user: ${database__connection__user}
      database__connection__password: ${database__connection__password}
      database__connection__database: ${database__connection__database}
      TZ: ${TZ}
      url: ${url}
    volumes:
      - conteudo:/var/lib/ghost/content
    networks:
      - proxy
    ports:
      - 8080:2368
```

</div>

## Variáveis de ambiente
Aqui estão as variáveis de ambiente que nós utilizamos, para um uso saudável com arquivo `.env`


```
database__client=mysql
database__connection__host=mysql
database__connection__user=ghost_user
database__connection__password=senhaDB
database__connection__database=ghost_db
TZ=America/Sao_Paulo
url=https://seudominio.org
```