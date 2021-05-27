---
layout: post
title:  "Anaconda Geospatial Environment"
date:   2021-05-27 09:30:00 +0700
categories: conda
---

Melalui Anaconda / Miniconda, sebuah environment untuk pengembangan script menggunakan bahasa pemrograman Python. Dua package pengolahan data geospasial yang di bahas di sini adalah `earthengine-api` dan `geopandas`. Adapun tambahan modul visualisasi dan pengolahan data di atas Earth Engine yang digunakan yaitu `eemont` dan `geemap`. Pengembangan script akan menggunakan Jupyter Lab.

## Pembuatan Environment

Buat environment baru untuk instalasi bersih masing-masing modul tanpa mengganggu environment yang sudah terinstal sebelumnya:

{% highlight shell %}
$ conda create -n geo
$ conda activate geo
$ conda config --env --add channels conda-forge
$ conda config --env --set channel_priority strict
{% endhighlight %}

## Instalasi Modul Python dan JupyterLab

Instalasi menggunakan channel `conda-forge` yang sudah dikonfigurasi sebelumnya

{% highlight shell %}
$ conda install geopandas
$ conda install earthengine-api geemap eemont
$ conda install jupyterlab
{% endhighlight %}

Environment geospasial menggunakan `geopandas` dan `earthengine-api` sudah dapat diakses dengan menggunakan Jupyter Lab.

{% highlight shell %}
$ jupyter-lab
{% endhighlight %}
