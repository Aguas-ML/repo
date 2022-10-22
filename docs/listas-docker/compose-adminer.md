---
layout: default
title: Stack para Adminer
parent: Notas Docker-compose
nav_order: 2
---

# Deploy do Adminer
{: .no_toc }

## Tabela de conteúdo
{: .no_toc .text-delta }

1. TOC
{:toc}

---

# Info básica
**Adminer** é uma ferramenta para gerenciamento de conteúdo em bancos de dados. Ele suporta nativamente MySQL, MariaDB, PostgreSQL, SQLite, MS SQL, Oracle, Elasticsearch e MongoDB.

**Link** do [site do Adminer](https://adminer.org/)


---

# Adminer em produção
Aqui segue um `< docker-compose.yml >` para que você possa levantar um container de Adminer em **produção**.


<div class="code-example" markdown="1">

```
  adminer:
    image: adminer
    container_name: adminer
    restart: always
    ports: ['8080:8080']
    networks:
      - proxy
```