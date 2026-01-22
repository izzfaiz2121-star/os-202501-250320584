
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

## Dasar Teori
1. FIFO (First-In, First-Out): Algoritma penggantian halaman yang paling sederhana. Halaman yang berada di memori paling lama (yang pertama kali masuk) akan menjadi halaman pertama yang diganti saat terjadi page fault.
2. LRU (Least Recently Used): Algoritma yang lebih adaptif dengan memanfaatkan prinsip lokalitas temporal. Halaman yang akan diganti adalah halaman yang paling lama tidak diakses/digunakan oleh CPU.
3. Page Fault: Kondisi yang terjadi ketika program mencoba mengakses halaman yang saat ini tidak dimuat di memori utama (RAM).
4. Page Hit: Kondisi ketika halaman yang dibutuhkan program sudah tersedia di memori utama.
   
---

## Kode / Perintah
Python

# Reference String & Konfigurasi Frame
reference_string = [7, 0, 1, 2, 0, 3, 0, 4, 2, 3, 0, 3, 2]
frames = 3

def print_process_table(title, steps):
    print(f"\n{title}")
    print("+" + "-"*8 + "+" + "-"*10 + "+" + "-"*10 + "+" + "-"*10 + "+" + "-"*10 + "+")
    print("| Page   | Frame 1  | Frame 2  | Frame 3  | Status   |")
    print("+" + "-"*8 + "+" + "-"*10 + "+" + "-"*10 + "+" + "-"*10 + "+" + "-"*10 + "+")
    for page, mem, status in steps:
        print(f"| {page:<6} | {mem[0]:<8} | {mem[1]:<8} | {mem[2]:<8} | {status:<8} |")
    print("+" + "-"*8 + "+" + "-"*10 + "+" + "-"*10 + "+" + "-"*10 + "+" + "-"*10 + "+")

# ================= FIFO IMPLEMENTATION =================
def fifo_page_replacement(ref, frames):
    memory = ['-'] * frames
    fifo_index = 0
    steps = []
    page_fault = 0
    for page in ref:
        if page in memory:
            steps.append((page, memory.copy(), "HIT"))
        else:
            page_fault += 1
            memory[fifo_index] = page
            fifo_index = (fifo_index + 1) % frames
            steps.append((page, memory.copy(), "FAULT"))
    return page_fault, steps

# ================= LRU IMPLEMENTATION =================
def lru_page_replacement(ref, frames):
    memory = ['-'] * frames
    last_used = {}
    steps = []
    page_fault = 0
    for time, page in enumerate(ref):
        if page in memory:
            steps.append((page, memory.copy(), "HIT"))
        else:
            page_fault += 1
            if '-' in memory:
                index = memory.index('-')
            else:
                lru_page = min(last_used, key=last_used.get)
                index = memory.index(lru_page)
                del last_used[lru_page]
            memory[index] = page
            steps.append((page, memory.copy(), "FAULT"))
        last_used[page] = time
    return page_fault, steps

# Eksekusi Simulasi
fifo_fault, fifo_steps = fifo_page_replacement(reference_string, frames)
lru_fault, lru_steps = lru_page_replacement(reference_string, frames)

print_process_table("SIMULASI FIFO", fifo_steps)
print_process_table("SIMULASI LRU", lru_steps)
---

## Hasil Eksekusi
Sertakan screenshot hasil percobaan atau diagram:
![Screenshot hasil](screenshots/example.png)

---

## Analisis
## Analisis Perbandingan

| Algoritma | Jumlah Page Fault | Keterangan |
| --- | --- | --- |
| **FIFO** | **10** | Mengganti halaman berdasarkan urutan masuk (paling "tua") tanpa melihat riwayat akses. |
| **LRU** | **8** | Mengganti halaman yang paling lama tidak digunakan; lebih adaptif terhadap pola akses. |

* **Mengapa Berbeda?** FIFO hanya mempertimbangkan waktu masuk, sehingga halaman yang sering dipakai tetap bisa terhapus jika sudah lama berada di memori. Sebaliknya, LRU memantau riwayat akses dan mempertahankan halaman yang baru saja digunakan.
* **Mana yang Lebih Efisien?** **LRU lebih efisien** karena menghasilkan *page fault* lebih sedikit (8 vs 10). LRU mengikuti prinsip *Locality of Reference*, yaitu kecenderungan program mengakses kembali data yang baru saja digunakan.

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
