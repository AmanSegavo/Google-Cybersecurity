# Aktivitas Portofolio: Menganalisis Serangan Jaringan (Network Attack Analysis)

**Program:** Google Cybersecurity Professional Certificate  
**Modul:** Connect and Protect: Networks and Network Security (Course 3)  
**Topik:** Investigasi Serangan Denial of Service (DoS) & Analisis Protokol TCP/IP  
**Studi Kasus:** Analisis Serangan TCP SYN Flood yang Mengakibatkan *Connection Timeout*  

---

## 1. Deskripsi Masalah & Skenario Insiden

Pengguna sistem melaporkan bahwa mereka tidak dapat mengakses situs web publik organisasi. Saat mencoba membuka halaman web melalui peramban (*browser*), pengguna menerima pesan kesalahan:  
`"Connection Timeout: The server at example.com is taking too long to respond."`

Sebagai analis keamanan siber (*cybersecurity analyst*), saya ditugaskan untuk menginvestigasi file log lalu lintas jaringan (*packet capture / log files*) untuk mengidentifikasi penyebab insiden, protokol yang terdampak, serta menyusun rekomendasi teknis guna memitigasi serangan.

---

## 2. Analisis File Log & Identifikasi Serangan

### Temuan Data Log Jaringan (`tcpdump` / Wireshark excerpt):
```text
12:00:01.102345 IP 198.51.100.23.49152 > 203.0.113.10.80: Flags [S], seq 1002345, win 65535, options [mss 1460,nop,wscale 6], length 0
12:00:01.102380 IP 198.51.100.23.49153 > 203.0.113.10.80: Flags [S], seq 1002346, win 65535, options [mss 1460,nop,wscale 6], length 0
12:00:01.102415 IP 203.0.113.45.52110 > 203.0.113.10.80: Flags [S], seq 3491201, win 65535, options [mss 1460,nop,wscale 6], length 0
12:00:01.102450 IP 192.0.2.77.60112 > 203.0.113.10.80: Flags [S], seq 8912301, win 65535, options [mss 1460,nop,wscale 6], length 0
... (Ribuan paket serupa per detik tanpa ada paket balasan ACK dari klien) ...
```

### Identifikasi Serangan:
Berdasarkan analisis data log di atas, serangan yang terjadi adalah **TCP SYN Flood Attack**, yang merupakan salah satu bentuk serangan **Denial of Service (DoS)** pada lapisan transpor (*Transport Layer / Layer 4* model OSI).

---

## 3. Mekanisme Kerja Serangan & Eksploitasi Protokol TCP

Protokol TCP menggunakan mekanisme **Three-Way Handshake** untuk membangun koneksi yang andal:

```text
Koneksi Normal (3-Way Handshake):
Client ────────────── [SYN] ─────────────> Server (Mengalokasikan memori)
Client <────────── [SYN-ACK] ───────────── Server
Client ────────────── [ACK] ─────────────> Server (Koneksi Terbentuk / ESTABLISHED)

Serangan SYN Flood:
Attacker (Spoofed IP) ── [SYN] ──────────> Server (Mengalokasikan antrean backlog)
Attacker (Spoofed IP) <─ [SYN-ACK] ─────── Server (Menunggu respon ACK...)
Attacker (Mengabaikan/Tidak Mengirim ACK)  Server (Koneksi menggantung / Half-Open)
```

### Bagaimana Penyerang Mengeksploitasi Kerentanan Ini:
1. Penyerang mengirimkan ribuan paket permintaan inisiasi koneksi (`SYN`) per detik ke port web server (Port 80 HTTP / 443 HTTPS).
2. Paket-paket tersebut menggunakan **alamat IP sumber palsu (*IP Spoofing*)** atau penyerang sengaja tidak mengirimkan paket konfirmasi balik (`ACK`).
3. Server merespons setiap permintaan dengan `SYN-ACK` dan mencadangkan memori untuk antrean koneksi setengah terbuka (*half-open connection backlog queue*).
4. Karena paket `ACK` akhir tidak pernah tiba, kapasitas memori antrean *backlog* server menjadi penuh (*exhausted*).

---

## 4. Mengapa Terjadi Kesalahan *"Connection Timeout"*?

Ketika antrean koneksi setengah terbuka (*SYN backlog table*) pada server web telah mencapai kapasitas maksimum:
* Server tidak lagi dapat menerima atau memproses permintaan koneksi baru dari pengguna yang sah (*legitimate users*).
* Permintaan dari pengguna yang sah diabaikan atau dibuang (*dropped*).
* Setelah melewati batas waktu tunggu tertentu (*timeout threshold*), peramban pengguna akan menampilkan pesan kesalahan **"Connection Timeout"**.

---

## 5. Rekomendasi Mitigasi & Pengerasan Keamanan (Remediation Plan)

Untuk mengatasi dan mencegah serangan TCP SYN Flood di masa mendatang, tim keamanan menerapkan langkah-langkah berikut:

| No | Tindakan Mitigasi | Deskripsi Teknis | Manfaat Keamanan |
|:---|:---|:---|:---|
| **1** | **Aktivasi TCP SYN Cookies** | Mengaktifkan `syncookies` pada kernel sistem operasi server (misal: Linux `sysctl -w net.ipv4.tcp_syncookies=1`). | Server tidak perlu mengalokasikan memori antrean sebelum menerima paket `ACK` yang sah. |
| **2** | **Firewall Rate-Limiting** | Mengonfigurasi iptables/firewall untuk membatasi jumlah paket `SYN` baru per detik per IP sumber. | Menahan banjir paket sebelum membebani *web service*. |
| **3** | **Optimalisasi Timeout TCP** | Mengurangi nilai `tcp_synack_retries` dan memperpendek durasi tunggu *half-open connections*. | Membebaskan antrean memori lebih cepat jika tidak ada balasan dari klien. |
| **4** | **Penerapan Anti-DDoS & Load Balancer** | Menggunakan layanan *Cloud DDoS Protection* (seperti Cloudflare atau AWS Shield) dan *Reverse Proxy*. | Menyaring trafik berbahaya di level penyedia sebelum mencapai server asal (*origin server*). |
