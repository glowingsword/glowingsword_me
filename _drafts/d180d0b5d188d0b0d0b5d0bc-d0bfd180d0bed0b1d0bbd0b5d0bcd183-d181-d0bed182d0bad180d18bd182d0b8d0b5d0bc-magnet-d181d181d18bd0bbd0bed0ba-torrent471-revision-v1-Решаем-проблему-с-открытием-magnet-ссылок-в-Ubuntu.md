---
id: 473
title: 'Решаем проблему с открытием magnet-ссылок в Ubuntu'
date: '2015-08-23T20:31:22+03:00'
author: 'Андрей Гуцу'
layout: revision
guid: 'http://glowingsword.ru/471-revision-v1/'
permalink: '/?p=473'
---

Если у вас в системе установлено несколько torrent-клиентов, и при нажатии на magnet-ссылку открывается не Ваш любимый клиент - Вам необходимо указать, какой torrent-клиент должен использоваться для открытия magnet-ссылок. Сделать это можно с помощью утилиты  xdg-mime.

Пример использования данной команды для выбора qBittorrent в качестве приложения, используемого по умолчанию для открытия magnet-ссылок
<code>xdg-mime default qBittorrent.desktop x-scheme-handler/magnet</code>