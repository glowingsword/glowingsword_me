---
id: 258
title: 'Cоздание небольшой локальной сети с помощью Ubuntu: настройка DHCP-сервера и DNS-кеширования'
date: '2013-03-07T12:40:47+02:00'
author: 'Андрей Гуцу'
layout: post
guid: 'http://blog.lordofgale.org/?p=258'
permalink: /c%d0%be%d0%b7%d0%b4%d0%b0%d0%bd%d0%b8%d0%b5-%d0%bd%d0%b5%d0%b1%d0%be%d0%bb%d1%8c%d1%88%d0%be%d0%b9-%d0%bb%d0%be%d0%ba%d0%b0%d0%bb%d1%8c%d0%bd%d0%be%d0%b9-%d1%81%d0%b5%d1%82%d0%b8-%d1%81-%d0%bf%d0%be/
categories:
    - ubuntu
    - сеть
---

<p>
Настраиваем DNS-кеширование и динамическую настройку узлов(что-бы не надо было ручками прописывать IP узла, маску подсети и прочее на каждом узле сети) . Для этого мы должны установить(если он ещё не установлен) пакет dnsmasq:
<pre>
<code class="bash">
apt-get install dnsmasq
</code>
</pre>
</p>
<p>
Настройка dnsmasq сводится к прописыванию настроек в конфигурационном файле /etc/dnsmasq.conf  нужных нам настроек. Открываем его командой:
<pre>
<code class="bash">
sudo gedit /etc/dnsmasq.conf
</code>
</pre>
</p>
<p>
<!--more-->
И прописываем следующие настройки:
<pre>
<code class="bash">
# Интерфейсы, которые будет слушать dnsmasq
# интерфейс localhost
interface=lo

# Не предоставлять DHCP(другие сервисы, кроме DNS) на указанном
# интерфейсе
no-dhcp-interface=lo

# интерфейс, смотрящий в нашу локальную сеть 
interface=eth1

# Адрес, который будет слушать dnsmasq для отслеживания запросов DNS
listen-address=127.0.0.1,192.168.0.1

# Диапазон адресов, которые будет раздавать узлам наш DHCP
dhcp-range=192.168.0.2,192.168.0.250

# Домен нашей локальной сети, у меня это dev
domain=dev,192.168.0.2,192.168.0.254

#Локальный домен
local=/dev/

# DHCP будет работать в режиме 3(роутер), адрес шлюза нашей сети 192.168.0.1
dhcp-option=3,192.168.0.1

# Некоторые программы запускают свой экземпляр dnsmasq
# Для того, что-бы исключить конфликты за интерфейсы, 
# мы делаем из доступными для всех интерфейсов
bind-interfaces

# Обычно dnsmasq пересылает DNS-запросы на адрес DNS-сервера, выбранного из  файла /etc/resolv.conf в случайном порядке. Данная опция говорит dnsmaq слать запросы на адреса в строгом порядке с, начиная с первого адреса, и в глубь списка.
strict-order

# Описание узлов сети, где мы указываем:  
#    MAC-адрес
#    имя узла(hostname)
#    IP 
#   время аренды
dhcp-host=52:54:00:12:03:85,vserv,192.168.0.3,infinite
dhcp-host=52:54:00:03:02:85,devserv,192.168.0.8,infinite

# Записи вида CNAME(псевдонимы для доменного имени узла)
cname=lordofgale.dev,devserv
cname=www.lordofgale.dev,devserv
</code>
</pre>
</p>
<p>
Редактируем файл “/etc/dhcp/dhclient.conf”:
<pre>
<code class="bash">
sudo gedit /etc/dhcp/dhclient.conf
</code>
</pre>
</p>
<p>
Ищем строку “prepend domain-name-servers 127.0.0.1;”, если перед ней был символ комментария, убираем его. Что-бы всё там выглядело примерно так:
<pre>
<code class="bash">
#supersede domain-name "fugue.com home.vix.com";
prepend domain-name-servers 127.0.0.1;
request subnet-mask, broadcast-address, time-offset, routers,
domain-name, domain-name-servers, host-name,
netbios-name-servers, netbios-scope;
</code>
</pre>
</p>
Редактируем файл /etc/resolv.conf, если у вас не установлен пакет resolver. Убеждаемся, что у нас прописан локальный nameserver с адресом  127.0.0.1:
<pre>
<code class="bash">
nameserver 127.0.0.1
search lan
</code>
</pre>

<p>
Перезагружаем сервис dnsmasq:
<pre>
<code class="bash">
sudo /etc/init.d/dnsmasq restart
</code>
</pre>
</p>
<p>
Проверяем работу dnsmasq, используя для этого команду:
<pre>
<code class="bash">
dig ubuntu.com
</code>
</pre>
</p>
<p>
Повторяем её, и получаем во второй раз результат  "Query time: 0 msec", что не может не радовать. Если сетевые настройки вашей сети были прописаны вручную, на всех узлах сети нужно настроить автоматическую настройку сети при помощи DHCP. Поздравляю, теперь ваша сеть настроена как надо, и узлы сети видны не только по IP, но и по именам узлов(hostname). Проверить это можно командой 
ping < имя узла>
</p>
<p>
Как всегда, после хорошо проделанной работы вы заслужили отдых, а значит - время пить чай. Можете уже ставить чайник и доставать печеньки. Удачи!</p>