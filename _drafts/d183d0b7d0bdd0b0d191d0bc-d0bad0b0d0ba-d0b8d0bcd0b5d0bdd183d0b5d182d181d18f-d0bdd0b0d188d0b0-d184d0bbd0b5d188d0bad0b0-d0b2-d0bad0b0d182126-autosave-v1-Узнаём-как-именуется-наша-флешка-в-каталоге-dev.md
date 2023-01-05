---
id: 131
title: 'Узнаём, как именуется наша флешка в каталоге /dev'
date: '2012-11-28T16:01:29+02:00'
author: 'Андрей Гуцу'
layout: revision
guid: 'http://blog.lordofgale.org/2012/11/126-autosave/'
permalink: '/?p=131'
---

<p>
Узнаём, как именуется наша флешка в каталоге /dev(к примеру, она может именоваться /dev/sda , /dev/sdb и т.д.) Для этого используем стандартные утилиты Linux, используемые для редактирования таблицы разделов на дисках.
</p>
<pre>
<code class="bash">
sudo fdisk -l
</code>
</pre>
<a href="http://blog.lordofgale.org/wp-content/uploads/2012/11/Screenshot-from-2012-11-28-151336.png"><img src="http://blog.lordofgale.org/wp-content/uploads/2012/11/Screenshot-from-2012-11-28-151336-300x187.png" alt="" title="Screenshot from 2012-11-28 15:13:36" width="300" height="187" class="alignleft size-medium wp-image-128" /></a>
<p>
На скриншоте видно, что устройство sdc имеет объём равный 31,6 Гб(а заявленный объём моего флеш-брелка ADATA S102 32Gb Pro как раз составляет 32 Гб). Что-бы убедиться, что я не ошибся, вызываю более информативную команду, которая указывает название устройств в своём выхлопе(рекомендую вместо fdisk всегда использовать parted).
</p>
<pre>
<code class="bash">
sudo parted -l
</code>
</pre>
<a href="http://blog.lordofgale.org/wp-content/uploads/2012/11/Screenshot-from-2012-11-28-151430.png"><img src="http://blog.lordofgale.org/wp-content/uploads/2012/11/Screenshot-from-2012-11-28-151430-300x187.png" alt="" title="Screenshot from 2012-11-28 15:14:30" width="300" height="187" class="alignleft size-medium wp-image-129" /></a>
<p>
Как видно, я не ошибся, и /dev/sdc - это действительно моя флешка ADATA. A /dev/sdc1 и /dev/sdc2 - это разделы, на которые я разбил доступное на ней дисковое пространство. Первый раздел(30Гб с копейками) является основным разделом, в формате NTFS. Его видно в Linux, Windows и MacOS X(должно быть видно, на маке не проверял). Второй раздел - типично линуксовый, он нужен для загрузчика, так как Grub 2 не способен загружаться с раздела NTFS, но может загружать ОС, расположенные на данном разделе.
</p>