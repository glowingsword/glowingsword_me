---
id: 358
title: 'Устранение проблемы с pulseaudio'
date: '2013-10-10T20:53:57+03:00'
author: 'Андрей Гуцу'
layout: post
guid: 'http://blog.glowingsword.ru/?p=358'
permalink: /%d1%83%d1%81%d1%82%d1%80%d0%b0%d0%bd%d0%b5%d0%bd%d0%b8%d0%b5-%d0%bf%d1%80%d0%be%d0%b1%d0%bb%d0%b5%d0%bc%d1%8b-%d1%81-pulseaudio/
categories:
    - web
---

После вчерашнего обновления системы у меня вдруг отвалился pulseaudio в Ubuntu 13.04. Весьма не вовремя кстати. Как раз, как я собрался посмотреть серию одного из моих любимых сериалов. Рестарт сервиса, перезагрузка сервиса, переустановка pulseaudio и прочие трюки ничего не дали. Тогда я взял содержимое от эталонного конфигурационного файла /etc/pulse/default.pa, вставил его вместо того, что было в данном файле у меня, назначил нужные права и после этого pulseaudio неожиданно заработал. А ведь до этого не помогало даже:

sudo apt-get --purge --reinstall install pulseaudio

Оказалось, что на default.pa были выставлены неверные права. Pulseaudio не имея возможности прочитать конфиг, не грузил нужные для работы модули, и это  приводило к ошибке  [pulseaudio] main.c: Daemon startup without any loaded modules, refusing to work.