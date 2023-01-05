---
id: 368
title: 'Не работает автодополнение в Bash несмотря на то, что установлена последняя версия bash-completion'
date: '2013-12-06T14:44:55+02:00'
author: 'Андрей Гуцу'
layout: post
guid: 'http://blog.glowingsword.ru/?p=368'
permalink: /%d0%bd%d0%b5-%d1%80%d0%b0%d0%b1%d0%be%d1%82%d0%b0%d0%b5%d1%82-%d0%b0%d0%b2%d1%82%d0%be%d0%b4%d0%be%d0%bf%d0%be%d0%bb%d0%bd%d0%b5%d0%bd%d0%b8%d0%b5-%d0%b2-bash-%d0%bd%d0%b5%d1%81%d0%bc%d0%be%d1%82/
categories:
    - linux
    - ubuntu
---

Сегодня обнаружил, что у меня не работает автодополнение в Bash(после ввода фрагмента команды достаточно нажать Tab, и срабатывает автодополнение). Пакет bash-completion при этом был установлен, и по идее всё должно было работать. Оказалось, что источник проблемы крылся в конфигурационном файле /etc/bash.bashrc. Достаточно было убрать символ комментария со всех строк, кроме первой, в данном фрагменте конфигурационного файла:

 # enable bash completion in interactive shells
 #if ! shopt -oq posix; then
 #  if [ -f /usr/share/bash-completion/bash_completion ]; then
 #    . /usr/share/bash-completion/bash_completion
 #  elif [ -f /etc/bash_completion ]; then
 #    . /etc/bash_completion
 #  fi
 #fi 

и перезапустить оболочку bash, как автодополнение заработало.