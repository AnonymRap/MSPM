# KB-EDR-011 - ASR Policy Tidak Ter-apply ke Endpoint

Kategori: Microsoft Defender for Endpoint (MDE) - EDR Endpoint. Artikel KB-EDR-011: ASR Policy Tidak Ter-apply ke Endpoint.

## KB-EDR-011 · 1. Metadata Artikel

- **KB ID:** KB-EDR-011
- **Article Title:** ASR Policy Tidak Ter-apply ke Endpoint
- **Category:** Endpoint Security
- **Product:** Microsoft Defender for Endpoint
- **Scope:** Windows Client / Windows Server
- **Severity:** Medium / High sesuai dampak
- **Owner:** Endpoint Security / EDR Operation
- **Status:** Draft for Review
- **Version:** 1.0
- **Review Cycle:** Mengikuti governance KB internal
- **Keywords:** ASR Policy Tidak Ter-apply ke Endpoint

## KB-EDR-011 · 2. Issue / Problem Description

Attack Surface Reduction policy yang menjadi bagian security configuration belum menunjukkan penerapan sesuai target pada endpoint.

### KB-EDR-011 · Potential / Business Impact

- Security configuration tidak sesuai intended baseline.
- UAT/security verification dapat gagal.

## KB-EDR-011 · 3. Governance & Policy Context

- ASR termasuk scope konfigurasi project internal; perubahan rule harus mengikuti approved security design.
- Hindari mengubah rule secara ad-hoc hanya untuk menghilangkan error.

## KB-EDR-011 · 4. Resolution / Standard Workaround

1. Konfirmasi device management/enrollment state.
2. Validasi ASR policy assignment dan target group.
3. Periksa policy status pada management platform dan endpoint evidence.
4. Validasi conflict atau prerequisite yang relevan berdasarkan approved design.
5. Sync/re-evaluate sesuai standard procedure dan collect error evidence bila masih gagal.

### KB-EDR-011 · Validation / Success Criteria

- ASR policy state sesuai target design atau exception disetujui dan didokumentasikan.

### KB-EDR-011 · Evidence Required

- Policy/rule name, assignment, device ID, status/error, before/after screenshot.

### KB-EDR-011 · Rollback / Safety Note

Jika remediation melibatkan perubahan konfigurasi, policy, onboarding state, service, atau device object, ikuti change control yang berlaku. Hentikan perubahan bila menimbulkan dampak baru dan kembalikan konfigurasi ke baseline terakhir yang disetujui jika rollback tersedia.

## KB-EDR-011 · 5. Communication & Soft Skill Guidance

### KB-EDR-011 · Communication ke End User

"Tim IT sedang melakukan validasi ASR policy yang tidak ter-apply. Perangkat tetap dapat digunakan kecuali terdapat instruksi lanjutan dari tim IT."

### KB-EDR-011 · Communication ke Customer / IT Admin

"Ditemukan kondisi ASR policy yang tidak ter-apply. Tim sedang memvalidasi konfigurasi, connectivity, endpoint health, dan evidence terkait sebelum menentukan remediation berikutnya."

- Pisahkan symptom, suspected cause, dan confirmed root cause.
- Jangan menyimpulkan penyebab sebelum evidence tersedia.
- Dokumentasikan perubahan konfigurasi dan hasil validasi.
- Gunakan bahasa netral dan berorientasi pemulihan layanan.

## KB-EDR-011 · 6. Escalation Path & Related Links

| **Level** | **Responsibility / Evidence** |
|---|---|
| L1 Team Rollout/Enrollment | Collect hostname, user, OS/build, screenshot, waktu kejadian, network/VPN status. |
| L2 Technical Consultans | Validasi portal state, onboarding, policy, sensor/service, connectivity, logs. |
| L3 Security / Infrastructure | Validasi GPO, Intune, proxy/firewall, policy conflict, platform configuration. |
| Microsoft Support | Escalate setelah prerequisite, configuration, connectivity, endpoint state, dan diagnostic evidence telah divalidasi. |

Microsoft references:

- Troubleshoot Defender for Endpoint onboarding: https://learn.microsoft.com/en-us/defender-endpoint/troubleshoot-onboarding
- Onboard devices to Defender for Endpoint: https://learn.microsoft.com/en-us/defender-endpoint/onboarding
