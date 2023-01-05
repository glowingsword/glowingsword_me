---
id: 468
title: 'Не запускается Docker 1.7.1 на Ubuntu 15.04'
date: '2015-08-05T00:16:39+03:00'
author: 'Андрей Гуцу'
layout: revision
guid: 'http://glowingsword.ru/465-autosave-v1/'
permalink: '/?p=468'
---

Обновил Docker до 1.7.1 - Docker перестал запускаться. Оказалось, что при его запуске возникает ошибка

<code>INFO[0000] Listening for HTTP on unix (/var/run/docker.sock)
ERRO[0000] [graphdriver] prior storage driver "aufs" failed: driver not supported
FATA[0000] Error starting daemon: error initializing graphdriver: driver not supported </code>

Для решения данной проблемы открываем файл /lib/systemd/system/docker.service и заменяем строку

<code>ExecStart=/usr/bin/docker daemon -H fd://</code>

на

<code>ExecStart=/usr/bin/docker daemon -H fd:// --storage-driver=overlay</code>

после чего Docker успешно запускается командами

<code>sudo systemctl daemon-reload
sudo systemctl start docker.service</code>

К сожалению, использование Overlay FS - не самый лучший выход для тех, у кого уже было создано немалое количество контейнеров, так как их придётся создавать заново. В случае если у вас уже создано немалое количество контейнеров, вместо перехода на Overlay FS возможно Вам стоит рассмотреть возможность понижения версии Docker.