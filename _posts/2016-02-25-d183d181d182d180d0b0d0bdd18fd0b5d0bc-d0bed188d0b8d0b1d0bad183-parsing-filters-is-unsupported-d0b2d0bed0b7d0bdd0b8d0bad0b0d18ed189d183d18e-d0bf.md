---
id: 522
title: 'Устраняем ошибку &#171;parsing filters is unsupported&#187; возникающую при извлечении rar-архивов в Linux'
date: '2016-02-25T19:36:18+02:00'
author: 'Андрей Гуцу'
layout: post
guid: 'https://glowingsword.ru/?p=522'
permalink: /%d1%83%d1%81%d1%82%d1%80%d0%b0%d0%bd%d1%8f%d0%b5%d0%bc-%d0%be%d1%88%d0%b8%d0%b1%d0%ba%d1%83-parsing-filters-is-unsupported-%d0%b2%d0%be%d0%b7%d0%bd%d0%b8%d0%ba%d0%b0%d1%8e%d1%89%d1%83%d1%8e-%d0%bf/
categories:
    - web
---

При распаковке архивов в формате rar в Ubuntu 15.10 столкнулся с ошибкой "parsing filters is unsupported". Для решения данной проблемы необходимо принудительно переустановить пакеты  p7zip-rar и unrar, после чего извлечение архивов в формате rar будет производиться корректно.

Переустановку упомянутых выше пакетов можно произвести командой

<code>sudo apt-get install --reinstall p7zip-rar unrar</code>