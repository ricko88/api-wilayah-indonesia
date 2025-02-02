API Data Wilayah Indonesia
==========================

Repository ini berisi source code untuk generate (REST) API statis berisi data wilayah Indonesia
serta perintah untuk mendeploynya ke _static hosting_ [Github Page](https://pages.github.com/).

Demo: [https://ricko88.github.io/api-wilayah-indonesia](https://ricko88.github.io/api-wilayah-indonesia)

#### Apa yang dimaksud API statis? 

API statis adalah API yang _endpoint_-nya terdiri dari file statis.

#### Keuntungan API statis?

* Dapat dihosting pada _static file hosting_ seperti Github Page, Netlify, dsb.
* Proses lebih cepat karena tidak membutuhkan server-side scripting.

#### Bagaimana cara kerjanya?

* Daftar provinsi, kab/kota, kecamatan, kelurahan/desa disimpan pada folder `data` berupa file `csv` (agar mudah diedit).
* Kemudian script `generate.php` dijalankan. Script ini akan membaca file `csv` didalam folder `data`, kemudian men-generate ribuan endpoint (file) kedalam folder `static/api`.
* API siap 'dihidangkan'.

#### Saya mau hosting di Github saya sendiri, bagaimana caranya?

* Klik fork di pojok kanan atas.
* Pada halaman forking, **HAPUS CENTANG** "Copy the master branch only".
* Klik "Create Fork".
* Setelah selesai di Fork, klik Settings (bukan setting account, tapi setting repository).
* Klik menu "Pages" untuk masuk ke menu pengaturan GitHub Pages.
* Pada menu pengaturan GitHub Pages:
  * Pilih Source: Deploy from a Branch
  * Branch: `gh-pages`
  * Direktori: `/root`
  * Klik Save
* Tunggu beberapa menit (5-10 menitan), kembali ke halaman home repository (https://github.com/usernamekamu/api-wilayah-indonesia).
* Kalau halaman sudah terdeploy, di bagian kanan halaman, akan muncul informasi "Environments". Kalau belum tunggu lagi beberapa menit, lalu refresh.
* Kalau sudah muncul informasi Environmentsnya, klik bagian "🚀 github-pages".
* Di halaman Deployments, klik "View Deployment" untuk melihat halaman yang berhasil terdeploy.
## ENDPOINTS

#### 1. Mengambil Daftar Provinsi

```
GET https://ricko88.github.io/api-wilayah-indonesia/api/provinces.json
```

Contoh Response:

```
[
  {
    "id": "11",
    "name": "ACEH"
  },
  {
    "id": "12",
    "name": "SUMATERA UTARA"
  },
  ...
]
```

#### 2. Mengambil Daftar Kab/Kota pada Provinsi Tertentu

```
GET https://ricko88.github.io/api-wilayah-indonesia/api/regencies/{provinceId}.json
```

Contoh untuk mengambil daftar kab/kota di provinsi Sumatera Barat (ID = 13):

```
GET https://ricko88.github.io/api-wilayah-indonesia/api/regencies/13.json
```

Contoh Response:

```
[{"id":"1301","province_id":"13","name":"KABUPATEN KEPULAUAN MENTAWAI"},{"id":"1302","province_id":"13","name":"KABUPATEN PESISIR SELATAN"},{"id":"1303","province_id":"13","name":"KABUPATEN SOLOK"},{"id":"1304","province_id":"13","name":"KABUPATEN SIJUNJUNG"},{"id":"1305","province_id":"13","name":"KABUPATEN TANAH DATAR"},{"id":"1306","province_id":"13","name":"KABUPATEN PADANG PARIAMAN"},{"id":"1307","province_id":"13","name":"KABUPATEN AGAM"},{"id":"1308","province_id":"13","name":"KABUPATEN LIMA PULUH KOTA"},{"id":"1309","province_id":"13","name":"KABUPATEN PASAMAN"},{"id":"1310","province_id":"13","name":"KABUPATEN SOLOK SELATAN"},{"id":"1311","province_id":"13","name":"KABUPATEN DHARMASRAYA"},{"id":"1312","province_id":"13","name":"KABUPATEN PASAMAN BARAT"},{"id":"1371","province_id":"13","name":"KOTA PADANG"},{"id":"1372","province_id":"13","name":"KOTA SOLOK"},{"id":"1373","province_id":"13","name":"KOTA SAWAH LUNTO"},{"id":"1374","province_id":"13","name":"KOTA PADANG PANJANG"},{"id":"1375","province_id":"13","name":"KOTA BUKITTINGGI"},{"id":"1376","province_id":"13","name":"KOTA PAYAKUMBUH"},{"id":"1377","province_id":"13","name":"KOTA PARIAMAN"}]
```

#### 3. Mengambil Daftar Kecamatan pada Kab/Kota Tertentu

```
GET https://ricko88.github.io/api-wilayah-indonesia/api/districts/{regencyId}.json
```

Contoh untuk mengambil daftar kecamatan di Kabupaten Pasaman Barat (ID = 1312):

```
GET https://ricko88.github.io/api-wilayah-indonesia/api/districts/1312.json
```

Contoh Response:

```
[{"id":"1312010","regency_id":"1312","name":"SUNGAI BEREMAS"},{"id":"1312020","regency_id":"1312","name":"RANAH BATAHAN"},{"id":"1312030","regency_id":"1312","name":"KOTO BALINGKA"},{"id":"1312040","regency_id":"1312","name":"SUNGAI AUR"},{"id":"1312050","regency_id":"1312","name":"LEMBAH MALINTANG"},{"id":"1312060","regency_id":"1312","name":"GUNUNG TULEH"},{"id":"1312070","regency_id":"1312","name":"TALAMAU"},{"id":"1312080","regency_id":"1312","name":"PASAMAN"},{"id":"1312090","regency_id":"1312","name":"LUHAK NAN DUO"},{"id":"1312100","regency_id":"1312","name":"SASAK RANAH PASISIE"},{"id":"1312110","regency_id":"1312","name":"KINALI"}]
```

#### 4. Mengambil Daftar Nagari pada Kecamatan Tertentu

```
GET https://ricko88.github.io/api-wilayah-indonesia/api/villages/{districtId}.json
```

Contoh untuk mengambil daftar kelurahan di Sungai Beremas (ID = 1103010):

```
GET https://ricko88.github.io/api-wilayah-indonesia/api/villages/1312010.json
```

Contoh Response:

```
[{"id":"1312010001","district_id":"1312010","name":"AIA BANGIH"}]
```



## LIMITASI

Karena API ini dihosting di Github Page, Github Page sendiri memberikan batasan bandwith 100GB/bulan. Rata-rata endpoint disini memiliki ukuran 1KB/endpoint, jadi kurang lebih request yang dapat digunakan adalah 100.000.000 request per bulan, atau sekitar 3.000.000 request/hari.

Karena limitasi ini, disarankan untuk hosting API ini di github kamu sendiri.

Untuk lebih detail tentang limitasi Github Page, bisa dilihat [disini](https://help.github.com/en/articles/about-github-pages#usage-limits).
