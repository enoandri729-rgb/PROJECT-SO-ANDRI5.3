# PROJECT-SO-ANDRI5.3

## Processing user instructions  
- The user provided instructions for Project 3: Backup Automation Script.
</think>### Backup Automation Script

Berikut adalah panduan lengkap untuk membuat script batch (.bat) sederhana di Windows untuk mengotomasi backup file penting. Script ini akan membuat folder backup berdasarkan tanggal, menyalin file, dan memverifikasi hasil. Ini cocok untuk backup rutin file kuliah, pekerjaan, atau dokumen pribadi.

#### Langkah 1: Identifikasi File Penting
Tentukan file atau folder yang perlu di-backup. Contoh:
- File dokumen: `C:\Users\YourName\Documents\*.docx` (semua file Word).
- Folder gambar: `C:\Users\YourName\Pictures\*` (semua file di folder Pictures).
- Folder proyek: `D:\KuliahFiles\*` (dari Project 1 sebelumnya).
- Sesuaikan dengan kebutuhan Anda; pastikan path benar.

#### Langkah 2: Lokasi Backup
Script akan membuat folder backup di `D:\Backup` dengan subfolder berdasarkan tanggal (mis. `D:\Backup\2023-10-05`). Ini memudahkan pelacakan backup harian.

#### Langkah 3: Buat Script Batch
1. Buka Notepad.
2. Salin kode script berikut (sesuaikan path file sesuai kebutuhan Anda):
   ```
   @echo off
   echo Starting backup process...
   mkdir D:\Backup\%date:~-10,4%-%date:~-5,2%-%date:~-2,2%
   copy C:\Users\YourName\Documents\*.docx D:\Backup\%date:~-10,4%-%date:~-5,2%-%date:~-2,2%
   xcopy C:\Users\YourName\Pictures\* D:\Backup\%date:~-10,4%-%date:~-5,2%-%date:~-2,2%\Pictures\ /E /I /Y
   xcopy D:\KuliahFiles\* D:\Backup\%date:~-10,4%-%date:~-5,2%-%date:~-2,2%\KuliahFiles\ /E /I /Y
   echo Backup completed!
   pause
   ```
   - `%date:~-10,4%-%date:~-5,2%-%date:~-2,2%`: Format tanggal sebagai YYYY-MM-DD (mis. 2023-10-05).
   - `copy`: Untuk file spesifik (mis. *.docx).
   - `xcopy /E /I /Y`: Untuk menyalin folder lengkap (/E: subfolder, /I: buat folder jika belum ada, /Y: overwrite tanpa konfirmasi).
3. Simpan sebagai `backup_automation.bat` di folder yang mudah diakses (mis. Desktop).

#### Langkah 4: Jalankan Script
1. Klik dua kali file `backup_automation.bat` (atau jalankan via CMD: `backup_automation.bat`).
2. Script akan membuat folder backup dan menyalin file.
3. Tunggu hingga muncul pesan "Backup completed!".

#### Langkah 5: Verifikasi
Buka CMD dan gunakan `dir` untuk cek folder backup:
```
dir D:\Backup\%date:~-10,4%-%date:~-5,2%-%date:~-2,2%
```
- Pastikan file dan folder muncul. Jika ada error (mis. "File not found"), periksa path di script.

#### Tips Tambahan
- **Otomasi Lebih Lanjut**: Jadwalkan script dengan Task Scheduler Windows untuk berjalan otomatis harian (cari "Task Scheduler" di Start, buat task baru, pilih script sebagai action).
- **Keamanan**: Backup ke drive eksternal atau cloud (mis. tambahkan perintah untuk copy ke USB drive).
- **Modifikasi**: Tambahkan lebih banyak file/folder dengan baris `copy` atau `xcopy` tambahan. Untuk backup penuh, gunakan `robocopy` (lebih kuat dari xcopy).
- **Troubleshooting**: Jika tanggal tidak format dengan benar, ganti `%date%` dengan `%date:/=-%` untuk Windows versi lama.
- **Waktu Pengerjaan**: Sekitar 5-10 menit untuk setup awal, lalu otomatis.
