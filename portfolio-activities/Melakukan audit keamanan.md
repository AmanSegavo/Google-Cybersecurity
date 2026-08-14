# Aktivitas Portofolio: Melakukan Audit Keamanan Siber (Security Audit)

**Program:** Google Cybersecurity Professional Certificate  
**Modul:** Play It Safe: Manage Security Risks (Course 2)  
**Studi Kasus:** Audit Kontrol Keamanan & Kepatuhan pada Botium Toys  

---

## 1. Ringkasan Eksekutif (Executive Summary)

**Botium Toys** adalah perusahaan mainan anak-anak skala menengah yang berkembang pesat dengan operasi e-commerce internasional dan lokasi fisik (kantor pusat, toko ritel, dan gudang). Seiring dengan ekspansi bisnis, manajemen Botium Toys memutuskan untuk melakukan audit keamanan menyeluruh guna mengevaluasi postur keamanan, mengidentifikasi celah kepatuhan (*compliance gaps*), serta menyusun rekomendasi mitigasi risiko sebelum meluncurkan sistem baru.

### Ruang Lingkup Audit (*Scope*):
- Sistem internal IT, server database lokal, dan perangkat lunak warisan (*legacy systems*).
- Transaksi pembayaran online pelanggan internasional (termasuk pelanggan dari Uni Eropa dan AS).
- Kontrol administratif, teknis, dan fisik di lokasi kantor, toko, dan gudang.
- Kepatuhan terhadap standar regulasi: **PCI DSS**, **GDPR**, dan **SOC 2**.

---

## 2. Daftar Periksa Kontrol Keamanan (Controls Checklist)

Evaluasi penerapan kontrol administratif, teknis, dan fisik pada Botium Toys:

| Kategori Kontrol | Kontrol Keamanan | Status Saat Ini (Ya/Tidak) | Penjelasan & Temuan Audit |
|:---|:---|:---:|:---|
| **Administratif** | **Prinsip Hak Akses Terendah (*Least Privilege*)** | ❌ Tidak | Seluruh karyawan saat ini memiliki akses luas ke seluruh data internal tanpa batasan peran kerja. |
| **Administratif** | **Pemisahan Tugas (*Separation of Duties*)** | ❌ Tidak | Belum ada pemisahan wewenang antara pengguna umum, pengembang, dan staf keuangan. |
| **Administratif** | **Rencana Pemulihan Bencana (*Disaster Recovery Plan*)** | ❌ Tidak | Belum ada prosedur tertulis dan teruji jika terjadi insiden kebocoran data atau kegagalan sistem. |
| **Administratif** | **Kebijakan Kata Sandi (*Password Policies*)** | ❌ Tidak | Kebijakan kata sandi masih sangat minim dan tidak ada panduan rotasi/kompleksitas kata sandi. |
| **Teknis** | **Sistem Deteksi Intrusi (*IDS - Intrusion Detection System*)** | ❌ Tidak | Departemen IT belum memiliki IDS untuk memantau aktivitas mencurigakan dan mendeteksi intrusi jaringan. |
| **Teknis** | **Cadangan Data (*Data Backups*)** | ❌ Tidak | Belum ada jadwal pencadangan data berkala untuk menjamin kelangsungan bisnis (*business continuity*). |
| **Teknis** | **Perangkat Lunak Antivirus (*Antivirus Software*)** | ✅ Ya | Antivirus telah terpasang di semua workstation dan dipantau secara berkala oleh departemen IT. |
| **Teknis** | **Pemeliharaan Sistem Warisan (*Legacy Systems*)** | ❌ Tidak | Sistem warisan masih digunakan namun pemantauan dan intervensi dilakukan ad-hoc tanpa jadwal rutin. |
| **Teknis** | **Enkripsi Data (*Data Encryption*)** | ❌ Tidak | Data keuangan dan data sensitif pelanggan belum dienkripsi saat disimpan (*at-rest*) maupun dikirim (*in-transit*). |
| **Teknis** | **Sistem Manajemen Kata Sandi (*Password Manager*)** | ❌ Tidak | Karyawan belum difasilitasi *password manager*, menyebabkan risiko pencatatan kata sandi tidak aman. |
| **Fisik** | **Kunci Pintu (*Locks: Office, Storefront, Warehouse*)** | ✅ Ya | Pintu kantor, etalase toko, dan gudang telah dilengkapi kunci fisik yang memadai. |
| **Fisik** | **Pengawasan CCTV (*CCTV Surveillance*)** | ✅ Ya | Kamera CCTV aktif dan berfungsi dengan baik di seluruh area strategis perusahaan. |
| **Fisik** | **Sistem Pencegah Kebakaran (*Fire Detection & Sprinklers*)** | ✅ Ya | Fasilitas fisik memiliki alarm kebakaran dan sistem sprinkler yang berfungsi normal. |

---

## 3. Daftar Periksa Kepatuhan Regulasi (Compliance Checklist)

### A. Payment Card Industry Data Security Standard (PCI DSS)
| Praktik Kepatuhan | Diterapkan (Ya/Tidak) | Penjelasan Temuan |
|:---|:---:|:---|
| Akses data kartu kredit hanya untuk pengguna terotorisasi | ❌ Tidak | Semua karyawan memiliki akses internal yang belum dibatasi ke data kartu kredit. |
| Data kartu kredit diproses dan disimpan di lingkungan aman | ❌ Tidak | Data kartu kredit tidak dienkripsi dan disimpan di lingkungan bersama. |
| Penerapan prosedur enkripsi data transaksi | ❌ Tidak | Belum ada enkripsi *end-to-end* pada *touchpoint* transaksi pelanggan. |
| Kebijakan manajemen kata sandi yang aman | ❌ Tidak | Kebijakan kata sandi masih lemah dan tidak ada sistem manajemen kata sandi. |

### B. General Data Protection Regulation (GDPR)
| Praktik Kepatuhan | Diterapkan (Ya/Tidak) | Penjelasan Temuan |
|:---|:---:|:---|
| Data pelanggan Uni Eropa (EU) dijaga kerahasiaan & keamanannya | ❌ Tidak | Tidak adanya enkripsi menempatkan PII pelanggan EU pada risiko kebocoran data tinggi. |
| Rencana notifikasi kebocoran data dalam 72 jam | ✅ Ya | Botium Toys telah memiliki SOP formal untuk memberitahu otoritas & pelanggan EU dalam waktu 72 jam jika terjadi *data breach*. |
| Klasifikasi dan inventarisasi aset data | ❌ Tidak | Aset perangkat keras telah diinventarisasi, namun data belum diklasifikasikan berdasarkan sensitivitas. |
| Penerapan kebijakan & proses privasi data | ✅ Ya | Kebijakan privasi telah didokumentasikan dan disosialisasikan kepada tim IT. |

### C. System and Organization Controls (SOC 2)
| Praktik Kepatuhan | Diterapkan (Ya/Tidak) | Penjelasan Temuan |
|:---|:---:|:---|
| Kebijakan akses pengguna (*User Access Policies*) | ❌ Tidak | Kontrol *Least Privilege* dan pemisahan tugas belum diimplementasikan. |
| Kerahasiaan data sensitif (PII / SPII) | ❌ Tidak | Data PII belum dienkripsi saat disimpan di database lokal. |
| Integritas data (*Data Integrity*) | ✅ Ya | Mekanisme validasi dan konsistensi data transaksi berfungsi dengan baik. |
| Akses data hanya untuk pihak berwenang | ❌ Tidak | Data dapat diakses oleh semua pengguna internal, otorisasi perlu dibatasi sesuai fungsi kerja (*role-based*). |

---

## 4. Rekomendasi Mitigasi Risiko & Rencana Tindakan

Berdasarkan temuan audit, berikut rekomendasi prioritas tinggi yang perlu disampaikan kepada pemangku kepentingan (*stakeholders*):

1. **Implementasi Kontrol Akses Berbasis Peran (*Role-Based Access Control / RBAC*) & Least Privilege:**
   * Batasi hak akses karyawan hanya pada data yang mutlak dibutuhkan untuk tugas mereka.
   * Cabut akses umum ke data kartu kredit pelanggan dan database utama.
2. **Penerapan Enkripsi Menyeluruh (*End-to-End Encryption*):**
   * Enkripsi seluruh data sensitif (kartu kredit, PII/SPII) saat transit menggunakan TLS 1.3 dan saat disimpan (*at-rest*) menggunakan AES-256 guna memenuhi standar PCI DSS dan GDPR.
3. **Penggelaran Sistem Deteksi Intrusi (IDS) & SIEM:**
   * Pasang *Network Intrusion Detection System* (NIDS) seperti Snort atau Suricata untuk memonitor lalu lintas jaringan mencurigakan dan mendeteksi upaya eksploitasi sejak dini.
4. **Penerapan Sistem Manajemen Kata Sandi & Kebijakan MFA:**
   * Wajibkan penggunaan *password manager* perusahaan dan terapkan Autentikasi Multifaktor (MFA) untuk seluruh akses administratif dan sistem internal.
5. **Klasifikasi Aset Data & Manajemen Patch Sistem Warisan:**
   * Lakukan klasifikasi data (Publik, Internal, Rahasia, Sangat Rahasia) serta jadwalkan pemeliharaan dan *patching* rutin untuk sistem warisan (*legacy systems*).