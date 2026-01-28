# Laporan Praktikum Minggu 10
Topik: Manajemen Memori – Page Replacement (FIFO & LRU)

---

## Identitas
- **Nama**  : Faizatun Khasanah  
- **NIM**   : 250320584
- **Kelas** : 1DSRA

---

## Deskripsi Singkat
Praktikum minggu ke-10 berfokus pada simulasi Manajemen Memori Virtual, khususnya pada strategi Page Replacement. Mahasiswa diajak untuk memahami bagaimana Sistem Operasi mengelola keterbatasan memori fisik (RAM) dengan cara menukar halaman (page) yang berada di memori utama. Fokus utama adalah mengimplementasikan dan membandingkan efisiensi antara algoritma FIFO dan LRU melalui perhitungan page fault.

---

## Dasar Teori
1. FIFO (First-In, First-Out): Algoritma penggantian halaman yang paling sederhana. Halaman yang berada di memori paling lama (yang pertama kali masuk) akan menjadi halaman pertama yang diganti saat terjadi page fault.
2. LRU (Least Recently Used): Algoritma yang lebih adaptif dengan memanfaatkan prinsip lokalitas temporal. Halaman yang akan diganti adalah halaman yang paling lama tidak diakses/digunakan oleh CPU.
3. Page Fault: Kondisi yang terjadi ketika program mencoba mengakses halaman yang saat ini tidak dimuat di memori utama (RAM).
4. Page Hit: Kondisi ketika halaman yang dibutuhkan program sudah tersedia di memori utama.
   
---

## Kode / Perintah

```python
# Dataset sesuai instruksi praktikum
pages = [7, 0, 1, 2, 0, 3, 0, 4, 2, 3, 0, 3, 2]
jumlah_frame = 3

def cetak_langkah(step, page, status, frames):
    # Mengonversi list frame menjadi string agar rapi saat dicetak
    frame_display = str(frames)
    print(f"Langkah {step:02d} | Page: {page} | Status: {status:4s} | Frame: {frame_display}")

print("=== SIMULASI PAGE REPLACEMENT (FIFO) ===")
frames_fifo = [] 
fifo_faults = 0
pointer = 0

for i, page in enumerate(pages):
    status = ""
    if page in frames_fifo:
        status = "HIT"
    else:
        status = "MISS"
        fifo_faults += 1
        if len(frames_fifo) < jumlah_frame:
            frames_fifo.append(page)
        else:
            frames_fifo[pointer] = page
            pointer = (pointer + 1) % jumlah_frame
            
    cetak_langkah(i+1, page, status, frames_fifo)

print(f"Total Page Fault (FIFO): {fifo_faults}\n")



print("=== SIMULASI PAGE REPLACEMENT (LRU) ===")
frames_lru = []
lru_faults = 0

for i, page in enumerate(pages):
    status = ""
    if page in frames_lru:
        status = "HIT"
        # Logika LRU: Pindahkan yang baru dipakai ke posisi paling kanan
        frames_lru.remove(page)
        frames_lru.append(page)
    else:
        status = "MISS"
        lru_faults += 1
        if len(frames_lru) < jumlah_frame:
            frames_lru.append(page)
        else:
            # Hapus yang paling kiri (paling jarang digunakan baru-baru ini)
            frames_lru.pop(0)
            frames_lru.append(page)
            
    cetak_langkah(i+1, page, status, frames_lru)

print(f"Total Page Fault (LRU): {lru_faults}")
```
---

Perintah eksekusi:
```text
python code/page_replacement.py
```
---

## Hasil Eksekusi
Sertakan screenshot hasil percobaan atau diagram:
![Hasil Simulasi Page Replacement](./screenshots/hasil_simulasi.png)

---

## Analisis
1. Tabel Perbandingan Algoritma

| Algoritma | Jumlah Page Fault | Keterangan |
| --- | --- | --- |
| **FIFO** | **10** | Membuang halaman berdasarkan waktu masuk tanpa melihat frekuensi akses. |
| **LRU** | **9** | Mempertahankan halaman yang baru saja digunakan untuk meminimalkan fault. |

2. * **Mengapa Berbeda?** FIFO hanya mempertimbangkan waktu masuk, sehingga halaman yang sering dipakai tetap bisa terhapus jika sudah lama berada di memori. Sebaliknya, LRU memantau riwayat akses dan mempertahankan halaman yang baru saja digunakan.
     
3. * **Mana yang Lebih Efisien?** **LRU lebih efisien** karena menghasilkan *page fault* lebih sedikit (8 vs 10). LRU mengikuti prinsip *Locality of Reference*, yaitu kecenderungan program mengakses kembali data yang baru saja digunakan.

---

## Kesimpulan

1. **Akurasi Simulasi**: Berdasarkan dataset uji, **LRU terbukti lebih optimal** dengan total 8 *page fault* dibandingkan FIFO yang mencapai 10 *page fault*.
2. **Karakteristik**: FIFO unggul dalam kemudahan implementasi (sederhana), namun LRU unggul dalam manajemen memori yang cerdas karena mempertimbangkan perilaku nyata penggunaan data.
3. **Manajemen Memori**: Pemilihan algoritma yang tepat sangat krusial; semakin sedikit *page fault*, semakin cepat performa sistem karena meminimalkan akses ke penyimpanan eksternal (*disk*).

---

### Quiz

1. **Apa perbedaan utama FIFO dan LRU?**
* **FIFO (First-In First-Out):** Menggunakan kriteria **waktu kedatangan**; halaman yang paling lama berada di memori akan diganti terlebih dahulu tanpa mempedulikan seberapa sering halaman tersebut diakses.
* **LRU (Least Recently Used):** Menggunakan kriteria **waktu penggunaan terakhir**; halaman yang paling lama tidak digunakan/diakses oleh CPU akan diganti karena dianggap tidak lagi dibutuhkan dalam waktu dekat.


2. **Mengapa FIFO dapat menghasilkan *Belady’s Anomaly*?**
* FIFO dapat mengalami *Belady's Anomaly* karena tidak memiliki *inclusion property* (sifat inklusi).
* Algoritma ini tidak menjamin bahwa set halaman dalam memori dengan kapasitas  frame merupakan bagian dari set halaman pada memori dengan kapasitas  frame.
* Akibatnya, pada pola referensi tertentu, menambah jumlah frame justru dapat membuang halaman yang akan segera dibutuhkan kembali, sehingga jumlah *page fault* meningkat.


3. **Mengapa LRU umumnya menghasilkan performa lebih baik dibanding FIFO?**
* **Lokalitas Temporal:** LRU bekerja berdasarkan prinsip bahwa halaman yang baru saja digunakan memiliki kemungkinan besar akan digunakan kembali dalam waktu dekat.
* **Adaptif terhadap Perilaku Program:** Berbeda dengan FIFO yang kaku terhadap urutan waktu masuk, LRU menyesuaikan isi memori dengan aktivitas akses CPU yang sebenarnya.
* **Optimalitas:** Dengan mempertahankan halaman yang aktif digunakan (seperti angka 0 dan 3 pada simulasi Anda), LRU secara efektif mengurangi frekuensi akses ke penyimpanan eksternal yang lambat.

---

## Refleksi Diri
Tuliskan secara singkat:
- Apa bagian yang paling menantang minggu ini?
  Tantangan: Memahami logika pembaruan stack pada LRU dan konsep Belady's Anomaly pada FIFO.  
- Bagaimana cara Anda mengatasinya?
  Melakukan simulasi mandiri menggunakan tabel dan memvalidasi hasilnya melalui output program secara bertahap.  

---

**Credit:**  
_Template laporan praktikum Sistem Operasi (SO-202501) – Universitas Putra Bangsa_
