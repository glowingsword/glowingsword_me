---
id: 295
title: 'Исправление конфликта openoffice4.0-debian-menus с libreoffice'
date: '2013-07-25T14:56:24+03:00'
author: 'Андрей Гуцу'
layout: revision
guid: 'http://blog.lordofgale.org/2013/07/292-autosave/'
permalink: '/?p=295'
---

<p>Вчера решил себе установить вышедший на днях офисный пакет Apache OpenOffice 4.0, при этом не удаляя LibreOffice. Оба пакета имеют сходный функционал, но при этом на данный момент некоторые возможности лучше реализованы в одном пакете, а другие - в другом пакете. Скачал тарбол с нужными deb-пакетами для Ubuntu 13.04 с сайта <a href="http://www.openoffice.org" title="http://www.openoffice.org">http://www.openoffice.org</a>, распаковал тарбол и  установил все пакеты командой:  
<pre>
<code class='bash'>
sudo dpkg -i *.deb
</code>
</pre>
</p>
<p>
После установки оказалось, что нужно было ещё установить пакет openoffice4.0-debian-menus_4.0-9702_all.deb из каталога desktop-integration. Без него установленный Open Office можно запускать только из командной строки, а ярлыки в Dash(в меню приложений) не появляются. Устанавливать же данный пакет не получается. Файл /usr/bin/soffice из пакета openoffice4.0-debian-menus конфликтует с уже установленным файлом /usr/bin/soffice пакета Libre Office. Исправляем возникшую проблему ручками. Распаковываем пакет openoffice4.0-debian-menus в каталог openoffice4.0-debian-menus_4.0-9702_all:
<pre>
<code class='bash'>
dpkg --extract openoffice4.0-debian-menus_4.0-9702_all.deb openoffice4.0-debian-menus_4.0
</code>
</pre>
</p>
<p>
Удаляем файл openoffice4.0-debian-menus_4.0/usr/bin/soffice командой:
<pre>
<code class='bash'>
rm openoffice4.0-debian-menus_4.0/usr/bin/soffice
</code>
</pre>
</p>
<p>
И собираем пакет openoffice4.0-debian-menus_4.0.deb командой:
<pre>
<code class='bash'>
fakeroot dpkg-deb --build openoffice4.0-debian-menus_4.0
</code>
</pre>
</p>
<p>
И устанавливаем полученный пакет командой:
<pre>
<code class='bash'>
sudo dpkg -i openoffice4.0-debian-menus_4.0.deb
</code>
</pre>
</p>
<p>Ну всё, проблема решена. Apache OpenOffice установлен одновременно с LibreOffice, конфликт устранён и вы можете работать с обоими офисными пакетами.</p>
