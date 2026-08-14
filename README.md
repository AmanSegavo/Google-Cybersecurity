# 🛡️ Google Cybersecurity Professional Certificate & Portfolio

[![GitHub](https://img.shields.io/badge/GitHub-AmanSegavo-blue?logo=github)](https://github.com/AmanSegavo)
[![Coursera](https://img.shields.io/badge/Coursera-Google%20Cybersecurity-0056D2?logo=coursera)](https://www.coursera.org/professional-certificates/google-cybersecurity)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

Repositori ini khusus mendokumentasikan sertifikat resmi, materi portofolio, dan aktivitas praktikum dari program **Google Cybersecurity Professional Certificate** serta program pelatihan Google lainnya.

---

## 📁 Struktur Direktori Repositori

```text
Google-Cybersecurity/
├── 📜 README.md                                  # Dokumentasi utama repositori
├── 📂 certificates/                             # Khusus sertifikat resmi dari Google
│   ├── Course 1 - Foundations of Cybersecurity (Google).pdf
│   ├── Course 2 - Play It Safe - Manage Security Risks (Google).pdf
│   ├── Course 3 - Connect and Protect - Networks and Network Security (Google).pdf
│   ├── Google - Stay Ahead of the AI Curve.pdf
│   └── Google DEX - Pengenalan Dasar AI.pdf
├── 📂 portfolio-activities/                     # Laporan aktivitas portofolio praktikum
│   └── Menggunakan perintah Linux untuk mengelola perizinan file.md
├── 📂 docs/                                     # Dokumen pendukung & contekan (cheat sheet)
│   ├── Create a cybersecurity portfolio.pdf
│   └── link.md
└── 📂 other-certifications/                     # Sertifikat di luar program Google (IBM, AWS, Dicoding)
    ├── AWS - AI Academy Certificate.png
    ├── IBM - What is Data Science.pdf
    ├── Dicoding - Belajar Dasar Cloud dan Gen AI di AWS.pdf
    └── Dicoding - Spec-Driven Development dengan Kiro.pdf
```

---

## 🎓 Sertifikat Resmi Google (Google Certificates)

Berikut adalah daftar sertifikat dari Google yang telah diselesaikan beserta tautan verifikasi resmi:

| No | Modul / Kursus | Institusi | File Sertifikat | Tautan Verifikasi Resmi |
|:---|:---|:---:|:---:|:---:|
| **1** | **Foundations of Cybersecurity** *(Course 1)* | Google | [Lihat PDF](./certificates/Course%201%20-%20Foundations%20of%20Cybersecurity%20(Google).pdf) | [Verifikasi Coursera (NEX8JMGB7VC8)](https://coursera.org/verify/NEX8JMGB7VC8) |
| **2** | **Play It Safe: Manage Security Risks** *(Course 2)* | Google | [Lihat PDF](./certificates/Course%202%20-%20Play%20It%20Safe%20-%20Manage%20Security%20Risks%20(Google).pdf) | [Verifikasi Coursera (ILX81GZNA3PC)](https://coursera.org/verify/ILX81GZNA3PC) |
| **3** | **Connect and Protect: Networks and Network Security** *(Course 3)* | Google | [Lihat PDF](./certificates/Course%203%20-%20Connect%20and%20Protect%20-%20Networks%20and%20Network%20Security%20(Google).pdf) | [Verifikasi Coursera (KD1HL280OQ03)](https://coursera.org/verify/KD1HL280OQ03) |
| **4** | **Stay Ahead of the AI Curve** | Google | [Lihat PDF](./certificates/Google%20-%20Stay%20Ahead%20of%20the%20AI%20Curve.pdf) | [Verifikasi Coursera (85LVQWY4AHMF)](https://coursera.org/verify/85LVQWY4AHMF) |
| **5** | **Pengenalan Dasar Artificial Intelligence** | Google (DEX) | [Lihat PDF](./certificates/Google%20DEX%20-%20Pengenalan%20Dasar%20AI.pdf) | *Sertifikat Program DEX Google Nasional* |

---

## 💼 Aktivitas Portofolio (Portfolio Activities)

### 📄 [Aktivitas: Menggunakan Perintah Linux untuk Mengelola Perizinan File](./portfolio-activities/Menggunakan%20perintah%20Linux%20untuk%20mengelola%20perizinan%20file.md)
* **Modul:** *Tools of the Trade: Linux and SQL* (Course 4)
* **Topik:** Audit keamanan file, analisis string izin 10-karakter, remediasi hak akses dengan perintah `chmod`, dan penerapan prinsip *Least Privilege*.
* **Ringkasan Perintah Inti:**
  ```bash
  # Memeriksa file termasuk file tersembunyi
  ls -la /home/researcher2/projects

  # Mencabut izin tulis untuk pengguna lain (Others)
  chmod o-w project_k.txt

  # Menghapus izin eksekusi dan membatasi izin tulis others
  chmod u-x,g-x,o-wx project_r.txt

  # Mengamankan file tersembunyi (User: rw, Group: r, Other: none)
  chmod 640 .project_x.txt

  # Mengunci folder rahasia hanya untuk pemilik
  chmod 700 drafts
  ```

---

## 📚 Dokumen Pendukung & Referensi

* 📖 **[Referensi & Cheat Sheet Perizinan Linux](./docs/link.md)**: Panduan notasi simbolik, notasi oktal numerik, dan manual Linux.
* 📑 **[Create a Cybersecurity Portfolio Guide](./docs/Create%20a%20cybersecurity%20portfolio.pdf)**: Panduan penyusunan portofolio profesional Google Cybersecurity.

---

## 🌐 Sertifikasi Lainnya (Non-Google)

Arsip sertifikat di luar Google dipisahkan secara terstruktur di folder [`other-certifications/`](./other-certifications/):
* 📜 [IBM - What is Data Science](./other-certifications/IBM%20-%20What%20is%20Data%20Science.pdf) — [Verifikasi Coursera (SEV06F1TUCAD)](https://coursera.org/verify/SEV06F1TUCAD)
* 📜 [AWS - AI Academy Certificate](./other-certifications/AWS%20-%20AI%20Academy%20Certificate.png)
* 📜 [Dicoding - Belajar Dasar Cloud dan Gen AI di AWS](./other-certifications/Dicoding%20-%20Belajar%20Dasar%20Cloud%20dan%20Gen%20AI%20di%20AWS.pdf) — [Verifikasi Dicoding (EYX4Q447JPDL)](https://dicoding.com/certificates/EYX4Q447JPDL)
* 📜 [Dicoding - Spec-Driven Development dengan Kiro](./other-certifications/Dicoding%20-%20Spec-Driven%20Development%20dengan%20Kiro.pdf) — [Verifikasi Dicoding (N9ZONWNG8XG5)](https://dicoding.com/certificates/N9ZONWNG8XG5)

---

## 👤 Profil Pembuat
* **Nama:** Abdurrahman Assegaf
* **GitHub:** [@AmanSegavo](https://github.com/AmanSegavo)
* **Instagram:** [@segafaman](https://www.instagram.com/segafaman/)
* **Program:** Google Cybersecurity Professional Certificate
