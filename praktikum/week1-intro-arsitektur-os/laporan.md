
# Laporan Praktikum Minggu [X]
Topik: Arsitektur Sistem Operasi dan Kernel

---

## Identitas
- **Nama**  : FAIZATUN KHASANAH
- **NIM**   : 250320584 
- **Kelas** : 1DSRA

---

## Tujuan  
> Mahasiswa mampu menjelaskan fungsi utama sistem operasi dan peran kernel serta system call.

---

## Dasar Teori
Tuliskan ringkasan teori (3–5 poin) yang mendasari percobaan.
1. Arsitektur Sistem Operasi
Arsitektur sisperasi menggambarkan bagaimana komponen sistem diatur dan saling berinteraksi dalam mengelola perangkat keras dan perangkat lunak. Struktur umumnya terdiri dari lapisan pengguna (user space), lapisan kernel (kernel space), antarmuka sistem (system call interface), serta perangkat keras (hardware).

2. Peran Kernel dalam Sistem Operasi
Kernel merupakan inti dari sistem operasi yang bertugas mengelola sumber daya komputer seperti CPU, memori, dan perangkat I/O. Kernel juga bertanggung jawab memastikan sistem tetap stabil dan aman saat menjalankan berbagai proses.

3. System Call (Panggilan Sistem)
System call berfungsi sebagai penghubung antara aplikasi di ruang pengguna dengan kernel. Melalui mekanisme ini, aplikasi dapat meminta layanan dari sistem operasi tanpa harus berinteraksi langsung dengan perangkat keras.

4. Jenis Arsitektur Kernel
Berdasarkan cara kerja dan pengelolaan komponennya, kernel dibedakan menjadi tiga jenis utama, yaitu monolithic kernel (semua layanan berjalan di ruang kernel), microkernel (hanya fungsi dasar di ruang kernel), dan hybrid kernel (kombinasi keduanya untuk menyeimbangkan kinerja dan stabilitas).

5. Keamanan dan Proteksi Sistem
Sistem operasi menerapkan pemisahan antara ruang pengguna dan ruang kernel untuk mencegah aplikasi biasa mengganggu fungsi inti sistem. Mekanisme ini menjaga keamanan, keandalan, serta mencegah kerusakan pada sistem operasi secara keseluruhan.



---

## Langkah Praktikum
1. Langkah-langkah yang dilakukan.  
2. Perintah yang dijalankan.  
3. File dan kode yang dibuat.  
4. Commit message yang digunakan.

---

## Kode / Perintah
Tuliskan potongan kode atau perintah utama:
```bash
uname -a
lsmod | head
dmesg | head
```

---

## Hasil Eksekusi
Sertakan screenshot hasil percobaan atau diagram:
![Screenshot hasil](<screenshots/Screenshot (38).png>)

---

## Analisis
- Jelaskan makna hasil percobaan.
1. uname -a
Menampilkan informasi lengkap tentang sistem operasi dan kernel yang digunakan, seperti versi, arsitektur, dan nama host. Ini menunjukkan identitas serta konfigurasi sistem yang sedang berjalan.

2. whoami
Menampilkan nama pengguna yang sedang aktif di sistem. Hasil ini menunjukkan konsep manajemen pengguna dan hak akses dalam sistem operasi Linux.

3. lsmod | head
Menampilkan daftar modul kernel yang sedang dimuat ke sistem (10 baris pertama). Ini menunjukkan bahwa kernel Linux bersifat modular dan dapat menambah atau melepas fungsi tertentu sesuai kebutuhan.

4. dmesg | head
Menampilkan log awal kernel saat proses booting atau deteksi perangkat keras. Hasil ini memperlihatkan bagaimana kernel berinteraksi dan mengenali komponen perangkat keras di sistem.
  
- Hubungkan hasil dengan teori (fungsi kernel, system call, arsitektur OS).
1. uname -a
Menampilkan informasi lengkap tentang sistem operasi dan kernel yang digunakan, seperti versi, arsitektur, dan nama host. Ini menunjukkan identitas serta konfigurasi sistem yang sedang berjalan.

2. whoami
Menampilkan nama pengguna yang sedang aktif di sistem. Hasil ini menunjukkan konsep manajemen pengguna dan hak akses dalam sistem operasi Linux.

3. lsmod | head
Menampilkan daftar modul kernel yang sedang dimuat ke sistem (10 baris pertama). Ini menunjukkan bahwa kernel Linux bersifat modular dan dapat menambah atau melepas fungsi tertentu sesuai kebutuhan.

4. dmesg | head
Menampilkan log awal kernel saat proses booting atau deteksi perangkat keras. Hasil ini memperlihatkan bagaimana kernel berinteraksi dan mengenali komponen perangkat keras di sistem.
  
- Apa perbedaan hasil di lingkungan OS berbeda (Linux vs Windows)?  
1. Akses Sistem
Linux bersifat terbuka (open source), sehingga pengguna dapat langsung melihat informasi kernel, modul, dan log sistem melalui terminal. Sebaliknya, Windows membatasi akses langsung ke kernel, dan informasi sistem umumnya diakses lewat antarmuka grafis.

2. Arsitektur Kernel
Linux menggunakan monolithic modular kernel yang fleksibel dan memungkinkan penambahan modul sesuai kebutuhan, sedangkan Windows menggunakan hybrid kernel yang lebih tertutup namun stabil dan aman.

3. Manajemen Pengguna
Linux membedakan pengguna biasa dan root dengan kontrol penuh melalui perintah terminal, sedangkan Windows menggunakan sistem akun Administrator dengan pengaturan hak akses melalui antarmuka grafis

---

## Kesimpulan
Tuliskan 2–3 poin kesimpulan dari praktikum ini.
1. Kernel adalah bagian utama sistem operasi yang mengatur kerja perangkat keras dan perangkat lunak agar sistem berjalan dengan baik.

2. Percobaan menunjukkan bahwa Linux memiliki kernel yang bersifat terbuka dan modular, sehingga pengguna dapat melihat serta mengelola komponen sistem dengan mudah.

3. Dibandingkan dengan Windows, Linux memberi akses lebih luas ke fungsi sistem, sedangkan Windows lebih tertutup untuk menjaga stabilitas dan keamanan.

---

## Quiz
1.  Sebutkan tiga fungsi utama sistem operasi
Tiga fungsi utama dari sistem operasi adalah:
- Manajemen Proses
Mengatur jalannya program di komputer, termasuk membuat, menjalankan, dan menghentikan proses agar semua berjalan secara bergantian dan efisien.

- Manajemen Memori
Mengatur penggunaan memori (RAM) oleh berbagai program agar tidak saling mengganggu dan memastikan memori digunakan secara optimal.

- Manajemen Perangkat I/O
Mengendalikan perangkat input dan output seperti keyboard, printer, dan penyimpanan, serta mengatur komunikasi antara perangkat keras dan perangkat lunak.
 
2. Jelaskan perbedaan antara kernel mode dan user mode.
   
- Kernel Mode

Pengertian:
Kernel mode adalah mode kerja di mana sistem operasi memiliki kendali penuh terhadap komputer, termasuk akses langsung ke memori dan perangkat keras. Semua proses penting sistem dijalankan di mode ini.

Fungsi:

Mengatur dan membagi penggunaan memori antar proses.

Mengelola perangkat input/output seperti keyboard, disk, dan printer.

Menangani penjadwalan proses agar semua berjalan bergantian dengan adil.

Menangani interupsi atau kesalahan dari perangkat keras.

Mengatur sistem file dan penyimpanan data.

Contoh:
Kernel dari sistem operasi (seperti Linux Kernel atau Windows Kernel), serta driver perangkat keras seperti driver printer atau kartu grafis.

- User Mode

Pengertian:
User mode adalah mode kerja di mana program pengguna dijalankan dengan akses terbatas. Program tidak bisa langsung mengakses perangkat keras dan harus melalui kernel jika membutuhkan layanan sistem.

Fungsi:

Menjalankan aplikasi pengguna seperti browser, editor teks, dan pemutar musik.

Melakukan perhitungan, pengolahan data, atau aktivitas pengguna lainnya.

Menyediakan antarmuka grafis (GUI) agar pengguna dapat berinteraksi dengan sistem operasi.

Contoh:
Aplikasi seperti Google Chrome, Microsoft Word, VLC Media Player, atau Terminal yang dijalankan oleh pengguna. 


3. Sebutkan contoh sistem operasi dengan arsitektur monolitik dan mikrokernel.

- Monolithic Kernel

Definisi:
Dalam sistem operasi yang memiliki jenis kernel monolitik, semua layanan utama seperti manajemen memori, penjadwalan proses, sistem file, serta kontrol perangkat keras dijalankan secara langsung dalam satu kesatuan kernel. Ini berarti bahwa semua fungsi kritis sistem berada dalam ruang yang sama (ruang kernel).

Metode ini mempercepat proses komunikasi antar komponen karena tidak ada banyak pemisahan, sehingga kinerjanya cenderung lebih efisien. Namun, karena semua bagian tergabung, pengelolaan sistem ini bisa lebih rumit dan rentan terhadap kesalahan jika salah satu komponen mengalami masalah.

Contoh Sistem Operasi dengan Kernel Monolitik:

Linux

UNIX

BSD (Distribusi Perangkat Lunak Berkeley)

Xv6

- Mikrokernel

Definisi:
Berbeda dengan kernel monolitik, mikrokernel hanya menjalankan fungsi-fungsi inti dari sistem operasi di dalam kernel — seperti manajemen proses, memori, dan komunikasi antar proses. Komponen tambahan lainnya (seperti driver, sistem file, dan layanan lain) beroperasi di ruang pengguna (ruang pengguna).

Dengan pendekatan ini, sistem menjadi lebih stabil dan lebih fleksibel, karena jika salah satu layanan mengalami masalah, hal itu tidak akan langsung berdampak pada kernel. Namun, komunikasi antara komponen bisa sedikit lebih lambat dibandingkan dengan arsitektur monolitik.

Contoh Sistem Operasi dengan Mikrokernel:

Minix

QNX

L4

GNU HURD

Mach
---

## Refleksi Diri
Tuliskan secara singkat:
- Apa bagian yang paling menantang minggu ini?
~Aspek yang paling sulit:
Kesulitan utama minggu ini adalah beradaptasi dengan sintaks dan fungsi dari perintah di terminal Linux.

- Bagaimana cara Anda mengatasinya
~Langkah yang diambil:
Saya menyiasatinya dengan banyak berlatih secara mandiri, mencoba beberapa perintah secara langsung, serta mencari penjelasan lebih lanjut dari teman dan sumber di internet.  

---

**Credit:**  
_Template laporan praktikum Sistem Operasi (SO-202501) – Universitas Putra Bangsa_
