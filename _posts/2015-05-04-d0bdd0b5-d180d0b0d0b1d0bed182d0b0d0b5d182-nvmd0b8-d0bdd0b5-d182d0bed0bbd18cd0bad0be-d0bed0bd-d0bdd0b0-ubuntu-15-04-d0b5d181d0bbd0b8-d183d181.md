---
id: 442
title: 'Не работает nvm(и не только он) на ubuntu 15.04 если установлен пакет node'
date: '2015-05-04T16:01:24+03:00'
author: 'Андрей Гуцу'
layout: post
guid: 'http://glowingsword.ru/?p=442'
permalink: /%d0%bd%d0%b5-%d1%80%d0%b0%d0%b1%d0%be%d1%82%d0%b0%d0%b5%d1%82-nvm%d0%b8-%d0%bd%d0%b5-%d1%82%d0%be%d0%bb%d1%8c%d0%ba%d0%be-%d0%be%d0%bd-%d0%bd%d0%b0-ubuntu-15-04-%d0%b5%d1%81%d0%bb%d0%b8-%d1%83%d1%81/
categories:
    - web
---

Столкнулся сегодня с забавной проблемой с node.js на ubuntu. При установке nvm(аналог rvm, только для Node.js) последний отказался работать. Приложение просто крашилось при запуске. Изучение процесса его работы с помощью strace показало, что команда бинарник node ведёт себя как-то странно

<code>open("/etc/ax25/axports", O_RDONLY)     = 4
fstat(4, {st_mode=S_IFREG|0644, st_size=200, ...}) = 0
mmap(NULL, 4096, PROT_READ|PROT_WRITE, MAP_PRIVATE|MAP_ANONYMOUS, -1, 0) = 0x7f0d3e465000
read(4, "# /etc/ax25/axports\n#\n# The form"..., 4096) = 200</code>

Оказалось, что выполнение команды node в ubuntu имеет определённую особенность. В частности, вызов данного приложения приводит к выводу предупреждения

<code>No AX.25 port data configured</code>

которое говорит о том, что в репозиториях ubuntu присуствует пакет node(ПО для радиолюбителей), которое по какой-то причине было установлено на ПК. В результате при запуске приложений вроде nvm происходит запуск команды node, которая(вот так сюрприз) не имеет ничего общего с node.js, ругается на то, что  порт AX.25 не настроен, и досрочно прекращает своё выполнение.

Решается данная проблема двумя способами.

<h3>Способ первый</h3>

<code>
sudo apt-get --purge remove node
sudo apt-get --purge remove nodejs
sudo apt-get install nodejs
sudo apt-get install npm
sudo ln -s /usr/bin/nodejs /usr/bin/node
</code>

<h3>Второй способ</h3>
Так-же решить данную проблему можно, отредактировав файл /usr/local/bin/nvm (у меня он установлен глобально), для чего необходимо заменить 

<code>#!/usr/bin/env node</code>

на 

<code>#!/usr/bin/env nodejs</code> 
￼
<h3>Подведём итоги</h3>
После выполнения любого из данных способов nvm будет работать корректно. Так как данная проблема касается не только nvm, мне больше по душе первый метод решения проблемы. Но если в душе вы - радиолюбитель, и без приложения node вам и жизнь не мила, Вам больше подойдёт второй способ решения данной проблемы.
