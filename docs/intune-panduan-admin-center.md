# Intune: Panduan Langkah di Intune Admin Center

Dokumen ini berisi langkah menu (klik per klik) di Microsoft Intune admin center untuk tugas admin yang paling sering: sync perangkat, membuat compliance policy, meng-assign aplikasi, dan membuat update ring Windows.

Terakhir diverifikasi: 24 November 2026 terhadap Microsoft Learn (lihat Sumber di akhir dokumen). Nama menu dapat berubah mengikuti pembaruan portal.

## Intune: Cara Sync Perangkat dari Admin Center

1. Login ke Microsoft Intune admin center.
2. Pilih Devices > All devices.
3. Pilih perangkat dari daftar.
4. Di bagian atas halaman overview perangkat, pilih ikon Sync.
5. Pilih Yes untuk konfirmasi.

Fungsi: memaksa perangkat check-in ke Intune untuk menerima tindakan atau policy yang tertunda, tanpa menunggu jadwal check-in berikutnya. Pada Windows, sync menjalankan sinkronisasi atas permintaan untuk beberapa workload: pemrosesan configuration policy, pembaruan deteksi dan status deployment aplikasi, serta pemrosesan script dan remediation.

Progres dapat dilihat di tab Device sync status pada halaman overview perangkat (berlaku untuk Windows dan iOS/iPadOS, dan membutuhkan toggle Preview new device view aktif).

## Intune: Cara Membuat Compliance Policy Windows

Prasyarat: langganan Intune dan perangkat Windows sudah enrolled (status compliance hanya terlihat pada perangkat yang enrolled). Microsoft Entra ID P1 atau P2 hanya dibutuhkan jika memakai Conditional Access.

Langkah:
1. Login ke Intune admin center.
2. Pilih Devices.
3. Di bawah Manage devices, pilih Compliance, lalu Create policy.
4. Platform: pilih Windows 10 and later, lalu Create.
5. Tab Basics: isi Name dan Description (opsional).
6. Tab Compliance settings: atur persyaratan. Opsional: di Custom Compliance, set ke Require (butuh script deteksi dan file JSON yang sudah diunggah lebih dulu).
7. Tab Actions for noncompliance: tindakan bawaan adalah Mark device noncompliant. Jadwalnya dapat diubah (misalnya satu hari) dan dapat ditambah tindakan seperti mengirim email ke user.
8. Tab Scope tags (opsional).
9. Tab Assignments: pilih Add groups. Policy Windows dapat di-assign ke user atau perangkat.
10. Tab Review + create: periksa lalu pilih Create.

Intune mengevaluasi user atau perangkat target saat mereka check-in.

## Intune: Cara Meng-assign Aplikasi ke Grup

1. Login ke Intune admin center.
2. Pilih Apps > All Apps.
3. Pilih aplikasi yang akan di-assign.
4. Di menu Manage, pilih Properties.
5. Scroll ke bagian Properties dan pilih Assignments.
6. Pilih Add Group.
7. Pilih assignment type.
8. Pilih Included Groups, pilih grup, lalu Select.
9. Pilih OK di panel Assign.
10. Untuk mengecualikan grup, pilih Exclude Groups, pilih grup, lalu Select dan OK.
11. Di panel Assignments aplikasi, pilih Save.

## Intune: Jenis Assignment Aplikasi

| Jenis | Arti |
|---|---|
| Required | Aplikasi diinstal pada perangkat di grup terpilih |
| Available for enrolled devices | User dapat menginstal aplikasi dari aplikasi atau situs Company Portal |
| Available with or without enrollment | Untuk user yang perangkatnya tidak enrolled. User harus punya lisensi Intune |
| Uninstall | Aplikasi dihapus dari perangkat di grup terpilih, hanya jika sebelumnya diinstal Intune lewat assignment Required atau Available dengan deployment yang sama |

Aturan penting:
- Intune mendukung assignment ke nested group.
- Satu grup tidak boleh ditarget oleh beberapa intent assignment untuk aplikasi yang sama. Membuat konflik assignment tidak disarankan.
- Jika grup di Microsoft Entra terhapus sementara (soft-deleted), assignment-nya tidak berlaku sampai grup dipulihkan.
- Assignment Available umumnya hanya valid untuk grup user, bukan grup perangkat. Pengecualian: aplikasi Win32 (dan beberapa tipe Android Enterprise) dapat di-assign Available ke grup user atau perangkat.

## Intune: Cara Membuat Update Ring Windows

Menu: Devices > By platform > Windows > Manage updates > Windows updates.

1. Pilih tab Update rings > Create profile.
2. Basics: isi nama dan deskripsi, lalu Next.
3. Update ring settings: atur pengaturan Update dan User experience, lalu Next. Update ring mengatur periode penundaan (deferral), pengaturan restart, deadline, active hours, dan notifikasi user.
4. Scope tags (opsional): pilih tag, lalu Next.
5. Assignments: pilih Select groups to include, dan opsional Select groups to exclude, lalu Next.
6. Review + create: periksa lalu Create.

Catatan:
- Assign update ring ke grup perangkat. Grup perangkat tidak membutuhkan user login agar policy berlaku.
- Perangkat yang dikelola Windows Autopatch biasanya tidak perlu diberi update ring kustom, karena Autopatch membuat dan mengelola ring sendiri.
- Feature update policy membutuhkan layanan Microsoft Account Sign-In Assistant (wlidsvc) aktif dan berjalan. Jika dinonaktifkan, Windows Update tidak menawarkan feature update.
- Menghapus ring menghentikan penegakan pengaturan oleh Intune, tetapi perangkat mempertahankan pengaturan terakhirnya.
- Windows Enterprise LTSC dan IoT Enterprise LTSC tidak mendukung beberapa kontrol feature update (misalnya pause feature update dan feature update deferral period). Quality update tetap didukung.
- Praktik umum: terapkan bertahap (pilot, kelompok terbatas, kelompok lebih luas, seluruh organisasi).

## Intune: Pemeriksaan Setelah Perubahan Policy atau Aplikasi

1. Sync perangkat (admin center atau Company Portal).
2. Cek status policy atau aplikasi di admin center.
3. Jika status belum berubah, cek last check-in perangkat dan assignment grup.
4. Jika ada error, lihat dokumen "Intune: Error Code Enrollment dan Aplikasi" dan "Intune: Troubleshooting dari Sisi Perangkat".

## Sumber

- Microsoft Learn, "Sync devices" (learn.microsoft.com/mem/intune/remote-actions/device-sync)
- Microsoft Learn, "Create a compliance policy in Microsoft Intune" (learn.microsoft.com/mem/intune/protect/create-compliance-policy)
- Microsoft Learn, "Assign apps to groups with Microsoft Intune" (learn.microsoft.com/mem/intune/apps/apps-deploy)
- Microsoft Learn, "Manage Windows 10 and 11 software updates in Intune" (learn.microsoft.com/mem/intune/protect/windows-10-update-rings)

Catatan: nama menu dan fitur dapat berubah. Verifikasi ke Microsoft Learn terbaru untuk keputusan production.
