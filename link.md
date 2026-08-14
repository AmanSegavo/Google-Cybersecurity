# Referensi & Tautan Penting: Google Cybersecurity & Manajemen Perizinan Linux

Dokumen ini berisi daftar tautan resmi, dokumentasi teknis, lembar contekan (*cheat sheet*), dan materi pendukung untuk modul **Google Cybersecurity Professional Certificate** serta pengelolaan izin file di Linux.

---

## 1. Tautan Resmi Google Cybersecurity Certificate
- **Coursera Program Utama:**  
  [Google Cybersecurity Professional Certificate - Coursera](https://www.coursera.org/professional-certificates/google-cybersecurity)
- **Kursus Terkait (Course 4 - Linux & SQL):**  
  [Tools of the Trade: Linux and SQL - Coursera](https://www.coursera.org/learn/linux-and-sql)
- **Google Career Certificates Portal:**  
  [Grow with Google - Cybersecurity Certificates](https://grow.google/certificates/cybersecurity/)

---

## 2. Dokumentasi Resmi Linux & Manual Pages
- **Manual Perintah `chmod` (Change Mode):**  
  [GNU Coreutils - chmod Invocation](https://www.gnu.org/software/coreutils/manual/html_node/chmod-invocation.html) | [Linux man page chmod(1)](https://man7.org/linux/man-pages/man1/chmod.1.html)
- **Manual Perintah `ls` (List Directory Contents):**  
  [GNU Coreutils - ls Invocation](https://www.gnu.org/software/coreutils/manual/html_node/ls-invocation.html) | [Linux man page ls(1)](https://man7.org/linux/man-pages/man1/ls.1.html)
- **Manual Perintah `chown` & `chgrp`:**  
  [Linux man page chown(1)](https://man7.org/linux/man-pages/man1/chown.1.html) | [Linux man page chgrp(1)](https://man7.org/linux/man-pages/man1/chgrp.1.html)
- **Standar Hirarki Sistem File Linux (FHS):**  
  [Filesystem Hierarchy Standard (FHS)](https://refspecs.linuxfoundation.org/fhs.shtml)

---

## 3. Standar & Praktik Keamanan Siber (Security Standards)
- **NIST Special Publication 800-53 (Access Control Guidelines):**  
  [NIST SP 800-53 Rev. 5 - Security and Privacy Controls](https://csrc.nist.gov/publications/detail/sp/800-53/rev-5/final)
- **CIS Benchmarks (Center for Internet Security - Linux Hardening):**  
  [CIS Linux Benchmarks](https://www.cisecurity.org/benchmark/linux)
- **Principle of Least Privilege (PoLP):**  
  [CISA - Least Privilege Security Principle](https://www.cisa.gov/resources-tools/resources/principles-least-privilege)

---

## 4. Lembar Contekan Cepat (*Cheat Sheet*) Perizinan Linux

### A. Format Notasi Simbolik
```bash
# Struktur: chmod [target][operator][izin] [file/direktori]
# Target: u (user/owner), g (group), o (other), a (all)
# Operator: + (tambah izin), - (cabut izin), = (tetapkan izin persis)
# Izin: r (read), w (write), x (execute)

# Contoh Penggunaan:
chmod u+x script.sh          # Tambah izin eksekusi untuk pemilik
chmod o-w dokumen.txt        # Hapus izin tulis untuk others
chmod g=rw file.txt          # Tetapkan izin grup tepat read & write
chmod u=rw,g=r,o= rahasia.md # User rw, group r, other tidak ada akses
```

### B. Format Notasi Numerik / Oktal
| Nilai Desimal | Biner | String Izin | Arti / Hak Akses |
| :---: | :---: | :---: | :--- |
| **0** | `000` | `---` | Tidak ada hak akses sama sekali |
| **1** | `001` | `--x` | Hanya izin eksekusi (*execute only*) |
| **2** | `010` | `-w-` | Hanya izin menulis (*write only*) |
| **3** | `011` | `-wx` | Menulis dan eksekusi (*write + execute*) |
| **4** | `100` | `r--` | Hanya izin membaca (*read only*) |
| **5** | `101` | `r-x` | Membaca dan eksekusi (*read + execute*) |
| **6** | `110` | `rw-` | Membaca dan menulis (*read + write*) |
| **7** | `111` | `rwx` | Hak akses penuh (*full read, write & execute*) |

### Nilai Oktal Standar yang Sering Digunakan:
- `chmod 755`: Standar direktori / file eksekusi (Pemilik: `rwx`, Grup & Other: `r-x`).
- `chmod 644`: Standar file teks umum (Pemilik: `rw-`, Grup & Other: `r--`).
- `chmod 600`: File sangat rahasia/private key (Pemilik: `rw-`, Grup & Other: `---`).
- `chmod 700`: Direktori pribadi (Pemilik: `rwx`, Grup & Other: `---`).
- `chmod 640`: File draf tim (Pemilik: `rw-`, Grup: `r--`, Other: `---`).

---

## 5. Perintah Tambahan Terkait Kepemilikan & Hak Akses
```bash
# Mengubah pemilik file
sudo chown nama_user nama_file

# Mengubah pemilik dan grup sekaligus secara rekursif
sudo chown -R user:grup /path/ke/direktori

# Melihat izin direktori secara spesifik (bukan isinya)
ls -ld nama_direktori

# Menampilkan izin beserta file tersembunyi
ls -la /path/ke/direktori
```
