# KB-EDR-006 - Microsoft Defender for Endpoint Connectivity / URL Access Issue

Kategori: Microsoft Defender for Endpoint (MDE) - EDR Endpoint. Artikel KB-EDR-006: Microsoft Defender for Endpoint Connectivity / URL Access Issue.

## KB-EDR-006 · 1. Metadata Artikel

- **KB ID:** KB-EDR-006
- **Article Title:** Microsoft Defender for Endpoint Connectivity / URL Access Issue
- **Category:** Endpoint Security
- **Product:** Microsoft Defender for Endpoint
- **Scope:** Windows Client / Windows Server
- **Severity:** Medium / High sesuai dampak
- **Owner:** Endpoint Security / EDR Operation
- **Status:** Draft for Review
- **Version:** 1.0
- **Review Cycle:** Mengikuti governance KB internal
- **Keywords:** Microsoft Defender for Endpoint Connectivity, URL Access Issue

## KB-EDR-006 · 2. Issue / Problem Description

Endpoint gagal atau tidak konsisten berkomunikasi dengan service Microsoft Defender for Endpoint karena jalur konektivitas perlu divalidasi.

### KB-EDR-006 · Potential / Business Impact

- Onboarding, telemetry, atau portal visibility dapat terdampak.
- Diagnostic result dapat menunjukkan communication failure.

## KB-EDR-006 · 3. Governance & Policy Context

- Whitelist harus mengikuti requirement Microsoft dan network governance yang disetujui.
- Jangan membuka broad internet access bila hanya endpoint/service tertentu yang dibutuhkan.

## KB-EDR-006 · 4. Resolution / Standard Workaround

1. Identifikasi network path endpoint: corporate LAN, VPN, proxy, firewall.
2. Validasi required Defender service endpoints berdasarkan deployment design dan dokumentasi Microsoft yang berlaku.
3. Pada environment project, pastikan akses yang diwajibkan seperti \*.endpoint.security.microsoft.com tidak diblokir bila domain tersebut termasuk design yang disetujui.
4. Periksa proxy/firewall/SSL inspection evidence.
5. Ulangi connectivity validation setelah perubahan network.

### KB-EDR-006 · Validation / Success Criteria

- Required service communication berhasil sesuai test yang digunakan project.
- Portal/telemetry behavior kembali tervalidasi.

### KB-EDR-006 · Evidence Required

- Source device/IP, destination/service, port/protocol, proxy/firewall logs, test timestamp.

### KB-EDR-006 · Rollback / Safety Note

Jika remediation melibatkan perubahan konfigurasi, policy, onboarding state, service, atau device object, ikuti change control yang berlaku. Hentikan perubahan bila menimbulkan dampak baru dan kembalikan konfigurasi ke baseline terakhir yang disetujui jika rollback tersedia.

## KB-EDR-006 · 5. Communication & Soft Skill Guidance

### KB-EDR-006 · Communication ke End User

"Tim IT sedang melakukan validasi konektivitas Microsoft Defender for Endpoint. Perangkat tetap dapat digunakan kecuali terdapat instruksi lanjutan dari tim IT."

### KB-EDR-006 · Communication ke Customer / IT Admin

"Ditemukan kondisi konektivitas Microsoft Defender for Endpoint. Tim sedang memvalidasi konfigurasi, connectivity, endpoint health, dan evidence terkait sebelum menentukan remediation berikutnya."

- Pisahkan symptom, suspected cause, dan confirmed root cause.
- Jangan menyimpulkan penyebab sebelum evidence tersedia.
- Dokumentasikan perubahan konfigurasi dan hasil validasi.
- Gunakan bahasa netral dan berorientasi pemulihan layanan.

## KB-EDR-006 · 6. Escalation Path & Related Links

| **Level** | **Responsibility / Evidence** |
|---|---|
| L1 Team Rollout/Enrollment | Collect hostname, user, OS/build, screenshot, waktu kejadian, network/VPN status. |
| L2 Technical Consultans | Validasi portal state, onboarding, policy, sensor/service, connectivity, logs. |
| L3 Security / Infrastructure | Validasi GPO, Intune, proxy/firewall, policy conflict, platform configuration. |
| Microsoft Support | Escalate setelah prerequisite, configuration, connectivity, endpoint state, dan diagnostic evidence telah divalidasi. |

Microsoft references:

- Troubleshoot Defender for Endpoint onboarding: https://learn.microsoft.com/en-us/defender-endpoint/troubleshoot-onboarding
- Onboard devices to Defender for Endpoint: https://learn.microsoft.com/en-us/defender-endpoint/onboarding
