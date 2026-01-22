
# Laporan Praktikum Minggu 9
Topik: Simulasi Algoritma Penjadwalan CPU
---

## Identitas
- **Nama**  : Faizatun Khasanah 
- **NIM**   : 250320584
- **Kelas** : 1DSRA

---

## Deskripsi Singkat
Pada praktikum minggu ini, mahasiswa akan **mengimplementasikan program simulasi sederhana algoritma penjadwalan CPU**, khususnya **FCFS atau SJF**. 

Berbeda dengan Minggu 5–6 yang berfokus pada perhitungan manual, pada minggu ini mahasiswa mulai **mengotomatisasi perhitungan menggunakan program**, menjalankan dataset uji, serta menyajikan hasil dalam bentuk tabel atau grafik. 

_Praktikum ini menjadi jembatan antara **pemahaman konseptual** dan **implementasi komputasional** algoritma sistem operasi._

---

## Tujuan
1. Membuat program simulasi algoritma penjadwalan FCFS atau SJF.  
2. Menjalankan program dengan dataset uji yang diberikan atau dibuat sendiri.  
3. Menyajikan output simulasi dalam bentuk tabel atau grafik.  
4. Menjelaskan hasil simulasi secara tertulis.  
5. Mengunggah kode dan laporan ke Git repository dengan rapi dan tepat waktu.

---

## Dasar Teori
1. First-Come, First-Served (FCFS) = algoritma ini bekerja dengan prinsip antrean. Proses yang pertama kali meminta jatah waktu CPU akan dilayani terlebih dahulu.
2. Shortest Job First (SJF) = Algoritma ini memprioritaskan proses yang memiliki waktu pengerjaan (burst time) terkecil.
3. Arrival Time (AT) = Waktu Kedatangan adalah waktu di mana sebuah proses masuk ke dalam antrean dan siap untuk dikerjakan oleh CPU.
4. Burst Time (BT) = Waktu Eksekusi adalah total waktu yang dibutuhkan oleh sebuah proses untuk diselesaikan oleh CPU.
5. Turnaround Time (TAT) – Waktu Total di Sistem adalah total waktu yang dihabiskan oleh suatu proses sejak ia datang sampai ia benar-benar selesai dikerjakan.
6. Waiting Time, yaitu jumlah waktu yang dihabiskan proses hanya untuk menunggu di antrean sebelum akhirnya dilayani CPU.



## Langkah Praktikum
1. Langkah-langkah yang dilakukan.  
2. Perintah yang dijalankan.  
3. File dan kode yang dibuat.  
4. Commit message yang digunakan.

---

## Kode / Perintah
Berikut adalah implementasi algoritma FCFS menggunakan bahasa pemrograman Python:

Python

def main():
    # --- DATASET ---
    proses_list = [
        {'id': 'P1', 'arrival': 0, 'burst': 6},
        {'id': 'P2', 'arrival': 1, 'burst': 8},
        {'id': 'P3', 'arrival': 2, 'burst': 7},
        {'id': 'P4', 'arrival': 3, 'burst': 3}
    ]

    # --- LOGIKA FCFS ---
    # Mengurutkan data berdasarkan waktu kedatangan (Arrival Time)
    proses_list.sort(key=lambda x: x['arrival'])

    waktu_sekarang = 0
    total_waiting = 0
    total_turnaround = 0

    print("\n=== SIMULASI CPU SCHEDULING (FCFS) ===")
    print(f"{'Proses':<8} {'Arrival':<8} {'Burst':<8} {'Waiting':<8} {'Turnaround':<10}")
    print("-" * 50)

    for p in proses_list:
        # Menangani kondisi idle jika CPU siap sebelum proses tiba
        if waktu_sekarang < p['arrival']:
            waktu_sekarang = p['arrival']

        start_time = waktu_sekarang
        finish_time = start_time + p['burst']

        # Kalkulasi Metrik
        turnaround = finish_time - p['arrival']
        waiting = turnaround - p['burst']

        total_waiting += waiting
        total_turnaround += turnaround
        
        # Update Timeline Sistem
        waktu_sekarang = finish_time

        print(f"{p['id']:<8} {p['arrival']:<8} {p['burst']:<8} {waiting:<8} {turnaround:<10}")

    # --- OUTPUT RATA-RATA ---
    rata_waiting = total_waiting / len(proses_list)
    rata_turnaround = total_turnaround / len(proses_list)

    print("-" * 50)
    print(f"Rata-rata Waiting Time    : {rata_waiting:.2f} ms")
    print(f"Rata-rata Turnaround Time : {rata_turnaround:.2f} ms")
    print("=" * 50 + "\n")

if __name__ == "__main__":
    main()

---

## Hasil Eksekusi
Sertakan screenshot hasil percobaan atau diagram:
(<screenshots/Screen Shot 2026-01-23 at 00.33.25.png>)
---

## Analisis
- Jelaskan makna hasil percobaan.
  Simulasi membuktikan bahwa algoritma FCFS menghasilkan urutan eksekusi yang kaku sesuai waktu kedatangan. Hasil 
  Average WT (8.75 ms) dan Average TAT (14.75 ms) menunjukkan bahwa meskipun adil secara urutan, efisiensi waktu 
  sangat bergantung pada durasi proses di awal antrean (potensi Convoy Effect)
   
- Hubungkan hasil dengan teori (fungsi kernel, system call, arsitektur OS).
  * Kernel Scheduler: Program ini mensimulasikan peran Short-term Scheduler di dalam Kernel yang mengelola antrean 
  Ready.

  * System Call & Context Switching: Dalam sistem asli, perpindahan dari satu proses ke proses berikutnya dipicu oleh 
  System Call yang memaksa CPU melakukan Context Switching (menyimpan status proses lama dan memuat proses baru).

  * Arsitektur OS: Simulasi berada di User Space, sementara penjadwalan asli berjalan di Kernel Space dengan hak 
  akses penuh ke hardware.

- Apa perbedaan hasil di lingkungan OS berbeda (Linux vs Windows)?
  * Algoritma Default: Linux menggunakan CFS (Completely Fair Scheduler), sedangkan Windows menggunakan Priority- 
  driven Multilevel Feedback Queue. Keduanya jauh lebih kompleks daripada FCFS.

  * Struktur Data: Linux mengelola proses lewat task_struct, sementara Windows menggunakan blok EPROCESS.

  * Performa: Kecepatan Context Switching dan presisi waktu (timer interrupt) pada Linux biasanya lebih konsisten 
  untuk tugas-tugas berbasis kernel dibanding Windows. 

---

## Kesimpulan

* Validasi Algoritma: Praktikum ini berhasil membuktikan bahwa algoritma FCFS bekerja secara linear berdasarkan urutan kedatangan. Hasil simulasi program menunjukkan akurasi yang identik dengan perhitungan manual, yaitu rata-rata Waiting Time 8.75 ms dan Turnaround Time 14.75 ms.

* Otomatisasi & Efisiensi: Penggunaan program simulasi terbukti jauh lebih efektif dibandingkan perhitungan manual, terutama dalam meminimalkan risiko human error dan mempercepat pengolahan data jika jumlah proses bertambah banyak.

* Pemahaman Sistem Operasi: Melalui simulasi ini, hubungan antara kode program dengan konsep internal OS menjadi lebih jelas, khususnya mengenai peran Kernel Scheduler dalam mengatur antrean proses serta bagaimana metrik waktu digunakan untuk mengukur performa sebuah sistem.
  
---

## Quiz
1. Mengapa simulasi diperlukan untuk menguji algoritma scheduling?
   Simulasi berfungsi sebagai lingkungan uji coba yang aman untuk mengukur performa algoritma tanpa mengganggu 
   stabilitas sistem operasi yang nyata. Selain itu, simulasi memudahkan pengembang untuk melakukan benchmarking atau 
   perbandingan efisiensi antar berbagai algoritma secara cepat.

2. Apa perbedaan hasil simulasi dengan perhitungan manual jika dataset besar?
   Pada dataset skala besar, perhitungan 
   manual memiliki risiko kesalahan manusia (human error) yang sangat tinggi dan membutuhkan waktu pengerjaan yang 
   tidak efektif. Sebaliknya, simulasi komputer memberikan akurasi mutlak dan kecepatan pemrosesan yang konstan 
   terlepas dari besarnya data.

3. Algoritma mana yang lebih mudah diimplementasikan? Jelaskan.
   FCFS adalah yang paling mudah diimplementasikan 
   karena hanya memerlukan struktur data antrean sederhana (Queue). Sementara itu, SJF lebih kompleks karena program 
   harus terus memantau dan membandingkan burst time proses yang ada di antrean sebelum mengambil keputusan eksekusi.
   
---

## Refleksi Diri
1. Bagian yang paling menantang?
   Bagian yang paling menantang adalah menangani logika idle time pada CPU, yaitu ketika CPU harus menunggu saat 
   tidak ada satupun proses yang tersedia di antrean (waktu sistem lebih kecil dari waktu kedatangan proses 
   berikutnya).

2. Cara mengatasinya? Menggunakan pengkondisian if untuk melakukan pengecekan waktu sistem secara dinamis. Jika waktu 
   sistem tertinggal, maka waktu sistem tersebut langsung disesuaikan (di-update) mengikuti waktu kedatangan proses 
   terdekat.
   
---

**Credit:**  
_Template laporan praktikum Sistem Operasi (SO-202501) – Universitas Putra Bangsa_
