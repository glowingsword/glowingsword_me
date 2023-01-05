---
id: 547
title: 'Ошибка Couldn&#8217;t open file for write: Permission denied при обновлении статистики awstat на серверах с ISPManager4'
date: '2016-08-16T20:41:23+03:00'
author: 'Андрей Гуцу'
layout: post
guid: 'https://21FA4F1A-0BE8-430A-92FD-074BEA963D57'
permalink: /%d0%be%d1%88%d0%b8%d0%b1%d0%ba%d0%b0-couldnt-open-file-for-write-permission-denied-%d0%bf%d1%80%d0%b8-%d0%be%d0%b1%d0%bd%d0%be%d0%b2%d0%bb%d0%b5%d0%bd%d0%b8%d0%b8-%d1%81%d1%82%d0%b0%d1%82%d0%b8/
categories:
    - web
---

Столкнулся с забавной ошибкой, возникающей на серверах с панелью управления ISPManager 4. Ошибка возникает из-за того, что на сервере присутствует задание cron по умолчанию, идущее в стандартной поставке с awstat и отвечающее за обновление статистики awstat, хотя на серверах с панелью управления вместо данного задания используется задание панели управления ISPManager 4, которое производит ротацию логов и корректно обвноление статистики awstat. Проявляется данная проблема в виде писем вида

Create/Update database for config "/etc/awstats/awstats.example.com.conf" by AWStats version 7.0
From data in log file "/var/www/testuser/data/logs/example.com.access.log"...
Phase 1 : First bypass old records, searching new record...
Direct access to last remembered record has fallen on another record.
So searching new records from beginning of log file...
Phase 2 : Now process new records (Flush history on disk after 20000 hosts)...
Error: Couldn't open file "/var/www/testuser/data/www/example.com/webstat/awstats082016.example.com.tmp.16953" for write: Permission denied
Setup ('/etc/awstats/awstats.example.com.conf' file, web server or permissions) may be wrong.
Check config file, permissions and AWStats documentation (in 'docs' directory).


которые периодически отправляются администратору сервера планоровщиком cron. Возникает данная проблема из-за заданий cron вида
https://gist.github.com/glowingsword/78d5159c382078b2d7c9b7d37fd23c45

указанных в файле /etc/cron.d/awstats. Для решения данной проблемы достаточно удалить файл /etc/cron.d/awstats, в котором, как правило присутсвуте указанное выше заданиe.