# Aktivitas Portofolio: Menggunakan Perintah Linux untuk Mengelola Perizinan File

**Program:** Google Cybersecurity Professional Certificate  
**Modul:** Tools of the Trade: Linux and SQL  
**Topik:** Manajemen Kontrol Akses & Perizinan File Sistem Linux  

---

## 1. Deskripsi Proyek (Project Description)

Sebagai seorang analis keamanan siber (*cybersecurity analyst*), memastikan bahwa integritas dan kerahasiaan data organisasi tetap terjaga merupakan tanggung jawab utama. Dalam proyek ini, saya bertugas mengaudit dan memperbarui izin akses file dan direktori pada sistem tim riset yang berlokasi di direktori `/home/researcher2/projects`.

### Tujuan Proyek:
- Memeriksa hak akses file dan direktori yang ada (termasuk file tersembunyi).
- Mengidentifikasi celah keamanan akibat izin yang terlalu terbuka (*over-permissive permissions*).
- Menyesuaikan perizinan file dan direktori menggunakan perintah Linux (`chmod`) agar sesuai dengan kebijakan otorisasi organisasi dan prinsip hak akses terendah (*Principle of Least Privilege*).

---

## 2. Memeriksa Detail File dan Direktori (Check File and Directory Details)

Langkah awal dalam audit keamanan adalah memeriksa seluruh konten dalam direktori kerja, termasuk file yang tersembunyi.

### Perintah:
```bash
ls -la /home/researcher2/projects
```

### Penjelasan Perintah & Argumen:
- `ls`: Perintah dasar Linux untuk membuat daftar file dan direktori (*list*).
- `-l`: Menggunakan format daftar panjang (*long listing format*), yang menampilkan informasi detail seperti string perizinan, jumlah hard link, pemilik (*owner*), grup (*group*), ukuran file, tanggal/waktu modifikasi terakhir, dan nama file.
- `-a`: Menampilkan semua file (*all*), termasuk file tersembunyi (*hidden files*) yang diawali dengan tanda titik (`.`).

### Contoh Output Terminal:
```text
drwxr-xr-x 3 researcher2 research_team 4096 Oct 15 10:00 .
drwxr-xr-x 3 researcher2 research_team 4096 Oct 15 09:50 ..
-rw-rw-rw- 1 researcher2 research_team  345 Oct 15 10:05 .project_x.txt
drwxrwxrwx 2 researcher2 research_team 4096 Oct 15 10:02 drafts
-rw-rw-rw- 1 researcher2 research_team 1024 Oct 15 10:01 project_k.txt
-rw-r--r-- 1 researcher2 research_team 2048 Oct 15 10:01 project_m.txt
-rwxrwxrwx 1 researcher2 research_team 4096 Oct 15 10:02 project_r.txt
-rw-rw-r-- 1 researcher2 research_team  512 Oct 15 10:01 project_t.txt
```

---

## 3. Menjelaskan String Perizinan (Describe the Permissions String)

Setiap entri file pada Linux memiliki string perizinan sepanjang 10 karakter (misalnya: `-rw-rw-r--` atau `drwxr-xr-x`).

### Struktur Karakter:
1. **Karakter ke-1 (Tipe File):**
   - `-` : File reguler / biasa.
   - `d` : Direktori (*directory*).
   - `l` : Symbolic link.
2. **Karakter ke 2-4 (User / Owner):** Hak akses untuk pemilik file (`u`).
3. **Karakter ke 5-7 (Group):** Hak akses untuk anggota grup pemilik (`g`).
4. **Karakter ke 8-10 (Other):** Hak akses untuk semua pengguna lain di sistem (`o`).

### Jenis Izin & Nilai Representasi:
| Izin | Simbol | Nilai Numerik (Oktal) | Arti pada File | Arti pada Direktori |
| :--- | :---: | :---: | :--- | :--- |
| **Read** | `r` | `4` | Membaca isi file | Melihat daftar isi direktori |
| **Write** | `w` | `2` | Mengubah/menghapus file | Membuat/menghapus file dalam direktori |
| **Execute** | `x` | `1` | Menjalankan file sebagai program/skrip | Masuk ke direktori (`cd`) |
| **No Access** | `-` | `0` | Tidak memiliki izin tersebut | Tidak memiliki izin tersebut |

---

## 4. Mengubah Perizinan File (Change File Permissions)

Berdasarkan kebijakan keamanan organisasi:
1. File **`project_k.txt`** tidak boleh dapat ditulis (*write*) oleh pengguna lain (*other*).
2. File **`project_r.txt`** tidak boleh memiliki izin eksekusi (*execute*) untuk siapa pun dan pengguna lain (*other*) tidak boleh memiliki izin menulis.

### Kasus 1: Memperbaiki `project_k.txt`
- **Izin Awal:** `-rw-rw-rw-` (User, Group, dan Other memiliki izin read dan write).
- **Celah Keamanan:** Pengguna luar tim dapat memanipulasi atau merusak isi file.
- **Tindakan:** Menghapus izin menulis (`w`) dari kategori `other` (`o`).

```bash
chmod o-w project_k.txt
```

- **Verifikasi:**
```bash
ls -l project_k.txt
# Output: -rw-rw-r-- 1 researcher2 research_team 1024 Oct 15 10:01 project_k.txt
```

### Kasus 2: Memperbaiki `project_r.txt`
- **Izin Awal:** `-rwxrwxrwx` (Full access untuk semua kategori).
- **Celah Keamanan:** File teks biasa tidak boleh memiliki izin eksekusi (`x`) karena dapat berisiko dieksploitasi untuk eksekusi skrip berbahaya. Selain itu, `other` tidak boleh memiliki izin menulis.
- **Tindakan:** Menghapus izin eksekusi (`x`) untuk user, group, dan other, serta menghapus izin tulis (`w`) untuk other.

```bash
chmod u-x,g-x,o-wx project_r.txt
```
*(Atau menggunakan notasi absolut: `chmod 664 project_r.txt`)*

- **Verifikasi:**
```bash
ls -l project_r.txt
# Output: -rw-rw-r-- 1 researcher2 research_team 4096 Oct 15 10:02 project_r.txt
```

---

## 5. Mengubah Perizinan File Tersembunyi (Change File Permissions on a Hidden File)

File tersembunyi `.project_x.txt` menyimpan draf rahasia yang sensitif.

### Kebijakan Otorisasi:
- Pemilik (`user`) hanya boleh memiliki izin **baca dan tulis** (atau sesuai skenario: hanya baca untuk proteksi manipulasi draf).
- Grup (`group`) hanya memiliki izin **baca** (*read*).
- Pengguna lain (`other`) **tidak boleh memiliki akses sama sekali** (*no access*).

### Tindakan:
- **Izin Awal:** `-rw-rw-rw-`
- **Perintah:**
```bash
chmod u=rw,g=r,o= .project_x.txt
```
*(Atau menggunakan notasi oktal: `chmod 640 .project_x.txt`)*

- **Verifikasi:**
```bash
ls -la .project_x.txt
# Output: -rw-r----- 1 researcher2 research_team 345 Oct 15 10:05 .project_x.txt
```

---

## 6. Mengubah Perizinan Direktori (Change Directory Permissions)

Direktori `drafts` berisi dokumen pekerjaan awal yang belum dipublikasikan.

### Kebijakan Otorisasi:
- Hanya pemilik (`researcher2`) yang boleh memiliki akses penuh (masuk ke direktori, membaca isi direktori, dan membuat/menghapus file di dalamnya).
- Anggota grup dan pengguna lain tidak diizinkan masuk ke direktori tersebut (*execute* dicabut) maupun melihat/mengubah isinya.

### Tindakan:
- **Izin Awal:** `drwxrwxrwx`
- **Perintah:**
```bash
chmod g-rwx,o-rwx drafts
```
*(Atau menggunakan notasi oktal: `chmod 700 drafts`)*

- **Verifikasi:**
```bash
ls -ld drafts
# Output: drwx------ 2 researcher2 research_team 4096 Oct 15 10:02 drafts
```

---

## 7. Tabel Ringkasan Audit & Perubahan Perizinan

| File / Direktori | Izin Awal | Izin Akhir | Perintah yang Digunakan | Justifikasi Keamanan |
| :--- | :---: | :---: | :--- | :--- |
| **`project_k.txt`** | `-rw-rw-rw-` | `-rw-rw-r--` | `chmod o-w project_k.txt` | Mencegah pihak luar (*other*) memodifikasi file riset tim. |
| **`project_r.txt`** | `-rwxrwxrwx` | `-rw-rw-r--` | `chmod u-x,g-x,o-wx project_r.txt` | Menghapus izin eksekusi yang tidak perlu dan membatasi akses tulis. |
| **`.project_x.txt`** | `-rw-rw-rw-` | `-rw-r-----` | `chmod 640 .project_x.txt` | Melindungi file rahasia dari akses publik (*others*) dan membatasi grup menjadi *read-only*. |
| **`drafts/`** | `drwxrwxrwx` | `drwx------` | `chmod 700 drafts` | Mengisolasi folder draf pribadi agar hanya dapat diakses oleh pemilik. |

---

## 8. Ringkasan & Dampak Keamanan (Summary & Security Impact)

Dalam aktivitas ini, pengelolaan hak akses file dan direktori berhasil diterapkan menggunakan perintah baris Linux (`ls`, `chmod`).

### Pelajaran Utama & Praktik Keamanan:
1. **Prinsip Hak Akses Terendah (*Principle of Least Privilege*):**  
   Pengguna dan proses hanya diberikan hak akses minimum yang diperlukan untuk menyelesaikan tugas mereka. Menghapus izin tulis dan eksekusi yang tidak perlu secara signifikan memperkecil bidang serangan (*attack surface*).
2. **Pentingnya Memeriksa File Tersembunyi:**  
   File konfigurasi dan data rahasia sering kali disembunyikan menggunakan awalan titik (`.`). Opsi `ls -a` sangat krusial untuk menemukan dan mengamankan file tersembunyi yang rentan terlewatkan dalam audit standar.
3. **Pemberian Izin Direktori yang Tepat:**  
   Izin eksekusi (`x`) pada direktori menentukan kemampuan pengguna untuk berpindah (*traversal*) ke dalam folder. Mencabut izin eksekusi bagi *other* dan *group* pada folder privat mencegah akses langsung ke file di dalamnya meskipun izin file di dalam direktori tersebut terbuka.
