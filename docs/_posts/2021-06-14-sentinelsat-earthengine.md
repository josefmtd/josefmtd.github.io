---
layout: post
title:  "Sentinel-5P Hub API dengan Earth Engine API"
date:   2021-06-14 19:00:00 +0700
categories: python
---

Sentinel-5 Precursor adalah salah satu satelit yang dapat memberikan informasi kualitas atmosfer dengan data gas pencemar seperti CO, NO2, O3, SO2, dan lain lain. Melalui Sentinel-5P Hub (https://s5phub.copernicus.eu/dhus), bisa dilakukan query dengan jenis produk (CO, NO2, O3), level pemrosesan (L1B, L2), tanggal penginderaan, dan poligon (area-of-interest). Selain melalui GUI dari link, menggunakan modul `sentinelsat`, dapat dilakukan query menggunakan API tersebut.

## Instalasi Environment Anaconda

Buat environment baru untuk instalasi bersih masing-masing modul tanpa mengganggu environment yang sudah terinstal sebelumnya:

{% highlight shell %}
$ conda create -n sentinel
$ conda activate sentinel
$ conda config --env --add channels conda-forge
$ conda config --env --set channel_priority strict
{% endhighlight %}

Instalasi menggunakan channel `conda-forge` yang sudah dikonfigurasi sebelumnya:

{% highlight shell %}
$ conda install earthengine-api geemap eemont
$ conda install sentinelsat
$ conda install jupyterlab
{% endhighlight %}

## Query Melalui SentinelAPI

Berikut contoh untuk menggunakan SentinelAPI untuk mendapatkan data 'L2__CO____' dari Sentinel-5P Hub.

{% highlight python %}
from sentinelsat import SentinelAPI, geojson_to_wkt, read_geojson
from datetime import date

username = 's5pguest'
password = 's5pguest'
hostname = 'https://s5phub.copernicus.eu/dhus'
api = SentinelAPI(username, password, hostname)

start_date = date(year = 2021, month = 6, day = 11)
end_date = date(year = 2021, month = 6, day = 12)
footprint = geojson_to_wkt(read_geojson(path_to_geojson))
products = api.query(footprint, date = (start_date, end_date), \
    platformname = 'Sentinel-5', producttype = 'L2__CO____', \
    processingmode = 'Offline')

list_keys = [key for key in products]
orbit_num = [products[key]['orbitnumber'] for key in list_keys]

{% endhighlight %}

Setelah mendapatkan list orbit dengan variabel `orbit_num`, maka bisa dilakukan filter dengan metadata `ORBIT` dari produk `L3_CO` yang tersedia di Google Earth Engine

{% highlight python %}
import ee
ee.Initialize()

product_name = 'COPERNICUS/S5P/OFFL/L3_CO'
band_name = 'CO_column_number_density'

data = ee.ImageCollection(product_name).select(band_name) \
    .filter(ee.Filter.inList('ORBIT', orbit_num)).mean()
{% endhighlight %}
