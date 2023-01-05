---
id: 449
title: 'Не сохраняются правила iptables в centos'
date: '2015-05-12T18:51:22+03:00'
author: 'Андрей Гуцу'
layout: revision
guid: 'http://glowingsword.ru/448-revision-v1/'
permalink: '/?p=449'
---

Столкнулся с забавной ошибкой, возникающей при сохранении правил iptables. При выполнении команды

#service iptables save

возникает ошибка

<code>iptables: Saving firewall rules to /etc/sysconfig/iptables: /etc/init.d/iptables: line 268: restorecon: command not found</code>
                                                           [FAILED]
Проблема решается простой установкой недостающего пакета

<code>yum install policycoreutils</code>

после чего сохранение правил происходит успешно.
