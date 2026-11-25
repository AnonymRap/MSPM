# KB-EDR-008 - Endpoint Tidak Mengirim Telemetry ke Defender Portal

Kategori: Microsoft Defender for Endpoint (MDE) - EDR Endpoint. Artikel KB-EDR-008: Endpoint Tidak Mengirim Telemetry ke Defender Portal.

## KB-EDR-008 · 1. Metadata Artikel

- **KB ID:** KB-EDR-008
- **Article Title:** Endpoint Tidak Mengirim Telemetry ke Defender Portal
- **Category:** Endpoint Security
- **Product:** Microsoft Defender for Endpoint
- **Scope:** Windows Client / Windows Server
- **Severity:** Medium / High sesuai dampak
- **Owner:** Endpoint Security / EDR Operation
- **Status:** Draft for Review
- **Version:** 1.0
- **Review Cycle:** Mengikuti governance KB internal
- **Keywords:** Endpoint Tidak Mengirim Telemetry ke Defender Portal

## KB-EDR-008 · 2. Issue / Problem Description

Endpoint sudah dikenal di Defender tetapi data/telemetry terbaru tidak terlihat sesuai kondisi yang diharapkan.

### KB-EDR-008 · Potential / Business Impact

- Monitoring dan investigation dapat menggunakan data yang tidak lagi aktual.
- Operational reporting perlu menandai health/telemetry exception.

## KB-EDR-008 · 3. Governance & Policy Context

- Jangan menyamakan device existence dengan healthy telemetry.
- Gunakan timestamp/evidence aktual dari portal dan endpoint.

## KB-EDR-008 · 4. Resolution / Standard Workaround

1. Validasi device identity untuk menghindari duplikasi object.
2. Periksa endpoint health dan service state.
3. Validasi connectivity/proxy/firewall path.
4. Run diagnostic collection jika dibutuhkan.
5. Setelah remediation, pantau update telemetry dan dokumentasikan timestamp keberhasilan.

### KB-EDR-008 · Validation / Success Criteria

- Telemetry kembali terlihat sesuai verification method project.
- Tidak ada unresolved connectivity/service error kritis pada evidence.

### KB-EDR-008 · Evidence Required

- Device ID, last seen/telemetry evidence, service state, network test, diagnostic logs.

### KB-EDR-008 · Rollback / Safety Note

Jika remediation melibatkan perubahan konfigurasi, policy, onboarding state, service, atau device object, ikuti change control yang berlaku. Hentikan perubahan bila menimbulkan dampak baru dan kembalikan konfigurasi ke baseline terakhir yang disetujui jika rollback tersedia.

## KB-EDR-008 · 5. Communication & Soft Skill Guidance

### KB-EDR-008 · Communication ke End User

"Tim IT sedang melakukan validasi telemetry endpoint ke Defender portal. Perangkat tetap dapat digunakan kecuali terdapat instruksi lanjutan dari tim IT."

### KB-EDR-008 · Communication ke Customer / IT Admin

"Ditemukan kondisi telemetry endpoint ke Defender portal. Tim sedang memvalidasi konfigurasi, connectivity, endpoint health, dan evidence terkait sebelum menentukan remediation berikutnya."

- Pisahkan symptom, suspected cause, dan confirmed root cause.
- Jangan menyimpulkan penyebab sebelum evidence tersedia.
- Dokumentasikan perubahan konfigurasi dan hasil validasi.
- Gunakan bahasa netral dan berorientasi pemulihan layanan.

## KB-EDR-008 · 6. Escalation Path & Related Links

| **Level** | **Responsibility / Evidence** |
|---|---|
| L1 Team Rollout/Enrollment | Collect hostname, user, OS/build, screenshot, waktu kejadian, network/VPN status. |
| L2 Technical Consultans | Validasi portal state, onboarding, policy, sensor/service, connectivity, logs. |
| L3 Security / Infrastructure | Validasi GPO, Intune, proxy/firewall, policy conflict, platform configuration. |
| Microsoft Support | Escalate setelah prerequisite, configuration, connectivity, endpoint state, dan diagnostic evidence telah divalidasi. |

Microsoft references:

- Troubleshoot Defender for Endpoint onboarding: https://learn.microsoft.com/en-us/defender-endpoint/troubleshoot-onboarding
- Onboard devices to Defender for Endpoint: https://learn.microsoft.com/en-us/defender-endpoint/onboarding
