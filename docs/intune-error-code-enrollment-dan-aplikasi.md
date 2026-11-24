# Intune: Error Code Enrollment dan Instalasi Aplikasi

Dokumen ini berisi daftar kode error Microsoft Intune yang sering muncul saat enrollment perangkat Windows, Windows Autopilot, dan instalasi aplikasi, lengkap dengan penyebab dan solusinya. Cari berdasarkan kode error (misalnya 0x80180014) atau teks pesan.

Terakhir diverifikasi: 24 November 2026 terhadap Microsoft Learn (lihat Sumber di akhir dokumen).

PERINGATAN: Beberapa solusi mengubah registry. Backup registry terlebih dahulu dan lakukan hanya oleh administrator.

## Intune: Error 0x8007064c "The machine is already enrolled"

Penyebab: komputer sudah pernah terdaftar, merupakan hasil clone dari komputer yang sudah terdaftar, atau masih ada sertifikat akun dari akun sebelumnya.

Solusi:
1. Hapus sertifikat Intune yang diterbitkan oleh Sc_Online_Issuing dari Local Computer > Personal > Certificates.
2. Hapus `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\OnlineManagement` beserta subkey-nya.
3. Daftarkan ulang (re-enroll).
4. Jika masih gagal, hapus `KEY_CLASSES_ROOT\Installer\Products\6985F0077D3EEB44AB6849B5D7913E95`, lalu daftarkan ulang.

## Intune: Error 8018000a "The device is already enrolled"

Penyebab: user lain sudah mendaftarkan perangkat ke Intune atau menggabungkannya ke Microsoft Entra ID. Di Settings > Accounts > Work Access tertulis "Another user on the system is already connected to a work or school."

Solusi: login sebagai user lain tersebut, hapus akun work or school di Settings > Accounts > Work Access, sign out, login dengan akun Anda, lalu enroll atau join ulang.

## Intune: Pesan "This account is not allowed on this phone"

Penyebab: user tidak memiliki lisensi Intune yang valid.

Solusi: berikan lisensi Intune yang valid kepada user, lalu enroll ulang.

## Intune: Pesan "MDM Terms of Use endpoint is not correctly configured"

Penyebab: (a) MDM untuk Microsoft 365 dan Intune dipakai bersamaan dan user tidak punya lisensi Intune atau Office 365, atau (b) URL terms and conditions MDM di Microsoft Entra ID kosong atau salah.

Solusi:
- Berikan lisensi Intune atau Microsoft 365 di Microsoft 365 admin center, atau
- Di Entra ID > Mobility (MDM and MAM) > Microsoft Intune, pilih Restore default MDM URLs, pastikan URL MDM terms of use adalah `https://portal.manage.microsoft.com/TermsofUse.aspx`, lalu simpan.

## Intune: Error 80180026 saat Join Entra ID

Penyebab: perangkat Windows 10 di-join ke Microsoft Entra ID saat MDM automatic enrollment aktif dan agen Intune PC terpasang.

Solusi: set MDM User scope ke None di Entra ID > Mobility (MDM and MAM) > Microsoft Intune, atau uninstall agen Intune PC.

## Intune: Error 0x80cf4017 "The software cannot be installed" atau "account certificate is not valid"

Penyebab: perangkat lunak klien sudah usang.

Solusi: unduh perangkat lunak klien dari Admin > Client Software Download di admin.manage.microsoft.com, lalu instal.

## Intune: Error 0x80180014 "Your organization does not support this version of Windows"

Penyebab: Windows MDM enrollment dinonaktifkan di tenant Intune.

Solusi: di Intune admin center buka Devices > Enrollment restrictions, pilih restriction tipe perangkat, lalu Properties > Edit (Platform settings), set Windows (MDM) ke Allow, kemudian Review + Save.

## Intune: Error "A setup failure has occurred during bulk enrollment"

Penyebab: akun Microsoft Entra di provisioning package (Package_GUID) tidak diizinkan menggabungkan perangkat ke Entra ID.

Solusi: di Entra ID > Devices > Device Settings, set "Users may join devices to Microsoft Entra ID" ke All, atau ke Selected lalu tambahkan akun provisioning package.

## Intune: Auto MDM Enroll Failed, Event 76, Error 0x8018002b

Penyebab: UPN memakai domain yang belum diverifikasi atau tidak routable seperti `.local`, atau MDM user scope diset None.

Solusi:
- Untuk UPN: ubah UPN suffix di Active Directory ke domain valid (misalnya contoso.com), lalu tunggu sinkronisasi atau jalankan Delta Sync.
- Untuk scope: set MDM user scope ke All, atau Some dengan grup terpilih, dan set MAM User scope ke None.

## Intune: Error Windows Autopilot

| Error | Penyebab | Solusi |
|---|---|---|
| "An error occurred while creating Autopilot profile" | Template nama perangkat tidak memenuhi aturan, misalnya `%serial%` huruf kecil | Nama maksimal 15 karakter, hanya huruf, angka, dan tanda hubung, bukan semua angka, tanpa spasi. Gunakan `%SERIAL%` atau `%RAND:<jumlah digit>%` |
| "Something went wrong. OOBEIDPS" | Proxy, firewall, atau perangkat jaringan memblokir Identity Provider | Izinkan akses internet yang dibutuhkan Autopilot (lihat Windows Autopilot networking requirements) |
| HRESULT 0x80180022 (enrollment Autopilot gagal) | Perangkat memakai Windows Home | Upgrade ke Windows Pro atau lebih tinggi |
| 0x801C03EA "Registering your device for mobile management (Failed: 3)" | TPM mendukung versi 2.0 tetapi belum di-upgrade ke 2.0 | Upgrade TPM ke 2.0. Jika masih gagal, cek apakah perangkat ada di dua grup dengan Autopilot profile berbeda, lalu hapus assignment ganda |
| 0x800705b4 "Securing your hardware" | Perangkat tidak punya TPM 2.0 fisik (TPM virtual dan TPM 1.2 tidak bekerja dengan self-deploying mode), atau versi Windows di bawah build 1709 (build 1809 untuk Entra hybrid join) | Pastikan ada TPM 2.0 fisik dan versi Windows memenuhi syarat |
| 0x80070774 "Something went wrong" | Biasanya Entra hybrid join dengan "Assign user" di Autopilot profile, atau objek Azure AD device milik objek Autopilot sudah dihapus | Di Devices > Windows > Windows devices, pilih perangkat, pilih Unassign user, lalu pastikan profile Hybrid Entra Autopilot ter-assign. Jika ada Event ID 30132 di log ODJ Connector Service, delegasikan izin objek komputer pada OU. Alternatif: hapus objek Autopilot lalu impor ulang hash |
| Enrollment Status Page (ESP) timeout | ESP melacak aplikasi Microsoft Store for Business, dan Conditional Access mewajibkan perangkat compliant untuk All Cloud apps dan Windows | Targetkan compliance policy Intune ke perangkat agar compliance ditentukan sebelum logon, atau pakai offline licensing untuk aplikasi store |

## Intune: Error Instalasi Aplikasi 0x87D1041C (aplikasi tidak terdeteksi)

Arti: instalasi sukses tetapi aplikasi tidak terdeteksi. Menurut dokumentasi, aplikasi sempat berhasil di-deploy, lalu dihapus (uninstall) oleh user. Penyebab lain yang disebut: informasi identitas paket tidak cocok dengan laporan perangkat, atau versi produk MSI yang memperbarui diri di luar Intune tidak cocok.

Tindakan resmi: minta user menginstal ulang dari Company Portal. Aplikasi Required akan terinstal ulang otomatis saat check-in berikutnya.

Petunjuk praktik (bukan dari tabel resmi): untuk aplikasi Win32 yang terinstal tetapi dilaporkan gagal, periksa juga detection rule aplikasi di Intune dan baca AppWorkload.log (lihat dokumen "Intune: Troubleshooting dari Sisi Perangkat").

## Intune: Error Aplikasi Paket Windows (Sideloading dan Signature)

| Kode | Arti | Tindakan |
|---|---|---|
| 0x80073CFF atau 0x80CF201C | Butuh sistem dengan sideloading aktif. Paket harus ditandatangani dengan signature tepercaya dan perangkat memiliki policy AllowAllTrustedApps aktif | Pastikan signature tepercaya dan policy AllowAllTrustedApps aktif |
| 0x80073CF0 | Paket tidak ditandatangani, atau nama publisher tidak cocok dengan subject sertifikat | Cek event log AppxPackagingOM |
| 0x80073CF3 | Paket konflik dengan paket terinstal, dependency tidak ditemukan, atau arsitektur prosesor tidak sesuai | Cek event log AppXDeployment-Server |
| 0x80073CFB | Paket sudah terinstal dan instalasi ulang diblokir | Naikkan nomor versi, build ulang dan tanda tangani ulang paket, hapus paket lama untuk semua user |
| 0x8000FFFF | Error tak terduga saat instalasi | Periksa log instalasi |

## Intune: Perilaku Retry Aplikasi

Aplikasi yang gagal dengan kode error yang bisa diulang (retryable) tetap tersedia untuk perangkat. Aplikasi dengan kode error yang tidak bisa diulang (nonretryable) harus menunggu tujuh hari sebelum tersedia lagi untuk perangkat.

## Sumber

- Microsoft Learn, "Troubleshoot Windows device enrollment errors in Intune" (learn.microsoft.com/troubleshoot/mem/intune/device-enrollment/troubleshoot-windows-enrollment-errors)
- Microsoft Learn, "App install error codes" (learn.microsoft.com/mem/intune/apps/app-install-error-codes)
- Microsoft Learn, "Sync devices" (learn.microsoft.com/mem/intune/remote-actions/device-sync)

Catatan: daftar ini tidak mencakup semua kode error. Detail dapat berubah. Verifikasi ke Microsoft Learn terbaru untuk keputusan production.
