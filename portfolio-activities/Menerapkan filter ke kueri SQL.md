# Aktivitas Portofolio: Menerapkan Filter ke Kueri SQL (Apply Filters to SQL Queries)

**Program:** Google Cybersecurity Professional Certificate  
**Modul:** Tools of the Trade: Linux and SQL (Course 4)  
**Topik:** Investigasi Insiden Keamanan & Manajemen Basis Data Relasional dengan SQL  
**Studi Kasus:** Analisis Upaya Login Mencurigakan dan Pembaruan Keamanan Mesin Karyawan  

---

## 1. Deskripsi Proyek (Project Description)

Sebagai seorang analis keamanan siber (*cybersecurity professional*) di sebuah organisasi skala besar, saya bertanggung jawab untuk memantau integritas sistem dan menyelidiki potensi insiden keamanan. Dalam proyek ini, saya melakukan investigasi terhadap aktivitas login yang mencurigakan serta mempersiapkan data untuk pembaruan keamanan perangkat komputer karyawan. Dengan memanfaatkan kueri SQL pada tabel `log_in_attempts` dan `employees`, saya menggunakan operator logika `AND`, `OR`, `NOT`, serta pencocokan pola `LIKE` untuk memfilter dan mengekstrak catatan spesifik yang krusial bagi analisis keamanan organisasi.

---

## 2. Struktur Tabel Basis Data

Investigasi ini melibatkan dua tabel utama dalam database organisasi:

1. **Tabel `log_in_attempts`**: Mencatat setiap upaya autentikasi pengguna ke dalam sistem.
   * `event_id` (INT): Kunci utama / ID unik upaya login.
   * `username` (VARCHAR): Nama akun pengguna.
   * `login_date` (DATE): Tanggal upaya login (format: YYYY-MM-DD).
   * `login_time` (TIME): Waktu upaya login (format: HH:MM:SS).
   * `country` (VARCHAR): Negara asal koneksi IP (misal: 'MEX', 'MEXICO', 'USA', 'CAN').
   * `ip_address` (VARCHAR): Alamat IP asal permintaan login.
   * `success` (BOOLEAN/INT): Status keberhasilan login (`1` / `TRUE` jika berhasil, `0` / `FALSE` jika gagal).

2. **Tabel `employees`**: Menyimpan data identitas, unit kerja, dan perangkat staf.
   * `employee_id` (INT): ID unik karyawan.
   * `device_id` (VARCHAR): ID perangkat / mesin komputer karyawan.
   * `first_name` & `last_name` (VARCHAR): Nama lengkap karyawan.
   * `department` (VARCHAR): Departemen kerja (misal: 'Marketing', 'Finance', 'Sales', 'Information Technology').
   * `office` (VARCHAR): Lokasi kantor dan gedung (misal: 'East-170', 'East-320', 'North-434', 'South-210').

---

## 3. Investigasi Upaya Login & Analisis Log Keamanan

### Langkah 1: Mengambil Upaya Login yang Gagal Setelah Jam Kerja
* **Kebutuhan Investigasi:**  
  Terdeteksi indikasi serangan *brute force* atau akses tidak sah di luar jam kerja normal (setelah pukul 18:00). Diperlukan data seluruh login yang gagal (`success = 0` / `FALSE`) yang terjadi setelah jam 18:00.
* **Kueri SQL:**
  ```sql
  SELECT *
  FROM log_in_attempts
  WHERE login_time > '18:00' AND success = 0;
  ```
* **Penjelasan Logika Filter:**  
  * `WHERE login_time > '18:00'`: Menyaring catatan yang memiliki waktu percobaan login di atas pukul 18:00:00.
  * `AND success = 0`: Memastikan hanya upaya login yang berstatus **gagal** yang ditampilkan.
  * Operator `AND` mengharuskan **kedua kondisi bernilai benar**, sehingga mengeliminasi aktivitas login sah pada jam kerja maupun login sukses setelah jam kerja.

---

### Langkah 2: Mengambil Upaya Login pada Tanggal Tertentu
* **Kebutuhan Investigasi:**  
  Sebuah insiden keamanan mencurigakan terjadi pada tanggal **09 Mei 2022 (`2022-05-09`)**. Untuk melihat pola aktivitas sebelum dan saat insiden berlangsung, tim analis perlu meninjau seluruh upaya login pada tanggal tersebut dan hari sebelumnya (**08 Mei 2022 / `2022-05-08`**).
* **Kueri SQL:**
  ```sql
  SELECT *
  FROM log_in_attempts
  WHERE login_date = '2022-05-08' OR login_date = '2022-05-09';
  ```
* **Penjelasan Logika Filter:**  
  * `login_date = '2022-05-08' OR login_date = '2022-05-09'`: Menginstruksikan database untuk mengambil baris data yang cocok dengan tanggal 8 Mei 2022 ATAU 9 Mei 2022.
  * Operator `OR` mengembalikan data jika salah satu dari kondisi tersebut terpenuhi, memungkinkan penarikan data lintas dua hari berturut-turut untuk analisis korelasi insiden.

---

### Langkah 3: Mengambil Upaya Login di Luar Wilayah Meksiko
* **Kebutuhan Investigasi:**  
  Tim keamanan telah mengonfirmasi bahwa aktivitas mencurigakan yang sedang diselidiki **bukan berasal dari kantor cabang di Meksiko**. Untuk mempersempit pencarian ke alamat IP asing yang berpotensi menjadi vektor serangan eksternal, perlu ditarik data login dari luar Meksiko (kolom `country` memiliki variasi penulisan seperti `'MEX'` dan `'MEXICO'`).
* **Kueri SQL:**
  ```sql
  SELECT *
  FROM log_in_attempts
  WHERE NOT country LIKE 'MEX%';
  ```
* **Penjelasan Logika Filter:**  
  * `LIKE 'MEX%'`: Karakter *wildcard* `%` mencocokkan string apa pun yang diawali dengan huruf "MEX", mencakup kode `'MEX'` maupun `'MEXICO'`.
  * `NOT`: Membalikkan evaluasi logika, sehingga mengecualikan seluruh catatan dari Meksiko dan hanya menampilkan upaya login dari negara lain.

---

## 4. Pembaruan Keamanan Perangkat Karyawan (*Machine Security Updates*)

### Langkah 4: Mengambil Data Karyawan Departemen Pemasaran di Gedung Timur
* **Kebutuhan Pembaruan:**  
  Tim keamanan siber akan melakukan pembaruan keamanan bertahap (*targeted patch deployment*) khusus untuk mesin karyawan di **Departemen Pemasaran (*Marketing*)** yang berlokasi di **Gedung Timur (*East Building*)**.
* **Kueri SQL:**
  ```sql
  SELECT *
  FROM employees
  WHERE department = 'Marketing' AND office LIKE 'East%';
  ```
* **Penjelasan Logika Filter:**  
  * `department = 'Marketing'`: Membatasi pencarian hanya untuk karyawan di divisi Pemasaran.
  * `AND office LIKE 'East%'`: Menggunakan *wildcard* `%` untuk mencocokkan semua nomor ruangan yang berada di Gedung Timur (misalnya `East-170`, `East-320`, `East-400`).
  * Operator `AND` memastikan hanya karyawan Pemasaran yang berkantor di Gedung Timur yang terdaftar untuk menerima pembaruan perangkat.

---

### Langkah 5: Mengambil Data Karyawan Departemen Penjualan dan Keuangan
* **Kebutuhan Pembaruan:**  
  Pembaruan perangkat lunak keamanan lainnya perlu segera dipasang pada seluruh mesin karyawan yang menangani transaksi dan data finansial, yaitu departemen **Penjualan (*Sales*)** dan **Keuangan (*Finance*)**.
* **Kueri SQL:**
  ```sql
  SELECT *
  FROM employees
  WHERE department = 'Finance' OR department = 'Sales';
  ```
* **Penjelasan Logika Filter:**  
  * `department = 'Finance' OR department = 'Sales'`: Memilih setiap karyawan yang bertugas di departemen Keuangan ataupun Penjualan.
  * Operator `OR` menjamin seluruh personel dari kedua departemen penting ini tercakup dalam daftar target inventaris pembaruan.

---

### Langkah 6: Mengambil Seluruh Karyawan yang Bukan dari Departemen TI
* **Kebutuhan Pembaruan:**  
  Tim IT telah menguji dan memasang pembaruan antivirus terbaru pada komputer internal mereka. Sekarang, pembaruan wajib disebarkan ke **seluruh departemen lain selain Departemen Teknologi Informasi (*Information Technology*)**.
* **Kueri SQL:**
  ```sql
  SELECT *
  FROM employees
  WHERE NOT department = 'Information Technology';
  ```
* **Penjelasan Logika Filter:**  
  * `NOT department = 'Information Technology'`: Mengecualikan seluruh karyawan departemen TI dan mengambil daftar lengkap karyawan dari semua departemen lainnya (HR, Marketing, Sales, Finance, Legal, Operasional).

---

## 5. Tabel Rekapitulasi Kueri SQL & Logika Filter Keamanan

| No | Tujuan Tugas Investigasi / Pembaruan | Tabel Sumber | Kueri SQL yang Digunakan | Operator Utama |
|:---:|:---|:---:|:---|:---:|
| **1** | Analisis login gagal setelah jam 18:00 | `log_in_attempts` | `SELECT * FROM log_in_attempts WHERE login_time > '18:00' AND success = 0;` | `AND`, `>` |
| **2** | Tinjauan login pada 8 & 9 Mei 2022 | `log_in_attempts` | `SELECT * FROM log_in_attempts WHERE login_date = '2022-05-08' OR login_date = '2022-05-09';` | `OR`, `=` |
| **3** | Filter login di luar wilayah Meksiko | `log_in_attempts` | `SELECT * FROM log_in_attempts WHERE NOT country LIKE 'MEX%';` | `NOT`, `LIKE` (`%`) |
| **4** | Identifikasi staf Marketing di Gedung Timur | `employees` | `SELECT * FROM employees WHERE department = 'Marketing' AND office LIKE 'East%';` | `AND`, `LIKE` (`%`) |
| **5** | Identifikasi staf Finance dan Sales | `employees` | `SELECT * FROM employees WHERE department = 'Finance' OR department = 'Sales';` | `OR`, `=` |
| **6** | Identifikasi seluruh staf non-IT | `employees` | `SELECT * FROM employees WHERE NOT department = 'Information Technology';` | `NOT`, `=` |

---

## 6. Ringkasan & Dampak Keamanan (Summary & Security Impact)

Melalui penerapan kueri SQL dengan operator logika `AND`, `OR`, `NOT`, dan pencocokan pola `LIKE`, proses investigasi keamanan dan manajemen inventaris perangkat dapat diselesaikan secara presisi dan efisien:

1. **Deteksi Ancaman Akurat:**  
   Penyaringan log waktu dan status autentikasi berhasil mengisolasi upaya login mencurigakan di luar jam operasional serta mendeteksi anomali akses lintas wilayah geografis tanpa mengganggu catatan log normal.
2. **Efisiensi Manajemen Patch & Pembaruan:**  
   Pemfilteran berbasis departemen dan lokasi fisik memungkinkan tim TI mendistribusikan *security patch* secara terukur sesuai prioritas risiko operasional (seperti mendahulukan departemen finansial dan mengisolasi unit kerja tertentu).
3. **Penerapan Keterampilan SQL dalam Praktik Keamanan:**  
   Keahlian menyusun kueri terstruktur merupakan fondasi penting bagi seorang analis SOC (*Security Operations Center*) dalam melakukan *threat hunting*, analisis log SIEM, dan penegakan kepatuhan keamanan data.
