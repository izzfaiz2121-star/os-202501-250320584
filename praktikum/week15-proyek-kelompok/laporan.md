# Laporan Proyek Kelompok: Mini Simulasi Sistem Operasi

**Mata Kuliah:** Praktikum Sistem Operasi

**Topik:** Integrasi CPU Scheduling, Page Replacement, dan Docker Containerization

---

## 1. Pendahuluan

### 1.1 Latar Belakang

Pemahaman mendalam mengenai mekanisme internal Sistem Operasi (SO) seperti penjadwalan proses dan manajemen memori seringkali sulit dicapai hanya melalui teori. Simulasi berbasis perangkat lunak menjadi sarana efektif untuk memvisualisasikan bagaimana algoritma OS bekerja dalam mengelola sumber daya terbatas secara efisien.

### 1.2 Tujuan

* Mengintegrasikan konsep **CPU Scheduling** dan **Page Replacement** ke dalam satu aplikasi terpadu.
* Mengimplementasikan workflow pengembangan perangkat lunak kolaboratif menggunakan Git.
* Memastikan portabilitas aplikasi menggunakan teknologi **Docker**.

---

### 2. Arsitektur Aplikasi

Aplikasi ini dirancang sebagai **aplikasi berbasis Command Line Interface (CLI)** dengan pendekatan **arsitektur modular**. Setiap modul memiliki tanggung jawab masing-masing dan saling terintegrasi melalui menu utama, sehingga memudahkan pengembangan, pengujian, dan pemeliharaan aplikasi.

Secara umum, arsitektur aplikasi terdiri dari beberapa komponen utama, yaitu:

1. **Main Program (`main.py`)**
   Berfungsi sebagai pengendali utama aplikasi yang menampilkan menu, menerima input pengguna, serta mengarahkan eksekusi ke modul yang dipilih.

2. **Modul CPU Scheduling**
   Modul ini mengimplementasikan algoritma penjadwalan proses seperti **First Come First Serve (FCFS)** dan **Shortest Job First (SJF)**. Modul ini bertanggung jawab dalam melakukan perhitungan waiting time, turnaround time, serta menampilkan hasil simulasi dalam bentuk tabel.

3. **Modul Page Replacement**
   Modul ini menangani simulasi manajemen memori dengan algoritma **FIFO** dan **Least Recently Used (LRU)**. Modul ini menghitung jumlah page fault dan hit ratio berdasarkan urutan page dan jumlah frame yang diberikan.

4. **Manajemen Data dan Utilitas**
   Data proses dan page dibaca dari file eksternal (CSV/TXT), serta hasil simulasi ditampilkan menggunakan fungsi utilitas untuk memastikan format output rapi dan mudah dipahami.

5. **Docker Containerization**
   Aplikasi dijalankan di dalam container Docker untuk memastikan konsistensi lingkungan eksekusi dan meningkatkan portabilitas aplikasi di berbagai sistem operasi.
---

## 3. Pembagian Peran dan Kontribusi

Pengerjaan proyek ini dilakukan secara kolaboratif dengan pembagian peran sebagai berikut:

| No | Nama Anggota              | Peran                          | Kontribusi Utama                                                                                                   |
|----|---------------------------|--------------------------------|--------------------------------------------------------------------------------------------------------------------|
| 1  | **Safyra Azahro**          | Project Lead / Integrator      | Mengkoordinasikan tim, melakukan merge pull request, serta memastikan integrasi modul dan Docker berjalan |
| 2  | **Aulia Zahra Fatmawati**  | Developer Modul A (Scheduling)| Mengimplementasikan modul CPU Scheduling (FCFS & SJF), menghitung waiting time dan turnaround time, serta menampilkan tabel hasil |
| 3  | **Ayu Ida Nuraini**        | Developer Modul B (Memory)    | Mengimplementasikan modul Page Replacement (FIFO & LRU), menghitung page fault dan hit ratio, serta menyiapkan input dataset |
| 4  | **Aisyah Nurur Rohmah**    | Dokumentasi & Visualisasi     | Menyiapkan screenshot hasil running aplikasi                                                                        |
| 5  | **Faizatun Khasanah**      | Dokumentasi Laporan           | Menyusun dan merapikan `laporan.md` dan `README.md`, serta penulisan analisis singkat                                |

---

## 4. Hasil Pengujian dan Analisis

### 4.1 Modul A – CPU Scheduling

Berdasarkan pengujian dengan algoritma **SJF (Shortest Job First)**:

* **Total Proses:** 5
* **Avg Waiting Time:** 5.25 ms
* **Avg Turnaround Time:** 11.25 ms

### 4.2 Modul B – Page Replacement

Berdasarkan pengujian dengan algoritma **LRU (Least Recently Used)**:

* **Jumlah Frame:** 3
* **Total Page Faults:** 13
* **Hit Ratio:**  0.31%

---

## 5. Jawaban Quiz

**1. Tantangan terbesar integrasi modul apa, dan bagaimana solusinya?**
Tantangan terbesarnya adalah menyamakan format data input.Scheduling butuh data waktu proses (arrival dan burst), sedangkan Page Replacement butuh urutan angka referensi halaman.

* **Solusi:** Solusinya adalah menggunakan format input terpisah untuk setiap modul, sehingga Scheduling membaca data waktu proses dan Page Replacement membaca deret angka sesuai kebutuhannya.
  
**2. Mengapa Docker membantu proses demo dan penilaian proyek?**
Docker membuat aplikasi dan semua kebutuhannya berjalan **terpisah dan rapi**. Jadi tim penilai tidak perlu repot menginstal apa pun; cukup jalankan perintah `docker run`, dan aplikasinya akan berjalan **sama persis** seperti di komputer pengembang.

**3. Jika dataset diperbesar 10x, modul mana yang paling terdampak performanya? Jelaskan.**
Modul **Page Replacement (terutama LRU)** paling terasa dampaknya karena setiap kali ada halaman baru, sistem harus mengecek dan memperbarui daftar halaman untuk mencari mana yang paling lama tidak dipakai. Semakin panjang urutan halaman, semakin lama prosesnya.

---

## 6. Penutup

Sebagai penutup, integrasi **CPU Scheduling**, **Page Replacement**, dan **Docker Containerization** membuat sistem lebih **terstruktur, efisien, dan mudah dijalankan**. CPU Scheduling mengatur pembagian waktu proses, Page Replacement mengelola penggunaan memori secara optimal, sementara Docker memastikan aplikasi dapat dijalankan dengan lingkungan yang sama di mana pun tanpa kendala instalasi. Dengan integrasi ini, sistem menjadi lebih andal, konsisten, dan siap digunakan baik untuk pengembangan maupun penilaian.

**Credit:**  
_Template laporan praktikum Sistem Operasi (SO-202501) – Universitas Putra Bangsa_
