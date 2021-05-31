---
layout: post
title:  "Manipulasi File netCDF4 dengan xarray dan dask"
date:   2021-05-31 10:30:00 +0700
categories: python
---

Menggunakan `xarray` dengan `dask`, kita dapat membuka file netCDF dan melakukan manipulasi seperti filter data. Untuk percobaan kali ini, saya menggunakan data FFMC hasil olahan dari data ERA-Interim yang disediakan oleh ECMWF.

## Unduh Data

Sebelum memulai, saya mengunduh data menggunakan wget

{% highlight shell %}
$ wget https://zenodo.org/record/3250992/files/ffmc.nc
{% endhighlight %}

## Jupyter Lab

{% highlight python %}
import xarray as xr
ds = xr.open_dataset('ffmc.nc', chunks='auto')
cond = (ds.lat > -10) & (ds.lat < 10) & (ds.lon > 90) & (ds.lon < 150)
ds_indo = ds.where(cond, drop = True)

ds_indo.to_netcdf('ffmc_indonesia.nc')
{% endhighlight %}
