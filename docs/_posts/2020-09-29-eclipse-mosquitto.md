---
layout: post
title:  "Eclipse Mosquitto via Docker Compose"
date:   2020-09-29 15:23:35 +0700
categories: docker
---

Docker Compose dapat mempermudah instalasi sebuah software. Artikel singkat kali ini membahas instalasi Eclipse Mosquitto menggunakan Docker Compose.
Eclipse Mosquitto adalah salah satu software popular yang umum dipakai pada sebuah projek Internet of Things.
Software Eclipse Mosquitto umumnya menggunakan port 1883 untuk protokol MQTT.

## Server Mosquitto Tanpa Password 

Gunakan [repositori Git][repositori-git] untuk melakukan instalasi Mosquitto. Untuk menjalankan Mosquitto tanpa username atau password, hapus folder `config` dan jalankan command

{% highlight shell %}
$ git clone https://github.com/josefmtd/mosquitto-docker
$ cd mosquitto-docker
$ rm -rf config
$ make install
{% endhighlight %}

## Server Mosquitto dengan Username dan Password

Untuk menggunakan username dan password, gunakan `Makefile` untuk penambahan username dan password untuk otentikasi MQTT.

{% highlight shell %}
$ git clone https://github.com/josefmtd/mosquitto-docker
$ cd mosquitto-docker
$ make install
{% endhighlight %}

Ubah file `.env` untuk mengganti `MQTT_USER` dan `MQTT_PASS` untuk otentikasi server MQTT. Setelah mengubah password jalankan command di bawah ini:

{% highlight shell %}
$ nano .env
$ make password
$ docker-compose restart
{% endhighlight %}

[repositori-git]: https://github.com/josefmtd/mosquitto-docker
