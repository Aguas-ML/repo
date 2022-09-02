---
layout: default
title: Compose para Wordpress
parent: Notas para docker
has_children: true
nav_order: 2
---

# Compose para Wordpress
{: .no_toc }

## Tabela de conteúdo
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## Inline code

Code can be rendered inline by wrapping it in single back ticks.

<div class="code-example" markdown="1">
Lorem ipsum dolor sit amet, `<inline code snippet>` adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.

## Heading with `<inline code snippet>` in it.
{: .no_toc }
</div>
```markdown
Lorem ipsum dolor sit amet, `<inline code snippet>` adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.

## Heading with `<inline code snippet>` in it.
```

---

## Syntax highlighted code blocks

Use Jekyll's built-in syntax highlighting with Rouge for code blocks by using three backticks, followed by the language name:

<div class="code-example" markdown="1">
```docker
version: "3"

networks:
  default:
    external:
      name: aguas-proxy

volumes:
  aguas_db:
  aguas_dados:
  
services:
  mysql:
    image: mysql:5.7
    volumes:
      - aguas_db:/var/lib/mysql
    ports:
      - 13304:3306
    restart: always
    environment:
      MYSQL_ROOT_PASSWORD: senhamysqlroot
      MYSQL_DATABASE: aguas_db
      MYSQL_USER: aguas_wp
      MYSQL_PASSWORD: senhamysql

  wordpress:
    image: wordpress:latest
    #ports:
    #  - 8090:80
    expose:
      - 80
    depends_on:
      - mysql
    restart: always
    environment:
      VIRTUAL_HOST: aguas.ml
      LETSENCRYPT_HOST: aguas.ml
      LETSENCRYPT_EMAIL: email@aguas.ml
      WORDPRESS_DB_HOST: mysql:3306
      WORDPRESS_DB_USER: aguas_wp
      WORDPRESS_DB_PASSWORD: senhamysql
      WORDPRESS_DB_NAME: aguas_db
    volumes:
      - aguas_dados:/var/www/html
```
</div>
{% highlight markdown %}
```js
// Javascript code with syntax highlighting.
var fun = function lang(l) {
  dateformat.i18n = require('./lang/' + l)
  return true;
}
```
{% endhighlight %}

---
