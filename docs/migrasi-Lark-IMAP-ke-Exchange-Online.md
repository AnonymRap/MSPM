# Migrasi Mail Lark (IMAP) ke Exchange Online via Outlook

## Ringkasan Migrasi Mail Lark ke Exchange Online

Migrasi ini memindahkan isi email dari **Lark Mail** ke mailbox **Exchange Online** (email Microsoft 365). Lark diakses lewat protokol **IMAP**, dan **Outlook** dipakai sebagai perantara: akun Lark dan akun Exchange Online ditambahkan ke satu Outlook, lalu folder dan email dipindahkan dari akun Lark ke akun Exchange Online.

Alur singkat:

1. Aktifkan akses IMAP di Lark dan siapkan password khusus.
2. Tambahkan akun Exchange Online di Outlook.
3. Tambahkan akun Lark sebagai akun IMAP di Outlook.
4. Tunggu folder Lark selesai sinkron.
5. Pindahkan (copy) folder dari akun Lark ke mailbox Exchange Online.
6. Verifikasi jumlah email dan lampiran.
7. Jika domain ikut dipindah, lakukan cutover MX dan sinkron ulang email yang masuk selama transisi.

## Cakupan dan Batasan Migrasi IMAP

- IMAP hanya membawa **email** (folder dan pesan). **Kalender, kontak, dan tugas tidak ikut** dan perlu dipindahkan terpisah.
- Migrasi lewat Outlook dikerjakan **manual per user**, cocok untuk jumlah user sedikit. Untuk banyak user, pertimbangkan IMAP migration batch di Exchange admin center (Migration > Add migration batch > IMAP migration), yang juga hanya memindahkan email.
- Ukuran mailbox Lark harus muat di kuota Exchange Online (umumnya 50 GB untuk paket Business dan 100 GB untuk E3/E5, cek paket yang dipakai).

## Prasyarat Migrasi Lark IMAP ke Exchange Online

- Mailbox Exchange Online sudah aktif dan lisensi Microsoft 365 sudah di-assign ke user.
- Outlook desktop sudah terpasang (lihat dokumen Install M365 Apps).
- Admin Lark mengizinkan member mengakses Lark Mail lewat third-party email client, dan user membuat **password khusus** (generated password) di Lark untuk login dari aplikasi email. Password login biasa tidak dipakai di sini.
- Ruang disk PC cukup, karena Outlook menyimpan salinan lokal mailbox (file data) selama proses.
- Koneksi internet stabil, karena proses bisa berjalan lama untuk mailbox besar.

## Langkah 1: Siapkan Akses IMAP di Lark

1. Pastikan admin Lark sudah mengaktifkan akses third-party email client untuk organisasi.
2. Di Lark Mail milik user, buka pengaturan akses dari aplikasi email pihak ketiga dan buat password khusus untuk login IMAP. Simpan password ini.
3. Catat alamat server IMAP dan SMTP Lark yang tertera di halaman pengaturan tersebut.

Nilai umum yang biasa dipakai (verifikasi ulang di halaman pengaturan Lark milik organisasi sebelum dipakai):

| Setting | Nilai umum |
|---|---|
| Server IMAP (incoming) | imap.larksuite.com, port 993, SSL/TLS |
| Server SMTP (outgoing) | smtp.larksuite.com, port 465, SSL/TLS |
| Username | Alamat email lengkap |
| Password | Password khusus (generated password) dari Lark |

## Langkah 2: Tambahkan Akun Exchange Online di Outlook

1. Buka Outlook > **File** > **Add Account**.
2. Masukkan alamat email Microsoft 365 user, login, dan tunggu mailbox selesai dimuat.

## Langkah 3: Tambahkan Akun Lark sebagai IMAP di Outlook

1. Di Outlook, **File** > **Add Account**, masukkan alamat email Lark.
2. Buka **Advanced options** dan centang **Let me set up my account manually**, lalu pilih **IMAP**.
3. Isi server IMAP, port, dan metode enkripsi sesuai Langkah 1, lalu masukkan password khusus Lark.
4. Isi juga pengaturan SMTP bila diminta, lalu selesaikan pengaturan akun.

## Langkah 4: Tunggu Sinkron Folder Lark

Setelah akun Lark tampil di Outlook, tunggu semua folder dan email selesai sinkron. Untuk mailbox besar, proses ini bisa memakan waktu lama. Jangan menutup Outlook di tengah proses dan pastikan koneksi stabil.

## Langkah 5: Pindahkan Email dari Lark ke Exchange Online

**Opsi A: copy folder langsung di Outlook (disarankan)**

1. Klik kanan folder di akun Lark (mis. Inbox), pilih **Copy Folder**, lalu pilih mailbox Exchange Online sebagai tujuan.
2. Kerjakan bertahap per folder, dan untuk folder besar per rentang tanggal, supaya mudah diulang jika ada gangguan.
3. Gunakan **copy**, bukan move, sampai hasilnya terverifikasi. Hapus data Lark hanya setelah semuanya aman.

**Opsi B: lewat file PST**

1. Export folder Lark ke file PST: **File** > **Open & Export** > **Import/Export** > **Export to a file** > **Outlook Data File (.pst)**.
2. Import file PST tersebut ke mailbox Exchange Online lewat menu Import/Export yang sama.

## Langkah 6: Verifikasi Hasil Migrasi

- Bandingkan jumlah email per folder antara akun Lark dan Exchange Online.
- Cek sampel email lama: tanggal, pengirim, isi, dan lampiran bisa dibuka.
- Cek folder Sent dan Drafts, serta struktur folder buatan user.
- Minta user memeriksa email penting sebelum akses Lark ditutup.

## Langkah 7: Cutover Domain (jika domain email ikut dipindah)

Langkah ini hanya diperlukan jika domain email dialihkan dari Lark ke Microsoft 365.

1. Tambahkan dan verifikasi domain di Microsoft 365 admin center.
2. Ubah DNS: **MX** ke Exchange Online (formatnya `namadomain-com.mail.protection.outlook.com`), **SPF** menyertakan `include:spf.protection.outlook.com`, dan **Autodiscover** (CNAME ke `autodiscover.outlook.com`).
3. Selama DNS berpropagasi, sebagian email baru masih bisa masuk ke Lark. Setelah propagasi selesai, lakukan sinkron ulang: copy email baru dari Lark Inbox ke Exchange Online.
4. Setelah semuanya stabil, nonaktifkan akses email Lark sesuai kebijakan.

## Troubleshooting Migrasi Lark IMAP ke Exchange Online

| Kendala | Penyebab umum | Solusi |
|---|---|---|
| Outlook gagal login ke Lark IMAP | Memakai password login biasa, atau akses third-party client belum diaktifkan admin | Pakai password khusus (generated password), minta admin mengaktifkan akses third-party client |
| Server tidak bisa dihubungi | Alamat server atau port salah, firewall memblokir port 993/465 | Cek ulang server dan port dari halaman pengaturan Lark, uji dari jaringan lain |
| Folder Sent, Trash, atau Drafts tidak sesuai | Mapping folder IMAP belum tepat | Atur folder khusus di pengaturan akun IMAP (Account Settings > More Settings > Folders; nama menu bisa berbeda antar versi) |
| Email ganda di Exchange Online | Proses copy diulang ke folder yang sama | Hapus folder tujuan yang bermasalah dan ulangi dari awal, hindari copy dua kali |
| Proses sangat lama atau Outlook tidak merespons | Mailbox besar, koneksi tidak stabil | Pecah per folder atau per rentang tanggal, pastikan koneksi stabil, jangan menutup Outlook |
| Beberapa email gagal dipindahkan | Ukuran email atau lampiran terlalu besar | Cek batas ukuran pesan, simpan lampiran besar terpisah |
| Kalender dan kontak tidak ikut | IMAP hanya membawa email | Pindahkan kalender dan kontak secara terpisah (ekspor dari Lark jika tersedia, atau input ulang) |
| Outlook menjadi lambat setelah migrasi | File data lokal sangat besar | Kurangi pengaturan Mail to keep offline pada akun Exchange Online |

## Checklist Migrasi Lark IMAP ke Exchange Online

- [ ] Mailbox dan lisensi Exchange Online aktif
- [ ] Akses third-party client di Lark aktif dan password khusus dibuat
- [ ] Akun Lark (IMAP) dan Exchange Online tampil di Outlook
- [ ] Semua folder Lark selesai sinkron
- [ ] Email sudah di-copy per folder ke Exchange Online
- [ ] Jumlah email dan lampiran sudah diverifikasi
- [ ] Kalender dan kontak sudah ditangani terpisah
- [ ] Cutover DNS selesai dan sinkron ulang email susulan (jika domain dipindah)
