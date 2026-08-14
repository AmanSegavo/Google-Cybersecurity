# 🛡️ Google Cybersecurity Professional Certificate & Portfolio

[![GitHub](https://img.shields.io/badge/GitHub-AmanSegavo-blue?logo=github)](https://github.com/AmanSegavo)
[![Coursera](https://img.shields.io/badge/Coursera-Google%20Cybersecurity-0056D2?logo=coursera)](https://www.coursera.org/professional-certificates/google-cybersecurity)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

Repositori ini berisi dokumentasi aktivitas portofolio praktikum, sertifikat kursus yang telah diselesaikan, dan materi referensi dari program **Google Cybersecurity Professional Certificate** (Coursera).

---

## 📁 Struktur Direktori Repositori

```text
Google-Cybersecurity/
├── 📜 README.md                                  # Dokumentasi utama repositori
├── 📂 certificates/                             # Arsip sertifikat resmi (PDF & Gambar)
│   ├── Course 1 - Foundations of Cybersecurity (Google).pdf
│   ├── Course 2 - Play It Safe - Manage Security Risks (Google).pdf
│   ├── Course 3 - Connect and Protect - Networks and Network Security (Google).pdf
│   ├── Google - Stay Ahead of the AI Curve.pdf
│   ├── IBM - What is Data Science.pdf
│   └── AWS - AI Academy Certificate.png
├── 📂 portfolio-activities/                     # Laporan aktivitas portofolio praktikum
│   └── Menggunakan perintah Linux untuk mengelola perizinan file.md
└── 📂 docs/                                     # Dokumen pendukung & contekan (cheat sheet)
    ├── Create a cybersecurity portfolio.pdf
    └── link.md
```

---

## 🎓 Sertifikat yang Telah Diselesaikan

Berikut adalah daftar sertifikat resmi yang telah diperoleh beserta tautan verifikasi online:

| No | Modul / Kursus | Institusi | File Sertifikat | Tautan Verifikasi Resmi |
|:---|:---|:---:|:---:|:---:|
| **1** | **Foundations of Cybersecurity** *(Course 1)* | Google | [Lihat PDF](./certificates/Course%201%20-%20Foundations%20of%20Cybersecurity%20(Google).pdf) | [Verifikasi Coursera (NEX8JMGB7VC8)](https://coursera.org/verify/NEX8JMGB7VC8) |
| **2** | **Play It Safe: Manage Security Risks** *(Course 2)* | Google | [Lihat PDF](./certificates/Course%202%20-%20Play%20It%20Safe%20-%20Manage%20Security%20Risks%20(Google).pdf) | [Verifikasi Coursera (ILX81GZNA3PC)](https://coursera.org/verify/ILX81GZNA3PC) |
| **3** | **Connect and Protect: Networks and Network Security** *(Course 3)* | Google | [Lihat PDF](./certificates/Course%203%20-%20Connect%20and%20Protect%20-%20Networks%20and%20Network%20Security%20(Google).pdf) | [Verifikasi Coursera (KD1HL280OQ03)](https://coursera.org/verify/KD1HL280OQ03) |
| **4** | **Stay Ahead of the AI Curve** | Google | [Lihat PDF](./certificates/Google%20-%20Stay%20Ahead%20of%20the%20AI%20Curve.pdf) | [Verifikasi Coursera (85LVQWY4AHMF)](https://coursera.org/verify/85LVQWY4AHMF) |
| **5** | **What is Data Science?** | IBM | [Lihat PDF](./certificates/IBM%20-%20What%20is%20Data%20Science.pdf) | [Verifikasi Coursera (SEV06F1TUCAD)](https://coursera.org/verify/SEV06F1TUCAD) |
| **6** | **AWS AI Academy** | AWS | [Lihat Gambar](./certificates/AWS%20-%20AI%20Academy%20Certificate.png) | *Sertifikat Pelatihan AWS* |

---

## 💼 Aktivitas Portofolio (Portfolio Activities)

### 📄 [Aktivitas: Menggunakan Perintah Linux untuk Mengelola Perizinan File](./portfolio-activities/Menggunakan%20perintah%20Linux%20untuk%20mengelola%20perizinan%20file.md)
* **Modul:** *Tools of the Trade: Linux and SQL* (Course 4)
* **Topik:** Audit keamanan file, pembongkaran string izin 10-karakter, remediasi akses dengan `chmod`, dan penerapan prinsip *Least Privilege*.
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

## 👤 Profil Pembuat
* **Nama:** Abdurrahman Assegaf
* **GitHub:** [@AmanSegavo](https://github.com/AmanSegavo)
* **Program:** Google Cybersecurity Professional Certificate
