# Eksplorasi Data

## 2.1 Tipe Data
Dataset **digitalkorlantas** dibangun dari berkas CSV ke tabel `digitalkorlantas` di PostgreSQL. Atribut diklasifikasikan sebagai berikut (gantikan contoh sesuai hasil Anda):
- **Numerik** – mis. `[isi: kolom numerik kunci]`; dipakai untuk metrik, agregasi, dan model.  
- **Temporal** – mis. `[isi: kolom tanggal/waktu]`; dipakai untuk tren, seasonality, dan jendela waktu.  
- **Kategorikal** – mis. `[isi: jenis_layanan/kanal/status]`; dipakai untuk frekuensi, proporsi, dan fitur dummy/target encoding.  
- **Boolean** – nilai ya/tidak; dipakai sebagai indikator sederhana.  
- **Teks** – mis. `keterangan`; dipakai untuk catatan, dapat dibersihkan/diturunkan menjadi fitur (opsional).

> **Catatan penamaan**: seluruh nama kolom dinormalisasi menjadi *snake_case* dan dijaga unik (mis. `jenis_layanan`, `waktu_transaksi`).

---

## 2.2 Kualitas Data

### 2.2.1 Outlier Analysis (Metode IQR)
Definisi:
\[
\mathrm{IQR}=Q3-Q1,\quad \mathrm{LowerBound}=Q1-1.5\,\mathrm{IQR},\quad \mathrm{UpperBound}=Q3+1.5\,\mathrm{IQR}.
\]
Temuan (isi sesuai data Anda):
- Kolom **[isi kolom numerik]**: **[isi jumlah]** observasi `< LowerBound`, **[isi jumlah]** observasi `> UpperBound`.
- Interpretasi awal: **[mis. durasi sangat panjang karena eskalasi / nilai tak logis (negatif untuk kuantitas)]**.

Kebijakan:
1) **Valid secara bisnis** → pertahankan, gunakan **robust scaling** / **winsorization**.  
2) **Tidak logis** → koreksi jika ada rujukan, atau keluarkan pada tahap *preparation*.

### 2.2.2 Konsistensi Data (terkait keberadaan)
Memeriksa koherensi **keberadaan/ketiadaan** antar‑kolom dan aturan bisnis:
- **Ketergantungan keberadaan**: jika `kolom_A` **ada/terisi**, maka `kolom_B` **wajib ada** (contoh: jika `jenis_layanan` = *X*, maka `biaya` tidak boleh null).  
- **Mutual exclusivity**: atribut yang semestinya **saling eksklusif** tidak boleh terisi bersamaan (contoh: `kanal_online` vs `kanal_luring`).  
- **Urutan waktu**: `waktu_mulai ≤ waktu_selesai`; nilai yang melanggar diklasifikasi anomali.  
- **Domain & kamus kode**: nilai kategori harus termasuk daftar yang disepakati; variasi ejaan/kapitalisasi dinormalisasi (*lowercase*, trim, pemetaan sinonim).  
- **Duplikasi**: baris identik penuh → dihapus; duplikasi parsial pada kunci bisnis → ditelaah manual.

Ringkasan pelanggaran keberadaan (isi dengan angka):
- **[aturan 1]**: ditemukan **[n]** kasus.  
- **[aturan 2]**: ditemukan **[n]** kasus.  
Tindakan: normalisasi, perbaikan nilai, atau eksklusi sesuai dampak analitis.

### 2.2.3 Missing Values
Rekapitulasi (isi dari hasil Anda):
- Kolom dengan *missing* tertinggi: **[top‑3 kolom & persentase]**.
- Pola *missing* bersyarat: **[mis. kolom_B sering kosong saat kolom_A kategori tertentu]**.

Kebijakan penanganan:
- **< 5%** → imputasi sederhana (median/modus) atau hapus baris jika non‑kritis.  
- **5–30%** → imputasi berbasis aturan/domain atau model‑based bila fitur penting.  
- **> 30–40%** → evaluasi kegunaan; pertimbangkan *drop* jika tidak esensial.  
- *Empty string/whitespace* pada kolom teks disetarakan menjadi **NULL**.

### 2.2.4 Lain‑lain (dll)
- **Encoding**: seluruh pipeline menggunakan **UTF‑8**; karakter non‑ASCII (termasuk emoji) dipertahankan kecuali mengganggu proses, dalam hal itu dilakukan pembersihan terarah.  
- **Rentang nilai**: pastikan tidak ada angka negatif untuk besaran yang semestinya non‑negatif (jumlah, durasi, biaya).  
- **Panjang teks**: batasi panjang ekstrem; hilangkan karakter kontrol/tidak tercetak.  
- **Indeks & kunci teknis** (opsional): tambahkan `PRIMARY KEY` dan indeks pada kolom waktu/kategori utama untuk efisiensi kueri.

---

## 2.3 Ringkasan
- Struktur data telah diidentifikasi (numerik, temporal, kategorikal, boolean, teks) dan siap dijadikan basis rekayasa fitur.  
- Kualitas data dievaluasi melalui **IQR outlier**, **konsistensi keberadaan antar‑kolom**, **missing values**, serta aspek lain (encoding, duplikasi, domain nilai).  
- Tindak lanjut pada **Data Preparation**: normalisasi kategori, imputasi *missing*, penanganan outlier (robust/winsorization), perbaikan pelanggaran aturan keberadaan, serta penambahan indeks bila diperlukan.
