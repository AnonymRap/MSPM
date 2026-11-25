# KB-EDR-002 - Device Berstatus Managed by Unknown

Kategori: Microsoft Defender for Endpoint (MDE) - EDR Endpoint. Artikel KB-EDR-002: Device Berstatus Managed by Unknown.

## KB-EDR-002 · 1. Metadata Artikel

- **KB ID:** KB-EDR-002
- **Article Title:** Device Berstatus Managed by Unknown
- **Category:** Endpoint Security
- **Product:** Microsoft Defender for Endpoint
- **Scope:** Windows Client / Windows Server
- **Severity:** Medium / High sesuai dampak
- **Owner:** Endpoint Security / EDR Operation
- **Status:** Draft for Review
- **Version:** 1.0
- **Review Cycle:** Mengikuti governance KB internal
- **Keywords:** Device Berstatus Managed by Unknown

## KB-EDR-002 · 2. Issue / Problem Description

Device sudah terlihat pada Microsoft Defender for Endpoint tetapi management state menunjukkan Managed by Unknown.

### KB-EDR-002 · Potential / Business Impact

- Management state belum dapat dikonfirmasi sesuai design.
- Tracking project dapat menjadi tidak akurat bila status ini langsung dihitung completed.

## KB-EDR-002 · 3. Governance & Policy Context

- Pisahkan Onboarding Status, Management Status, dan Sensor/Health Status dalam reporting.
- Gunakan evidence sebelum mengubah enrollment/device object.

## KB-EDR-002 · 4. Resolution / Standard Workaround

1. Konfirmasi device tersedia di Defender portal.
2. Validasi onboarding method yang digunakan.
3. Validasi endpoint health dan Defender-related service/configuration.
4. Jalankan MDE Client Analyzer untuk diagnostic evidence jika dibutuhkan.
5. Validasi connectivity dan device management/enrollment state sesuai design.
6. Monitor perubahan management state setelah remediation.

### KB-EDR-002 · Validation / Success Criteria

- Management state sesuai design atau root cause terdokumentasi untuk escalation.
- Endpoint tetap terdeteksi dan health dapat diverifikasi.

### KB-EDR-002 · Evidence Required

- Defender Device ID, Intune/Entra Device ID jika relevan.
- Managed by status screenshot.
- Client Analyzer / service status.

### KB-EDR-002 · Rollback / Safety Note

Jika remediation melibatkan perubahan konfigurasi, policy, onboarding state, service, atau device object, ikuti change control yang berlaku. Hentikan perubahan bila menimbulkan dampak baru dan kembalikan konfigurasi ke baseline terakhir yang disetujui jika rollback tersedia.

## KB-EDR-002 · 5. Communication & Soft Skill Guidance

### KB-EDR-002 · Communication ke End User

"Tim IT sedang melakukan validasi management status Managed by Unknown. Perangkat tetap dapat digunakan kecuali terdapat instruksi lanjutan dari tim IT."

### KB-EDR-002 · Communication ke Customer / IT Admin

"Ditemukan kondisi management status Managed by Unknown. Tim sedang memvalidasi konfigurasi, connectivity, endpoint health, dan evidence terkait sebelum menentukan remediation berikutnya."

- Pisahkan symptom, suspected cause, dan confirmed root cause.
- Jangan menyimpulkan penyebab sebelum evidence tersedia.
- Dokumentasikan perubahan konfigurasi dan hasil validasi.
- Gunakan bahasa netral dan berorientasi pemulihan layanan.

## KB-EDR-002 · 6. Escalation Path & Related Links

| **Level** | **Responsibility / Evidence** |
|---|---|
| L1 Team Rollout/Enrollment | Collect hostname, user, OS/build, screenshot, waktu kejadian, network/VPN status. |
| L2 Technical Consultans | Validasi portal state, onboarding, policy, sensor/service, connectivity, logs. |
| L3 Security / Infrastructure | Validasi GPO, Intune, proxy/firewall, policy conflict, platform configuration. |
| Microsoft Support | Escalate setelah prerequisite, configuration, connectivity, endpoint state, dan diagnostic evidence telah divalidasi. |

Microsoft references:

- Troubleshoot Defender for Endpoint onboarding: https://learn.microsoft.com/en-us/defender-endpoint/troubleshoot-onboarding
- Onboard devices to Defender for Endpoint: https://learn.microsoft.com/en-us/defender-endpoint/onboarding
