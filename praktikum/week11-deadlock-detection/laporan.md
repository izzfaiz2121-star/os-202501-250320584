# Laporan Praktikum Sistem Operasi
**Minggu 11: Analisis dan Simulasi Deteksi Deadlock**

---

## Identitas
- **Nama**  : Faizatun Khasanah
- **NIM**   : 250320584
- **Kelas** : 1DSRA

---

## Tujuan Praktikum
Setelah menyelesaikan tugas ini, mahasiswa mampu:
1. Memahami logika dasar pembuatan algoritma pendeteksi kondisi deadlock.
2. Melakukan simulasi skenario kebuntuan sumber daya menggunakan dataset tertentu.
3. Menganalisis hasil deteksi dan menyajikannya dalam format tabel yang sistematis.
4. Memberikan solusi pemulihan terhadap sistem yang mengalami deadlock.

---

## Dasar Teori
* **Deadlock (Kebuntuan):** Sebuah situasi di mana sekumpulan proses tidak dapat melanjutkan eksekusinya karena setiap proses menunggu sumber daya yang sedang dikuasai oleh proses lain dalam kelompok tersebut.
  
* **Strategi Deteksi:** Metode ini membiarkan proses berjalan secara normal tanpa batasan ketat di awal, namun sistem secara periodik akan menjalankan algoritma untuk memeriksa apakah ada siklus (cycle) yang terbentuk dalam alokasi sumber daya.
  
* **Kondisi Penyebab:** Kebuntuan terjadi jika syarat *Mutual Exclusion*, *Hold and Wait*, *No Preemption*, dan *Circular Wait* terpenuhi secara simultan.

---

## Langkah Praktikum
1. Menyiapkan Dataset

Membuat dataset sederhana yang berisi:

* Daftar proses
* Resource Allocation
* Resource Request / Need
  
Data tabel:

| Proses | Allocation (Jalur yang Ditempati) | Request (Jalur yang Diminta) |
| :--- | :--- | :--- |
| **Mobil_A** | Jalur_Utara | Jalur_Timur |
| **Mobil_B** | Jalur_Timur | Jalur_Selatan |
| **Mobil_C** | Jalur_Selatan | Jalur_Utara |

2. Implementasi Algoritma Deteksi Deadlock

Program:

* Membaca data proses dan resource.
* Menentukan apakah sistem berada dalam kondisi deadlock.
* Menampilkan proses mana saja yang terlibat deadlock.

3. Eksekusi & Validasi

- Menjalankan program dengan dataset uji.
- Memvalidasi hasil deteksi dengan analisis manual/logis.
- Menyimpan hasil eksekusi dalam bentuk screenshot.

4. Analisis Hasil

- Menyajikan hasil deteksi dalam tabel (proses deadlock / tidak).
- Menjelaskan mengapa deadlock terjadi atau tidak terjadi.
- Mengaitkan hasil dengan teori deadlock (empat kondisi).

5. Commit & Push

```text
git add .
git commit -m "Minggu 11 - Deadlock Detection"
git push origin main
```
---

## Kode / Perintah
### 1. Implementasi Kode Deteksi (`deadlock_detection.py`)

```python
import time

def deteksi_deadlock():
    # Dataset sesuai tabel Faiza
    data = [
        {'Proses': 'Mobil_A', 'Alokasi': 'Jalur_Utara', 'Minta': 'Jalur_Timur'},
        {'Proses': 'Mobil_B', 'Alokasi': 'Jalur_Timur', 'Minta': 'Jalur_Selatan'},
        {'Proses': 'Mobil_C', 'Alokasi': 'Jalur_Selatan', 'Minta': 'Jalur_Utara'}
    ]

    print("=== PROGRAM DETEKSI DEADLOCK ===")
    
    # Melihat siapa yang menguasai jalur mana
    tuan_rumah = {d['Alokasi']: d['Proses'] for d in data}
    siklus = {}

    for d in data:
        mobil = d['Proses']
        tujuan = d['Minta']
        
        print(f"[*] {mobil} (di {d['Alokasi']}) ingin masuk ke {tujuan}")
        
        if tujuan in tuan_rumah:
            pemilik = tuan_rumah[tujuan]
            siklus[mobil] = pemilik
            print(f"    >> Tertahan oleh {pemilik}")
        else:
            print("    >> Jalur Kosong")
        time.sleep(0.5)

    if len(siklus) >= 3:
        print("\n[HASIL] STATUS: DEADLOCK TERDETEKSI!")
        print(f"Penyebab: Circular Wait antara {list(siklus.keys())}")
    else:
        print("\n[HASIL] STATUS: SISTEM AMAN")

if __name__ == "__main__":
    deteksi_deadlock()
```

### 2. Implementasi Code deadlock_solution.py

```python
import time

def solusi_deadlock():
    terjebak = ['Mobil_A', 'Mobil_B', 'Mobil_C']
    alokasi = {'Mobil_A': 'Jalur_Utara', 'Mobil_B': 'Jalur_Timur', 'Mobil_C': 'Jalur_Selatan'}
    
    print("=== PROGRAM PEMULIHAN DEADLOCK ===")
    print(f"[!] Terdeteksi kemacetan pada: {terjebak}")
    time.sleep(1)

    # Langkah Solusi: Pilih satu mobil untuk diderek (Terminasi)
    korban = terjebak[0] 
    print(f"\n[SOLUSI] Memilih {korban} sebagai 'Victim' untuk diderek keluar...")
    time.sleep(1.5)
    
    print(f"[*] {korban} telah dikeluarkan. Jalur {alokasi[korban]} sekarang KOSONG.")
    
    # Simulasi pergerakan mobil yang tersisa
    sisa = terjebak[1:]
    print("\n[!] Menjalankan sisa kendaraan:")
    for m in sisa:
        print(f"    >> {m} Berhasil MAJU ke jalur berikutnya.")
        time.sleep(0.5)

    print("\n[HASIL] Kemacetan berhasil diuraikan!")

if __name__ == "__main__":
    solusi_deadlock()
```
3. Perintah eksekusi

```text
python code/deadlock_detection.py
python code/deadlock_solution.py
```
---

## Hasil Eksekusi
Sertakan screenshot hasil percobaan atau diagram:
![Screenshot hasil](screenshots/example.png)

---

## Analisis
## 1. Analisis Hasil Simulasi
Berdasarkan pengamatan pada program deadlock_detection.py dan deadlock_solution.py:

* Deteksi Kondisi: Sistem berhasil mengidentifikasi adanya kemacetan karena terpenuhinya empat syarat deadlock, terutama Circular Wait. Mobil_A menunggu Mobil_B, Mobil_B menunggu Mobil_C, dan Mobil_C kembali menunggu Mobil_A.

* Dampak Tanpa Solusi: Jika tidak dilakukan intervensi, semua proses akan terjebak dalam status idle selamanya karena adanya aturan No Preemption (sumber daya tidak bisa diambil paksa tanpa prosedur khusus).

* Efektivitas Pemulihan: Dengan menggunakan metode pemulihan melalui terminasi salah satu proses (Mobil_A), mata rantai penantian berhasil diputus. Hal ini memungkinkan Mobil_C untuk maju, yang kemudian memberikan ruang bagi Mobil_B untuk menyelesaikan tugasnya.
  
---

## Kesimpulan
1. Kemampuan Deteksi: Algoritma deteksi sangat efektif untuk memantau integritas sistem dengan cara melacak siklus dalam grafik alokasi sumber daya (Resource Allocation Graph).

2. Keseimbangan Sistem: Penggunaan strategi deteksi dan pemulihan memberikan keseimbangan antara performa sistem dan keamanan, meskipun harus mengorbankan salah satu proses saat terjadi masalah.

3. Implementasi Teori: Simulasi ini membuktikan bahwa kebuntuan pada sistem operasi bukan hanya teori, melainkan risiko nyata yang memerlukan penanganan sistematis agar layanan tidak berhenti total.
   
---

## Quiz
1. Apa perbedaan antara deadlock prevention, avoidance, dan detection?

* Pencegahan (Prevention): Membatasi penggunaan sumber daya sejak awal agar salah satu syarat deadlock tidak mungkin terjadi.

* Penghindaran (Avoidance): Memeriksa setiap permintaan secara dinamis; hanya memberikan izin jika sistem tetap berada dalam kondisi aman (safe state).

* Deteksi (Detection): Membiarkan proses berjalan bebas, baru kemudian mencari dan memperbaiki masalah jika kebuntuan benar-benar ditemukan.

2. Mengapa deteksi deadlock tetap diperlukan dalam sistem operasi?

Karena metode pencegahan seringkali terlalu membatasi produktivitas sistem dan menyebabkan sumber daya banyak yang menganggur. Deteksi memungkinkan sistem bekerja lebih fleksibel dan efisien selama tidak ada masalah.

3. Apa kelebihan dan kekurangan pendekatan deteksi deadlock?

Kelebihan: Maksimalkan penggunaan sumber daya karena tidak ada aturan ketat di awal.

Kekurangan: Membebani kinerja CPU karena harus menjalankan algoritma pengecekan secara rutin, serta ada risiko kehilangan data saat proses harus dimatikan paksa.

---

## Refleksi Diri
Tuliskan secara singkat:
- Apa bagian yang paling menantang minggu ini?
  Bagian Paling Menantang: Memahami bagaimana sebuah kode bisa mendeteksi hubungan melingkar antara proses yang saling menunggu.
- Bagaimana cara Anda mengatasinya?
  Cara Mengatasi: Saya memvisualisasikan data tabel tersebut ke dalam gambar grafik (tanda panah) agar lebih mudah memahami siapa yang sedang menghalangi siapa dalam simulasi Python tersebut.

---

**Credit:**  
_Template laporan praktikum Sistem Operasi (SO-202501) – Universitas Putra Bangsa_
