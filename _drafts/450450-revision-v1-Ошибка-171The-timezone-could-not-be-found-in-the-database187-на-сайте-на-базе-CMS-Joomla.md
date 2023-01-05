---
id: 453
title: 'Ошибка &#171;The timezone could not be found in the database&#187; на сайте на базе CMS Joomla'
date: '2015-05-12T19:31:06+03:00'
author: 'Андрей Гуцу'
layout: revision
guid: 'http://glowingsword.ru/450-revision-v1/'
permalink: '/?p=453'
---

Если во время работы сайта на CMS Joomla возникает ошибка

 0 DateTime::__construct() [datetime.--construct]: Failed to parse time string (jerror) at position 0 (j): The timezone could not be found in the database

Как правило, данная ошибка вызвана не корректно указанным путём к каталогам logs и tmp, или при отсутствии прав на запись данных каталогов и не имеет отношения к  информации timezone в базе данных. После исправления значения опций 

public $log_path = '/var/www/username/public_html/logs';
public $tmp_path = '/var/www/username/public_html/tmp';

на корректные, где вместо "/var/www/username/public_html" должен быть указан полный путь к домашнему каталогу Вашего сайта, данная ошибка в большинстве случаев перестаёт проявляться.