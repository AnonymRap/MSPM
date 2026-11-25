# KB-EDR-003 - GPO Onboarding Microsoft Defender for Endpoint Tidak Ter-apply

Kategori: Microsoft Defender for Endpoint (MDE) - EDR Endpoint. Artikel KB-EDR-003: GPO Onboarding Microsoft Defender for Endpoint Tidak Ter-apply.

## KB-EDR-003 · 1. Metadata Artikel

- **KB ID:** KB-EDR-003
- **Article Title:** GPO Onboarding Microsoft Defender for Endpoint Tidak Ter-apply
- **Category:** Endpoint Security
- **Product:** Microsoft Defender for Endpoint
- **Scope:** Windows Client / Windows Server
- **Severity:** Medium / High sesuai dampak
- **Owner:** Endpoint Security / EDR Operation
- **Status:** Draft for Review
- **Version:** 1.0
- **Review Cycle:** Mengikuti governance KB internal
- **Keywords:** GPO Onboarding Microsoft Defender for Endpoint Tidak Ter-apply

## KB-EDR-003 · 2. Issue / Problem Description

Endpoint yang ditargetkan untuk onboarding melalui Group Policy belum menerima atau menjalankan konfigurasi onboarding.

### KB-EDR-003 · Potential / Business Impact

- Device tidak dapat dipastikan onboard ke EDR.
- Rollout batch dapat tertahan.

## KB-EDR-003 · 3. Governance & Policy Context

- Perubahan GPO mengikuti change control dan scope OU/security filtering yang disetujui.
- Jangan menonaktifkan security control lain untuk memaksa onboarding.

## KB-EDR-003 · 4. Resolution / Standard Workaround

1. Konfirmasi device masuk scope GPO yang benar.
2. Validasi policy processing pada endpoint dan deployment package/configuration yang digunakan.
3. Periksa hasil onboarding pada endpoint, karena Group Policy console tidak menunjukkan keberhasilan akhir onboarding device.
4. Validasi prerequisite dan connectivity.
5. Kumpulkan diagnostic evidence bila onboarding tetap gagal.

### KB-EDR-003 · Validation / Success Criteria

- Endpoint menerima onboarding configuration.
- Device tervalidasi pada Defender portal.

### KB-EDR-003 · Evidence Required

- Hostname, OU/scope, policy result, event/log evidence, portal screenshot.

### KB-EDR-003 · Rollback / Safety Note

Jika remediation melibatkan perubahan konfigurasi, policy, onboarding state, service, atau device object, ikuti change control yang berlaku. Hentikan perubahan bila menimbulkan dampak baru dan kembalikan konfigurasi ke baseline terakhir yang disetujui jika rollback tersedia.

## KB-EDR-003 · 5. Communication & Soft Skill Guidance

### KB-EDR-003 · Communication ke End User

"Tim IT sedang melakukan validasi GPO onboarding yang belum ter-apply. Perangkat tetap dapat digunakan kecuali terdapat instruksi lanjutan dari tim IT."

### KB-EDR-003 · Communication ke Customer / IT Admin

"Ditemukan kondisi GPO onboarding yang belum ter-apply. Tim sedang memvalidasi konfigurasi, connectivity, endpoint health, dan evidence terkait sebelum menentukan remediation berikutnya."

- Pisahkan symptom, suspected cause, dan confirmed root cause.
- Jangan menyimpulkan penyebab sebelum evidence tersedia.
- Dokumentasikan perubahan konfigurasi dan hasil validasi.
- Gunakan bahasa netral dan berorientasi pemulihan layanan.

## KB-EDR-003 · 6. Escalation Path & Related Links

| **Level** | **Responsibility / Evidence** |
|---|---|
| L1 Team Rollout/Enrollment | Collect hostname, user, OS/build, screenshot, waktu kejadian, network/VPN status. |
| L2 Technical Consultans | Validasi portal state, onboarding, policy, sensor/service, connectivity, logs. |
| L3 Security / Infrastructure | Validasi GPO, Intune, proxy/firewall, policy conflict, platform configuration. |
| Microsoft Support | Escalate setelah prerequisite, configuration, connectivity, endpoint state, dan diagnostic evidence telah divalidasi. |

Microsoft references:

- Troubleshoot Defender for Endpoint onboarding: https://learn.microsoft.com/en-us/defender-endpoint/troubleshoot-onboarding
- Onboard devices to Defender for Endpoint: https://learn.microsoft.com/en-us/defender-endpoint/onboarding
