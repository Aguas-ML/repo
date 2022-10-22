---
layout: default
title: Stack para Wordpress
parent: Notas Docker-compose
has_children: true
nav_order: 4
---

# Compose para farmOS
{: .no_toc }

## Tabela de conteúdo
{: .no_toc .text-delta }

1. TOC
{:toc}

---

# Info básica
**farmOS** é um um aplicativo para gerenciamento, planejamento e manutenção de registros de propriedades rurais.

**Link** do [site do farmOS](https://farmos.org)


---

# Docker-compose para farmOS
Aqui segue um `< docker-compose.yml >` para que você possa levantar uma stack de farmOS e MySQL. Você pode perceber que criamos um volume persistente, verifique se é isto que você deseja também.

<div class="code-example" markdown="1">

```
version: '3'

networks:
  default:
    external:
      name: proxy

volumes:
  websites:

services:
  mitmacs:
    image: farmos/farmos:latest
    restart: always
    volumes:
      - websites:/opt/drupal/web/sites
    ports:
      - '8010:80'
    networks:
      - proxy
```