# ⚖️ Dataset Putusan Narkotika – PN Mataram

Dataset dokumen putusan pengadilan perkara **Pidana Khusus – Narkotika dan Psikotropika** dari **Pengadilan Negeri Mataram**, dikumpulkan dari [Direktori Putusan Mahkamah Agung RI](https://putusan3.mahkamahagung.go.id/direktori.html) untuk keperluan mata kuliah **Temu Kembali Informasi (TKI)**.

Dokumen putusan bersifat terbuka dan tidak terikat HaKI, sehingga dapat dipakai sebagai korpus untuk eksperimen *information retrieval*, *text mining*, dan NLP hukum berbahasa Indonesia.

## 📁 Struktur Repository

```
Dataset-Narkotika_XXX_YYY/
├── Dataset/
│   ├── Narkotika.zip          # 5 dokumen putusan (PDF)
│   └── Overview/
│       └── Overview.xlsx      # ringkasan 50 putusan
└── README.md
```

## 📊 Ringkasan Dataset

| Atribut | Keterangan |
|---|---|
| Sumber | Direktori Putusan Mahkamah Agung RI |
| Kategori | Pidana Khusus › Narkotika dan Psikotropika |
| Lembaga peradilan | Pengadilan Negeri Mataram (`PN Mtr`) |
| Jenis perkara | `Pid.Sus` – tingkat pertama |
| Dokumen PDF | 5 putusan (`Narkotika.zip`) |
| Data ringkasan | 50 putusan (`Overview.xlsx`) |
| Bahasa | Indonesia |
| Format | PDF (dokumen), XLSX (ringkasan) |

Lima PDF pada `Narkotika.zip` adalah bagian dari 50 putusan yang diringkas pada `Overview.xlsx` (No 1, 13, 25, 38, 50 pada kolom `No`).

## 🧾 Struktur `Overview.xlsx`

| Kolom | Isi |
|---|---|
| `No` | Nomor urut |
| `No Putusan` | Nomor perkara, mis. `77/Pid.Sus/2026/PN Mtr` |
| `Lembaga Peradilan` | Pengadilan yang memutus |
| `Barang Bukti` | Daftar barang bukti yang ditetapkan dalam amar putusan |
| `Amar Putusan` | Isi diktum setelah kata *MENGADILI* hingga sebelum *Demikianlah diputuskan* |

Sheet kedua, `Daftar Dataset (5 PDF)`, memetakan 5 putusan ke nama file PDF-nya.

## 🛠️ Cara Pembuatan

Ringkasan dibuat otomatis oleh `Tugas2_TKI_Ekstraksi_Putusan.ipynb`:

1. Teks tiap PDF diekstrak dengan `pdftotext`.
2. Noise bawaan situs (watermark, header *Direktori Putusan*, footer *Halaman x dari y*, teks *Disclaimer*) dibuang.
3. Nomor putusan dan lembaga diambil dari kepala putusan; amar diambil dari blok `MENGADILI:`; barang bukti diambil dari butir *Menetapkan barang bukti berupa*.
4. Hasil disusun menjadi `Overview.xlsx` dan 5 PDF dikemas menjadi `Narkotika.zip`.

## 🔎 Contoh Penggunaan

```python
import pandas as pd

df = pd.read_excel("Dataset/Overview/Overview.xlsx", sheet_name="Overview")
print(df.shape)                                   # (50, 5)
print(df[df["Barang Bukti"].str.contains("sabu", case=False)].shape[0])
```

## ⚠️ Catatan

- Ekstraksi memakai *regular expression*, sehingga sebagian kecil teks (mis. salah ketik pada dokumen asli) mengikuti apa adanya.
- Dokumen berasal dari sumber publik Mahkamah Agung RI; nama terdakwa dalam dokumen sudah sebagaimana dipublikasikan di sumbernya.
- Dataset ini untuk tujuan akademik.

## 👥 Kelompok

| Nama | NIM |
|---|---|
| Fauzil Adhim | 202310370311364 |
| Farrel Juan Abimanyu | 202310370311368 |