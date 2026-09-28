# Install Microsoft 365 Apps (M365 Apps)

## Ringkasan Install M365 Apps

Microsoft 365 Apps adalah paket aplikasi Office (Word, Excel, PowerPoint, Outlook, OneNote, dan aplikasi lain sesuai paket lisensi) yang diinstal di perangkat dan dilisensikan per user lewat akun Microsoft 365.

Ada tiga cara install M365 Apps:

| Metode | Cocok untuk | Dikerjakan oleh |
|---|---|---|
| Self-install lewat portal | Sedikit perangkat, user boleh install sendiri | User |
| Office Deployment Tool (ODT) | Banyak perangkat, tanpa Intune, atau butuh konfigurasi khusus | Admin / IT |
| Intune (Microsoft 365 Apps app) | Perangkat sudah enrolled di Intune, deployment terpusat | Admin Intune |

## Prasyarat Install M365 Apps

- Lisensi Microsoft 365 yang mencakup aplikasi desktop (mis. Apps for business, Business Standard/Premium, E3/E5) sudah di-assign ke user di M365 admin center (Users > Active users > Licenses and apps).
- Perangkat memakai Windows 10/11 yang masih didukung, dengan hak administrator lokal untuk install.
- Koneksi internet stabil. Proses install mengunduh data cukup besar dan butuh ruang disk yang cukup.
- Office lama (versi MSI, Office 2016/2019) sebaiknya dilepas dulu supaya tidak konflik.
- Untuk self-install: admin mengizinkan user menginstal sendiri (di admin center, cek pengaturan opsi instalasi Office di Org settings; nama menu bisa sedikit berbeda antar versi portal).

## Metode 1: Self-install Microsoft 365 Apps lewat portal

1. Buka https://www.office.com dan login dengan akun kerja (akun M365).
2. Klik **Install apps** (atau **Install and more** > **Install Microsoft 365 apps**).
3. Unduh installer, jalankan, lalu tunggu sampai selesai.
4. Buka salah satu aplikasi (mis. Word), login dengan akun kerja, dan pastikan aktivasi berhasil.

## Metode 2: Install M365 Apps dengan Office Deployment Tool (ODT)

1. Unduh Office Deployment Tool dari Microsoft Download Center, lalu extract sehingga muncul `setup.exe`.
2. Buat file `configuration.xml` (bisa dibuat lewat Office Customization Tool di config.office.com).
3. Jalankan di Command Prompt sebagai administrator:
   - `setup.exe /download configuration.xml` (opsional, untuk menyiapkan file install secara offline)
   - `setup.exe /configure configuration.xml`

Contoh `configuration.xml`:

```xml
<Configuration>
  <Add OfficeClientEdition="64" Channel="MonthlyEnterprise">
    <Product ID="O365BusinessRetail">
      <Language ID="MatchOS" />
    </Product>
  </Add>
  <Updates Enabled="TRUE" />
  <RemoveMSI />
  <Display Level="Full" AcceptEULA="TRUE" />
</Configuration>
```

Catatan: `O365BusinessRetail` untuk Microsoft 365 Apps for business, `O365ProPlusRetail` untuk Microsoft 365 Apps for enterprise. Baris `<RemoveMSI />` menghapus Office versi MSI yang lama.

## Metode 3: Deploy M365 Apps lewat Intune

1. Buka Intune admin center > **Apps** > **All apps** > **Add**.
2. Pilih tipe **Microsoft 365 Apps (Windows 10 and later)**.
3. Atur app suite: aplikasi yang disertakan, arsitektur (64-bit), update channel, dan opsi menghapus versi Office lain.
4. Assign ke grup user atau perangkat dengan tipe **Required**.
5. Pantau status di halaman aplikasi (Device install status). Perangkat harus sudah enrolled dan check-in ke Intune.

## Verifikasi Install M365 Apps

- Buka Word > **File** > **Account**. Pastikan tertulis produk Microsoft 365 Apps dan status **Product Activated**.
- Di https://www.office.com > My account, cek perangkat yang sudah terpasang.
- Untuk deployment Intune, pastikan status install di Intune admin center berubah menjadi **Installed**.

## Troubleshooting Install M365 Apps

| Kendala | Penyebab umum | Solusi |
|---|---|---|
| Install berhenti atau lambat di tengah jalan | Koneksi terputus, proxy atau firewall memblokir domain Microsoft, ruang disk kurang | Cek koneksi, izinkan URL dan IP Microsoft 365 di firewall/proxy, kosongkan disk, ulangi install |
| Konflik dengan Office lama | Office MSI atau versi lama masih terpasang | Uninstall lewat Settings > Apps, gunakan `<RemoveMSI />` di ODT, atau pakai Microsoft Support and Recovery Assistant (SaRA) |
| Muncul "Unlicensed Product" atau "Product Deactivated" | Lisensi belum di-assign, atau login memakai akun yang salah | Assign lisensi di admin center, sign out semua akun di Office, login ulang dengan akun kerja, tunggu beberapa menit |
| Tombol Install tidak muncul di portal | User tidak punya lisensi Apps, atau admin membatasi instalasi mandiri | Cek lisensi user dan pengaturan opsi instalasi di admin center |
| Deployment Intune status Failed atau Pending | Perangkat belum enrolled atau belum check-in, assignment salah grup | Sync perangkat, cek assignment, lihat log di `C:\ProgramData\Microsoft\IntuneManagementExtension\Logs` |
| Aplikasi tidak ter-update | Update channel atau policy update membatasi | Buka Account > Update Options > Update Now, atau cek policy update dari Intune/GPO |

## Checklist Install M365 Apps

- [ ] Lisensi user sudah di-assign
- [ ] Office lama sudah dilepas
- [ ] Install selesai tanpa error
- [ ] Login dan aktivasi berhasil di Word
- [ ] Outlook, Excel, dan PowerPoint terbuka normal
- [ ] Update channel sesuai standar perusahaan
