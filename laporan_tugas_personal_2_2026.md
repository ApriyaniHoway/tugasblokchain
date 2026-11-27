# Laporan Tugas Personal 2 — Blockchain Level 6–9

- **Nama:** APRIYANI SUSANA HOWAY
- **NIM (4 digit terakhir):** 2084
- **Dibuat:** 2026-11-26 15:38 (waktu proses 1.8 detik)
- **Kode verifikasi:** `4859214E66CD`

> Bagian hasil dibuat otomatis. Jangan diubah: dosen menghitung ulang semua angka dari data Anda.
> Isi bagian **Analisis** dengan kata-kata Anda sendiri.

## Level 6 — Mining data pribadi dan jejak difficulty

Data yang ditambang: `APRIYANI SUSANA HOWAY |2084|2005-04-11`

| Difficulty | Nonce  | Percobaan | Teori 16^d | Hash                    |
| ---------- | ------ | --------- | ---------- | ----------------------- |
| 1          | 20     | 21        | 16         | `05226d244cb97ed8eaca…` |
| 2          | 295    | 296       | 256        | `0059aaba31afa4238815…` |
| 3          | 16083  | 16.084    | 4.096      | `000b5e182353347a92f5…` |
| 4          | 284386 | 284.387   | 65.536     | `000056adcc216145366a…` |

- Difficulty awal (dari NIM): **3**, target waktu blok 10 detik
- Waktu blok simulasi (dari NIM + tanggal + bulan lahir): 8, 0, 8, 24, 0, 4, 0, 4 detik
- Jejak difficulty (Modifikasi 6): **3, 4, 4, 3, 4, 5, 6, 7**

## Level 7 — Kunci dan tanda tangan dari data pribadi

- Kunci publik (32 karakter awal): `92472525e3606029210ceeb7d8ae3b92…`
- Alamat Anda: `a4eb00012c984c9f46be266c2ae4fbadcb394559`
- Transaksi: kirim **1** ke TEMAN_A
- Tanda tangan: `0a1b8d27e8f06dc1b073cb8e9c42f29cfcea3d28e92f5ced…`
- Tanda tangan selalu sama saat diulang: True
- Transaksi sah: **True**; setelah amount diubah: **False**
- Penipu memakai alamat Anda: tanda tangannya valid dengan kuncinya = True, transaksinya sah = **False**

## Level 8 — Jaringan dan fork pribadi

- Jumlah node: **4**; blok pribadi tiap node: [3, 1, 3, 1]
- Panjang rantai saat fork: [5, 3, 5, 3]
- Setelah resolve_conflicts: [5, 5, 5, 5], sepakat = **False**
- Setelah blok pemecah seri: [6, 6, 6, 6], sepakat = **True**
- Pemenang fork: **SONIA-1**; blok terbuang (orphan): **5**
- Hash ujung rantai: `00e680b1a0d97fe17253d2c8…`

## Level 9 — Ekonomi dengan halving

- Hadiah awal: **36**, halving setiap **3** blok
- Hadiah blok 1–6 (Modifikasi 9): **36, 36, 36, 18, 18, 18**

| Alamat               | Saldo |
| -------------------- | ----- |
| APRIYANI SUSANA HOWAY| 105   |
| TEMAN_A              | 33    |
| TEMAN_B              | 24    |

- Total suplai: **162**
- Belanja melebihi saldo ditolak: True
- Validasi ekonomi: **True**; setelah hadiah blok 1 dicurangi: **False**

## Analisis (isi dengan kata-kata Anda sendiri)

1. **Level 6.** Bandingkan kolom Percobaan dengan Teori 16^d pada tabel Anda. Mengapa bisa berbeda jauh? Lalu jelaskan jejak difficulty Anda (3, 4, 4, 3, 4, 5, 6, 7): pada langkah mana difficulty naik, tetap, dan turun, dan mengapa?

   \_Jawaban:\_Jumlah percobaan pada tabel bisa berbeda jauh dari teori \(16^d\) karena teori tersebut merupakan nilai rata-rata atau perkiraan jumlah percobaan untuk menemukan hash yang sesuai. Dalam proses mining, setiap nonce menghasilkan hash yang acak sehingga terkadang hasilnya ditemukan lebih cepat atau justru membutuhkan percobaan lebih banyak. Pada data saya, difficulty 4 membutuhkan 284.387 percobaan, jauh lebih banyak daripada perkiraan teori sebanyak 65.536 percobaan.

Pada jejak difficulty, nilai awalnya adalah 3 dengan target waktu 10 detik. Difficulty naik jika waktu mining kurang dari 5 detik, tetap jika waktunya antara 5 sampai 20 detik, dan turun jika lebih dari 20 detik. Jadi, urutannya adalah:

- Dari 3 menjadi 3 karena waktu 8 detik, difficulty tetap.
- Dari 3 menjadi 4 karena waktu 0 detik, difficulty naik.
- Tetap 4 karena waktu 8 detik.
- Turun dari 4 menjadi 3 karena waktu 24 detik.
- Naik menjadi 4 karena waktu 0 detik.
- Naik menjadi 5 karena waktu 4 detik.
- Naik menjadi 6 karena waktu 0 detik.
- Naik menjadi 7 karena waktu 4 detik.

2. **Level 7.** Mengapa tanda tangan Anda selalu sama setiap kali program dijalankan, padahal di Level 7 asli berubah-ubah? Mengapa transaksi penipu tidak sah walaupun tanda tangannya valid?

   \_Jawaban:\_Tanda tangan digital selalu sama karena pada modifikasi Level 7 digunakan metode sign_deterministic, yaitu metode tanda tangan yang menghasilkan tanda tangan secara deterministik. Artinya, jika pesan dan kunci privatnya sama, tanda tangan yang dihasilkan juga akan selalu sama. Berbeda dengan Level 7 asli yang menggunakan metode tanda tangan dengan nilai acak sehingga hasilnya dapat berubah-ubah.

Transaksi penipu tidak sah walaupun tanda tangannya valid dengan kuncinya sendiri karena alamat pengirim tidak sesuai dengan kunci publik yang digunakan untuk membuat tanda tangan. Sistem memeriksa apakah alamat pengirim benar-benar berasal dari kunci publik tersebut. Jadi, seseorang tidak bisa menggunakan alamat milik orang lain hanya dengan membuat tanda tangan menggunakan kuncinya sendiri.

3. **Keamanan kunci.** Kunci privat Anda dibuat dari nama, NIM, dan tanggal lahir. Mengapa cara ini SANGAT BERBAHAYA di dunia nyata? Siapa saja yang bisa mencuri dana alamat Anda? (Cari tahu istilah _brain wallet_.)

   \_Jawaban:\_Membuat kunci privat dari nama, NIM, dan tanggal lahir sangat berbahaya jika digunakan di dunia nyata karena informasi tersebut bukan rahasia dan bisa diketahui atau ditebak oleh orang lain. Jika seseorang mengetahui data pribadi tersebut dan mengetahui cara pembuatan kuncinya, orang tersebut dapat menghitung kunci privat yang sama dan mengambil dana dari alamat tersebut.

Cara ini berkaitan dengan istilah brain wallet, yaitu metode menyimpan atau membuat kunci cryptocurrency berdasarkan sesuatu yang diingat manusia, seperti kata-kata, kalimat, atau informasi pribadi. Brain wallet sangat berisiko jika menggunakan informasi yang mudah ditebak karena penyerang dapat mencoba berbagai kemungkinan untuk menemukan kunci privat. Orang yang mengetahui data pribadi saya, atau siapa pun yang berhasil menebak kombinasi data dan algoritmanya, berpotensi mencuri dana. Oleh karena itu, di dunia nyata kunci privat harus dibuat secara acak dengan tingkat keamanan yang tinggi dan tidak berasal dari data pribadi.

4. **Level 8.** Jaringan Anda punya 4 node dan pemenangnya SONIA-1 dengan 5 blok terbuang. Jelaskan mengapa node itu menang. Mengapa jaringan Anda sempat tidak sepakat, dan bagaimana blok pemecah seri menyelesaikannya?

   \_Jawaban:\_Node SONIA-1 menjadi pemenang fork karena memiliki rantai dengan panjang 5 blok dan terpilih sebagai rantai yang digunakan oleh jaringan ketika terjadi konflik. Pada awalnya, jaringan tidak sepakat karena terdapat dua kelompok node dengan panjang rantai yang berbeda, yaitu sebagian memiliki 5 blok dan sebagian lainnya memiliki 3 blok. Kondisi ini disebut fork, yaitu ketika jaringan memiliki lebih dari satu versi rantai blockchain.

Setelah proses resolve_conflicts, semua node memiliki panjang rantai yang sama, yaitu 5 blok. Namun, jaringan masih belum sepakat karena terdapat dua rantai berbeda yang sama-sama memiliki panjang 5 blok. Untuk menyelesaikannya, dibuat blok pemecah seri sehingga salah satu rantai menjadi lebih panjang. Akhirnya, semua node memiliki rantai sepanjang 6 blok dan mencapai kesepakatan. Dalam proses tersebut terdapat 5 blok yang menjadi orphan atau blok yang tidak digunakan dalam rantai utama.

5. **Level 9.** Dengan hadiah awal 36 dan halving setiap 3 blok, berapa batas total suplai jika mining berjalan selamanya? Tunjukkan perhitungannya, lalu kaitkan dengan batas 21 juta Bitcoin.

   \_Jawaban:\_Dengan hadiah awal sebesar 36 dan halving setiap 3 blok, hadiah mining akan terus berkurang menjadi setengahnya setiap melewati 3 blok. Jika mining berjalan selamanya, total suplai maksimum yang dihasilkan dari hadiah mining adalah deret geometri tak hingga.

Jadi, batas total suplai dari hadiah mining adalah 216 koin. Perhitungan ini mengasumsikan hadiah dapat terus dibagi menjadi pecahan tanpa batas. Jika sistem hanya mengizinkan bilangan bulat, hasil akhirnya dapat berbeda karena pembulatan.

Konsep ini mirip dengan Bitcoin yang memiliki batas suplai maksimum 21 juta BTC. Bitcoin menggunakan mekanisme halving untuk mengurangi hadiah bagi penambang secara berkala sehingga jumlah Bitcoin baru yang beredar semakin sedikit. Dengan demikian, halving membantu mengendalikan penerbitan koin dan membuat suplai menjadi terbatas.

---

## Data verifikasi (JANGAN DIUBAH)

<!-- DATA-VERIFIKASI -->

```json
{
  "tugas": "personal-2 (Level 6-9)",
  "profil": {
    "nama": "APRIYANI SUSANA HOWAY",
    "nim4": "2026",
    "tanggal_lahir": "2005-04-11",
    "kota_asal": "SORONG",
    "hobi": "TIDUR"
  },
  "level6": {
    "data_ditambang": "APRIYANI SUSANA HOWAY|2084|2005-04-11",
    "mining": [
      {
        "difficulty": 1,
        "nonce": 20,
        "hash": "05226d244cb97ed8eacaec0eda976999a6313ba256b0deeb7023975612067929",
        "percobaan": 21,
        "teori": 16
      },
      {
        "difficulty": 2,
        "nonce": 295,
        "hash": "0059aaba31afa4238815909cdc9bc30889a467daef6dec7125f7dcf5674773e7",
        "percobaan": 296,
        "teori": 256
      },
      {
        "difficulty": 3,
        "nonce": 16083,
        "hash": "000b5e182353347a92f587f2f0fdaa2a1fe7a8e19a9b92b5674bbc5781cdedbb",
        "percobaan": 16084,
        "teori": 4096
      },
      {
        "difficulty": 4,
        "nonce": 284386,
        "hash": "000056adcc216145366af510e66e5deea304938fdcdf3d4fc5aed070e79bca18",
        "percobaan": 284387,
        "teori": 65536
      }
    ],
    "difficulty_awal": 3,
    "daftar_waktu_detik": [8, 0, 8, 24, 0, 4, 0, 4],
    "target_detik": 10,
    "jejak_difficulty": [3, 4, 4, 3, 4, 5, 6, 7]
  },
  "level7": {
    "kunci_publik_awal": "92472525e3606029210ceeb7d8ae3b92",
    "alamat": "a4eb00012c984c9f46be266c2ae4fbadcb394559",
    "transaksi": {
      "sender": "a4eb00012c984c9f46be266c2ae4fbadcb394559",
      "recipient": "TEMAN_A",
      "amount": 1
    },
    "tanda_tangan": "0a1b8d27e8f06dc1b073cb8e9c42f29cfcea3d28e92f5ced7ff50875e1b67f867dfc40d3b479dc6d71cd02c4a672e2f2b8ccb6d7cd25b4ce4340720762455f01",
    "tanda_tangan_selalu_sama": true,
    "sah": true,
    "sah_setelah_amount_diubah": false,
    "ttd_penipu_valid_dengan_kuncinya": true,
    "transaksi_penipu_sah": false
  },
  "level8": {
    "jumlah_node": 4,
    "blok_pribadi_per_node": [3, 1, 3, 1],
    "panjang_saat_fork": [5, 3, 5, 3],
    "panjang_setelah_resolve": [5, 5, 5, 5],
    "sepakat_setelah_resolve": false,
    "perlu_pemecah_seri": true,
    "panjang_setelah_pemecah_seri": [6, 6, 6, 6],
    "sepakat_setelah_pemecah_seri": true,
    "pemenang_fork": "APRIYANI -1",
    "blok_terbuang": 5,
    "hash_ujung": "00e680b1a0d97fe17253d2c89b602034e66bffae316e7f3d58800941295480cd"
  },
  "level9": {
    "hadiah_awal": 36,
    "interval_halving": 3,
    "hadiah_per_blok": [36, 36, 36, 18, 18, 18],
    "saldo": {
      "APRIYANI SUSANA HOWAY": 105,
      "TEMAN_A": 33,
      "TEMAN_B": 24
    },
    "total_suplai": 162,
    "belanja_melebihi_saldo_ditolak": true,
    "validasi_ekonomi": true,
    "hash_ujung": "00bea6f2454e172ea192b3f173905771f41a431e3a11d535d104c2a6aa53e727",
    "validasi_setelah_hadiah_dicurangi": false
  },
  "kode_verifikasi": "4859214E66CD"
}
```
