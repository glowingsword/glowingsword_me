---
id: 501
date: '2015-11-28T16:50:03+02:00'
author: 'Андрей Гуцу'
layout: revision
guid: 'https://glowingsword.ru/500-revision-v1/'
permalink: '/?p=501'
---

Сегодня при обновлении пакетов в Centos 7 обратил внимание на ошибку

Delta RPMs disabled because /usr/bin/applydeltarpm not installed.

Узнаём какой пакет предоставляет приложение /usr/bin/applydeltarpm с помощью команды

<code>yum provides '*/applydeltarpm'</code>

Результат выполнения команды

deltarpm-3.6-3.el7.x86_64 : Create deltas between rpms
Repo        : base
Matched from:
Filename    : /usr/bin/applydeltarpm

deltarpm-3.6-3.el7.x86_64 : Create deltas between rpms
Repo        : @base
Matched from:
Filename    : /usr/bin/applydeltarpm

И устанавливаем необходимые пакет

<code>yum install deltarpm</code>