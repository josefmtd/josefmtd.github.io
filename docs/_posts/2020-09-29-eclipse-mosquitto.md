---
layout: post
title:  "Eclipse Mosquitto via Docker Compose"
date:   2020-09-29 15:23:35 +0700
categories: docker
---

Docker Compose dapat mempermudah instalasi sebuah software. Artikel singkat kali ini membahas instalasi Eclipse Mosquitto menggunakan Docker Compose.
Eclipse Mosquitto adalah salah satu software popular yang umum dipakai pada sebuah projek Internet of Things.
Software Eclipse Mosquitto umumnya menggunakan port 1883 untuk protokol MQTT.

Gunakan [repositori Git][repositori-git] untuk melakukan instalasi Mosquitto. Untuk menjalankan Mosquitto tanpa username atau password, hapus folder `config` dan jalankan command

{% highlight %}
$ make install
{% endhighlight %}

[repositori-git]: https://github.com/josefmtd/mosquitto-docker
