# Aktivitas Portofolio: Analisis Pengerasan Jaringan & Penilaian Risiko Keamanan (Network Hardening Assessment)

**Program:** Google Cybersecurity Professional Certificate  
**Modul:** Connect and Protect: Networks and Network Security (Course 3)  
**Topik:** Penilaian Risiko Keamanan Jaringan, Manajemen Patch Database, dan Kebijakan Keamanan Informasi  
**Studi Kasus:** Pengerasan Keamanan Jaringan pada Organisasi Media Sosial  

---

## 1. Ringkasan Eksekutif (Executive Summary)

Sebagai bagian dari tim keamanan siber di sebuah organisasi media sosial yang berkembang pesat, saya melakukan **Penilaian Risiko Keamanan Jaringan (*Security Risk Assessment*)** untuk mengevaluasi infrastruktur internal. Hasil penilaian mengidentifikasi dua kerentanan berisiko tinggi (*high-risk vulnerabilities*):
1. **Perangkat Lunak Database Lokal yang Ketinggalan Zaman (*Outdated Database Software*)**: Server database utama belum diperbarui dan rentan terhadap eksploitasi kerentanan keamanan yang telah diketahui (*Known CVEs*).
2. **Kebiasaan Berbagi Kata Sandi di Antara Karyawan (*Widespread Password Sharing*)**: Staf antar departemen kerap meminjamkan kredensial akun untuk kemudahan akses, yang merusak akuntabilitas (*non-repudiation*) dan kontrol akses.

Laporan ini menyajikan analisis dampak ancaman di masa depan, solusi pengerasan jaringan (*network hardening techniques*), serta draf pembaruan **Kebijakan Keamanan Informasi Organisasi**.

---

## 2. Analisis Kerentanan & Potensi Ancaman Masa Depan

### A. Kerentanan 1: Database yang Belum Ditambal (*Unpatched Database*)
* **Vektor Ancaman:**  
  Versi database yang sudah usang memiliki celah keamanan publik (misalnya SQL Injection tingkat lanjut, *Remote Code Execution / RCE*, atau *Buffer Overflow*).
* **Potensi Dampak di Masa Depan:**  
  Jika database tidak segera ditambal (*patched*), penyerang eksternal dapat mengeksploitasi kerentanan tersebut untuk mencuri data pribadi jutaan pengguna media sosial, memodifikasi catatan transaksi, atau menanamkan *ransomware* yang mengakibatkan kerugian finansial masif dan sanksi regulasi.

### B. Kerentanan 2: Berbagi Kata Sandi Antar Karyawan (*Password Sharing*)
* **Vektor Ancaman:**  
  Penggunaan satu akun oleh banyak orang meniadakan kontrol akses individual (*broken identity verification*).
* **Potensi Dampak di Masa Depan:**  
  Jika salah satu workstation karyawan terinfeksi *malware/keylogger*, atau jika ada karyawan yang berhenti (mantan karyawan), akun tersebut tetap dapat diakses tanpa otorisasi. Selain itu, investigasi forensik jika terjadi kebocoran internal menjadi mustahil karena jejak audit (*audit trail*) tidak dapat mengidentifikasi individu pelaku.

---

## 3. Solusi Pengerasan Jaringan & Tindakan Remediasi

| Area Pengerasan | Tindakan Teknis yang Direkomendasikan | Alat / Metode yang Digunakan |
|:---|:---|:---|
| **Manajemen Patch Database** | Melakukan peningkatan (*upgrade*) versi database ke versi stabil terbaru dan membuat jadwal *patching* otomatis berkala. | Sistem Manajemen Patch Otomatis (misal: Red Hat Satellite / Ansible), Pengujian di Lingkungan Staging. |
| **Kontrol Akses & Autentikasi** | Menghapus akun bersama, membuat akun individu berbasis peran (*RBAC*), dan mewajibkan MFA. | Autentikasi Multifaktor (MFA / 2FA via Aplikasi Autentikator/FIDO2), SSO dengan kontrol hak akses terendah. |
| **Manajemen Kata Sandi** | Menyediakan aplikasi pengelola kata sandi terpusat bagi seluruh staf untuk menyimpan kata sandi unik dan kompleks. | *Enterprise Password Manager* (misal: 1Password / Bitwarden Enterprise). |
| **Segmentasi Jaringan Database** | Mengisolasi server database di dalam subnet privat (VLAN terpisah) yang dilindungi *internal firewall*. | Firewall Antar-VLAN, Pembatasan Akses IP Whitelisting hanya untuk server aplikasi. |

---

## 4. Pembaruan Kebijakan Keamanan Informasi Organisasi

Untuk memastikan keberlanjutan praktik pengerasan jaringan, kebijakan keamanan informasi organisasi diperbarui dengan klausul wajib berikut:

### 1. Praktik Pengerasan Umum & Jadwal Pemeliharaan:
* **Frekuensi Pembaruan:** Pemindaian kerentanan (*vulnerability scanning*) wajib dilakukan setiap **bulan**, dan instalasi *security patches* kritis wajib diselesaikan dalam waktu **maksimal 14 hari** setelah rilis resmi vendor.
* **Segmentasi Lingkungan:** Seluruh pembaruan perangkat lunak harus diuji terlebih dahulu di lingkungan *Staging/Testing* sebelum diterapkan ke lingkungan produksi (*Production*).

### 2. Kebijakan Manajemen Identitas & Kredensial:
* **Larangan Mutlak Berbagi Kredensial:** Setiap karyawan wajib memiliki akun pribadi dengan prinsip satu pengguna satu akun (*Unique Account Identifier*). Berbagi kata sandi kepada rekan kerja atau pihak luar dilarang keras.
* **Standar Kata Sandi:** Panjang minimal 14 karakter, kombinasi huruf besar, huruf kecil, angka, dan simbol.
* **Autentikasi Multifaktor (MFA):** Wajib aktif untuk seluruh akses ke jaringan organisasi (VPN, email, database, dan portal admin).

### 3. Konsekuensi Ketidakpatuhan (*Consequences of Non-Compliance*):
Kegagalan mematuhi kebijakan ini dapat mengakibatkan:
1. Pencabutan hak akses sistem secara langsung.
2. Peninjauan kinerja disipliner internal hingga pemutusan hubungan kerja (PHK).
3. Tuntutan hukum perdata/pidana jika pelanggaran terbukti menyebabkan insiden kebocoran data sensitif perusahaan.

---

## 5. Kesimpulan & Manfaat bagi Organisasi

Penerapan langkah-langkah pengerasan jaringan di atas menutup celah kritis pada database dan manajemen akses. Dengan adanya SOP terdokumentasi dan kebijakan keamanan yang tegas, organisasi dapat melindungi reputasi merek, menjamin privasi data pengguna, dan mempermudah tim keamanan siber dalam memantau maupun menyelesaikan masalah jaringan (*troubleshooting*) di masa depan.
