# KB-EDR-009 - Device Offboarding dan Re-Onboarding MDE

Kategori: Microsoft Defender for Endpoint (MDE) - EDR Endpoint. Artikel KB-EDR-009: Device Offboarding dan Re-Onboarding MDE.

## KB-EDR-009 · 1. Metadata Artikel

- **KB ID:** KB-EDR-009
- **Article Title:** Device Offboarding dan Re-Onboarding MDE
- **Category:** Endpoint Security
- **Product:** Microsoft Defender for Endpoint
- **Scope:** Windows Client / Windows Server
- **Severity:** Medium / High sesuai dampak
- **Owner:** Endpoint Security / EDR Operation
- **Status:** Draft for Review
- **Version:** 1.0
- **Review Cycle:** Mengikuti governance KB internal
- **Keywords:** Device Offboarding dan Re-Onboarding MDE

## KB-EDR-009 · 2. Issue / Problem Description

Device memerlukan offboarding/re-onboarding setelah troubleshooting membuktikan kondisi onboarding atau management state perlu dibangun ulang.

### KB-EDR-009 · Potential / Business Impact

- Perubahan onboarding state merupakan tindakan material terhadap coverage EDR.
- Eksekusi yang tidak terkontrol dapat menimbulkan gap monitoring.

## KB-EDR-009 · 3. Governance & Policy Context

- Gunakan hanya setelah troubleshooting baseline selesai.
- Wajib mengikuti approved change/work instruction dan mencatat before/after evidence.
- Pastikan package/method sesuai operating system dan deployment method yang disetujui.

## KB-EDR-009 · 4. Resolution / Standard Workaround

1. Dokumentasikan alasan dan evidence yang mendasari re-onboarding.
2. Pastikan approval/change record tersedia jika diwajibkan.
3. Lakukan offboarding menggunakan metode resmi yang disetujui environment.
4. Validasi removal/offboarding state sesuai acceptance criteria internal.
5. Lakukan onboarding kembali menggunakan deployment method yang disetujui.
6. Validasi device identity, portal presence, management state, policy, dan health.

### KB-EDR-009 · Validation / Success Criteria

- Device kembali onboard dan dapat diverifikasi di portal.
- Management/policy state memenuhi target atau exception terdokumentasi.

### KB-EDR-009 · Evidence Required

- Before/after screenshots, device IDs, approval/change record, onboarding method, diagnostic result.

### KB-EDR-009 · Rollback / Safety Note

Jika remediation melibatkan perubahan konfigurasi, policy, onboarding state, service, atau device object, ikuti change control yang berlaku. Hentikan perubahan bila menimbulkan dampak baru dan kembalikan konfigurasi ke baseline terakhir yang disetujui jika rollback tersedia.

## KB-EDR-009 · 5. Communication & Soft Skill Guidance

### KB-EDR-009 · Communication ke End User

"Tim IT sedang melakukan validasi proses offboarding dan re-onboarding MDE. Perangkat tetap dapat digunakan kecuali terdapat instruksi lanjutan dari tim IT."

### KB-EDR-009 · Communication ke Customer / IT Admin

"Ditemukan kondisi proses offboarding dan re-onboarding MDE. Tim sedang memvalidasi konfigurasi, connectivity, endpoint health, dan evidence terkait sebelum menentukan remediation berikutnya."

- Pisahkan symptom, suspected cause, dan confirmed root cause.
- Jangan menyimpulkan penyebab sebelum evidence tersedia.
- Dokumentasikan perubahan konfigurasi dan hasil validasi.
- Gunakan bahasa netral dan berorientasi pemulihan layanan.

## KB-EDR-009 · 6. Escalation Path & Related Links

| **Level** | **Responsibility / Evidence** |
|---|---|
| L1 Team Rollout/Enrollment | Collect hostname, user, OS/build, screenshot, waktu kejadian, network/VPN status. |
| L2 Technical Consultans | Validasi portal state, onboarding, policy, sensor/service, connectivity, logs. |
| L3 Security / Infrastructure | Validasi GPO, Intune, proxy/firewall, policy conflict, platform configuration. |
| Microsoft Support | Escalate setelah prerequisite, configuration, connectivity, endpoint state, dan diagnostic evidence telah divalidasi. |

Microsoft references:

- Troubleshoot Defender for Endpoint onboarding: https://learn.microsoft.com/en-us/defender-endpoint/troubleshoot-onboarding
- Onboard devices to Defender for Endpoint: https://learn.microsoft.com/en-us/defender-endpoint/onboarding
