# KB-EDR-013 - Windows 11 MDE Sense Client Missing / Onboarding Failure

Kategori: Microsoft Defender for Endpoint (MDE) - EDR Endpoint. Artikel KB-EDR-013: Windows 11 MDE Sense Client Missing / Onboarding Failure.

## KB-EDR-013 · 1. Metadata Artikel

- **KB ID:** KB-EDR-013
- **Article Title:** Windows 11 MDE Sense Client Missing / Onboarding Failure
- **Category:** Endpoint Security
- **Product:** Microsoft Defender for Endpoint
- **Scope:** Windows Client / Windows Server
- **Severity:** Medium / High sesuai dampak
- **Owner:** Endpoint Security / EDR Operation
- **Status:** Draft for Review
- **Version:** 1.0
- **Review Cycle:** Mengikuti governance KB internal
- **Keywords:** Windows 11 MDE Sense Client Missing, Onboarding Failure

## KB-EDR-013 · 2. Issue / Problem Description

Pada Windows 11, onboarding gagal dan troubleshooting menunjukkan komponen/sensor MDE yang diharapkan tidak tersedia atau tidak berjalan sesuai kondisi normal.

### KB-EDR-013 · Potential / Business Impact

- Device tidak dapat dinyatakan successfully onboarded sampai sensor/portal state tervalidasi.
- Rollout batch perlu menahan completion status untuk device terdampak.

## KB-EDR-013 · 3. Governance & Policy Context

- Jangan mengunduh atau mengganti komponen Defender dari sumber tidak resmi.
- Validasi OS/build, servicing state, prerequisite, dan official Microsoft guidance sebelum repair.

## KB-EDR-013 · 4. Resolution / Standard Workaround

1. Catat exact Windows edition/build dan onboarding method.
2. Validasi prerequisite dan endpoint servicing state.
3. Periksa service/sensor presence serta event/error evidence.
4. Validasi connectivity dan jalankan diagnostic tooling yang disetujui.
5. Gunakan remediation resmi Microsoft/enterprise servicing process berdasarkan evidence; lalu ulangi onboarding bila diperlukan.
6. Validasi device di Defender portal dan dokumentasikan hasil.

### KB-EDR-013 · Validation / Success Criteria

- Sensor/onboarding state tervalidasi dan device tampil sesuai acceptance criteria.

### KB-EDR-013 · Evidence Required

- Windows edition/build, service/sensor state, event/error code, servicing evidence, Analyzer output, portal screenshot.

### KB-EDR-013 · Rollback / Safety Note

Jika remediation melibatkan perubahan konfigurasi, policy, onboarding state, service, atau device object, ikuti change control yang berlaku. Hentikan perubahan bila menimbulkan dampak baru dan kembalikan konfigurasi ke baseline terakhir yang disetujui jika rollback tersedia.

## KB-EDR-013 · 5. Communication & Soft Skill Guidance

### KB-EDR-013 · Communication ke End User

"Tim IT sedang melakukan validasi Sense client atau onboarding Windows 11. Perangkat tetap dapat digunakan kecuali terdapat instruksi lanjutan dari tim IT."

### KB-EDR-013 · Communication ke Customer / IT Admin

"Ditemukan kondisi Sense client atau onboarding Windows 11. Tim sedang memvalidasi konfigurasi, connectivity, endpoint health, dan evidence terkait sebelum menentukan remediation berikutnya."

- Pisahkan symptom, suspected cause, dan confirmed root cause.
- Jangan menyimpulkan penyebab sebelum evidence tersedia.
- Dokumentasikan perubahan konfigurasi dan hasil validasi.
- Gunakan bahasa netral dan berorientasi pemulihan layanan.

## KB-EDR-013 · 6. Escalation Path & Related Links

| **Level** | **Responsibility / Evidence** |
|---|---|
| L1 Team Rollout/Enrollment | Collect hostname, user, OS/build, screenshot, waktu kejadian, network/VPN status. |
| L2 Technical Consultans | Validasi portal state, onboarding, policy, sensor/service, connectivity, logs. |
| L3 Security / Infrastructure | Validasi GPO, Intune, proxy/firewall, policy conflict, platform configuration. |
| Microsoft Support | Escalate setelah prerequisite, configuration, connectivity, endpoint state, dan diagnostic evidence telah divalidasi. |

Microsoft references:

- Troubleshoot Defender for Endpoint onboarding: https://learn.microsoft.com/en-us/defender-endpoint/troubleshoot-onboarding
- Onboard devices to Defender for Endpoint: https://learn.microsoft.com/en-us/defender-endpoint/onboarding
