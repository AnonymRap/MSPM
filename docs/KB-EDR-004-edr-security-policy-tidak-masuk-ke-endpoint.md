# KB-EDR-004 - EDR / Security Policy Tidak Masuk ke Endpoint

Kategori: Microsoft Defender for Endpoint (MDE) - EDR Endpoint. Artikel KB-EDR-004: EDR / Security Policy Tidak Masuk ke Endpoint.

## KB-EDR-004 · 1. Metadata Artikel

- **KB ID:** KB-EDR-004
- **Article Title:** EDR / Security Policy Tidak Masuk ke Endpoint
- **Category:** Endpoint Security
- **Product:** Microsoft Defender for Endpoint
- **Scope:** Windows Client / Windows Server
- **Severity:** Medium / High sesuai dampak
- **Owner:** Endpoint Security / EDR Operation
- **Status:** Draft for Review
- **Version:** 1.0
- **Review Cycle:** Mengikuti governance KB internal
- **Keywords:** EDR, Security Policy Tidak Masuk ke Endpoint

## KB-EDR-004 · 2. Issue / Problem Description

Device sudah onboard tetapi EDR atau security policy yang diharapkan belum ter-apply atau menunjukkan error.

### KB-EDR-004 · Potential / Business Impact

- Security baseline pada endpoint belum sesuai target.
- Compliance terhadap acceptance criteria deployment belum dapat dinyatakan.

## KB-EDR-004 · 3. Governance & Policy Context

- Validasi assignment dan management authority sebelum remediation.
- Delete/re-enroll hanya jika device/enrollment state memang sudah divalidasi membutuhkan tindakan tersebut.

## KB-EDR-004 · 4. Resolution / Standard Workaround

1. Konfirmasi device ada di Defender portal.
2. Konfirmasi device object dan enrollment state pada management platform yang digunakan.
3. Validasi policy assignment dan target membership.
4. Periksa policy status dan device check-in/sync evidence.
5. Validasi connectivity.
6. Collect logs/error code sebelum re-enrollment atau escalation.

### KB-EDR-004 · Validation / Success Criteria

- Policy menunjukkan state sesuai hasil yang ditargetkan atau exception terdokumentasi.
- Status device dan management state konsisten.

### KB-EDR-004 · Evidence Required

- Hostname, Defender/Intune/Entra Device ID, policy name, assignment, status, last check-in, screenshots, error code.

### KB-EDR-004 · Rollback / Safety Note

Jika remediation melibatkan perubahan konfigurasi, policy, onboarding state, service, atau device object, ikuti change control yang berlaku. Hentikan perubahan bila menimbulkan dampak baru dan kembalikan konfigurasi ke baseline terakhir yang disetujui jika rollback tersedia.

## KB-EDR-004 · 5. Communication & Soft Skill Guidance

### KB-EDR-004 · Communication ke End User

"Tim IT sedang melakukan validasi EDR atau security policy yang belum masuk. Perangkat tetap dapat digunakan kecuali terdapat instruksi lanjutan dari tim IT."

### KB-EDR-004 · Communication ke Customer / IT Admin

"Ditemukan kondisi EDR atau security policy yang belum masuk. Tim sedang memvalidasi konfigurasi, connectivity, endpoint health, dan evidence terkait sebelum menentukan remediation berikutnya."

- Pisahkan symptom, suspected cause, dan confirmed root cause.
- Jangan menyimpulkan penyebab sebelum evidence tersedia.
- Dokumentasikan perubahan konfigurasi dan hasil validasi.
- Gunakan bahasa netral dan berorientasi pemulihan layanan.

## KB-EDR-004 · 6. Escalation Path & Related Links

| **Level** | **Responsibility / Evidence** |
|---|---|
| L1 Team Rollout/Enrollment | Collect hostname, user, OS/build, screenshot, waktu kejadian, network/VPN status. |
| L2 Technical Consultans | Validasi portal state, onboarding, policy, sensor/service, connectivity, logs. |
| L3 Security / Infrastructure | Validasi GPO, Intune, proxy/firewall, policy conflict, platform configuration. |
| Microsoft Support | Escalate setelah prerequisite, configuration, connectivity, endpoint state, dan diagnostic evidence telah divalidasi. |

Microsoft references:

- Troubleshoot Defender for Endpoint onboarding: https://learn.microsoft.com/en-us/defender-endpoint/troubleshoot-onboarding
- Onboard devices to Defender for Endpoint: https://learn.microsoft.com/en-us/defender-endpoint/onboarding
