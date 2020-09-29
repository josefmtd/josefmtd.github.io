---
layout: post
title:  "Docker Compose dan Docker Engine di Ubuntu 20.04"
date:   2020-08-26 16:00:00 +0700
categories: docker
---

Docker adalah software yang dirancang untuk membuat dan menjalankan aplikasi dalam sebuah kontainer. Kontainer terdiri dari segala kebutuhan sebuah aplikasi mulai dari library dan berbagai dependency lain dalam sebuah OS disimpan pada suatu package.
Docker dapat dilakukan untuk mengisolasi masing-masing aplikasi yang dapat memiliki dependency yang berbeda.
Untuk menggunakan Docker, ada tool Docker Engine dan Docker Compose. Docker Engine adalah aplikasi kontainerisasi untuk membuat aplikasi.
Docker Engine adalah aplikasi client-server menggunakan daemon `dockerd` untuk membuat kontainer, image, network, dan volume.

Docker Engine dapat diakses melalui CLI `docker`, namun untuk aplikasi multikontainer umumnya digunakan Docker Compose.
Docker Compose menggunakan file `docker-compose.yml` untuk mendefinisikan suatu aplikasi dan kontainer yang diperlukan.

## Instalasi Docker Engine

Instal dependencies yang dibutuhkan oleh Docker Engine

{% highlight shell %}
$ sudo apt-get update

$ sudo apt-get install \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg-agent \
    software-properties-common
{% endhighlight %}

Tambahkan apt-repository untuk Docker Engine

{% highlight shell %}
$ curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add –
$ add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu focal stable"
{% endhighlight %}

Instal Docker Engine dan tambahkan akses user ke Docker CLI

{% highlight shell %}
$ sudo apt install docker-ce docker-ce-cli containerd.io -y
$ sudo usermod -aG docker $USER
{% endhighlight %}

## Instalasi Docker Compose

Docker Compose dapat diinstal menggunakan pip3 atau dengan mengunduh file `docker-compose` dari source GitHub.

{% highlight shell %}
$ sudo pip3 install docker-compose
{% endhighlight %}

atau

{% highlight shell %}
$ sudo curl -L "https://github.com/docker/compose/releases/download/1.27.4/docker-compose-Linux-x86_64" -o /usr/local/bin/docker-compose
$ sudo chmod +x /usr/local/bin/docker-compose
{% endhighlight %}
