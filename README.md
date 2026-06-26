# PANDUAN EKSEKUSI PROYEK (README)
**Mata Kuliah:** Komputasi Awan (RKK401)
**Judul Proyek:** Kalkulator Cerdas Prediksi Harga Properti AI Menggunakan Arsitektur Event-Driven Microservices

---

### IDENTITAS MAHASISWA
* **Nama:** Nathanael Indra R P
* **NIM:** 163231004
* **Kelas:** RK – A1
* **Program Studi:** Teknik Robotika dan Kecerdasan Buatan
* **Fakultas:** Teknologi Maju dan Multidisiplin, Universitas Airlangga

---

### 1. DESKRIPSI SINGKAT SISTEM
Sistem ini merupakan aplikasi prediksi harga properti (real estat) berbasis *Machine Learning* (XGBoost) yang diimplementasikan menggunakan arsitektur **Event-Driven Microservices**. Sistem memisahkan beban komputasi secara fungsional ke dalam tiga layanan awan:
1.  **Frontend (Vercel / Local Browser):** Antarmuka pengguna (*Client-side*).
2.  **Message Broker (Firebase Realtime Database):** Menjembatani antrean data secara asinkron.
3.  **AI Inference Worker (Kaggle Cloud):** Mengeksekusi pemodelan *Machine Learning* dan memberikan hasil prediksi secara *real-time*.

---

### 2. STRUKTUR BERKAS (FILE)
Di dalam folder pengumpulan ini, terdapat berkas-berkas berikut:
* `Kalkulator_Harga_Properti.ipynb` : Skrip Python (Jupyter Notebook) yang berisi kode prapemrosesan data, pelatihan model XGBoost, dan *worker* layanan *cloud*.
* `index.html` : Berkas antarmuka web (Frontend).
* `train.csv` & `test.csv` : Dataset historis harga rumah yang digunakan untuk proses analisis.
* `Laporan_Project_Cloud_Computing.pdf` : Laporan komprehensif proyek.
* `README.md` : Panduan eksekusi sistem (berkas ini).

---

### 3. PANDUAN EKSEKUSI (STEP-BY-STEP)

Untuk menjalankan ulang sistem ini dan melakukan pengujian secara mandiri, mohon ikuti langkah-langkah berikut:

#### Langkah A: Menjalankan Backend AI Worker (Kaggle)
1. Buka *platform* **Kaggle** (https://www.kaggle.com) dan buat *Notebook* baru.
2. Unggah (*upload*) berkas `Kalkulator_Harga_Properti.ipynb` ke dalam *Notebook* tersebut melalui menu *File > Import Notebook*.
3. Unggah dataset `train.csv` dan `test.csv` melalui menu *Add Data* di panel sebelah kanan Kaggle.
4. *(Catatan: Kunci kredensial Firebase berformat `.json` umumnya telah diintegrasikan atau disertakan di dalam folder jika diperlukan untuk autentikasi koneksi).*
5. Pastikan fitur **Internet** pada Kaggle *Notebook* telah diaktifkan (melalui panel *Settings* di sebelah kanan).
6. Jalankan **Sel 1 (Cell 1)** untuk memulai proses analisis data, *Hyperparameter Tuning*, pelatihan model XGBoost, dan pengeksporan model (`.pkl`).
7. Setelah Sel 1 selesai, jalankan **Sel 2 (Cell 2)**. Sel ini akan berjalan terus-menerus (*infinite loop*) dan menampilkan status: `📡 AI XGBoost Standby. Terhubung ke Firebase. Menunggu request...`. **Biarkan sel ini tetap menyala**.

#### Langkah B: Menjalankan Frontend Web
1. Buka berkas `index.html` langsung menggunakan peramban web (*browser*) apa saja (seperti Google Chrome atau Mozilla Firefox).
   * *(Alternatif: Jika sistem telah di-deploy ke Vercel, Anda dapat langsung mengunjungi tautan URL Vercel yang telah disediakan di dalam laporan).*

#### Langkah C: Menguji Prediksi Real-Time
1. Pada halaman web yang telah terbuka, masukkan nilai spesifikasi properti pada kolom yang tersedia (Luas Bangunan, Jumlah Kamar Tidur, Jumlah Kamar Mandi, dan Kapasitas Garasi).
2. Klik tombol **"Mulai Prediksi"**.
3. Perhatikan halaman web. Status akan berubah menjadi "Meminta AI di Kaggle untuk menghitung...".
4. **Buka kembali *tab* Kaggle Notebook Anda**. Pada *log output* Sel 2, Anda akan melihat respons masuk secara instan: 
   `⬇️ Menerima request dari Web...` dan `⬆️ Hasil XGBoost dikirim: Rp ...`
5. **Kembali ke *tab* halaman web**, dan taksiran harga rumah akan langsung muncul di layar secara *real-time* tanpa perlu memuat ulang (*refresh*) halaman.

---

### 4. CATATAN PENILAIAN
Keberhasilan pengujian ini mendemonstrasikan efisiensi arsitektur *Cloud Computing* di mana peramban web lokal (*client*) tidak terbebani oleh proses komputasi *Machine Learning* yang berat, melainkan mendelegasikan tugas tersebut sepenuhnya kepada infrastruktur awan (Kaggle) melalui komunikasi *Event-Driven* (Firebase).
