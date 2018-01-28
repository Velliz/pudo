---
title: DataTable Class
category: Advanced
order: 4
---

**PHP Guide**

DataTable adalah plugin jQuery yang paling populer digunakan untuk menampilkan data dalam bentuk tabel.
Puko menyediakan fasilitas berupa kelas yang dapat menyederhanakan penggunaan DataTable terutama jika mengunakan
fasilitas Server Processing. Untuk memulai, buat objek dari kelas DataTable dengan sintak berikut.

```php
$table = new DataTables();
```

Lalu definisikan kolom anda, terutama nama kolom yang di *select* dari database.

```php
$table->SetColumnSpec(array(
    "nama",
    "umur",
    "alamat",
    "email"
));
```

Jika sudah, anda harus menuliskan *query sql* untuk diproses oleh kelas DataTable.

```php
$data->SetQuery("SELECT * FROM mahasiswa");
```

> Perhatian: tidak diperkenankan menambahkan tanda ; pada akhir query karena kelas DataTable akan melakukan pembungkusan query.

Lalu, anda dapat menampilkan data dengan menggunakan sintak berikut.

```php
echo $data->GetDataTables(function ($result) {
    foreach ($result as $key => $val) {
        //modify data results here
    }
    return $result;
});
die();
```

Perlu diperhatikan bahwa fungsi **GetDataTables** menggunakan *callbacks* berupa *function* anonim.
Fitur ini berguna jika seandainya anda ingin melakukan transformasi data sebelum data hasil *select*
ditampilkan.

> Perhatian: pemanggilan die() diperlukan untuk memberhentikan proses pembungkusan output lanjut pada puko framework.

**JavaScript Guide**

Pastikan anda telah memiliki file yang dibutuhkan dan ter-import dengan benar kedalam file html.
Biasanya, pada puko templating engine versi 1.1.2 keatas penamaanya seperti berikut.

```html
{!js(<script src="assets/js/jquery.dataTables.min.js"></script>)}
{!js(<script src="assets/js/dataTables.bootstrap.min.js"></script>)}
```

> Perhatian: disarankan menggunakan DataTables versi 1.10 atau yang lebih baru.

Pastikan anda juga telah melakukan forwarding file tersebut ke master template.
Biasanya, di master template akan ada tag input berikut.

```html
<html>
    <head>...</head>
    <body>
    ...
    {CONTENT}
    ...
    {!part(css)}
    {!part(js)}
    </body>
</html>
```

Kemudian, anda bisa menambahkan instansiasi kode JavaScript dari DataTables seperti dicontohkan berikut ini.

```javascript
$('#table-printed').DataTable({
    ajax: {
        url: "",
        data: {},
        type: "GET",
        dataType: "json",
        complete: function (evt) {
            //kode ketika berhasil
        }
    },
    columns: [
        {"orderable": true},
        {"orderable": true},
        {"orderable": true},
        {"orderable": false}
    ],
    processing: true,
    serverSide: true,
    dom: 'Bfrtip',
    buttons: [
        'copyHtml5',
        'excelHtml5',
        'csvHtml5',
        'pdfHtml5'
    ]
});
```

> Perhatian: jumlah *orderable* dalam *columns* harus sama dengan *SetColumnSpec* pada kode PHP.

Untuk saat ini, anda hanya bisa melakukan pemanggilan $.ajax() dengan metode GET.
Penggunaan lebih lanjut akan ditambahkan saat basis kode framework diperbarui.