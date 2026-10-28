# nyuw

Aplikasi Android yang otomatis mematikan akses internet untuk aplikasi yang jarang dipakai.

Jika sebuah aplikasi tidak dibuka selama beberapa hari (bawaan 2 hari), nyuw mematikan data latar belakang, data seluler, dan Wi-Fi untuk aplikasi tersebut, sama seperti pengaturan manual di Info Aplikasi. Dengan begitu kuota dan baterai tidak terpakai oleh aplikasi yang sudah lama tidak dibuka.

| | |
|---|---|
| Paket | `com.nyuw.hans` |
| Versi | V1 |
| Target | Android 14 (API 34) |
| Minimum | Android 5.0 (API 21) |

## Fitur

- Mendeteksi aplikasi yang tidak dibuka dalam 1 sampai 30 hari (dapat diatur).
- Mematikan data latar belakang, data seluler, dan Wi-Fi untuk aplikasi target.
- Pencocokan tombol berdasarkan teks menu (Indonesia dan Inggris), bukan posisi layar, sehingga tidak terikat satu merek HP.
- Mode otomatis saat HP dibuka (maksimal 5 aplikasi sekali jalan, paling cepat tiap 6 jam). Dapat dimatikan.
- Mode manual: pilih sendiri aplikasi yang ingin dimatikan.
- Daftar pengecualian untuk aplikasi yang tidak boleh diubah.
- Pemulihan: internet aplikasi yang sudah dimatikan dapat dinyalakan kembali dari dalam nyuw.
- Log hasil setiap proses.
- Aplikasi sistem, keyboard, launcher, dan nyuw sendiri tidak pernah diproses.

## Cara kerja

1. Akses Penggunaan dipakai untuk mengetahui kapan terakhir sebuah aplikasi dibuka.
2. Layanan Aksesibilitas membuka halaman Info Aplikasi, masuk ke menu penggunaan data, lalu mengatur tombolnya.
3. Aplikasi yang berhasil diproses dicatat agar dapat dipulihkan.

## Instalasi

1. Unduh `nyuw-V1.apk` dari halaman Releases.
2. Pasang APK. Izinkan instalasi dari sumber tidak dikenal jika diminta.
3. Buka nyuw dan aktifkan dua izin: Akses Penggunaan dan Aksesibilitas.

### Android 13 ke atas

Aplikasi yang dipasang di luar Play Store dibatasi untuk Aksesibilitas. Jika pilihan nyuw berwarna abu-abu:

1. Buka Info Aplikasi nyuw.
2. Tekan titik tiga di kanan atas.
3. Pilih **Izinkan setelan terbatas**.
4. Kembali ke pengaturan Aksesibilitas dan aktifkan nyuw.

## Penggunaan

1. Atur batas hari tidak dipakai.
2. Tekan **Scan aplikasi jarang dipakai**.
3. Centang aplikasi yang akan dimatikan, lalu tekan **Matikan internet yang dicentang**.
4. Biarkan layar selama proses berjalan. Hasilnya tercatat di Log.
5. Untuk memulihkan, centang aplikasi pada daftar yang dimatikan lalu tekan **Pulihkan yang dicentang**.

## Izin

| Izin | Kegunaan |
|---|---|
| Akses Penggunaan | Mengetahui waktu terakhir aplikasi dibuka |
| Layanan Aksesibilitas | Mengatur tombol data di Info Aplikasi |
| Daftar aplikasi terpasang | Menampilkan aplikasi yang dapat dipilih |

## Privasi

nyuw tidak meminta izin Internet dan tidak mengirim data apa pun keluar dari perangkat. Pengaturan, daftar pengecualian, dan log disimpan secara lokal.

## Keterbatasan

- Pencocokan memakai teks menu bahasa Indonesia dan Inggris. Sebagian ROM dengan istilah atau logika tombol berbeda mungkin belum didukung penuh.
- Sebagian perangkat membatasi pembukaan Pengaturan dari latar belakang. Jika mode otomatis tidak berjalan, gunakan mode manual.
- Selama proses berjalan, layar berpindah ke halaman Pengaturan.

Jika ada perangkat yang gagal, buat Issue dengan tangkapan layar halaman penggunaan data aplikasi tersebut dan isi Log nyuw.

## Struktur source

    app/src/main/
    |-- AndroidManifest.xml
    |-- java/com/nyuw/hans/
    |   |-- MainActivity.java   tampilan dan kontrol
    |   |-- NyuwService.java    layanan aksesibilitas (otomatisasi)
    |   |-- Apps.java           deteksi aplikasi jarang dipakai
    |   `-- Store.java          pengaturan, pengecualian, log
    `-- res/                    ikon, teks, konfigurasi aksesibilitas
