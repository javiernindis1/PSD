# Business Understanding

## 1. Latar Belakang Masalah

Identifikasi jenis burung berdasarkan suara merupakan topik yang penting
dalam bidang ekologi, konservasi lingkungan, dan pemantauan keanekaragaman hayati.
Metode identifikasi secara manual membutuhkan keahlian khusus,
waktu yang lama, serta tidak efisien jika jumlah data suara sangat besar.

Dengan berkembangnya teknologi pengolahan sinyal dan machine learning,
identifikasi suara burung dapat dilakukan secara otomatis
menggunakan data sinyal audio atau time-series.
Pendekatan ini diharapkan dapat membantu peneliti dan praktisi
dalam melakukan klasifikasi jenis burung
secara lebih cepat dan akurat.

---

## 2. Permasalahan Bisnis

Permasalahan utama yang dihadapi adalah:
- Sulitnya mengidentifikasi jenis burung secara manual hanya dari suara
- Keterbatasan waktu dan sumber daya manusia dalam analisis data suara
- Potensi kesalahan subjektif dalam identifikasi manual

Oleh karena itu, dibutuhkan sebuah sistem
yang mampu mengklasifikasikan jenis burung
secara otomatis berdasarkan karakteristik suara.

---

## 3. Tujuan Proyek

Tujuan dari proyek ini adalah:
1. Membangun model machine learning
   yang mampu mengklasifikasikan jenis burung
   berdasarkan sinyal suara (time-series)
2. Menggunakan fitur yang relevan (MFCC)
   untuk merepresentasikan karakteristik suara
3. Mengevaluasi performa model
   menggunakan metrik klasifikasi yang sesuai
4. Mengembangkan model yang siap
   untuk dideploy dalam aplikasi sederhana (Streamlit)

---

## 4. Ruang Lingkup Proyek

Ruang lingkup proyek ini meliputi:
- Dataset suara burung **DucksAndGeese**
- Klasifikasi multikelas (5 jenis burung)
- Ekstraksi fitur MFCC dari sinyal suara
- Pemodelan menggunakan Support Vector Machine (SVM)
- Evaluasi menggunakan data testing
- Deployment model dalam bentuk aplikasi berbasis web

Hal-hal yang **tidak termasuk** dalam proyek ini:
- Pengumpulan data audio baru
- Pelabelan manual data suara
- Penggunaan deep learning berskala besar

---

## 5. Kriteria Keberhasilan (Success Criteria)

Proyek ini dianggap berhasil apabila:
- Model mampu mencapai akurasi yang baik pada data testing
- Tidak terjadi bias prediksi terhadap kelas tertentu
- Model mampu memberikan prediksi yang konsisten
- Sistem dapat dijalankan kembali tanpa mengulang proses training
- Model dapat digunakan pada tahap deployment
  untuk melakukan prediksi data baru

---

## 6. Manfaat Proyek

Manfaat yang diharapkan dari proyek ini antara lain:
- Membantu proses identifikasi burung secara otomatis
- Mengurangi ketergantungan pada identifikasi manual
- Menjadi dasar pengembangan sistem klasifikasi audio lanjutan
- Memberikan studi kasus penerapan CRISP-DM
  pada permasalahan klasifikasi suara

---

## 7. Pendekatan Solusi

Pendekatan yang digunakan dalam proyek ini adalah:
1. Mengolah sinyal suara dalam bentuk time-series
2. Melakukan preprocessing dan ekstraksi fitur MFCC
3. Menggunakan algoritma SVM dengan kernel RBF
4. Mengevaluasi performa model secara kuantitatif
5. Menyajikan hasil dalam bentuk aplikasi sederhana

Pendekatan ini dipilih karena sesuai
untuk dataset berukuran kecil hingga menengah
dan memiliki performa yang baik
dalam tugas klasifikasi audio.

---

## 8. Kesimpulan Business Understanding

Berdasarkan analisis kebutuhan dan permasalahan,
penerapan machine learning untuk klasifikasi suara burung
merupakan solusi yang relevan dan efektif.

Dengan memanfaatkan fitur MFCC dan algoritma SVM,
proyek ini diharapkan dapat menghasilkan model
yang akurat, stabil, dan siap digunakan
pada aplikasi nyata.
