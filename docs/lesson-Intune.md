KNOWLEDGE BASE
MICROSOFT INTUNE
Purpose: Knowledge base teks untuk Retrieval-Augmented Generation (RAG) LLM.
Target: IT Helpdesk, Endpoint Management, System Administrator, Security Operations, dan pembelajaran
Microsoft Intune.
Basis: Dokumentasi Microsoft Learn yang ditinjau pada September 2026. Detail lisensi dan fitur dapat berubah
mengikuti perkembangan produk.
1. MICROSOFT INTUNE OVERVIEW
Microsoft Intune adalah layanan cloud Microsoft untuk mengelola perangkat, aplikasi, dan data organisasi. Intune
mendukung pengelolaan endpoint melalui kemampuan Mobile Device Management (MDM) dan Mobile Application
Management (MAM).
Intune dapat digunakan untuk mengelola Windows, macOS, iOS/iPadOS, Android, dan Linux pada skenario yang
didukung. Administrator dapat melakukan enrollment, konfigurasi perangkat, deployment aplikasi, compliance
management, endpoint security, update management, remote actions, reporting, dan troubleshooting.
Intune terintegrasi erat dengan Microsoft Entra ID. Integrasi ini memungkinkan identitas pengguna dan perangkat
digunakan sebagai bagian dari kontrol akses organisasi.
Konsep utama: Device Enrollment, Device Configuration, Compliance, Application Management, Endpoint
Security, Conditional Access, Windows Autopilot, Reporting, RBAC, dan Remote Device Actions.
2. INTUNE ADMIN CENTER
Microsoft Intune dikelola melalui Intune admin center. Administrator menggunakan portal ini untuk membuat policy,
mengelola perangkat dan aplikasi, melihat status compliance, melakukan tindakan remote, serta memonitor dan
melakukan troubleshooting.
Alur administrasi umum adalah: siapkan tenant → konfigurasi identitas dan enrollment → buat configuration profile
→ buat compliance policy → konfigurasi endpoint security → deploy aplikasi → enroll perangkat → monitor dan
remediasi.
3. DEVICE ENROLLMENT
Device enrollment adalah proses mendaftarkan perangkat ke Microsoft Intune sehingga perangkat dapat
menerima policy, configuration profile, application deployment, dan management actions.
Pada Windows, metode enrollment dapat mencakup automatic enrollment, Windows Autopilot, BYOD/user
enrollment, bulk enrollment, Group Policy, dan co-management dengan Configuration Manager.
Automatic enrollment memungkinkan perangkat melakukan enrollment ke Intune ketika memenuhi kondisi tertentu
seperti join atau register ke Microsoft Entra ID. Metode ini dapat digunakan pada skenario BYOD, bulk enrollment,
Group Policy, Windows Autopilot, dan co-management.
Setelah enrollment, perangkat memperoleh hubungan management dengan layanan Intune dan dapat menerima
konfigurasi yang ditargetkan kepadanya.
Masalah umum enrollment: user tidak memiliki lisensi yang sesuai, MDM authority/configuration belum benar,
automatic enrollment belum aktif, device restriction policy menolak enrollment, masalah Microsoft Entra
registration/join, atau perangkat belum melakukan sinkronisasi.
4. DEVICE CONFIGURATION PROFILES
Configuration profile digunakan untuk menerapkan konfigurasi dan pengaturan perangkat. Administrator dapat
membuat profile berdasarkan platform dan kebutuhan organisasi.
Settings Catalog menyediakan banyak pengaturan yang dapat dikonfigurasi melalui Intune. Configuration profile
dapat digunakan untuk mengatur security settings, system behavior, restrictions, browser settings, network
settings, privacy settings, dan konfigurasi perangkat lainnya.
Policy biasanya ditargetkan kepada user group atau device group. Administrator perlu memperhatikan konflik
apabila beberapa policy mengatur setting yang sama.
Prinsip troubleshooting: periksa assignment, status profile, scope group, konflik policy, platform applicability,
dan status check-in perangkat.
5. COMPLIANCE POLICY
Compliance policy menentukan persyaratan yang harus dipenuhi perangkat agar dianggap compliant. Contohnya
dapat mencakup password/security requirements, encryption, firewall, antivirus/antimalware, minimum OS version,
dan kondisi keamanan lain yang didukung platform.
Compliance status dapat digunakan sebagai signal untuk Microsoft Entra Conditional Access. Dengan integrasi ini,
organisasi dapat mensyaratkan perangkat memenuhi kondisi tertentu sebelum mengakses resource organisasi.
Compliance policy berbeda dari configuration profile. Configuration profile menerapkan pengaturan; compliance
policy mengevaluasi apakah perangkat memenuhi persyaratan.
Contoh: Configuration profile mengaktifkan firewall. Compliance policy dapat memeriksa apakah firewall aktif. Jika
perangkat tidak memenuhi requirement, status compliance dapat menjadi noncompliant.
6. CONDITIONAL ACCESS
Microsoft Entra Conditional Access adalah mekanisme kontrol akses berbasis kondisi. Conditional Access dapat
menggunakan berbagai signal seperti user, device, application, location, sign-in risk, dan device compliance.
Dalam integrasi dengan Intune, status compliance perangkat dapat digunakan sebagai signal untuk menentukan
apakah akses ke resource organisasi diizinkan atau memerlukan tindakan tambahan.
Contoh kebijakan: user mencoba mengakses Microsoft 365 → Conditional Access mengevaluasi kondisi →
perangkat harus compliant dan/atau user harus melakukan MFA → akses diberikan jika kondisi terpenuhi.
Conditional Access membutuhkan lisensi Microsoft Entra yang sesuai. Microsoft menyatakan Conditional Access
memerlukan Microsoft Entra ID P1 atau P2; Microsoft 365 Business Premium juga menyediakan kemampuan
Conditional Access.
7. APPLICATION MANAGEMENT
Intune dapat digunakan untuk menambahkan, mengonfigurasi, deploy, update, dan menghapus aplikasi pada
perangkat yang dikelola.
Aplikasi dapat ditargetkan kepada user atau device melalui assignment. Administrator perlu menentukan apakah
aplikasi bersifat Required, Available, atau menggunakan tipe assignment lain yang tersedia untuk platform dan
aplikasi tersebut.
Jika aplikasi tidak terinstall, pemeriksaan awal meliputi: apakah aplikasi sudah ditargetkan, apakah device/user
termasuk group assignment, apakah device sudah check-in, apakah requirement aplikasi terpenuhi, apakah
dependency tersedia, dan apakah terdapat error installation.
Intune juga mendukung pengelolaan aplikasi tanpa enrollment melalui Mobile Application Management untuk
skenario tertentu.
8. APP PROTECTION POLICY / MAM
App Protection Policy digunakan untuk melindungi data organisasi pada level aplikasi. Pendekatan ini
memungkinkan perlindungan data pada aplikasi yang didukung tanpa selalu membutuhkan full device enrollment.
Contoh kontrol app protection dapat mencakup pembatasan copy/paste, penyimpanan data organisasi, transfer
data ke aplikasi lain, penggunaan aplikasi yang tidak disetujui, dan persyaratan akses aplikasi.
MAM sangat berguna untuk skenario BYOD karena organisasi dapat menerapkan kontrol terhadap data
perusahaan tanpa harus mengelola seluruh perangkat pribadi dengan tingkat kontrol yang sama seperti perangkat
corporate-owned.
9. WINDOWS AUTOPILOT
Windows Autopilot adalah teknologi deployment Windows yang membantu mengotomatisasi provisioning dan
enrollment perangkat organisasi.
Autopilot dapat menggunakan Windows yang sudah terpasang dari OEM sehingga organisasi tidak selalu perlu
membuat custom OS image. Saat perangkat menjalani proses Out-of-Box Experience, konfigurasi Autopilot dapat
mengarahkan perangkat untuk terhubung dengan organisasi dan melakukan enrollment ke Intune.
Windows Autopilot membutuhkan konfigurasi enrollment yang sesuai. Administrator perlu menyiapkan device
identity, Autopilot profile, automatic enrollment, dan assignment yang diperlukan.
Tujuan utama: mengurangi pekerjaan manual saat provisioning perangkat baru dan memberikan konfigurasi
standar organisasi.
10. ENDPOINT SECURITY
Endpoint security di Intune menyediakan policy khusus untuk membantu mengamankan endpoint. Area yang
dapat dikelola mencakup antivirus, firewall, attack surface reduction, account protection, disk encryption, endpoint
detection and response, dan security settings lain yang didukung.
Endpoint security policy sebaiknya dirancang berdasarkan kebutuhan organisasi dan tidak hanya mengandalkan
satu policy. Administrator perlu menguji policy pada pilot group sebelum rollout lebih luas.
Intune juga dapat berintegrasi dengan Microsoft Defender for Endpoint untuk memberikan signal keamanan
tambahan dan workflow remediation.
11. SECURITY BASELINES
Security baseline adalah kumpulan pengaturan keamanan yang telah dipilih sebelumnya berdasarkan
rekomendasi keamanan Microsoft. Administrator dapat menggunakan baseline sebagai starting point kemudian
menyesuaikannya dengan kebutuhan organisasi.
Security baseline bukan pengganti seluruh security architecture. Setting baseline tetap perlu diuji karena
kebutuhan aplikasi, user, dan lingkungan organisasi dapat berbeda.
Salah satu fungsi baseline adalah membantu organisasi menerapkan konfigurasi keamanan secara lebih
konsisten.
12. WINDOWS UPDATE MANAGEMENT
Intune dapat digunakan untuk mengelola update Windows melalui policy seperti update rings dan mekanisme
update management yang tersedia.
Update policy digunakan untuk menentukan bagaimana dan kapan perangkat menerima update. Administrator
perlu memperhatikan deployment rings, restart behavior, deadlines, deferral, dan kebutuhan testing.
Praktik umum adalah melakukan deployment secara bertahap: pilot → kelompok terbatas → kelompok lebih luas
→ seluruh organisasi.
13. DEVICE ACTIONS
Intune menyediakan remote actions untuk membantu administrasi dan lifecycle management perangkat. Tindakan
yang tersedia bergantung pada platform, enrollment method, dan konfigurasi.
Contoh tindakan yang umum adalah sync, restart, lock, wipe, retire, dan tindakan lain yang tersedia pada platform.
Perbedaan penting: Retire biasanya digunakan untuk menghapus management/organizational data sesuai
skenario tanpa melakukan reset penuh perangkat, sedangkan Wipe digunakan untuk melakukan
penghapusan/reset perangkat sesuai opsi yang dipilih.
Sebelum melakukan tindakan destruktif seperti wipe, administrator harus memastikan perangkat, user, data, dan
kebutuhan recovery telah diverifikasi.
14. RBAC DAN SCOPE TAGS
Role-Based Access Control (RBAC) mengatur hak akses administrator di Intune. Administrator sebaiknya
diberikan permission sesuai kebutuhan tugasnya menggunakan prinsip least privilege.
Scope tags membantu membatasi atau mengorganisasi objek yang dapat dilihat atau dikelola oleh administrator
tertentu sesuai desain administrasi organisasi.
Praktik yang baik adalah menghindari penggunaan Global Administrator untuk pekerjaan operasional sehari-hari
apabila role yang lebih terbatas sudah mencukupi.
15. MICROSOFT ENTRA ID INTEGRATION
Microsoft Entra ID menyediakan identity foundation yang terintegrasi dengan Intune. User dan device identity
dapat digunakan untuk enrollment, assignment, authentication, dan access control.
Microsoft Entra join, registration, dan hybrid join memiliki skenario yang berbeda. Administrator harus menentukan
model identity yang sesuai dengan architecture organisasi.
Group di Microsoft Entra dapat digunakan untuk menargetkan policy, application, configuration profile, dan
berbagai assignment Intune.
16. REPORTING DAN MONITORING
Monitoring Intune dilakukan dengan melihat device status, policy status, application status, compliance status,
enrollment status, dan audit information.
Ketika troubleshooting, jangan hanya melihat status perangkat. Periksa juga user, group membership, policy
assignment, last check-in, policy conflict, application requirement, dan error message/code.
Audit logs dapat membantu mengetahui aktivitas administratif seperti perubahan policy atau konfigurasi.
17. DEVICE CHECK-IN DAN SYNC
Device check-in adalah komunikasi antara perangkat yang dikelola dan layanan Intune. Policy, configuration,
application information, dan management commands bergantung pada komunikasi ini.
Jika perubahan policy belum terlihat pada perangkat, langkah awal adalah memastikan device memiliki koneksi
internet, status enrollment masih aktif, dan perangkat melakukan sync.
Manual sync dapat membantu mempercepat penerimaan policy, tetapi tidak menjamin semua perubahan
langsung diterapkan.
18. TROUBLESHOOTING FRAMEWORK
Gunakan urutan berikut ketika menangani masalah Intune:
1. Identifikasi user dan device yang bermasalah.
2. Pastikan device terdaftar dan enrolled dengan benar.
3. Periksa last check-in.
4. Periksa group membership.
5. Periksa policy/application assignment.
6. Periksa status policy atau application.
7. Periksa conflict dan applicability.
8. Periksa error code dan log yang tersedia.
9. Lakukan sync atau remediasi yang sesuai.
10. Verifikasi hasil setelah remediation.
11. Dokumentasikan root cause dan resolution.
19. TROUBLESHOOTING: APLIKASI TIDAK TERINSTALL
Problem: Aplikasi yang ditargetkan melalui Intune tidak muncul atau tidak terinstall.
Possible causes: assignment salah, device/user tidak masuk group, device belum check-in, requirement tidak
terpenuhi, dependency gagal, aplikasi tidak kompatibel, atau proses instalasi menghasilkan error.
Verification: periksa assignment, group membership, application status, device status, requirement, dependency,
dan error detail.
Resolution: perbaiki assignment atau requirement, lakukan sync, kemudian monitor kembali application
installation status.
20. TROUBLESHOOTING: DEVICE NONCOMPLIANT
Problem: Device menunjukkan status Noncompliant.
Possible causes: satu atau lebih compliance requirement tidak terpenuhi, device belum melakukan check-in,
policy belum diterapkan, atau terdapat kondisi keamanan yang tidak sesuai.
Verification: buka compliance status dan identifikasi requirement yang gagal. Kemudian periksa konfigurasi
perangkat dan status policy.
Resolution: perbaiki kondisi yang gagal, lakukan sync/check-in, lalu verifikasi status compliance kembali.
21. TROUBLESHOOTING: POLICY TIDAK TERAPLIKASI
Problem: Configuration profile tidak diterapkan.
Possible causes: assignment tidak tepat, device tidak termasuk target, platform tidak sesuai, setting conflict,
device belum check-in, atau policy tidak applicable.
Verification: periksa assignment status, device/user group, platform, profile status, conflict, dan last check-in.
Resolution: perbaiki assignment atau policy, hilangkan conflict jika diperlukan, lalu lakukan sync dan verifikasi.
22. BEST PRACTICES
Gunakan pilot group sebelum deployment besar. Pisahkan policy berdasarkan fungsi. Gunakan naming
convention yang konsisten. Gunakan group assignment secara terstruktur. Terapkan least privilege untuk
administrator. Dokumentasikan perubahan policy. Monitor deployment setelah perubahan. Uji policy pada
perangkat yang representatif sebelum production rollout.
Untuk security policy, hindari perubahan massal tanpa testing karena perubahan konfigurasi dapat memengaruhi
akses, aplikasi, user experience, dan keamanan perangkat.
23. CONTOH NAMING CONVENTION
Configuration profile: CFG-WIN11-Baseline-Standard
Compliance policy: CMP-WIN11-Standard
Application: APP-M365-Required
Security policy: SEC-WIN11-Firewall
Update ring: UPD-WIN11-Pilot
Group: GRP-INTUNE-WIN11-Pilot
Format penamaan dapat disesuaikan dengan standar organisasi.
24. SCENARIO: LAPTOP BARU
Scenario: Perusahaan membeli laptop Windows baru.
Flow: Device identity disiapkan → Windows Autopilot profile ditetapkan → user menjalankan OOBE → device
terhubung ke organisasi → automatic enrollment berjalan → configuration profile diterapkan → security policy
diterapkan → aplikasi Required di-deploy → compliance dievaluasi → Conditional Access dapat menggunakan
compliance sebagai signal akses.
Tujuan: mengurangi konfigurasi manual dan memberikan baseline konfigurasi yang konsisten.
25. SCENARIO: BYOD
Scenario: User menggunakan laptop atau smartphone pribadi untuk mengakses resource perusahaan.
Organisasi dapat memilih full device management atau pendekatan app protection/MAM sesuai platform,
kebutuhan keamanan, dan policy organisasi.
Pada skenario MAM, fokus perlindungan dapat berada pada data organisasi di dalam aplikasi yang didukung,
bukan mengambil alih seluruh perangkat.
26. SCENARIO: DEVICE HILANG
Jika perangkat organisasi hilang, administrator harus memverifikasi identitas device dan user terlebih dahulu.
Kemudian administrator dapat menggunakan remote action yang sesuai dengan kebijakan organisasi, misalnya
lock atau wipe jika tersedia dan diperlukan.
Untuk perangkat yang menyimpan data sensitif, keputusan remote action harus mengikuti incident response
procedure organisasi.
27. INTUNE DAN ZERO TRUST
Intune dapat menjadi bagian dari pendekatan Zero Trust dengan menyediakan informasi dan kontrol terhadap
endpoint. Prinsip Zero Trust yang umum adalah verify explicitly, use least privilege, dan assume breach.
Intune sendiri bukan keseluruhan implementasi Zero Trust. Ia merupakan salah satu komponen endpoint
management dan security yang dapat bekerja bersama Microsoft Entra, Defender, Microsoft 365, dan layanan
keamanan lainnya.
28. FAQ
Apa itu Microsoft Intune?
Microsoft Intune adalah layanan cloud untuk mengelola perangkat, aplikasi, dan data organisasi.
Apa perbedaan MDM dan MAM?
MDM berfokus pada pengelolaan perangkat. MAM berfokus pada pengelolaan dan perlindungan data pada
aplikasi.
Apakah Intune hanya untuk Windows?
Tidak. Intune mendukung berbagai platform seperti Windows, macOS, iOS/iPadOS, Android, dan Linux pada
skenario yang didukung.
Apa fungsi Compliance Policy?
Compliance Policy mengevaluasi apakah perangkat memenuhi persyaratan keamanan yang ditentukan
organisasi.
Apa fungsi Configuration Profile?
Configuration Profile menerapkan pengaturan atau konfigurasi tertentu ke perangkat atau user.
Apa hubungan Intune dengan Conditional Access?
Intune dapat memberikan status compliance perangkat sebagai signal yang digunakan Microsoft Entra Conditional
Access untuk membuat keputusan akses.
Apa itu Windows Autopilot?
Windows Autopilot membantu mengotomatisasi provisioning dan enrollment perangkat Windows organisasi.
Mengapa policy tidak masuk ke device?
Penyebab dapat berupa assignment, group membership, platform applicability, conflict, enrollment, atau device
check-in.
Apa yang harus diperiksa jika aplikasi tidak terinstall?
Periksa assignment, group membership, device check-in, requirement, dependency, application status, dan error
code.
29. RAG RETRIEVAL GUIDANCE
Untuk RAG LLM, setiap knowledge chunk sebaiknya memiliki konteks yang cukup untuk dipahami tanpa
bergantung pada chunk lain.
Gunakan metadata seperti: category, topic, platform, problem_type, keywords, source, dan last_reviewed.
Pertanyaan user sebaiknya dipetakan ke intent seperti Overview, Enrollment, Compliance, Configuration,
Application, Security, Autopilot, Conditional Access, Reporting, atau Troubleshooting.
Untuk troubleshooting, retrieval sebaiknya memprioritaskan chunk yang mengandung Problem, Possible Causes,
Verification, Resolution, dan Prevention.
Jangan membuat LLM menganggap informasi yang sudah berubah sebagai fakta permanen. Untuk informasi
seperti licensing, supported platforms, UI menu, feature availability, dan preview features, tambahkan tanggal
review dan gunakan dokumentasi Microsoft terbaru sebagai sumber verifikasi.
30. SUMBER RESMI
Dokumentasi utama Microsoft Intune: Microsoft Learn — Microsoft Intune documentation.
Dokumentasi deployment dan enrollment: Microsoft Learn — Intune deployment and enrollment guides.
Dokumentasi Conditional Access: Microsoft Learn — Microsoft Entra Conditional Access.
Dokumentasi licensing: Microsoft Learn — Microsoft Intune licensing plans and options.
Dokumentasi security: Microsoft Learn — Protect data and devices with Microsoft Intune.
Catatan: Knowledge base ini dirancang sebagai dasar RAG dan bukan pengganti dokumentasi resmi. Detail fitur,
licensing, platform support, dan antarmuka admin dapat berubah. Untuk keputusan production, verifikasi terhadap
Microsoft Learn terbaru.
