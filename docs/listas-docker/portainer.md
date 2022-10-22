---
layout: default
title: Deploy do Portainer
parent: Notas Docker-compose
has_children: true
nav_order: 3
---

# Deploy do Portainer
{: .no_toc }

## Tabela de conteúdo
{: .no_toc .text-delta }

1. TOC
{:toc}

---

# Info básica
**Portainer** é um sistema livre e aberto de gestão de conteúdo para internet, baseado em PHP com banco de dados MySQL.

**Link** do [site do Portainer](https://wordpress.org)


---

# Portainer em produção
Aqui segue um `< docker-compose.yml >` para que você possa levantar uma stack de Porainer em produção. Você pode perceber que é preciso acesso `ssh` e ter sob controle o `docker` e o `docker-compose`. Verifique se é isto que você deseja também.


<div class="code-example" markdown="1">

```
docker stack deploy -c portainer.yml portainer

docker run -d -p 8000:8000 -p 9443:9443 --name portainer --restart=always \
    -v /var/run/docker.sock:/var/run/docker.sock \
    -v portainer_data:/data portainer/portainer-ee:latest \
    --templates https://raw.githubusercontent.com/edutcm/edustack/main/templates.json
```

</div>