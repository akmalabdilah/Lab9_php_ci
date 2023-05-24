# Pemograman Web2 Pertemuan 12

## Profil
| #               | Biodata                      |
| --------------- | ---------------------------- |
| **Nama**        | M. AKMAL AL ABDILAH          |
| **NIM**         | 312110034                    |
| **Kelas**       | TI.21.A.1                    |
| **Mata Kuliah** | Pemrograman Web 2            |

<p align="center">
 <img src="https://user-images.githubusercontent.com/91085882/137566814-9c8c078c-1c3e-475c-b23d-7f4922f74beb.gif"/>
</p>
<p align="center">
<a href="https://github.com/akmalabdilah"><img title="Author" src="https://img.shields.io/discord/102860784329052160?color=BLUE&label=M.%20AKMAL%20AL%20ABDILAH1&logo=GITHUB&logoColor=BLACK&style=plastic"></a>
<p align="center">



<hr>

## Praktikum 10 : Pagination dan Pencarian

<hr>

**Instruksi Praktikum**
1. Persiapkan text editor misalnya **VSCode.**
2. Buka kembali folder dengan nama **lab11_php_ci** pada docroot webserver **(htdocs)**
3. Ikuti langkah-langkah praktikum yang akan dijelaskan berikutnya.<br>
**Langkah-langkah Praktikum**<br>
**Membuat Pagination**<br>
Pagination merupakan proses yang digunakan untuk membatasi tampilan yang panjang
dari data yang banyak pada sebuah website. Fungsi pagination adalah memecah
tampilan menjadi beberapa halaman tergantung banyaknya data yang akan ditampilkan
pada setiap halaman.

Pada Codeigniter 4, fungsi pagination sudah tersedia pada Library sehingga cukup
mudah menggunakannya.
Untuk membuat pagination, buka Kembali **Controller Artikel**, kemudian modifikasi
kode pada method admin_index seperti berikut.
```
public function admin_index()
{
$title = 'Daftar Artikel';
$model = new ArtikelModel();
$data = [
'title' => $title,
'artikel' => $model->paginate(10), #data dibatasi 10 record per
halaman
'pager' => $model->pager,
];
return view('artikel/admin_index', $data);
}
```
![11_Lab11Web](Gambar/92.Gambar_admin_index_pagination.jpg)

Gambar 1. modifikasi
kode pada method admin_index

Kemudian buka file **views/artikel/admin_index.php** dan tambahkan kode berikut
dibawah deklarasi tabel data.
```
<?= $pager->links(); ?>
```
![11_Lab11Web](Gambar/93.Gambar_admin_index_pagination_link.jpg)

Gambar 2. Pagination_link

Selanjutnya buka kembali menu daftar artikel, tambahkan data lagi untuk melihat
hasilnya.

![11_Lab11Web](Gambar/96.Gambar_Pagination.jpg)

Gambar 3. Pagination

**Membuat Pencarian**<br>
Pencarian data digunakan untuk memfilter data.<br>
Untuk membuat pencarian data, buka kembali **Controller Artikel**, pada method
**admin_index** ubah kodenya seperti berikut:
```
public function admin_index()
{
$title = 'Daftar Artikel';
$q = $this->request->getVar('q') ?? '';
$model = new ArtikelModel();
$data = [
'title' => $title,
'q' => $q,
'artikel' => $model->like('judul', $q)->paginate(10), # data
dibatasi 10 record per halaman
'pager' => $model->pager,
];
return view('artikel/admin_index', $data);
}
```
![11_Lab11Web](Gambar/97.Gambar_Pagination.admin.index.filter.data.jpg)

Gambar 4. Pagination.admin.index.filter.data

Kemudian buka kembali file **views/artikel/admin_index.php** dan tambahkan form
pencarian sebelum deklarasi tabel seperti berikut:
```
<form method="get" class="form-search">
<input type="text" name="q" value="<?= $q; ?>" placeholder="Cari data">
<input type="submit" value="Cari" class="btn btn-primary">
</form>
```
Dan pada link pager ubah seperti berikut.
```
<?= $pager->only(['q'])->links(); ?>
```
![11_Lab11Web](Gambar/98.Gambar_form_pencarian.jpg)
![11_Lab11Web](Gambar/99.Gambar_form_pencarian-1.jpg)

Gambar 5. form_pencarian_admin_index.php

Selanjutnya ujicoba dengan membuka kembali halaman admin artikel, masukkan kata
kunci tertentu pada form pencarian.

![11_Lab11Web](Gambar/100.Gambar_Pencarian_Data.jpg)

Gambar 6. Pencarian Data

**Upload Gambar**<br>
Menambahkan fungsi unggah gambar pada tambah artikel. Buka kembali **Controller**
Artikel, sesuaikan kode pada method **add** seperti berikut:
```
public function add()
{
// validasi data.
$validation = \Config\Services::validation();
$validation->setRules(['judul' => 'required']);
$isDataValid = $validation->withRequest($this->request)->run();
if ($isDataValid)
{
$file = $this->request->getFile('gambar');
$file->move(ROOTPATH . 'public/gambar');
$artikel = new ArtikelModel();
$artikel->insert([
'judul' => $this->request->getPost('judul'),
'isi' => $this->request->getPost('isi'),
'slug' => url_title($this->request->getPost('judul')),
'gambar' => $file->getName(),
]);
return redirect('admin/artikel');
}
$title = "Tambah Artikel";
return view('artikel/form_add', compact('title'));
}
```
![11_Lab11Web](Gambar/101.Gambar_Fungsi_method_add_gambar.jpg)

Gambar 7. Upload Gambar

Kemudian pada file **views/artikel/form_add.php** tambahkan field input file seperti
berikut.
```
<p>
<input type="file" name="gambar">
</p>
```
Dan sesuaikan tag form dengan menambahkan *ecrypt type* seperti berikut.
```
<form action="" method="post" enctype="multipart/form-data">
```
![11_Lab11Web](Gambar/102.Gambar_form_add.php_gambar.jpg)

Gambar 8. add ecrypt type

Ujicoba file upload dengan mengakses menu tambah artikel.


![11_Lab11Web](Gambar/104.Gambar_Upload_Gambar.jpg)

Gambar 9. Upload Gambar

<hr>

# Pertanyaan dan Tugas

<hr>

**Selesaikan programnya sesuai Langkah-langkah yang ada. Anda boleh melakukan
improvisasi>**

>**Jawab:**
 
 **`Tambah Artikel & Upload Gambar`**
 
Saya Buat Artikel Keempat dan mengupload gambar artikel :

![11_Lab11Web](Gambar/105.Gambar_Upload_Gambar-1.jpg)

Gambar 10. Upload Gambar


![11_Lab11Web](Gambar/107.Gambar_Tambah_artikel.jpg)

Disini saya sudah setting untuk tampilan saya batasi 4 halaman :

Dan Selanjutnya kita buat artikel lagi dan kita buka Navigasi Halaman Ke 2 :

![11_Lab11Web](Gambar/107.Gambar_Tambah_artikel-1.jpg)

 **`Cari/Filter Artikel`**
 
 saya coba Cari/filter untuk Artikel Kelima :
 
 ![11_Lab11Web](Gambar/108.Gambar_Cari_artikel.jpg)

 **`Tampilan Artikel Di portal Berita`**
 
  ![11_Lab11Web](Gambar/109.Gambar_Tampilan_portal-berita.jpg)
  
  
  <hr>
  
  Cukup Sekian Penjelasan Dari saya
  
  **SELESAI**
  <hr>

<div>
<h2 align="center">Thanks For Reading!!!</h2>
<div align="center">
<img src="https://user-images.githubusercontent.com/91085882/222731693-24383140-7623-4e7a-a528-6621380b7be8.gif">

