---
id: 448
title: 'Не сохраняются правила iptables в centos'
date: '2015-05-12T18:51:22+03:00'
author: 'Андрей Гуцу'
layout: post
guid: 'http://glowingsword.ru/?p=448'
permalink: /%d0%bd%d0%b5-%d1%81%d0%be%d1%85%d1%80%d0%b0%d0%bd%d1%8f%d1%8e%d1%82%d1%81%d1%8f-%d0%bf%d1%80%d0%b0%d0%b2%d0%b8%d0%bb%d0%b0-iptables-%d0%b2-centos/
categories:
    - web
---

Столкнулся с забавной ошибкой, возникающей при сохранении правил iptables. При выполнении команды

#service iptables save

возникает ошибка

<code>iptables: Saving firewall rules to /etc/sysconfig/iptables: /etc/init.d/iptables: line 268: restorecon: command not found</code>
                                                           [FAILED]
Проблема решается простой установкой недостающего пакета

<code>yum install policycoreutils</code>

после чего сохранение правил происходит успешно.
