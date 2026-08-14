# Panduan Lengkap: Membuat Portofolio Keamanan Siber Profesional (Cybersecurity Portfolio Guide)

**Program:** Google Cybersecurity Professional Certificate  
**Kategori:** Pengembangan Karier & Dokumentasi Portofolio Profesional  

---

## 1. Apa Itu Portofolio Keamanan Siber & Mengapa Diperlukan?

**Portofolio Keamanan Siber** adalah kumpulan dokumentasi terstruktur yang membuktikan keahlian teknis, pemahaman metodologi, dan pengalaman praktis seorang profesional keamanan siber. 

### Perbedaan Portofolio vs Resume:
* **Resume (1–2 Halaman):** Berisi ringkasan riwayat pendidikan, pengalaman kerja, sertifikasi, dan daftar ringkas keahlian.
* **Portofolio:** Menampilkan **karya nyata, laporan investigasi insiden, analisis log, skrip automasi, dan audit kontrol** yang membuktikan bahwa Anda benar-benar mampu melakukan pekerjaan yang Anda lamar (*proof of competence*).

---

## 2. Pilihan Platform untuk Menghosting Portofolio Anda

Terdapat 4 opsi utama untuk membangun dan mempublikasikan portofolio keamanan siber:

```text
┌─────────────────────────┬──────────────────────────────────────────────────────────┐
│ Opsi Platform           │ Karakteristik & Keunggulan                               │
├─────────────────────────┼──────────────────────────────────────────────────────────┤
│ 1. Repositori Git       │ Standar industri developer & cybersecurity analyst.      │
│    (GitHub / GitLab)    │ Mendukung Markdown, pelacakan versi, dan gratis dihosting.│
├─────────────────────────┼──────────────────────────────────────────────────────────┤
│ 2. Google Sites         │ Tampilan web visual responsif, mudah disesuaikan, dan    │
│                         │ memiliki URL publik yang mudah dibagikan.                │
├─────────────────────────┼──────────────────────────────────────────────────────────┤
│ 3. Cloud Storage        │ Berbagi tautan folder online dengan calon pemberi kerja; │
│    (Google Drive/Dropbox│ pembaruan dokumen otomatis tersinkronisasi.              │
├─────────────────────────┼──────────────────────────────────────────────────────────┤
│ 4. Folder Dokumen Lokal │ Arsip terstruktur di hard drive komputer pribadi untuk   │
│                         │ manajemen berkas cepat saat persiapan melamar pekerjaan. │
└─────────────────────────┴──────────────────────────────────────────────────────────┘
```

---

## 3. Proyek Portofolio Utama dalam Google Cybersecurity Certificate

Sepanjang program sertifikat Google Cybersecurity, terdapat berbagai proyek berbasis skenario dunia nyata yang dapat dimasukkan ke dalam portofolio Anda:

1. 📄 **[Melakukan Audit Keamanan Siber (Botium Toys)](./Melakukan%20audit%20keamanan.md)**: Evaluasi kontrol administratif, teknis, dan fisik serta audit kepatuhan regulasi (PCI DSS, GDPR, SOC 2).
2. 📄 **[Menggunakan Kerangka Kerja NIST CSF untuk Merespons Insiden](./Menggunakan%20kerangka%20kerja%20keamanan%20siber%20NIST%20untuk%20merespons%20insiden%20keamanan.md)**: Penerapan 5 fungsi NIST (*Identify, Protect, Detect, Respond, Recover*) pada insiden DDoS ICMP flood.
3. 📄 **[Menganalisis Serangan Jaringan (TCP SYN Flood)](./Menganalisis%20serangan%20jaringan.md)**: Investigasi paket log jaringan (*tcpdump*), dekonstruksi *three-way handshake*, dan mitigasi *connection timeout*.
4. 📄 **[Analisis Pengerasan Jaringan & Penilaian Risiko](./Analisis%20pengerasan%20jaringan.md)**: Analisis risiko database usang & *password sharing*, serta penyusunan Kebijakan Keamanan Informasi.
5. 📄 **[Menggunakan Perintah Linux untuk Mengelola Perizinan File](./Menggunakan%20perintah%20Linux%20untuk%20mengelola%20perizinan%20file.md)**: Audit perizinan file & direktori menggunakan `ls -la` dan remediasi izin dengan `chmod` berbasis *Least Privilege*.
6. 📄 **Menerapkan Filter ke Kueri SQL**: Investigasi insiden login mencurigakan dan pemfilteran log database menggunakan klausa `WHERE`, `AND`, `OR`, `LIKE`, dan `BETWEEN`.
7. 📄 **Mendokumentasikan Insiden dengan Jurnal Penangan Insiden (*Incident Handler's Journal*)**: Dokumentasi kronologis penanganan insiden menggunakan alat SIEM (Splunk/Chronicle).
8. 📄 **Automasi Keamanan dengan Algoritma Python**: Pembuatan skrip Python untuk mengotomasi pembaruan dan parsing daftar alamat IP yang diizinkan (*allowlist/denylist*).

---

## 4. Etika & Praktik Terbaik Portofolio Keamanan Siber

* ⚠️ **Larangan Data Sensitif/Hak Cipta:** Jangan pernah menyertakan informasi pribadi asli (*PII*), kunci privat/rahasia API (*secret keys*), atau data rahasia perusahaan tempat Anda bekerja. Gunakan data sintetis atau skenario praktikum.
* 🔒 **Pengaturan Privasi:** Jika menggunakan situs atau repositori khusus yang belum siap, Anda dapat mengatur repositori ke mode *Private* hingga portofolio selesai disunting dan siap dipublikasikan.
* ✍️ **Gunakan Kata-Kata Sendiri:** Calon pemberi kerja lebih menghargai kemampuan Anda dalam menjelaskan metodologi, pola pikir analisis, dan justifikasi keamanan daripada sekadar menyalin template jawaban.