# KB-EDR-001 - Device Tidak Muncul di Microsoft Defender Portal Setelah Onboarding

Kategori: Microsoft Defender for Endpoint (MDE) - EDR Endpoint. Artikel KB-EDR-001: Device Tidak Muncul di Microsoft Defender Portal Setelah Onboarding.

## KB-EDR-001 · 1. Metadata Artikel

- **KB ID:** KB-EDR-001
- **Article Title:** Device Tidak Muncul di Microsoft Defender Portal Setelah Onboarding
- **Category:** Endpoint Security
- **Product:** Microsoft Defender for Endpoint
- **Scope:** Windows Client / Windows Server
- **Severity:** Medium / High sesuai dampak
- **Owner:** Endpoint Security / EDR Operation
- **Status:** Draft for Review
- **Version:** 1.0
- **Review Cycle:** Mengikuti governance KB internal
- **Keywords:** Device Tidak Muncul di Microsoft Defender Portal Setelah Onboarding

## KB-EDR-001 · 2. Issue / Problem Description

Endpoint telah menjalani onboarding, namun device belum terlihat pada inventory Microsoft Defender portal. Microsoft menyatakan bahwa jika onboarding selesai tetapi device belum muncul pada Devices list setelah satu jam, kondisi tersebut dapat mengindikasikan masalah onboarding atau connectivity.

### KB-EDR-001 · Potential / Business Impact

- Status proteksi/reporting endpoint belum dapat diverifikasi.
- Deployment success tidak boleh disimpulkan hanya dari eksekusi script/GPO.

## KB-EDR-001 · 3. Governance & Policy Context

- Pastikan OS dan prerequisite onboarding sesuai baseline yang disetujui.
- Gunakan deployment method yang telah ditetapkan dalam design implementasi.
- Hindari offboard/re-onboard sebagai langkah awal tanpa evidence.

## KB-EDR-001 · 4. Resolution / Standard Workaround

1. Validasi device pada Microsoft Defender portal.
2. Konfirmasi deployment method yang digunakan: GPO, Intune, script, atau metode lain yang disetujui.
3. Jika memakai GPO, pastikan konfigurasi onboarding diterima endpoint; console GPO sendiri tidak membuktikan onboarding endpoint sukses.
4. Validasi connectivity ke service Microsoft Defender yang diwajibkan oleh design.
5. Jalankan MDE Client Analyzer bila diperlukan untuk evidence diagnostik.
6. Setelah remediation, validasi ulang device pada portal.

### KB-EDR-001 · Validation / Success Criteria

- Device muncul pada portal.
- Onboarding state dan endpoint health sesuai acceptance criteria project.

### KB-EDR-001 · Evidence Required

- Hostname, OS/build, onboarding method.
- Screenshot portal dan endpoint.
- Connectivity result dan Client Analyzer output bila digunakan.

### KB-EDR-001 · Rollback / Safety Note

Jika remediation melibatkan perubahan konfigurasi, policy, onboarding state, service, atau device object, ikuti change control yang berlaku. Hentikan perubahan bila menimbulkan dampak baru dan kembalikan konfigurasi ke baseline terakhir yang disetujui jika rollback tersedia.

## KB-EDR-001 · 5. Communication & Soft Skill Guidance

### KB-EDR-001 · Communication ke End User

"Tim IT sedang melakukan validasi status onboarding Microsoft Defender for Endpoint. Perangkat tetap dapat digunakan kecuali terdapat instruksi lanjutan dari tim IT."

### KB-EDR-001 · Communication ke Customer / IT Admin

"Ditemukan kondisi status onboarding Microsoft Defender for Endpoint. Tim sedang memvalidasi konfigurasi, connectivity, endpoint health, dan evidence terkait sebelum menentukan remediation berikutnya."

- Pisahkan symptom, suspected cause, dan confirmed root cause.
- Jangan menyimpulkan penyebab sebelum evidence tersedia.
- Dokumentasikan perubahan konfigurasi dan hasil validasi.
- Gunakan bahasa netral dan berorientasi pemulihan layanan.

## KB-EDR-001 · 6. Escalation Path & Related Links

| **Level** | **Responsibility / Evidence** |
|---|---|
| L1 Team Rollout/Enrollment | Collect hostname, user, OS/build, screenshot, waktu kejadian, network/VPN status. |
| L2 Technical Consultans | Validasi portal state, onboarding, policy, sensor/service, connectivity, logs. |
| L3 Security / Infrastructure | Validasi GPO, Intune, proxy/firewall, policy conflict, platform configuration. |
| Microsoft Support | Escalate setelah prerequisite, configuration, connectivity, endpoint state, dan diagnostic evidence telah divalidasi. |

Microsoft references:

- Troubleshoot Defender for Endpoint onboarding: https://learn.microsoft.com/en-us/defender-endpoint/troubleshoot-onboarding
- Onboard devices to Defender for Endpoint: https://learn.microsoft.com/en-us/defender-endpoint/onboarding
