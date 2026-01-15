
# Laporan Praktikum Minggu 6
Topik: Penjadwalan CPU – Round Robin (RR) dan Priority Scheduling

---

## Identitas
- **Nama**  : Faizatun Khasanah  
- **NIM**   : 250320584  
- **Kelas** : 1DSRA

---

## A. Deskripsi Singkat
Tuliskan tujuan praktikum minggu ini.   
> Pada praktikum minggu ini, mahasiswa akan mempelajari **dua algoritma lanjutan penjadwalan CPU**, yaitu:
- **Round Robin (RR)**  
- **Priority Scheduling**

Kedua algoritma ini banyak digunakan pada sistem modern karena mempertimbangkan **keadilan waktu eksekusi (time quantum)** dan **tingkat prioritas proses**.  
Mahasiswa akan melakukan simulasi perhitungan manual untuk menghitung *waiting time* dan *turnaround time*, serta menganalisis efek perbedaan *time quantum* dan prioritas terhadap performa CPU scheduling.

---
## B. Tujuan
Setelah menyelesaikan tugas ini, mahasiswa mampu:
1. Menghitung *waiting time* dan *turnaround time* pada algoritma RR dan Priority.  
2. Menyusun tabel hasil perhitungan dengan benar dan sistematis.  
3. Membandingkan performa algoritma RR dan Priority.  
4. Menjelaskan pengaruh *time quantum* dan prioritas terhadap keadilan eksekusi proses.  
5. Menarik kesimpulan mengenai efisiensi dan keadilan kedua algoritma.  

---

## C. Dasar Teori
1. _Round Robin (RR)_ adalah algoritma penjadwalan tindakan yang membagi waktu CPU ke setiap proses secara bergiliran menggunakan satuan waktu yang tetap.
2. _Time Quantum (q)_ adalah Durasi maksimum proses menggunakan CPU sebelum di ambil alih.
3. _Turnaround Time (TT)_ adalah Waktu kedatangan hingga penyelesaian proses.
4. _Waiting Time (WT)_ adalah Total waktu proses menunggu di antrian siap.
5. _Priority Scheduling_ adalah algoritma yang mengalokasikan CPU ke proses dengan prioritas tertinggi.
   
---

## Langkah Praktikum
1. Langkah-langkah yang dilakukan.  
2. Perintah yang dijalankan.  
3. File dan kode yang dibuat.  
4. Commit message yang digunakan.

---

## D. Kode / Perintah
1. **Siapkan Data Proses**
   Gunakan contoh data berikut (boleh dimodifikasi sesuai kebutuhan):
   | Proses | Burst Time | Arrival Time | Priority |
   |:--:|:--:|:--:|:--:|
   | P1 | 5 | 0 | 2 |
   | P2 | 3 | 1 | 1 |
   | P3 | 8 | 2 | 4 |
   | P4 | 6 | 3 | 3 |

2. **Eksperimen 1 – Round Robin (RR)**
   - Gunakan *time quantum (q)* = 3.  
   - Hitung *waiting time* dan *turnaround time* untuk tiap proses.  
   - Simulasikan eksekusi menggunakan Gantt Chart (manual atau spreadsheet).  
     ```
     | P1 | P2 | P3 | P4 | P1 | P3 | ...
     0    3    6    9   12   15   18  ...
     ```
   - Catat sisa *burst time* tiap putaran.

3. **Eksperimen 2 – Priority Scheduling (Non-Preemptive)**
   - Urutkan proses berdasarkan nilai prioritas (angka kecil = prioritas tinggi).  
   - Lakukan perhitungan manual untuk:
     ```
     WT[i] = waktu mulai eksekusi - Arrival[i]
     TAT[i] = WT[i] + Burst[i]
     ```
   - Buat tabel perbandingan hasil RR dan Priority.

4. **Eksperimen 3 – Analisis Variasi Time Quantum (Opsional)**
   - Ubah *quantum* menjadi 2 dan 5.  
   - Amati perubahan nilai rata-rata *waiting time* dan *turnaround time*.  
   - Buat tabel perbandingan efek *quantum*.

5. **Eksperimen 4 – Dokumentasi**
   - Simpan semua hasil tabel dan screenshot ke:
     ```
     praktikum/week6-scheduling-rr-priority/screenshots/
     ```
   - Buat tabel perbandingan seperti berikut:

     | Algoritma | Avg Waiting Time | Avg Turnaround Time | Kelebihan | Kekurangan |
     |------------|------------------|----------------------|------------|-------------|
     | RR | ... | ... | Adil terhadap semua proses | Tidak efisien jika quantum tidak tepat |
     | Priority | ... | ... | Efisien untuk proses penting | Potensi *starvation* pada prioritas rendah |

6. **Commit & Push**
   ```bash
   git add .
   git commit -m "Minggu 6 - CPU Scheduling RR & Priority"
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
Tuliskan jawaban di bagian Quiz pada laporan:

1. Apa perbedaan utama antara Round Robin dan Priority Scheduling?
   * Perbedaan utama antara kedua metode ini terletak pada pendekatan penjadwalan yang digunakan:

   - Round Robin (RR): Berbasis waktu. Setiap proses mendapatkan slot waktu yang sama secara bergiliran tanpa 
     mempertimbangkan kepentingan masing-masing proses.
 
   - Priority Scheduling: Berfokus pada tingkat kepentingan. Proses yang memiliki prioritas tertinggi akan diproses 
     terlebih dahulu, tanpa mempertimbangkan urutan kedatangan atau durasi eksekusinya.

2. Apa pengaruh besar/kecilnya time quantum terhadap performa sistem?
   * Ukuran time quantum sangat memengaruhi efektivitas sistem:

     - Terlalu Besar: RR akan berfungsi seperti First-Come First-Served (FCFS). Waktu respons menjadi buruk karena 
       proses harus menunggu lama untuk mendapatkan giliran pelaksanaan.

     - Terlalu Kecil: Akibat terlalu banyaknya context switch (perpindahan antar proses). Hal ini menyebabkan overhead 
       sistem meningkat, sehingga sebagian besar daya prosesor digunakan hanya untuk berpindah antar proses, bukan 
       untuk menyelesaikan pekerjaan.

3. Mengapa algoritma Priority dapat menyebabkan starvation?
  * Starvation (keadaan di mana proses tidak pernah mendapat eksekusi) terjadi akibat proses dengan prioritas lebih 
    rendah selalu terabaikan oleh proses baru yang memiliki prioritas lebih tinggi. Jika aliran proses prioritas 
    tinggi terus menerus masuk, proses dengan prioritas rendah akan terjebak selamanya dalam antrean (ready queue).

    Catatan: Masalah ini umumnya diatasi dengan teknik Aging, yang bertujuan untuk meningkatkan prioritas proses 
    secara bertahap berdasarkan lama waktu tunggunya.
    
---

## Refleksi Diri
Tuliskan secara ringkas:
- Apa bagian yang paling menantang minggu ini?
  bagian paling sulit adalah menghitung waktu tunggu dan waktu penyelesaian pada algoritma Round Robin, khususnya 
  saat time quantum berukuran kecil.
- Apa pendekatan Anda untuk menyelesaikannya?
- Mengorganisir tabel dan Gantt Chart dengan cara yang sistematis agar urutan proses dapat dilihat dengan jelas.

**Credit:**  
_Template laporan praktikum Sistem Operasi (SO-202501) – Universitas Putra Bangsa_
