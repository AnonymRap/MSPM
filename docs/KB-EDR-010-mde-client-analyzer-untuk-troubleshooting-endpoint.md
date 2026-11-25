# KB-EDR-010 - MDE Client Analyzer untuk Troubleshooting Endpoint

Kategori: Microsoft Defender for Endpoint (MDE) - EDR Endpoint. Artikel KB-EDR-010: MDE Client Analyzer untuk Troubleshooting Endpoint.

## KB-EDR-010 · 1. Metadata Artikel

- **KB ID:** KB-EDR-010
- **Article Title:** MDE Client Analyzer untuk Troubleshooting Endpoint
- **Category:** Endpoint Security
- **Product:** Microsoft Defender for Endpoint
- **Scope:** Windows Client / Windows Server
- **Severity:** Medium / High sesuai dampak
- **Owner:** Endpoint Security / EDR Operation
- **Status:** Draft for Review
- **Version:** 1.0
- **Review Cycle:** Mengikuti governance KB internal
- **Keywords:** MDE Client Analyzer untuk Troubleshooting Endpoint

## KB-EDR-010 · 2. Issue / Problem Description

MDE Client Analyzer digunakan sebagai diagnostic evidence ketika root cause onboarding, connectivity, atau endpoint health belum jelas.

### KB-EDR-010 · Potential / Business Impact

- Mempercepat evidence collection untuk L2/L3.
- Membantu escalation dengan data diagnostik yang lebih lengkap.

## KB-EDR-010 · 3. Governance & Policy Context

- Diagnostic output dapat berisi informasi environment; simpan dan bagikan sesuai data-handling policy.
- Analyzer bukan pengganti root-cause validation.

## KB-EDR-010 · 4. Resolution / Standard Workaround

1. Tentukan symptom dan scope device sebelum menjalankan diagnostic collection.
2. Gunakan MDE Client Analyzer sesuai panduan Microsoft/approved internal procedure.
3. Review output untuk evidence yang relevan dengan onboarding, connectivity, service, atau configuration.
4. Korelasikan hasil analyzer dengan portal state dan endpoint logs.
5. Lampirkan evidence yang relevan ke ticket/escalation tanpa menyebarkan data yang tidak diperlukan.

### KB-EDR-010 · Validation / Success Criteria

- Diagnostic package/result berhasil dikumpulkan dan dapat digunakan untuk menentukan remediation atau escalation.

### KB-EDR-010 · Evidence Required

- Analyzer output, hostname, OS/build, timestamp, issue description, portal screenshots.

### KB-EDR-010 · Rollback / Safety Note

Jika remediation melibatkan perubahan konfigurasi, policy, onboarding state, service, atau device object, ikuti change control yang berlaku. Hentikan perubahan bila menimbulkan dampak baru dan kembalikan konfigurasi ke baseline terakhir yang disetujui jika rollback tersedia.

## KB-EDR-010 · 5. Communication & Soft Skill Guidance

### KB-EDR-010 · Communication ke End User

"Tim IT sedang melakukan validasi pengumpulan diagnostic evidence dengan MDE Client Analyzer. Perangkat tetap dapat digunakan kecuali terdapat instruksi lanjutan dari tim IT."

### KB-EDR-010 · Communication ke Customer / IT Admin

"Ditemukan kondisi pengumpulan diagnostic evidence dengan MDE Client Analyzer. Tim sedang memvalidasi konfigurasi, connectivity, endpoint health, dan evidence terkait sebelum menentukan remediation berikutnya."

- Pisahkan symptom, suspected cause, dan confirmed root cause.
- Jangan menyimpulkan penyebab sebelum evidence tersedia.
- Dokumentasikan perubahan konfigurasi dan hasil validasi.
- Gunakan bahasa netral dan berorientasi pemulihan layanan.

## KB-EDR-010 · 6. Escalation Path & Related Links

| **Level** | **Responsibility / Evidence** |
|---|---|
| L1 Team Rollout/Enrollment | Collect hostname, user, OS/build, screenshot, waktu kejadian, network/VPN status. |
| L2 Technical Consultans | Validasi portal state, onboarding, policy, sensor/service, connectivity, logs. |
| L3 Security / Infrastructure | Validasi GPO, Intune, proxy/firewall, policy conflict, platform configuration. |
| Microsoft Support | Escalate setelah prerequisite, configuration, connectivity, endpoint state, dan diagnostic evidence telah divalidasi. |

Microsoft references:

- Troubleshoot Defender for Endpoint onboarding: https://learn.microsoft.com/en-us/defender-endpoint/troubleshoot-onboarding
- Onboard devices to Defender for Endpoint: https://learn.microsoft.com/en-us/defender-endpoint/onboarding
