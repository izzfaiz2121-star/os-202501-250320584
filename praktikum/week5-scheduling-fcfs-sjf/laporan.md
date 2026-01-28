
# Laporan Praktikum Minggu 5
Topik: Penjadwalan CPU FCFS dan SJF
---

## Identitas
- **Nama**  : FAIZATUN  KHASANAH
- **NIM**   : 250320584
- **Kelas** : 1DSRA
---

## Tujuan
1. Mampu menghitung waiting time dan turnaround time untuk algoritma FCFS dan SJF.
2. Mampu menyajikan hasil perhitungan dalam tabel yang rapi dan mudah dibaca.
3. Mampu membandingkan performa FCFS dan SJF berdasarkan hasil analisis.
4. Mampu menjelaskan kelebihan dan kekurangan masing-masing algoritma.
5. Mampu menyimpulkan kapan algoritma FCFS atau SJF lebih sesuai digunakan.

---

## Dasar Teori
Dalam sistem operasi multitasking, Penjadwalan CPU (CPU Scheduling) adalah proses fundamental di mana sistem operasi (OS) memutuskan proses mana di antrian ready yang akan dialokasikan ke CPU. Tujuannya adalah untuk memaksimalkan penggunaan CPU dan throughput, serta meminimalkan waktu tunggu (waiting time) dan waktu penyelesaian (turnaround time) bagi pengguna.

- First Come First Served (FCFS): Ini adalah algoritma penjadwalan paling sederhana. Proses yang meminta CPU terlebih dahulu akan dilayani terlebih dahulu (sesuai urutan Arrival Time). Implementasinya mudah menggunakan antrian FIFO (First-In, First-Out), namun dapat menyebabkan convoy effect di mana proses singkat harus menunggu proses panjang yang datang lebih dulu.

- Shortest Job First (SJF): Algoritma ini mengalokasikan CPU ke proses dengan estimasi waktu eksekusi (Burst Time) terpendek. Jika ada dua proses dengan burst time yang sama, FCFS digunakan. SJF terbukti optimal dalam memberikan rata-rata waktu tunggu minimum, nam

---

## Langkah Praktikum
1. Mempersiapkan data proses (Contoh: P1, P2, P3, P4) dengan Burst Time dan Arrival Time yang ditentukan.
2. Mempersiapkan spreadsheet (Google Sheets/Excel) atau alat hitung manual.
3. Melakukan Eksperimen 1 untuk menghitung Waiting Time (WT) dan Turnaround Time (TAT) menggunakan algoritma FCFS.
4. Membuat Gantt Chart sederhana untuk visualisasi FCFS.
5. Melakukan Eksperimen 2 untuk menghitung WT dan TAT menggunakan algoritma SJF (non-preemptive).
6. Membuat tabel perbandingan untuk Average WT dan Average TAT dari kedua algoritma.
7. Menganalisis hasil perbandingan untuk menentukan kelebihan dan kekurangan masing-masing.
8. Mendokumentasikan seluruh hasil simulasi, perhitungan, dan analisis dalam file laporan.md.
9. Melakukan commit dan push hasil praktikum ke repositori GitHub.
    
---

## Kode / Perintah
Waiting Time (WT) = Start Time - Arrival Time
Turnaround Time (TAT) = Finish Time - Arrival Time atau  Waiting Time + Burst Time

Average Waiting Time (WT) = Total Waiting Time / Jumlah Proses
Average Turnaround Time (TAT) = Total Turnaround Time / Jumlah Proses

---

## Hasil Eksekusi
Sertakan screenshot hasil percobaan atau diagram:
![Screenshot hasil](screenshots/example.png)

## Eksperimen 1 – FCFS (First Come First Served)
> Proses dieksekusi berdasarkan urutan kedatangan (Arrival Time). 
Urutan Eksekusi: P1 -> P2 -> P3 -> P4

> Gantt Chart FCFS:

+----------+----------------+--------------+------+
|    P1    |       P2       |      P3      |  P4  |
+----------+----------------+--------------+------+
0          6               14             21     24

> Tabel Perhitungan FCFS:

Proses,Arrival Time,Burst Time,Start Time,Finish Time,Waiting Time,Turnaround Time
P1,0,6,0,6,0,6
P2,1,8,6,14,5,13
P3,2,7,14,21,12,19
P4,3,3,21,24,18,21
Total,,,,,35,59
Average,,,,,"8,75","14,75"

## Eksperimen 2 – SJF (Shortest Job First)
> Proses dieksekusi berdasarkan Burst Time terpendek dari antrian proses yang telah tiba.

> Urutan Eksekusi: P1 -> P4 -> P3 -> P2

> Gantt Chart SJF:
+----------+------+--------------+----------------+
|    P1    |  P4  |      P3      |       P2       |
+----------+------+--------------+----------------+
0          6      9             16               24




---

## Analisis
Berdasarkan metrik yang diperoleh, SJF lebih unggul dalam menekan rata-rata waktu tunggu dibandingkan FCFS. Pada FCFS, terjadi fenomena convoy effect di mana P4 (proses singkat) harus mengantri sangat lama karena tertahan oleh proses besar di depannya. SJF mengatasi hal ini dengan "melompati" antrian untuk mengerjakan P4 lebih awal, sehingga efisiensi sistem meningkat secara rata-rata.
---

## Kesimpulan
1. Penjadwalan SJF memberikan performa lebih baik dalam meminimalkan rata-rata waktu tunggu proses.

2. FCFS sangat mudah diimplementasikan namun kurang efisien jika terdapat variasi durasi proses yang besar.

3. Pemilihan algoritma harus disesuaikan dengan kebutuhan sistem; SJF untuk kecepatan rata-rata, FCFS untuk keadilan urutan.

---

## Quiz
1. Apa perbedaan utama antara FCFS dan SJF?
   FCFS berorientasi pada waktu tiba (kronologi), sedangkan SJF berorientasi pada durasi pengerjaan (efisiensi).
2. Mengapa SJF dapat menghasilkan rata-rata waktu tunggu minimum?
   Dengan mendahulukan beban kerja terkecil, jumlah proses yang mengantri berkurang lebih cepat, yang secara matematis 
   menurunkan total waktu tunggu.
3. Apa kelemahan SJF jika diterapkan pada sistem interaktif?
   Munculnya risiko starvation, di mana proses berdurasi lama tertunda terus-menerus karena tertutup oleh proses baru 
   yang lebih singkat.

---

## Refleksi Diri
Tuliskan secara singkat:
- Apa bagian yang paling menantang minggu ini?
  Bagian paling menantang adalah melakukan analisis perubahan urutan antrian pada SJF setelah proses pertama selesai.
   
- Bagaimana cara Anda mengatasinya?
  aya membedah langkah demi langkah menggunakan spreadsheet untuk memantau status antrian pada setiap unit waktu. 

---

**Credit:**  
_Template laporan praktikum Sistem Operasi (SO-202501) – Universitas Putra Bangsa_
