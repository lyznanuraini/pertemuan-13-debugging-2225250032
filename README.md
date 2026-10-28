# Pertemuan 13 - Debugging dan Testing

Nama: Lyzna Nuraini
NIM: 2225250032
Kelas: 3E

## Kasus
Program memproses data nilai mahasiswa yang memiliki beberapa bug logika pada perhitungan rata-rata, penentuan status kelulusan pada nilai batas, dan penentuan nilai tertinggi.

## Test Case
| ID | Target | Input | Expected | Actual Awal | Status Awal |
|---|---|---|---|---|---|
| T1 | rata-rata | [80, 60, 90, 70] | 75.0 | 60.0 | FAIL |
| T2 | rata-rata | [100, 80] | 90.0 | 36.0 | FAIL |
| T3 | status | 60 | Lulus | Tidak lulus | FAIL |
| T4 | status | 59 | Tidak lulus | Tidak lulus | PASS |
| T5 | tertinggi | [80, 60, 90, 70] | 90 | 0 | FAIL |

## Bug Report
1. **B01 - Pembagi Statis pada Rata-Rata**:
   - Gejala: Hasil rata-rata salah jika jumlah elemen list tidak sama dengan 5.
   - Lokasi: Fungsi `hitung_rata_rata`.
   - Akar Penyebab: Menggunakan pembagi hardcoded `/ 5`.
   - Perbaikan: Mengubah pembagi menjadi `/ len(nilai)` dan menambahkan penanganan list kosong.

2. **B02 - Bug Operator Batas Kelulusan**:
   - Gejala: Nilai 60 dinyatakan "Tidak lulus".
   - Lokasi: Fungsi `status`.
   - Akar Penyebab: Penggunaan operator `>` alih-alih `>=`.
   - Perbaikan: Mengubah kondisi menjadi `if nilai >= 60:`.

3. **B03 - Logika Nilai Tertinggi Salah**:
   - Gejala: Mengembalikan nilai `0` alih-alih nilai tertinggi.
   - Lokasi: Fungsi `nilai_tertinggi`.
   - Akar Penyebab: Inisialisasi awal `tertinggi = 0` dan pembandingan menggunakan `<` alih-alih `>`.
   - Perbaikan: Menginisialisasi `tertinggi = nilai[0]` dan membandingkan `x > tertinggi`.

## Retest
| ID | Input | Expected | Actual Retest | Status |
|---|---|---|---|---|
| T1 | [80, 60, 90, 70] | 75.0 | 75.0 | PASS |
| T2 | [100, 80] | 90.0 | 90.0 | PASS |
| T3 | 60 | Lulus | Lulus | PASS |
| T4 | 59 | Tidak lulus | Tidak lulus | PASS |
| T5 | [80, 60, 90, 70] | 90 | 90 | PASS |

## Cara Menjalankan
```bash
python3 praktik/praktik_4_debugging.py
