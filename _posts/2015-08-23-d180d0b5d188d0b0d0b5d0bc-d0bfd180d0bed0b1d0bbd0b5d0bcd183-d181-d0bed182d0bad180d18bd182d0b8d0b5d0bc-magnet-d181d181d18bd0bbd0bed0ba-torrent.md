---
id: 471
title: 'Решаем проблему с открытием magnet-ссылок в Ubuntu'
date: '2015-08-23T20:30:29+03:00'
author: 'Андрей Гуцу'
layout: post
guid: 'http://glowingsword.ru/?p=471'
permalink: /%d1%80%d0%b5%d1%88%d0%b0%d0%b5%d0%bc-%d0%bf%d1%80%d0%be%d0%b1%d0%bb%d0%b5%d0%bc%d1%83-%d1%81-%d0%be%d1%82%d0%ba%d1%80%d1%8b%d1%82%d0%b8%d0%b5%d0%bc-magnet-%d1%81%d1%81%d1%8b%d0%bb%d0%be%d0%ba-torrent/
categories:
    - web
---

Если у вас в системе установлено несколько torrent-клиентов, и при нажатии на magnet-ссылку открывается не Ваш любимый клиент - Вам необходимо указать, какой torrent-клиент должен использоваться для открытия magnet-ссылок. Сделать это можно с помощью утилиты  xdg-mime.

Пример использования данной команды для выбора qBittorrent в качестве приложения, используемого по умолчанию для открытия magnet-ссылок
<code>xdg-mime default qBittorrent.desktop x-scheme-handler/magnet</code>