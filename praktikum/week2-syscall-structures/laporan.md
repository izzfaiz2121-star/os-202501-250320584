
# Laporan Praktikum Minggu [X]
Struktur System Call dan Fungsi Kernel

---

## Identitas
- **Nama**  : Faizatun Khasanah 
- **NIM**   : 250320584
- **Kelas** : 1DSRA

---

A. Deskripsi Singkat
Pada praktikum minggu ini, mahasiswa akan mempelajari mekanisme system call dan struktur sistem operasi.
System call adalah antarmuka antara program aplikasi dan kernel yang memungkinkan aplikasi berinteraksi dengan perangkat keras secara aman melalui layanan OS.

Mahasiswa akan melakukan eksplorasi terhadap:

Jenis-jenis system call yang umum digunakan (file, process, device, communication).
Alur eksekusi system call dari mode user menuju mode kernel.
Cara melihat daftar system call yang aktif di sistem Linux.

---


## Tujuan
1. Jelaskan konsep dan fungsi panggilan sistem dalam sistem operasi.
   >  Sistem call adalah fitur yang disediakan oleh sistem operasi untuk memungkinkan aplikasi mengakses layanan 
      kernel dan data sistem secara transparan.
   >  Fungsi utamanya adalah akses perangkat keras, abstraksi perangkat keras, keamanan, dan pemrosesan.
2. Mengidentifikasi jenis dan fungsi sistem call
   Jenis-Jenis Panggilan Sistem memiliki fungsi-fungsi berikut:
   > Fungsi kontrol proses adalah untuk mengelola aktivitas dan alur kerja sehari-hari.
   > Fungsi manajemen file adalah untuk mengoperasikan sistem file dan direktori.
   > Fungsi manajemen perangkat adalah untuk mengontrol perangkat input/output.
   > Tujuan pemeliharaan informasi adalah untuk memperoleh dan memodifikasi informasi sistem.
   > Fungsi komunikasi adalah komunikasi antar proses.
   > Fungsi proteksi adalah untuk mengontrol akses dan keamanan sistem.
3. Mengamati alur perpindahan mode user ke kernel saat system call terjadi.
    Alur perpindahan mode pengguna ke kernel bertujuan untuk memastikan bahwa, bahkan dengan banyak aplikasi yang 
    berjalan,
    sistem operasi memiliki kendali atas semua sumber daya komputer dan menjaga stabilitas, keamanan, dan kinerja 
    sistem secara komprehensif.

5. Menggunakan Linux untuk menganalisis dan merekam panggilan sistem.
   
---

## Dasar Teori
*_System call_ adalah fungsi yang disediakan oleh sistem operasi untuk memungkinkan aplikasi mengakses layanan internal kernel.
*_System Call_ digunakan sebagai transisi antara mode kernel dan mode pengguna.

* Aplikasi tidak dapat mengakses perangkat keras atau data sistem secara langsung; sebaliknya, mereka harus menggunakan _System Call_.
* Tanpa _System Call_, aplikasi tidak dapat berinteraksi dengan perangkat keras atau komponen sistem (CPU, Memori, Penyimpanan, Perangkat I/O). * _Kernel_ memastikan bahwa setiap proses berjalan dengan lancar dan efisien.

* _System Call_ memungkinkan portabilitas kode antar proses.

---

## Langkah Praktikum
1. Langkah-langkah yang dilakukan.  
2. Perintah yang dijalankan.  
3. File dan kode yang dibuat.  
4. Commit message yang digunakan.

---

## Kode / Perintah
1. **Setup Environment**
   - Gunakan Linux (Ubuntu/WSL).
   - Pastikan perintah `strace` dan `man` sudah terinstal.
   - Konfigurasikan Git (jika belum dilakukan di minggu sebelumnya).

2. **Eksperimen 1 – Analisis System Call**
   Jalankan perintah berikut:
   ```bash
   strace ls
   ```
   > Catat 5–10 system call pertama yang muncul dan jelaskan fungsinya.  
   Simpan hasil analisis ke `results/syscall_ls.txt`.

3. **Eksperimen 2 – Menelusuri System Call File I/O**
   Jalankan:
   ```bash
   strace -e trace=open,read,write,close cat /etc/passwd
   ```
   > Analisis bagaimana file dibuka, dibaca, dan ditutup oleh kernel.

4. **Eksperimen 3 – Mode User vs Kernel**
   Jalankan:
   ```bash
   dmesg | tail -n 10
   ```
   > Amati log kernel yang muncul. Apa bedanya output ini dengan output dari program biasa?

5. **Diagram Alur System Call**
   - Buat diagram yang menggambarkan alur eksekusi system call dari program user hingga kernel dan kembali lagi ke user mode.
   - Gunakan draw.io / mermaid.
   - Simpan di:
     ```
     praktikum/week2-syscall-structure/screenshots/syscall-diagram.png
     ```

6. **Commit & Push**
   ```bash
   git add .
   git commit -m "Minggu 2 - Struktur System Call dan Kernel Interaction"
   git push origin main
   ```  
---

## Hasil Eksekusi
Sertakan screenshot hasil percobaan atau diagram:
![Screenshot hasil](screenshots/example.png)

---

## Analisis
- Jelaskan makna hasil percobaan.  
- Hubungkan hasil dengan teori (fungsi kernel, system call, arsitektur OS).  
- Apa perbedaan hasil di lingkungan OS berbeda (Linux vs Windows)?  

---

## Kesimpulan
Tuliskan 2–3 poin kesimpulan dari praktikum ini.

---

## Quiz
1. [Pertanyaan 1]  
   **Jawaban:**  
2. [Pertanyaan 2]  
   **Jawaban:**  
3. [Pertanyaan 3]  
   **Jawaban:**  

---

## Refleksi Diri
Tuliskan secara singkat:
- Apa bagian yang paling menantang minggu ini?  
- Bagaimana cara Anda mengatasinya?  

---

**Credit:**  
_Template laporan praktikum Sistem Operasi (SO-202501) – Universitas Putra Bangsa_
