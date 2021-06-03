---
layout: post
title:  "Earth Engine API Service Account Tasks"
date:   2021-05-31 10:30:00 +0700
categories: earthengine
---

Jika Anda menggunakan `earthengine-api` dengan GCP Service Account, maka Anda tidak dapat melihat rincian task di Google Earth Engine Code Editor, untuk itu gunakan CLI yang disediakan oleh Earth Engine Python API.
CLI tersebut adalah `earthengine`, Anda dapat mengakses beberapa fungsi seperti `task list`, namun pastikan Anda punya akses ke key JSON untuk login dari service account tersebut

{% highlight shell %}
$ earthengine --service_account_file /path/to/key.json task list
{% endhighlight %}

Jika ada task yang error, gunakan `task cancel task_id` atau `task cancel all` agar proses bisa diberhentikan seluruhnya.
