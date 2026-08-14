# 🛡️ Google Cybersecurity Professional Certificate - Portfolio Activity

Repositori ini berisi dokumentasi aktivitas portofolio dari program **Google Cybersecurity Professional Certificate** (Coursera) pada modul **Tools of the Trade: Linux and SQL**.

---

## 📋 Daftar Isi / Konten

1. 📄 **[Aktivitas: Menggunakan Perintah Linux untuk Mengelola Perizinan File](./Menggunakan%20perintah%20Linux%20untuk%20mengelola%20perizinan%20file.md)**  
   Dokumentasi lengkap audit keamanan siber, analisis string perizinan 10-karakter, dan remediasi hak akses file/direktori dengan perintah `chmod` berdasarkan prinsip *Least Privilege*.

2. 🔗 **[Referensi & Cheat Sheet Perizinan Linux](./link.md)**  
   Kumpulan referensi resmi (Coursera, Google, NIST, CIS, Linux Man Pages) dan lembar contekan (*cheat sheet*) notasi simbolik serta oktal.

---

## 🚀 Ringkasan Perintah Linux yang Digunakan

```bash
# 1. Menampilkan detail file termasuk file tersembunyi
ls -la /home/researcher2/projects

# 2. Mencabut izin tulis untuk pengguna lain (Others)
chmod o-w project_k.txt

# 3. Menghapus izin eksekusi dan mencabut izin tulis untuk others
chmod u-x,g-x,o-wx project_r.txt

# 4. Mengamankan file tersembunyi (User: rw, Group: r, Others: none)
chmod 640 .project_x.txt

# 5. Mengunci direktori rahasia hanya untuk pemilik
chmod 700 drafts
```

---

## 👤 Profil & Kontak
- **Author:** [Abdurrahman Assegaf (AmanSegavo)](https://github.com/AmanSegavo)
- **Program:** Google Cybersecurity Professional Certificate
