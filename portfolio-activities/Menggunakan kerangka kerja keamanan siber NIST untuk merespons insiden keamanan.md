# Aktivitas Portofolio: Menggunakan Kerangka Kerja Keamanan Siber NIST untuk Merespons Insiden Keamanan

**Program:** Google Cybersecurity Professional Certificate  
**Modul:** Play It Safe: Manage Security Risks & Networks and Network Security  
**Kerangka Kerja:** NIST Cybersecurity Framework (NIST CSF) — *Identify, Protect, Detect, Respond, Recover*  
**Studi Kasus:** Analisis Laporan Insiden Serangan DDoS ICMP Flood  

---

## 1. Ringkasan Insiden (Incident Summary)

Perusahaan mengalami gangguan keamanan siber berskala besar ketika seluruh layanan jaringan internal dan eksternal tiba-tiba berhenti merespons (*connection disruption*). Setelah dilakukan investigasi oleh tim keamanan siber, insiden tersebut diidentifikasi sebagai serangan **Distributed Denial of Service (DDoS)** yang memanfaatkan banjir paket **ICMP (Internet Control Message Protocol flood attack)**.

Tim keamanan siber merespons dengan memblokir lalu lintas serangan pada *firewall*, menonaktifkan sementara layanan jaringan non-kritis guna mengurangi beban bandwidth internal, dan memulihkan kembali layanan jaringan penting hingga operasional normal kembali tercapai.

---

## 2. Penerapan 5 Pilar NIST Cybersecurity Framework (NIST CSF)

```text
┌──────────────┐     ┌──────────────┐     ┌──────────────┐     ┌──────────────┐     ┌──────────────┐
│ 1. IDENTIFY  │ ──> │  2. PROTECT  │ ──> │  3. DETECT   │ ──> │  4. RESPOND  │ ──> │  5. RECOVER  │
│(Identifikasi)│     │(Perlindungan)│     │ (Deteksi)    │     │  (Respons)   │     │ (Pemulihan)  │
└──────────────┘     └──────────────┘     └──────────────┘     └──────────────┘     └──────────────┘
```

---

### 🔍 1. Identify (Identifikasi)
* **Aktor Ancaman & Vektor Serangan:**  
  Aktor ancaman eksternal (*malicious actor*) melancarkan serangan *ICMP flood* dengan volume paket *ping request* (ICMP Echo Request) yang masif untuk membanjiri antarmuka jaringan dan menghabiskan sumber daya komputasi router/server.
* **Ruang Lingkup Insiden:**  
  Seluruh jaringan internal perusahaan, server aplikasi web publik, dan gerbang koneksi (*gateway*) mengalami kelumpuhan total (*denial of service*).
* **Aset yang Terdampak:**  
  Ketersediaan (*availability*) dari seluruh server produksi, database transaksi, dan portal layanan pelanggan.

---

### 🛡️ 2. Protect (Perlindungan)
Tindakan teknis yang diimplementasikan untuk melindungi jaringan dari eksploitasi serupa di masa depan:
* **Konfigurasi Firewall Rate-Limiting:**  
  Menerapkan aturan *firewall* baru untuk membatasi laju (*rate limit*) penerimaan paket ICMP yang masuk per detik.
* **Penerapan IDS/IPS:**  
  Mengonfigurasi sistem *Intrusion Detection System / Intrusion Prevention System* (IDS/IPS) dengan tanda tangan aturan (*rule signatures*) untuk secara otomatis menjatuhkan (*drop*) paket ICMP yang memiliki karakteristik anomali atau mencurigakan.
* **Segmentasi Jaringan & Pembatasan Port:**  
  Menutup port dan protokol diagnostik yang tidak esensial dari jaringan publik eksternal.

---

### 📡 3. Detect (Deteksi)
Mekanisme pemantauan untuk mendeteksi ancaman secara dini:
* **Verifikasi Alamat IP Sumber (*Source IP Verification*):**  
  Mengonfigurasi fitur verifikasi IP pada *firewall* (seperti *Reverse Path Forwarding / uRPF*) guna mendeteksi paket ICMP dengan alamat IP palsu (*spoofed IP addresses*).
* **Perangkat Lunak Pemantau Jaringan (*Network Monitoring & Telemetry*):**  
  Mengintegrasikan alat pemantau lalu lintas jaringan (misalnya Prometheus, Grafana, atau PRTG) untuk memberikan peringatan dini (*alerting*) saat terjadi lonjakan trafik bandwidth yang tidak wajar.

---

### ⚡ 4. Respond (Respons)
Prosedur penanganan insiden untuk memitigasi dampak serangan saat terjadi:
1. **Isolasi Sistem:** Mengisolasi node atau subnet yang terdampak untuk mencegah efek domino pada segmen jaringan lainnya.
2. **Prioritas Pemulihan Layanan Kritis:** Mematikan layanan non-kritis terlebih dahulu agar bandwidth dan kapasitas CPU dialokasikan penuh untuk memulihkan layanan inti.
3. **Analisis Log Jaringan:** Mengumpulkan dan menganalisis log dari *firewall*, router, dan server web untuk mengekstrak indikator kompromi (*Indicator of Compromise / IoC*).
4. **Eskalasi & Pelaporan:** Melaporkan kronologi insiden, estimasi kerugian waktu henti (*downtime*), dan langkah penanganan kepada manajemen eksekutif serta pihak otoritas hukum jika diperlukan.

---

## 5. Recover (Pemulihan)
Rencana pemulihan untuk mengembalikan seluruh sistem ke kondisi operasional normal:
1. **Blokir Sumber Serangan di Perimeter:** Memastikan lalu lintas serangan telah sepenuhnya diblokir di level *perimeter firewall* atau *upstream ISP*.
2. **Verifikasi Beban Lalu Lintas:** Menunggu *timeout* dari sisa paket banjir ICMP dan memastikan antrean paket kembali stabil pada ambang batas normal.
3. **Penyalaan Bertahap (*Phased Re-enabling*):** Menyalakan kembali sistem dan layanan jaringan non-kritis satu per satu sambil terus memantau performa latensi dan kestabilan koneksi.
4. **Evaluasi Pasca-Insiden (*Post-Incident Review / Lessons Learned*):** Melakukan tinjauan menyeluruh bersama tim IT untuk menyempurnakan buku panduan penanganan insiden (*Incident Response Playbook*).

---

## 6. Tabel Matriks Analisis Insiden NIST CSF

| Fungsi NIST | Tindakan yang Diambil | Hasil & Dampak Keamanan |
|:---|:---|:---|
| **Identify** | Menganalisis sifat serangan DDoS ICMP Flood dan memetakan aset yang lumpuh. | Penentuan akar masalah dan estimasi ruang lingkup insiden secara akurat. |
| **Protect** | Menerapkan aturan *rate-limiting* ICMP di firewall dan filter pada IDS/IPS. | Memperkuat perimeter jaringan terhadap serangan banjir paket berulang. |
| **Detect** | Mengonfigurasi inspeksi *anti-spoofing* IP dan pemantauan anomali lalu lintas. | Deteksi dini dan peringatan otomatis terhadap lonjakan trafik tidak normal. |
| **Respond** | Mengisolasi segmen, mematikan servis non-kritis, dan menganalisis log. | Pengurangan dampak kerusakan dan pemulihan fokus pada sistem utama. |
| **Recover** | Mengembalikan layanan bertahap dan menyusun laporan *Lessons Learned*. | Sistem kembali normal dan ketahanan operasional jangka panjang meningkat. |
