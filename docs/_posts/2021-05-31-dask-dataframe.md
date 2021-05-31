---
layout: post
title:  "Pembacaan File CSV dengan Dask"
date:   2021-05-31 10:30:00 +0700
categories: python
---

Menggunakan `dask`, kita dapat membuka banyak file csv secara sekaligus, untuk contoh percobaan kali ini data saya ambil dari FIRMS NASA. Melalui satelit NPP-Suomi, data hotspot per tahun untuk masing-masing negara dapat diakses melalui link:
https://firms.modaps.eosdis.nasa.gov/country/

## Unduh Data

Unduh data dari masing-masing tahun menggunakan wget

{% highlight shell %}
$ wget https://firms.modaps.eosdis.nasa.gov/data/country/viirs-snpp/2012/viirs-snpp_2012_Indonesia.csv
$ wget https://firms.modaps.eosdis.nasa.gov/data/country/viirs-snpp/2013/viirs-snpp_2013_Indonesia.csv
$ wget https://firms.modaps.eosdis.nasa.gov/data/country/viirs-snpp/2014/viirs-snpp_2014_Indonesia.csv
$ wget https://firms.modaps.eosdis.nasa.gov/data/country/viirs-snpp/2015/viirs-snpp_2015_Indonesia.csv
$ wget https://firms.modaps.eosdis.nasa.gov/data/country/viirs-snpp/2016/viirs-snpp_2016_Indonesia.csv
$ wget https://firms.modaps.eosdis.nasa.gov/data/country/viirs-snpp/2017/viirs-snpp_2017_Indonesia.csv
$ wget https://firms.modaps.eosdis.nasa.gov/data/country/viirs-snpp/2018/viirs-snpp_2018_Indonesia.csv
{% endhighlight %}

## Jupyter Lab

Menggunakan `dask` untuk membaca file `.csv` dengan wildcard

{% highlight python %}
import dask.dataframe as dd
df = dd.read_csv('viirs-snpp_*_Indonesia.csv')
{% endhighlight %}

Pilih filter menggunakan syntax DataFrame, memilih data dengan tingkat kepercayaan tinggi, kondisi malam hari, dan tipe kebakaran vegetasi (`df.type == 0`).

{% highlight python %}
condition = (df.confidence == 'h') & \
    (df.daynight == 'N') & \
    (df.type == 0)
{% endhighlight %}

Ambil seluruh data yang sesuai dengan filter `condition` dan export sebagai satu file `.csv`

{% highlight python %}
fire = df[condition].copy().reset_index(drop = True)
fire.to_csv('hotspot_indonesia.csv', single_file = True)
{% endhighlight %}
