# KB-EDR-012 - Device Control / USB Blocking Policy Tidak Berfungsi

Kategori: Microsoft Defender for Endpoint (MDE) - EDR Endpoint. Artikel KB-EDR-012: Device Control / USB Blocking Policy Tidak Berfungsi.

## KB-EDR-012 · 1. Metadata Artikel

- **KB ID:** KB-EDR-012
- **Article Title:** Device Control / USB Blocking Policy Tidak Berfungsi
- **Category:** Endpoint Security
- **Product:** Microsoft Defender for Endpoint
- **Scope:** Windows Client / Windows Server
- **Severity:** Medium / High sesuai dampak
- **Owner:** Endpoint Security / EDR Operation
- **Status:** Draft for Review
- **Version:** 1.0
- **Review Cycle:** Mengikuti governance KB internal
- **Keywords:** Device Control, USB Blocking Policy Tidak Berfungsi

## KB-EDR-012 · 2. Issue / Problem Description

Device Control atau USB mass-storage blocking policy belum menghasilkan behavior sesuai target security design.

### KB-EDR-012 · Potential / Business Impact

- Kontrol removable storage mungkin belum sesuai intended security posture.
- Testing/UAT control dapat gagal.

## KB-EDR-012 · 3. Governance & Policy Context

- Device Control termasuk scope konfigurasi project internal.
- Jangan melakukan allow/block exception tanpa business/security approval.

## KB-EDR-012 · 4. Resolution / Standard Workaround

1. Konfirmasi device menerima management policy yang benar.
2. Validasi Device Control policy assignment dan target membership.
3. Periksa policy state/error pada management platform dan endpoint.
4. Uji menggunakan test case UAT yang disetujui.
5. Jika ada exception/conflict, dokumentasikan evidence sebelum perubahan.

### KB-EDR-012 · Validation / Success Criteria

- Test case UAT menghasilkan behavior sesuai policy design.
- Policy status dan endpoint evidence konsisten.

### KB-EDR-012 · Evidence Required

- Policy name, assignment, device/user, test case, result, screenshots, error/detail logs.

### KB-EDR-012 · Rollback / Safety Note

Jika remediation melibatkan perubahan konfigurasi, policy, onboarding state, service, atau device object, ikuti change control yang berlaku. Hentikan perubahan bila menimbulkan dampak baru dan kembalikan konfigurasi ke baseline terakhir yang disetujui jika rollback tersedia.

## KB-EDR-012 · 5. Communication & Soft Skill Guidance

### KB-EDR-012 · Communication ke End User

"Tim IT sedang melakukan validasi Device Control atau USB blocking policy. Perangkat tetap dapat digunakan kecuali terdapat instruksi lanjutan dari tim IT."

### KB-EDR-012 · Communication ke Customer / IT Admin

"Ditemukan kondisi Device Control atau USB blocking policy. Tim sedang memvalidasi konfigurasi, connectivity, endpoint health, dan evidence terkait sebelum menentukan remediation berikutnya."

- Pisahkan symptom, suspected cause, dan confirmed root cause.
- Jangan menyimpulkan penyebab sebelum evidence tersedia.
- Dokumentasikan perubahan konfigurasi dan hasil validasi.
- Gunakan bahasa netral dan berorientasi pemulihan layanan.

## KB-EDR-012 · 6. Escalation Path & Related Links

| **Level** | **Responsibility / Evidence** |
|---|---|
| L1 Team Rollout/Enrollment | Collect hostname, user, OS/build, screenshot, waktu kejadian, network/VPN status. |
| L2 Technical Consultans | Validasi portal state, onboarding, policy, sensor/service, connectivity, logs. |
| L3 Security / Infrastructure | Validasi GPO, Intune, proxy/firewall, policy conflict, platform configuration. |
| Microsoft Support | Escalate setelah prerequisite, configuration, connectivity, endpoint state, dan diagnostic evidence telah divalidasi. |

Microsoft references:

- Troubleshoot Defender for Endpoint onboarding: https://learn.microsoft.com/en-us/defender-endpoint/troubleshoot-onboarding
- Onboard devices to Defender for Endpoint: https://learn.microsoft.com/en-us/defender-endpoint/onboarding
