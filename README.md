# 🏡 Kalkulator Cerdas Prediksi Harga Properti AI
**Proyek Akhir Komputasi Awan (RKK401) - Arsitektur Event-Driven Microservices**

## 👥 Identitas Kelompok (RK-A1)
* **NATHANAEL INDRA R P** (163231004)
* **RIDHOILLAH RACHMANSYAH** (163231011)

## 📌 Deskripsi Proyek
Proyek ini adalah implementasi konsep **Cloud Computing (Microservices & MLOps)**. Kami membangun sistem kecerdasan buatan berbasis web untuk memprediksi harga properti berdasarkan dataset Kaggle menggunakan algoritma **XGBoost**. 

Sistem ini menghindari arsitektur monolitik dan mengadopsi pemisahan fungsional:
1.  **Frontend (Vercel/PaaS):** Antarmuka web statis yang sangat ringan.
2.  **Message Broker (Firebase BaaS):** Mengelola antrean *request* secara asinkron (*Event-Driven*).
3.  **Backend AI (Kaggle IaaS):** *Worker* yang berjalan di cloud untuk melakukan *load* model ML dan mengeksekusi komputasi berat.

---

## 📂 Struktur Folder Pengumpulan
Sesuai dengan ketentuan tugas, folder ini berisi:
* `/Dataset` : Berisi `train.csv` dan `test.csv` (Dataset Kaggle asli).
* `Kaggle_Backend_XGBoost.ipynb` : Skrip utama Python untuk *data preprocessing*, *training*, *hyperparameter tuning*, dan *Real-time AI Worker*.
* `index.html` : Skrip antarmuka web (Frontend UI).
* `Laporan_Project_Cloud_Computing.pdf` : Laporan lengkap analisis dan pembahasan arsitektur cloud.
* `firebase-key.json` : File kredensial (kunci) untuk mengakses broker Firebase kami. *(Penting untuk koneksi Worker)*

---

## 🚀 Cara Menjalankan Ulang Sistem (Reproduce) Secara Mandiri

Bapak/Ibu Dosen dapat menjalankan ulang sistem ini secara utuh dengan mengikuti 2 tahapan berikut:

### TAHAP 1: Menyalakan Backend AI di Kaggle (Worker)
1. Buka [Kaggle](https://www.kaggle.com/) dan buat *Notebook* baru, atau cukup unggah (import) file `Kaggle_Backend_XGBoost.ipynb` yang kami lampirkan.
2. Unggah file dataset (`train.csv` & `test.csv`) ke dalam environment Kaggle tersebut.
3. Unggah file kredensial `firebase-key.json` yang kami lampirkan ke dalam environment Kaggle.
4. Sesuaikan *path* dataset dan file JSON di dalam kode *Notebook* sesuai dengan letak file di Kaggle Anda.
5. **Jalankan Cell 1 (Training & Export):** Cell ini akan membersihkan data, melatih AI dengan XGBoost, mencari parameter terbaik (*tuning*), mengevaluasi metrik (MAE & R2), lalu mengekspor model menjadi file `xgboost_harga_rumah_tuned.pkl`.
6. **Jalankan Cell 2 (AI Worker Server):** Setelah Cell 1 selesai, jalankan Cell 2. Cell ini akan terus berputar (*infinite running loop*) dan bertindak sebagai server. Anda akan melihat log konfirmasi:  
   `📡 AI XGBoost Standby. Terhubung ke Firebase. Menunggu request...`

### TAHAP 2: Menggunakan Frontend Web (Client)
1. Buka file `index.html` menggunakan peramban (browser) apa pun (Chrome/Edge/Firefox). Sebagai alternatif, Bapak/Ibu juga dapat mengakses *live URL* Vercel kami di: `[MASUKKAN_URL_VERCEL_ANDA_DI_SINI]`
2. Masukkan spesifikasi rumah pada form yang disediakan (misal: Luas 1500, Kamar 3, Kamar Mandi 2, Garasi 2).
3. Klik tombol **"Mulai Prediksi"**.
4. **Perhatikan *split screen* (Layar Web & Layar Kaggle):** * Di browser web, teks akan berubah menjadi menunggu respons AI.
   * Di tab Kaggle (Tahap 1), akan muncul log secara seketika (*real-time*) bahwa data berhasil ditarik, diolah ke dalam model XGBoost, dan dikirim kembali.
   * Di browser web, hasil estimasi harga (dalam Rupiah) akan langsung ter-render di layar tanpa perlu *refresh* halaman.

---
*Proyek ini mendemonstrasikan efektivitas komputasi awan dalam mendelegasikan beban proses Machine Learning tingkat lanjut dari sisi pengguna ke ekosistem infrastruktur awan.*
