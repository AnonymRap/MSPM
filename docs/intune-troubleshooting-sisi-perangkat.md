# Intune: Troubleshooting dari Sisi Perangkat (Windows)

Dokumen ini menjelaskan cara memeriksa perangkat Windows yang bermasalah dengan Microsoft Intune: cek status join, cek enrollment, memaksa sync, dan membaca log. Gunakan saat policy, aplikasi, atau enrollment tidak berjalan di perangkat.

Terakhir diverifikasi: 24 November 2026 terhadap Microsoft Learn (lihat bagian Sumber di akhir dokumen).

## Intune: Urutan Cek Cepat di Perangkat

1. Pastikan perangkat terhubung ke internet.
2. Cek apakah perangkat sudah terdaftar di Entra ID dan Intune (bagian "Cek status join dengan dsregcmd" dan "Cek enrollment otomatis").
3. Lakukan sync manual (bagian "Memaksa sync dari perangkat").
4. Baca log Intune Management Extension (bagian "Lokasi log Intune Management Extension").
5. Cocokkan error dengan dokumen "Intune: Error Code Enrollment dan Aplikasi".

## Intune: Cek Status Join dengan dsregcmd

Perintah `dsregcmd /status` menampilkan status join perangkat ke Microsoft Entra ID (sebelumnya Azure AD).

Cara menjalankan:
- Buka Command Prompt atau PowerShell, jalankan `dsregcmd /status`.
- Jalankan dalam konteks user agar status user dan SSO valid.
- Untuk diagnostik dalam konteks SYSTEM, jalankan dari command prompt dengan hak administrator (elevated). KeySignTest juga membutuhkan hak administrator.

Arti field penting:

| Field | Arti |
|---|---|
| AzureAdJoined | YES jika perangkat join ke Microsoft Entra ID |
| DomainJoined | YES jika perangkat join ke domain Active Directory |
| EnterpriseJoined | YES jika join ke AD on-premises. Perangkat tidak bisa EnterpriseJoined sekaligus AzureAdJoined |
| DeviceAuthStatus | SUCCESS jika perangkat ada dan aktif di Entra ID. FAILED (Device is either disabled or deleted) jika perangkat dinonaktifkan atau dihapus |
| NgcSet | YES jika kunci Windows Hello diset untuk user yang sedang login |
| AzureAdPrt | YES jika ada Primary Refresh Token untuk user yang sedang login |

Kombinasi AzureAdJoined = YES dan DomainJoined = YES (EnterpriseJoined = NO) berarti perangkat Microsoft Entra hybrid joined.

Jika field URL MDM (MdmUrl) kosong, berarti MDM belum dikonfigurasi atau user tidak termasuk cakupan (scope) MDM enrollment. Catatan: adanya URL MDM tidak menjamin perangkat sudah dikelola MDM.

## Intune: Membaca Error pada dsregcmd (Hybrid Join Gagal)

Bagian Diagnostic Data muncul hanya jika perangkat domain-joined tetapi gagal Microsoft Entra hybrid join.

| Field | Arti |
|---|---|
| Error Phase | Tahap join yang gagal: pre-check, discover, auth, atau join |
| Client ErrorCode | Kode error klien (HRESULT) |
| Server ErrorCode | Kode error dari server, jika ada |
| Server Message | Pesan dari server |
| Https Status | Status HTTP dari server |
| Request ID | ID permintaan klien, berguna untuk mencocokkan dengan log server |

Petunjuk: error pada AD Connectivity Test biasanya menyebabkan gagal di fase pre-check. Error pada AD Configuration Test biasanya menyebabkan gagal di fase discover dengan kode 0x801c001d.

## Intune: Cek Enrollment Otomatis di Perangkat

Untuk memastikan perangkat sudah otomatis terdaftar (enrolled) ke Intune:

1. Buka Settings > Accounts > Access work or school.
2. Pilih akun yang tergabung, lalu pilih Info.
3. Di bagian Advanced Diagnostic Report, pilih Create Report.
4. Buka file MDMDiagReport di browser, lalu cari teks MDMDeviceWithAAD.
5. Jika teks itu ada, perangkat sudah terdaftar otomatis.

## Intune: Memaksa Sync dari Perangkat

Ada tiga cara memaksa perangkat check-in ke Intune:

- **Settings:** buka Settings > Accounts > Access work or school, pilih akun, lalu sync.
- **Company Portal:** buka aplikasi Company Portal > Settings > Sync. Cara ini memicu check-in MDM dan check-in Intune Management Extension (IME) sekaligus. Alternatif: Devices > Check Status.
- **Restart layanan IME:** buka Task Manager, cari IntuneManagementExtension di tab Services, klik kanan, pilih Restart.

Dari sisi admin, sync dilakukan lewat Intune admin center (lihat dokumen "Intune: Panduan Admin Center").

## Intune: Jadwal Check-in Windows

- Setelah enrollment: setiap 3 menit selama 15 menit, lalu setiap 15 menit selama 2 jam, kemudian sekitar setiap 8 jam.
- Check-in rutin (maintenance sync): sekitar setiap 8 jam. Perangkat hanya diizinkan satu maintenance sync setiap 6,5 jam.
- Setelah policy berubah: waktu bervariasi, dari segera sampai beberapa jam. Perangkat offline menerima perubahan pada sync berikutnya.
- Intune Management Extension (IME) memeriksa instalasi baru atau pembaruan setiap 8 jam, terpisah dari check-in MDM. Setelah Enrollment Status Page (ESP) atau Autopilot device preparation selesai, IME langsung memeriksa assignment aplikasi Win32 yang baru.

Sync manual mempercepat penerimaan policy tetapi tidak menjamin semua perubahan langsung diterapkan.

## Intune: Lokasi Log Intune Management Extension

Log IME ada di folder:

`C:\ProgramData\Microsoft\IntuneManagementExtension\Logs`

Buka dengan CMTrace.exe. File penting:

| File log | Fungsi |
|---|---|
| IntuneManagementExtension.log | Log utama: check-in, pemrosesan policy, pelaporan |
| AppWorkload.log | Aktivitas deployment aplikasi Win32 |
| AgentExecutor.log | Eksekusi script PowerShell |
| AppActionProcessor.log | Pengecekan deteksi dan applicability aplikasi |
| HealthScripts.log | Eksekusi remediation |
| ClientHealth.log | Kesehatan IME |

## Intune: Prasyarat Intune Management Extension (IME)

IME dibutuhkan untuk aplikasi Win32 dan script PowerShell. Syaratnya:
- IME versi 1.58.103.0 atau lebih baru (IME memperbarui dirinya otomatis).
- Windows yang didukung, tidak termasuk Windows in S mode.
- Perangkat join ke Microsoft Entra ID (hybrid joined atau registered).
- Perangkat sudah enrolled di Intune (GPO, manual, atau co-management). Pada perangkat co-managed, workload Apps harus Pilot Intune atau Intune agar aplikasi Win32 berjalan.
- Perangkat dapat menjangkau endpoint Intune lewat firewall atau proxy.

## Intune: IME Tidak Terunduh atau Aplikasi Tidak Terinstal

Periksa berurutan:
1. Perangkat join ke Microsoft Entra ID dan memenuhi prasyarat IME.
2. Script atau aplikasi Win32 sudah di-assign ke grup user atau perangkat yang benar.
3. Perangkat dapat menjangkau Intune (internet dan Windows Push Notification Services).
4. Perangkat tidak dalam S mode.
5. File `C:\Program Files (x86)\Microsoft Intune Management Extension\Microsoft.Management.Services.IntuneWindowsAgent.exe.config` tidak rusak atau diubah manual.
6. Aplikasi tidak diinstal di luar mekanisme otomatis Intune (script, instalasi manual, atau repackaging). Hanya instalasi otomatis saat sync yang didukung.
7. Jika proxy hanya diset per user: login dengan akun user, atau jalankan `bitsadmin /util /setieproxy` untuk mengatur proxy BITS.

Jika layanan aplikasi Microsoft Intune Windows Agent di Entra ID dinonaktifkan, payload yang ditargetkan ke user berhenti bekerja. Perbaikannya (menghapus service principal lewat Microsoft Graph) sebaiknya dilakukan oleh administrator yang paham Graph Explorer.

## Intune: Policy Menunjukkan Not Applicable atau Conflict

- **Not applicable:** pengaturan tidak didukung pada versi atau edisi Windows di perangkat (misalnya butuh Windows versi lebih baru, atau edisi Pro/Enterprise/Education, bukan Home).
- **Conflict:** dua policy mengatur setting yang sama dengan nilai berbeda. Konflik ditampilkan di Intune dan harus diselesaikan manual.

## Sumber

- Microsoft Learn, "Use the Intune Management Extension on Windows devices" (learn.microsoft.com/mem/intune/apps/intune-management-extension)
- Microsoft Learn, "Troubleshoot devices by using the dsregcmd command" (learn.microsoft.com/entra/identity/devices/troubleshoot-device-dsregcmd)
- Microsoft Learn, "Troubleshoot device profiles in Intune" (learn.microsoft.com/intune/device-configuration/troubleshoot-device-profiles)
- Microsoft Learn, "Sync devices" (learn.microsoft.com/mem/intune/remote-actions/device-sync)

Catatan: tampilan menu dan detail fitur Microsoft dapat berubah. Untuk keputusan production, verifikasi ke Microsoft Learn terbaru.
