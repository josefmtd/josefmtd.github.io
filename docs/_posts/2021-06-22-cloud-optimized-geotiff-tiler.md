---
layout: post
title:  "Cloud Optimized GeoTIFF Tiler (TiTiler)"
date:   2021-06-14 19:00:00 +0700
categories: python
---

Melalui file Cloud Optimized GeoTIFF (COG) yang ditaruh di Cloud Computing Platform seperti Amazon S3 atau Google Cloud Storage, kita dapat menjalankan suatu Tiling API. Salah satunya adalah TiTiler, berikut secara singkat instalasinya di Anaconda Environment di atas operating system Windows 10.

```
$ conda create -n tiler python=3.9
$ conda activate tiler
$ conda install -c conda-forge rasterio
$ pip install titiler.application uvicorn
$ git clone https://github.com/developmentseed/titiler.git
$ cd titiler
$ uvicorn titiler.application.main:app --reload
```

Setelah aplikasi ini berjalan, Anda dapat menggunakan `http://localhost:8000` untuk keperluan tiling service.
