# KB-EDR-007 - Microsoft Defender Antivirus / EDR Service Tidak Berjalan

Kategori: Microsoft Defender for Endpoint (MDE) - EDR Endpoint. Artikel KB-EDR-007: Microsoft Defender Antivirus / EDR Service Tidak Berjalan.

## KB-EDR-007 · 1. Metadata Artikel

- **KB ID:** KB-EDR-007
- **Article Title:** Microsoft Defender Antivirus / EDR Service Tidak Berjalan
- **Category:** Endpoint Security
- **Product:** Microsoft Defender for Endpoint
- **Scope:** Windows Client / Windows Server
- **Severity:** Medium / High sesuai dampak
- **Owner:** Endpoint Security / EDR Operation
- **Status:** Draft for Review
- **Version:** 1.0
- **Review Cycle:** Mengikuti governance KB internal
- **Keywords:** Microsoft Defender Antivirus, EDR Service Tidak Berjalan

## KB-EDR-007 · 2. Issue / Problem Description

Satu atau lebih service terkait Microsoft Defender atau EDR pada endpoint berhenti atau gagal berjalan.

### KB-EDR-007 · Potential / Business Impact

- Sensor/inspection/telemetry function perlu divalidasi.
- Endpoint dapat menunjukkan health atau management state yang tidak sesuai.

## KB-EDR-007 · 3. Governance & Policy Context

- Jangan mengubah service startup/security setting tanpa evidence dan change approval.
- Periksa kemungkinan policy atau product conflict sebelum permanent change.

## KB-EDR-007 · 4. Resolution / Standard Workaround

1. Catat nama service yang terdampak dan current state.
2. Collect error/event evidence saat service gagal start.
3. Validasi prerequisite, policy, dan endpoint health.
4. Gunakan MDE Client Analyzer bila sesuai untuk memperkaya diagnostic evidence.
5. Remediate hanya berdasarkan root cause yang terverifikasi lalu restart/validate sesuai prosedur change.

### KB-EDR-007 · Validation / Success Criteria

- Service state sesuai expected baseline.
- Endpoint health dan portal status tervalidasi.

### KB-EDR-007 · Evidence Required

- Service name/state, event logs, error code, policy state, Client Analyzer output.

### KB-EDR-007 · Rollback / Safety Note

Jika remediation melibatkan perubahan konfigurasi, policy, onboarding state, service, atau device object, ikuti change control yang berlaku. Hentikan perubahan bila menimbulkan dampak baru dan kembalikan konfigurasi ke baseline terakhir yang disetujui jika rollback tersedia.

## KB-EDR-007 · 5. Communication & Soft Skill Guidance

### KB-EDR-007 · Communication ke End User

"Tim IT sedang melakukan validasi service Defender atau EDR yang tidak berjalan. Perangkat tetap dapat digunakan kecuali terdapat instruksi lanjutan dari tim IT."

### KB-EDR-007 · Communication ke Customer / IT Admin

"Ditemukan kondisi service Defender atau EDR yang tidak berjalan. Tim sedang memvalidasi konfigurasi, connectivity, endpoint health, dan evidence terkait sebelum menentukan remediation berikutnya."

- Pisahkan symptom, suspected cause, dan confirmed root cause.
- Jangan menyimpulkan penyebab sebelum evidence tersedia.
- Dokumentasikan perubahan konfigurasi dan hasil validasi.
- Gunakan bahasa netral dan berorientasi pemulihan layanan.

## KB-EDR-007 · 6. Escalation Path & Related Links

| **Level** | **Responsibility / Evidence** |
|---|---|
| L1 Team Rollout/Enrollment | Collect hostname, user, OS/build, screenshot, waktu kejadian, network/VPN status. |
| L2 Technical Consultans | Validasi portal state, onboarding, policy, sensor/service, connectivity, logs. |
| L3 Security / Infrastructure | Validasi GPO, Intune, proxy/firewall, policy conflict, platform configuration. |
| Microsoft Support | Escalate setelah prerequisite, configuration, connectivity, endpoint state, dan diagnostic evidence telah divalidasi. |

Microsoft references:

- Troubleshoot Defender for Endpoint onboarding: https://learn.microsoft.com/en-us/defender-endpoint/troubleshoot-onboarding
- Onboard devices to Defender for Endpoint: https://learn.microsoft.com/en-us/defender-endpoint/onboarding
