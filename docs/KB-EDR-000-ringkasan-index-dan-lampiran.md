# KB EDR Endpoint - Ringkasan, Struktur Artikel, dan Lampiran

Knowledge base operasional Microsoft Defender for Endpoint (MDE) untuk implementasi, troubleshooting, handover, dan BAU support. Satu issue = satu KB article. Setiap artikel memisahkan symptom, governance, resolution, validation, evidence, communication, dan escalation path.

## Document Overview

Dokumen ini menyatukan artikel operasional EDR endpoint dalam format yang konsisten untuk implementasi Microsoft Defender for Endpoint. Artikel dirancang agar dapat digunakan saat stabilization, UAT, knowledge transfer, dan BAU support.

## Standard Struktur Artikel

1. Metadata Artikel
2. Issue / Problem Description
3. Governance & Policy Context
4. Resolution / Standard Workaround
5. Communication & Soft Skill Guidance
6. Escalation Path & Related Links

## KB Index

| KB ID | Artikel |
|---|---|
| KB-EDR-001 | Device Tidak Muncul di Microsoft Defender Portal Setelah Onboarding |
| KB-EDR-002 | Device Berstatus Managed by Unknown |
| KB-EDR-003 | GPO Onboarding Microsoft Defender for Endpoint Tidak Ter-apply |
| KB-EDR-004 | EDR / Security Policy Tidak Masuk ke Endpoint |
| KB-EDR-005 | Device Hilang dari Intune Setelah MDE Onboarding |
| KB-EDR-006 | Microsoft Defender for Endpoint Connectivity / URL Access Issue |
| KB-EDR-007 | Microsoft Defender Antivirus / EDR Service Tidak Berjalan |
| KB-EDR-008 | Endpoint Tidak Mengirim Telemetry ke Defender Portal |
| KB-EDR-009 | Device Offboarding dan Re-Onboarding MDE |
| KB-EDR-010 | MDE Client Analyzer untuk Troubleshooting Endpoint |
| KB-EDR-011 | ASR Policy Tidak Ter-apply ke Endpoint |
| KB-EDR-012 | Device Control / USB Blocking Policy Tidak Berfungsi |
| KB-EDR-013 | Windows 11 MDE Sense Client Missing / Onboarding Failure |

## KB-EDR Lampiran · Appendix A - Standard Evidence Checklist

| **Evidence** | **Mandatory / Conditional** |
|---|---|
| Hostname / Asset ID | Mandatory |
| OS / Edition / Build | Mandatory |
| Defender Device ID | Mandatory jika tersedia |
| Intune Device ID | Conditional |
| Entra Device ID | Conditional |
| Onboarding Method | Mandatory |
| Managed By / Management State | Mandatory untuk management issue |
| Policy Name / Assignment / Status | Mandatory untuk policy issue |
| Connectivity Test / Proxy / Firewall Evidence | Mandatory untuk connectivity issue |
| Error Code / Event Logs | Mandatory bila tersedia |
| MDE Client Analyzer | Mandatory berdasarkan troubleshooting path |
| Before / After Screenshot | Mandatory untuk closure evidence |
| Change / Approval Reference | Mandatory jika remediation memerlukan controlled change |

## KB-EDR Lampiran · Appendix B - Completion Status Recommendation

| **Status** | **Definition** |
|---|---|
| Not Started | Belum masuk troubleshooting/onboarding. |
| In Progress | Sedang dilakukan onboarding atau troubleshooting. |
| Pending Dependency | Menunggu network, GPO, Intune, user/device, atau approval dependency. |
| Technical Validation | Remediation selesai dan menunggu verification/monitoring. |
| Completed | Acceptance criteria article terpenuhi dan evidence lengkap. |
| Exception / Escalated | Root cause belum terselesaikan; evidence dan escalation path telah dicatat. |

## KB-EDR Lampiran · Appendix C - Source Notes

Baseline dokumen mengacu pada materi project internal yang ditemukan sebelumnya, termasuk scope MDE onboarding via GPO, Windows/Windows Server/Linux onboarding, ASR, Device Control, stabilization monitoring, UAT, project documentation, knowledge transfer, prerequisite OS/network, serta preventive health activities.

Official Microsoft references used for the baseline:

- https://learn.microsoft.com/en-us/defender-endpoint/troubleshoot-onboarding
- https://learn.microsoft.com/en-us/defender-endpoint/onboarding
