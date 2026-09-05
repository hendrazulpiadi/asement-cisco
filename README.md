# Asesmen Praktikum Cisco Dasar — "Dari Console hingga Internet"

Aplikasi web asesmen akhir untuk modul praktikum Cisco Dasar. Siswa mengerjakan soal
pemahaman, refleksi praktik, dan menilai keyakinan konfigurasi (Router & Switch).
Hasil tersimpan otomatis di tiga tempat: browser (lokal), Google Sheets, dan cloud JSONBin.
Guru dapat membuka rekap seluruh kelas setelah memasukkan PIN.

## Isi / Fitur

- **Identitas peserta** — nama, kelas, no. absen, tanggal.
- **Cek Pemahaman (12 soal objektif)** — penilaian otomatis dengan skor & tingkat penguasaan.
- **Refleksi Praktik (6 bagian)** — skala keyakinan 1–5 dan pertanyaan esai.
- **Penyimpanan berlapis** — localStorage (offline), Google Sheets, dan JSONBin (cloud).
- **Mode Rekap Guru** — tabel rekap, rata-rata nilai, ekspor CSV/JSON, sinkronisasi data
  dari JSONBin, dilindungi PIN `071098`.

## Teknologi yang Dipakai

| Teknologi | Fungsi |
|-----------|--------|
| HTML5 + CSS3 (vanilla, single file) | Antarmuka & tampilan responsif |
| JavaScript (ES6, vanilla) | Logika asesmen, validasi, perhitungan skor |
| `localStorage` | Penyimpanan hasil di browser perangkat |
| Google Apps Script Web App | Pengiriman data tambahan (backup) ke Google Sheets |
| JSONBin API v3 | Database cloud (bin `6a9c56afda38895dfe3d4fa0`) |
| Git & GitHub | Version control dan hosting repository |

## Proses Bisnis Aplikasi

1. **Siswa membuka halaman** — mengisi identitas, menjawab 12 soal objektif dan
   melengkapi bagian refleksi.
2. **Submit** — sistem menghitung benar/salah dan 12 soal, lalu:
   - menyimpan entri ke `localStorage`,
   - mengirim copy ke Google Sheets (backup),
   - sinkronisasi ke JSONBin (baca data cloud → gabung → tulis ulang).
3. **Hasil tampil** — skor persentase, tingkat penguasaan, dan umpan balik; siswa dapat
   mengunduh hasil sebagai JSON lebih lanjut.
4. **Guru membuka Mode Rekap Guru** — memasukkan PIN `071098` untuk mengakses panel,
   menarik seluruh data siswa dari JSONBin ("Muat dari JSONBin"), menampilkan tabel rekap
   dan statistik, lalu mengekspor rekap sebagai CSV/JSON untuk evaluasi kelas.

Skor (persentase) dipetakan: ≥90 Sangat Baik, ≥75 Baik, ≥60 Cukup, <60 Perlu Penguatan.

## Log Git Push (dari awal hingga final)

Repository: `https://github.com/hendrazulpiadi/asement-cisco.git` (branch `main`)

| Hash | Tanggal | Keterangan |
|------|---------|------------|
| `b446412` | 2026-09-05 | Asesmen praktikum Cisco dasar |
| `7aed57f` | 2026-09-06 | Update endpoint Google Sheets web app |
| `6d4781f` | 2026-09-06 | Integrasi penyimpanan JSONBin (cloud) dengan Access Key |
| `c4ddbea` | 2026-09-06 | Tambah PIN akses Mode Rekap Guru |

## Cara Menjalankan

Buka `index.html` langsung di perangkat (double-click) atau host secara statis
(GitHub Pages, Netlify, dsb.). Tidak perlu instalasi atau build.

## Catatan Keamanan

- PIN rekap guru dan Access Key JSONBin tersimpan di kode (file publik). Untuk produksi
  skala besar, sebaiknya dipindah ke backend / environment terenkripsi.
- Bin JSONBin ber-visibility **private**; hanya dapat diakses dengan Access Key.