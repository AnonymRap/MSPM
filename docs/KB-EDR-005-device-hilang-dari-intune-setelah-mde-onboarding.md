# KB-EDR-005 - Device Hilang dari Intune Setelah MDE Onboarding

Kategori: Microsoft Defender for Endpoint (MDE) - EDR Endpoint. Artikel KB-EDR-005: Device Hilang dari Intune Setelah MDE Onboarding.

## KB-EDR-005 · 1. Metadata Artikel

- **KB ID:** KB-EDR-005
- **Article Title:** Device Hilang dari Intune Setelah MDE Onboarding
- **Category:** Endpoint Security
- **Product:** Microsoft Defender for Endpoint
- **Scope:** Windows Client / Windows Server
- **Severity:** Medium / High sesuai dampak
- **Owner:** Endpoint Security / EDR Operation
- **Status:** Draft for Review
- **Version:** 1.0
- **Review Cycle:** Mengikuti governance KB internal
- **Keywords:** Device Hilang dari Intune Setelah MDE Onboarding

## KB-EDR-005 · 2. Issue / Problem Description

Endpoint masih terkait proses MDE tetapi device object tidak ditemukan atau tidak lagi sesuai kondisi yang diharapkan pada Intune.

### KB-EDR-005 · Potential / Business Impact

- Policy delivery melalui management plane dapat terdampak.
- Troubleshooting dapat salah arah bila object identity tidak dicocokkan.

## KB-EDR-005 · 3. Governance & Policy Context

- Pastikan identity device dicocokkan sebelum delete/recreate.
- Re-enrollment merupakan remediation terkontrol, bukan langkah default.

## KB-EDR-005 · 4. Resolution / Standard Workaround

1. Catat hostname serta Defender, Intune, dan Entra identifiers yang tersedia.
2. Validasi keberadaan device pada masing-masing portal.
3. Periksa enrollment state dan management authority.
4. Validasi apakah policy assignment masih relevan.
5. Jika hasil investigasi mengharuskan re-enrollment, lakukan sesuai approved work instruction dan change control.
6. Validasi kembali device identity serta policy setelah remediation.

### KB-EDR-005 · Validation / Success Criteria

- Device object dan management state kembali sesuai design.
- Policy delivery dapat diverifikasi.

### KB-EDR-005 · Evidence Required

- Device IDs, enrollment state, screenshots sebelum/sesudah, change record bila ada.

### KB-EDR-005 · Rollback / Safety Note

Jika remediation melibatkan perubahan konfigurasi, policy, onboarding state, service, atau device object, ikuti change control yang berlaku. Hentikan perubahan bila menimbulkan dampak baru dan kembalikan konfigurasi ke baseline terakhir yang disetujui jika rollback tersedia.

## KB-EDR-005 · 5. Communication & Soft Skill Guidance

### KB-EDR-005 · Communication ke End User

"Tim IT sedang melakukan validasi device object atau enrollment state Intune. Perangkat tetap dapat digunakan kecuali terdapat instruksi lanjutan dari tim IT."

### KB-EDR-005 · Communication ke Customer / IT Admin

"Ditemukan kondisi device object atau enrollment state Intune. Tim sedang memvalidasi konfigurasi, connectivity, endpoint health, dan evidence terkait sebelum menentukan remediation berikutnya."

- Pisahkan symptom, suspected cause, dan confirmed root cause.
- Jangan menyimpulkan penyebab sebelum evidence tersedia.
- Dokumentasikan perubahan konfigurasi dan hasil validasi.
- Gunakan bahasa netral dan berorientasi pemulihan layanan.

## KB-EDR-005 · 6. Escalation Path & Related Links

| **Level** | **Responsibility / Evidence** |
|---|---|
| L1 Team Rollout/Enrollment | Collect hostname, user, OS/build, screenshot, waktu kejadian, network/VPN status. |
| L2 Technical Consultans | Validasi portal state, onboarding, policy, sensor/service, connectivity, logs. |
| L3 Security / Infrastructure | Validasi GPO, Intune, proxy/firewall, policy conflict, platform configuration. |
| Microsoft Support | Escalate setelah prerequisite, configuration, connectivity, endpoint state, dan diagnostic evidence telah divalidasi. |

Microsoft references:

- Troubleshoot Defender for Endpoint onboarding: https://learn.microsoft.com/en-us/defender-endpoint/troubleshoot-onboarding
- Onboard devices to Defender for Endpoint: https://learn.microsoft.com/en-us/defender-endpoint/onboarding
