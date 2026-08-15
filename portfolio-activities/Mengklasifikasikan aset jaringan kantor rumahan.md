# Aktivitas Portofolio: Mengklasifikasikan Aset Jaringan Kantor Rumahan (Home Network Asset Inventory & Classification)

**Program:** Google Cybersecurity Professional Certificate  
**Modul:** Assets, Threats, and Vulnerabilities (Course 5)  
**Topik:** Manajemen Aset, Inventarisasi Perangkat Jaringan, dan Klasifikasi Sensitivitas Risiko  
**Studi Kasus:** Manajemen Aset Jaringan untuk Bisnis Skala Kecil Berbasis Rumah (*Home-Based Small Business*)  

---

## 1. Deskripsi Proyek (Project Description)

Dalam era transformasi digital, informasi merupakan aset paling berharga yang dimiliki oleh setiap organisasi dan sebagian besar diakses melalui jaringan. Setiap perangkat yang terhubung ke jaringan merupakan potensi titik masuk (*entry point*) bagi aktor ancaman untuk mengeksploitasi aset lain di dalam sistem. 

Sebagai pemilik dan pengelola bisnis kecil berbasis rumah (*home-based small business*), saya melakukan **inventarisasi dan klasifikasi aset perangkat jaringan**. Proyek ini bertujuan untuk mengidentifikasi perangkat yang terhubung, mendokumentasikan karakteristik operasionalnya, serta menetapkan tingkat klasifikasi sensitivitas data berdasarkan tingkat kepentingannya guna memastikan perlindungan keamanan siber yang tepat dan proporsional.

---

## 2. Kategori & Tingkat Klasifikasi Sensitivitas Aset

Berdasarkan kerangka kerja keamanan informasi, tingkat sensitivitas aset diklasifikasikan ke dalam 4 tingkatan:

| Tingkat Sensitivitas | Tingkat Akses (*Access Designation*) | Definisi & Contoh Data / Perangkat |
|:---|:---|:---|
| **Restricted** *(Terbatas)* | **Need-to-know** *(Hanya yang Membutuhkan)* | Aset paling kritis yang berisi data keuangan, rahasia dagang, atau data pribadi sensitif (PII). Kebocoran data akan berdampak fatal pada kelangsungan bisnis. |
| **Confidential** *(Rahasia)* | **Limited to specific users** *(Pengguna Tertentu)* | Aset operasional penting seperti router jaringan, cadangan data (*backups*), atau kredensial sistem yang hanya boleh diakses oleh administrator. |
| **Internal-only** *(Internal)* | **Users on-premises** *(Pengguna di Lokasi)* | Aset jaringan yang dapat diakses oleh staf atau perangkat di area internal (perangkat IoT, smartphone tamu, printer bersama). |
| **Public** *(Publik)* | **Anyone** *(Semua Orang)* | Informasi atau aset yang ditujukan untuk konsumsi publik tanpa pembatasan kerahasiaan (website pemasaran, brosur). |

---

## 3. Tabel Inventaris & Klasifikasi Aset Jaringan (*Asset Inventory Table*)

Berikut adalah inventaris lengkap seluruh perangkat yang terhubung ke jaringan kantor rumahan:

| No | Aset (*Asset*) | Akses Jaringan (*Network Access*) | Pemilik (*Owner*) | Lokasi (*Location*) | Catatan Karakteristik & Risiko (*Notes*) | Klasifikasi Sensitivitas (*Sensitivity*) |
|:---:|:---|:---:|:---|:---:|:---|:---:|
| **1.0** | **Network Router** | Continuous | Internet service provider (ISP) | On-premises | Memiliki frekuensi 2.4 GHz dan 5 GHz. Seluruh perangkat jaringan rumah terhubung ke frekuensi 5 GHz. Mengelola gerbang utama lalu lintas data. | **Confidential** |
| **2.0** | **Desktop** | Occasional | Homeowner | On-premises | Menyimpan informasi pribadi sensitif, seperti dokumen identitas keluarga dan foto pribadi. | **Restricted** |
| **3.0** | **Guest Smartphone** | Occasional | Friend / Tamu | On and Off-premises | Terhubung ke jaringan Wi-Fi rumah saat berkunjung. Tidak dikelola oleh pemilik bisnis sehingga berpotensi membawa malware. | **Internal-only** |
| **4.0** | **Work Laptop** | Continuous | Business Owner | On and Off-premises | Menyimpan faktur tagihan klien, laporan pajak, kontrak bisnis, dan data keuangan sensitif. Dilindungi enkripsi disk penuh (*BitLocker*). | **Restricted** |
| **5.0** | **Network Attached Storage (NAS)** | Continuous | Business Owner | On-premises | Menyimpan arsip database pelanggan dan cadangan (*automated backup*) harian seluruh sistem. Akses dibatasi menggunakan kredensial admin. | **Confidential** |
| **6.0** | **Smart Security Camera (IoT)** | Continuous | Homeowner | On-premises | Memantau pintu masuk kantor rumahan dan menyiarkan video pengawasan langsung. Terhubung ke SSID tamu 2.4 GHz yang terisolasi. | **Internal-only** |

---

## 4. Analisis Rinci Karakteristik & Evaluasi Risiko Setiap Perangkat

### 1. Work Laptop (Laptop Kerja Bisnis) — `Restricted`
* **Karakteristik & Data:** Perangkat utama untuk menjalankan operasional bisnis, menyimpan laporan keuangan, data sensitif klien, dan akses ke rekening perbankan perusahaan.
* **Justifikasi Sensitivitas:** Jika laptop ini diretas atau dicuri, kerugian finansial dan reputasi bisnis akan sangat parah. Oleh karena itu, diklasifikasikan sebagai **Restricted** dan wajib dilengkapi autentikasi biometrik serta enkripsi disk penuh (*Full-Disk Encryption*).

### 2. Network Attached Storage / NAS (Server Penyimpanan Cadangan) — `Confidential`
* **Karakteristik & Data:** Server lokal yang terhubung kabel LAN ke router untuk melakukan sinkronisasi pencadangan otomatis data bisnis dan database.
* **Justifikasi Sensitivitas:** Berisi cadangan data berharga. Kerusakan atau enkripsi oleh *ransomware* akan menghentikan kelangsungan bisnis. Diklasifikasikan sebagai **Confidential** dengan akses terbatas hanya untuk pemilik (*admin credentials*).

### 3. Smart Security Camera / Kamera Pengawas IoT — `Internal-only`
* **Karakteristik & Data:** Perangkat pintar yang merekam video area kantor rumahan secara *real-time*.
* **Justifikasi Sensitivitas:** Perangkat IoT sering kali memiliki kerentanan *firmware*. Agar tidak menjadi pintu masuk untuk menyerang laptop kerja atau NAS, perangkat ini diklasifikasikan sebagai **Internal-only** dan diisolasi pada jaringan Wi-Fi khusus (*VLAN / Guest SSID*).

---

## 5. Rekomendasi Mitigasi & Pengamanan Jaringan Kantor Rumahan

Berdasarkan hasil inventarisasi aset, berikut langkah pengamanan yang diterapkan:
1. **Segmentasi Jaringan Wi-Fi (Dual-Band Isolation):**
   * **SSID Utama (5 GHz):** Khusus untuk perangkat kerja kritis (*Work Laptop* dan *NAS*).
   * **SSID Tamu / IoT (2.4 GHz):** Diisolasi untuk perangkat pintar (*Smart Camera*) dan smartphone tamu agar tidak dapat berkomunikasi langsung dengan aset bisnis (*Client Isolation*).
2. **Penegakan Prinsip Hak Akses Terendah (*Least Privilege*):**
   * Mengubah kata sandi default pada router dan kamera keamanan IoT.
   * Menonaktifkan manajemen router dari jarak jauh (*Remote Management via WAN*).
3. **Pencadangan 3-2-1 (*Backup Strategy*):**
   * Menyimpan data cadangan pada NAS lokal serta salinan terenkripsi sekunder di penyimpanan cloud yang aman.

---

## 6. Ringkasan & Dampak Keamanan (Summary & Security Impact)

Inventarisasi dan klasifikasi aset perangkat jaringan memberikan visibilitas penuh terhadap seluruh titik akhir (*endpoints*) yang terhubung ke jaringan kantor rumahan:
* Mengidentifikasi aset bernilai tinggi (*Restricted & Confidential*) yang memerlukan kontrol keamanan berlapis.
* Mencegah pergerakan lateral (*lateral movement*) penyerang dari perangkat IoT atau smartphone tamu ke data keuangan bisnis melalui segmentasi jaringan.
* Membantu memprioritaskan alokasi anggaran dan upaya keamanan siber secara terukur dan efektif.
