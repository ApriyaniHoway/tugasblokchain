
# Laporan Tugas Personal Blockchain Level 1–5

- **Nama:** APRIYANI SUSANA HOWAY
- **NIM (4 digit terakhir):** 2084
- **Dibuat:** 2026-11-22 19:22  (waktu proses 16.9 detik)
- **Kode verifikasi:** `4EB78DD33083`

> Bagian hasil dibuat otomatis. Jangan diubah: dosen menghitung ulang semua angka dari data Anda.
> Isi bagian **Analisis** dengan kata-kata Anda sendiri.

## Level 1 — Hash data pribadi

| Hasil | Nilai |
|---|---|
| SHA-256 nama | `f033a95196154cfd492f3c5e2ff69e7f9e56fd8f45b953e78e93f59a013697b7` |
| hash_dict profil | `6c2e9c365eef51119c4fa2f9f211583fa7e88a114c6c4e92eb0b6946de5115be` |
| hash_dict profil (urutan key dibalik) | `6c2e9c365eef51119c4fa2f9f211583fa7e88a114c6c4e92eb0b6946de5115be` |
| Bit berubah: tanggal lahir vs tanggal lahir + 1 hari | 47.27% |
| ID mahasiswa (Modifikasi 1) | `1b27aa28` |

## Level 2 — Blockchain personal

- Proof genesis: **2084** (dari NIM)
- Proof blok 2, 3, 4: **74156, 129201, 210659**
- Pemilik setiap blok: `1b27aa28`
- Rantai valid: True

## Level 3 — Pemalsuan data pribadi

- Posisi yang dipalsukan: **3**
- Data asli: `APRIYANI SUSANA HOWAY hobi TIDUR'
- Data palsu: `APRIYANI SUSANA HOWAY hobi TIDUR (DIPALSUKAN)`
- Valid sebelum dipalsukan: True
- Tautan putus di indeks: **4**
- Valid setelah dipalsukan: **False**
- Valid setelah disambung ulang: **True**

## Level 4 — Transaksi dari data pribadi

| Blok | Pengirim | Penerima | Jumlah |
|---|---|---|---|
| 2 | APRIYANI SUSANA HOWAY  | TEMAN_A | 1 |
| 2 | TEMAN_A | APRIYANI SUSANA HOWAY | 1 |
| 3 | APRIYANI SUSANA HOWAY | DOSEN | 27 |

- Ringkasan saldo (Modifikasi 4): masuk **1**, keluar **28**, bersih **-27**
- Kirim ke diri sendiri ditolak: True
- Amount 0 ditolak: True

## Level 5 — Proof of Work dengan nonce (deterministik)

| Blok | Nonce | Hash |
|---|---|---|
| 0 | 169298 | `00004ba6c356a51b01c58883…` |
| 1 | 216730 | `00005d0a8507aa3f2a5f567d…` |
| 2 | 41967 | `000083deb0dd092dd3ccf64e…` |
| 3 | 97075 | `0000f9d74dc74443e450d599…` |

- Valid: True → setelah blok 1 dipalsukan: **False**
- Percobaan hash untuk menambang ulang blok 1–3: **58.096**
- Valid setelah ditambang ulang: True

## Analisis (isi dengan kata-kata Anda sendiri)

1. **Level 1.** Bandingkan SHA-256 nama Anda dengan milik seorang teman. Apakah ada pola yang mirip? Jelaskan juga mengapa dua hash profil Anda sama, dan mengapa hanya menambah 1 hari pada tanggal lahir mengubah 47.27% bit.

   _Jawaban:_Hash SHA-256 saya dan teman kemungkinan besar akan berbeda karena setiap nama menghasilkan nilai hash yang unik. Walaupun ada kemiripan nama, perubahan satu karakter saja dapat menghasilkan hash yang sangat berbeda. Dua hash profil saya tetap sama meskipun urutan key dibalik karena fungsi hash_dict mengurutkan key terlebih dahulu sebelum melakukan hashing. Sementara itu, perubahan tanggal lahir hanya satu hari menghasilkan perubahan 47,27% bit. Hal ini menunjukkan sifat avalanche effect, yaitu perubahan kecil pada data masukan dapat menyebabkan perubahan besar pada hasil hash.

2. **Level 2.** Kode Anda dan teman sama persis, tetapi proof Anda (74156, 129201, 210659) berbeda. Jelaskan penyebabnya.

   _Jawaban:_Meskipun kode program yang digunakan sama, nilai proof saya dan teman dapat berbeda karena proof genesis dibuat berdasarkan empat digit terakhir NIM masing-masing. Pada blockchain saya, proof genesis bernilai 2026. Nilai proof blok berikutnya juga dipengaruhi oleh proof sebelumnya dan hash blok sebelumnya. Karena identitas awal setiap mahasiswa berbeda, hasil proses pencarian proof dapat menghasilkan angka yang berbeda pula.

3. **Level 3.** Anda memalsukan posisi 3 dan tautan putus terdeteksi di indeks 4, sedangkan valid setelah dipalsukan = False. Jelaskan hasil ini, lalu bandingkan dengan teman yang posisi pemalsuannya berbeda.

   _Jawaban:_Saya memalsukan data pada posisi blok 3 dengan menambahkan teks (DIPALSUKAN) pada data asli. Setelah data diubah, hash blok tersebut ikut berubah sehingga hash yang tersimpan pada blok berikutnya tidak lagi sesuai. Karena itu, sistem mendeteksi tautan yang putus pada indeks 4 dan menyatakan blockchain tidak valid (False). Setelah blok berikutnya disambungkan ulang, rantai kembali valid (True). Jika teman memalsukan posisi yang berbeda, lokasi tautan yang rusak juga dapat berbeda, tergantung posisi blok yang diubah.

4. **Level 4.** Jelaskan dari mana angka masuk 1, keluar 28, dan bersih -27 berasal. Mengapa transaksi ke diri sendiri perlu ditolak?

   _Jawaban:_Jumlah saldo masuk sebesar 1 berasal dari transaksi TEMAN_A kepada saya sebesar 1. Jumlah saldo keluar sebesar 28 berasal dari dua transaksi, yaitu pengiriman kepada TEMAN_A sebesar 1 dan kepada DOSEN sebesar 27. Dengan demikian, saldo bersih saya adalah 1 dikurangi 28, yaitu -27. Transaksi ke diri sendiri perlu ditolak agar tidak terjadi transaksi yang tidak memiliki tujuan perpindahan nilai dan agar aturan transaksi dalam sistem tetap konsisten.

5. **Level 5.** Penyerang butuh 58.096 percobaan hash untuk memalsukan rantai Anda. Mengapa nonce Anda selalu sama setiap kali program dijalankan, padahal di demo Level 5 asli nonce berubah-ubah?

   _Jawaban:_Nonce saya selalu sama setiap kali program dijalankan karena blockchain deterministik menggunakan data awal, timestamp, transaksi, dan aturan Proof of Work yang tetap. Dengan masukan yang sama, proses hashing dan pencarian nonce akan menghasilkan nilai yang sama. Berbeda dengan demo Level 5 asli yang menggunakan data atau timestamp yang dapat berubah, sehingga hasil nonce juga dapat berubah. Sifat deterministik ini memudahkan pengujian karena hasil program dapat diulang dan dibandingkan.

6. **Etika data.** Anda baru saja menyimpan nama dan tanggal lahir di dalam blockchain. Jika ini blockchain publik, apa risikonya? Kaitkan dengan sifat immutability dan UU No. 27 Tahun 2022 tentang Pelindungan Data Pribadi, terutama hak untuk menghapus data.

   _Jawaban:_Jika nama dan tanggal lahir saya disimpan di blockchain publik, data tersebut berisiko diketahui, disalin, dan digunakan oleh orang lain tanpa izin. Risiko ini semakin besar karena blockchain memiliki sifat immutability, yaitu data yang sudah tercatat sulit diubah atau dihapus karena saling terhubung melalui hash. Hal ini dapat menimbulkan masalah dengan UU Nomor 27 Tahun 2022 tentang Pelindungan Data Pribadi. Dalam Pasal 8, seseorang memiliki hak untuk mengakhiri pemrosesan, menghapus, dan/atau memusnahkan data pribadinya sesuai ketentuan hukum. Pasal 43 juga mengatur kewajiban pengendali data untuk menghapus data pribadi dalam kondisi tertentu, termasuk jika terdapat permintaan dari subjek data. Oleh karena itu, data pribadi sebaiknya tidak disimpan secara langsung di blockchain publik. Lebih baik menyimpan data pribadi di tempat yang aman dan hanya menyimpan hash atau bukti verifikasi di blockchain.

---

## Data verifikasi (JANGAN DIUBAH)

<!-- DATA-VERIFIKASI -->
```json
{
  "profil": {
    "nama": "APRIYANI SUSANA HOWAY",
    "nim4": "2084",
    "tanggal_lahir": "2005-04-11",
    "kota_asal": "SORONG",
    "hobi": "TUDUR"
  },
  "level1": {
    "hash_nama": "f033a95196154cfd492f3c5e2ff69e7f9e56fd8f45b953e78e93f59a013697b7",
    "hash_profil": "6c2e9c365eef51119c4fa2f9f211583fa7e88a114c6c4e92eb0b6946de5115be",
    "hash_profil_urutan_terbalik": "6c2e9c365eef51119c4fa2f9f211583fa7e88a114c6c4e92eb0b6946de5115be",
    "avalanche_tanggal_persen": 47.27,
    "id_mahasiswa": "1b27aa28"
  },
  "level2": {
    "proof_genesis": 2026,
    "proof_blok": [
      74156,
      129201,
      210659
    ],
    "pemilik_semua_blok": [
      "1b27aa28"
    ],
    "valid": true
  },
  "level3": {
    "posisi_dipalsukan": 3,
    "data_asli": "APRIYANI SUSANA HOWAY h0bi TIDUR",
    "data_palsu": "APRIYANI SUSANA HOWAY hobi TIBUR (DIPALSUKAN)",
    "valid_asli": true,
    "tautan_putus_di": 4,
    "valid_setelah_dipalsukan": false,
    "valid_setelah_disambung_ulang": true
  },
  "level4": {
    "riwayat": [
      [
        2,
        {
          "sender": "APRIYANI SUSANA HOWAY",
          "recipient": "TEMAN_A",
          "amount": 1
        }
      ],
      [
        2,
        {
          "sender": "TEMAN_A",
          "recipient": "APRIYANI SUSANAN HOWAY",
          "amount": 1
        }
      ],
      [
        3,
        {
          "sender": "APRIYANI SUSANA HOWAY",
          "recipient": "DOSEN",
          "amount": 27
        }
      ]
    ],
    "ringkasan_saldo": {
      "masuk": 1,
      "keluar": 28,
      "bersih": -27
    },
    "kirim_ke_diri_sendiri_ditolak": true,
    "amount_nol_ditolak": true,
    "jumlah_blok": 3
  },
  "level5": {
    "nonce": [
      169298,
      216730,
      41967,
      97075
    ],
    "hash": [
      "00004ba6c356a51b01c5888334f70988b58d68b37657f83f8c26453b1e4412c6",
      "00005d0a8507aa3f2a5f567d4a31dd164a45d7e557d12334ea36265e2152e5d6",
      "000083deb0dd092dd3ccf64e169706bae3951e119b555b8c2899b3639ddbdae1",
      "0000f9d74dc74443e450d5999445944d5e6862d1b88a5735138b5c72285ac1e4"
    ],
    "valid": true,
    "valid_setelah_dipalsukan": false,
    "percobaan_tambang_ulang": 58096,
    "valid_setelah_tambang_ulang": true
  },
  "kode_verifikasi": "4EB78DD33083"
}
```
