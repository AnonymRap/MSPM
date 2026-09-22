# Onboarding Microsoft Defender for Endpoint (MDE) EDR

## Pengertian Onboarding

Onboarding adalah proses mendaftarkan dan menghubungkan endpoint ke layanan Microsoft Defender for Endpoint agar perangkat dapat mengirim telemetry, menerima kebijakan keamanan, menghasilkan alert, serta mendukung investigasi dan respons insiden.

Setelah onboarding berhasil, perangkat akan muncul pada portal Microsoft Defender dan mulai mengirim data keamanan ke cloud Microsoft.

## Prasyarat Onboarding

Sebelum melakukan onboarding, pastikan:

- Memiliki lisensi Microsoft Defender for Endpoint yang valid.
- Endpoint memiliki koneksi internet ke layanan Microsoft Defender.
- Endpoint memenuhi persyaratan sistem operasi yang didukung.
- Memiliki akses Administrator pada endpoint.
- Endpoint dapat mengakses URL dan service Microsoft Defender yang diperlukan.

## Metode Onboarding

Microsoft Defender for Endpoint mendukung beberapa metode onboarding.

### Local Script

Metode onboarding menggunakan script yang diunduh dari Microsoft Defender Portal.

Cocok untuk:

- Pengujian awal.
- Jumlah perangkat sedikit.
- Proof of Concept (POC).

Alur:

```text
Microsoft Defender Portal
        ↓
Download Onboarding Package
        ↓
Jalankan Script
        ↓
Device Terhubung ke MDE
```

### Group Policy (GPO)

Menggunakan Active Directory Group Policy untuk mendistribusikan onboarding package ke perangkat domain.

Cocok untuk:

- Lingkungan On-Premises Active Directory.
- Manajemen perangkat berbasis domain.

### Microsoft Intune

Menggunakan Microsoft Intune untuk deployment onboarding secara terpusat.

Cocok untuk:

- Cloud-managed device.
- Hybrid device.
- Remote workforce.

Alur:

```text
Intune
   ↓
Configuration Profile
   ↓
Endpoint
   ↓
MDE Onboarding
```

### Microsoft Configuration Manager (SCCM/MECM)

Digunakan pada organisasi yang mengelola endpoint menggunakan SCCM/MECM.

Cocok untuk:

- Lingkungan enterprise yang sudah menggunakan Configuration Manager.

### VDI Onboarding

Digunakan untuk:

- Azure Virtual Desktop
- Citrix
- VMware Horizon

Memerlukan onboarding package khusus untuk lingkungan Virtual Desktop Infrastructure (VDI).

## Langkah Onboarding Melalui Portal

### 1. Login Microsoft Defender Portal

Akses:

```text
https://security.microsoft.com
```

### 2. Buka Endpoint Settings

Menu:

```text
Settings
    ↓
Endpoints
    ↓
Device Management
    ↓
Onboarding
```

### 3. Pilih Operating System

Contoh:

- Windows 11
- Windows 10
- Windows Server 2019
- Windows Server 2022
- Linux
- macOS

### 4. Pilih Deployment Method

Contoh:

- Local Script
- Group Policy
- Intune
- Configuration Manager

### 5. Download Onboarding Package

Portal akan menghasilkan package onboarding sesuai metode yang dipilih.

### 6. Jalankan Onboarding

Jalankan package pada endpoint target.

### 7. Verifikasi Status

Buka:

```text
Assets
    ↓
Devices
```

Pastikan device muncul dengan status:

```text
Onboarded
```

## Verifikasi Onboarding Windows

### Melalui Command Prompt

```cmd
sc query sense
```

Hasil normal:

```text
SERVICE_NAME: Sense
STATE: RUNNING
```

### Melalui PowerShell

```powershell
Get-Service Sense
```

Hasil:

```text
Status : Running
```

### Verifikasi Registry

```text
HKLM\SOFTWARE\Microsoft\Windows Advanced Threat Protection
```

Jika onboarding berhasil, registry MDE akan tersedia.

## Microsoft Defender for Endpoint Sensor

Service utama yang digunakan:

```text
Microsoft Defender for Endpoint Service
```

Nama service:

```text
Sense
```

Fungsi:

- Mengumpulkan telemetry.
- Mengirim data ke cloud Microsoft.
- Menjalankan fitur EDR.

## Health Status Device

Status yang dapat muncul pada portal:

### Active

Device berhasil onboard dan aktif mengirim telemetry.

### Inactive

Device tidak mengirim telemetry dalam periode tertentu.

### Pending

Device sedang dalam proses onboarding.

### Unsupported

Versi sistem operasi tidak didukung.

## Data yang Dikirim Setelah Onboarding

Setelah onboarding berhasil, endpoint mulai mengirim telemetry berikut:

### Process Events

Contoh:

- powershell.exe
- cmd.exe
- rundll32.exe

### Network Events

Contoh:

- Outbound Connection
- DNS Query
- RDP Connection

### File Events

Contoh:

- File Created
- File Modified
- File Deleted

### Registry Events

Contoh:

- Run Key Modification
- Service Configuration

### Logon Events

Contoh:

- Interactive Logon
- Remote Logon
- Administrative Logon

## Verifikasi Menggunakan Advanced Hunting

Contoh query untuk memastikan device mengirim telemetry:

```kql
DeviceInfo
| where DeviceName contains "PC01"
```

Contoh verifikasi event:

```kql
DeviceProcessEvents
| where Timestamp > ago(1d)
```

Jika hasil muncul, telemetry sudah diterima oleh Microsoft Defender for Endpoint.

## Troubleshooting Onboarding

### Device Tidak Muncul di Portal

Periksa:

- Koneksi internet.
- Proxy Configuration.
- Firewall Rules.
- Onboarding Package yang digunakan.

### Service Sense Tidak Berjalan

Periksa:

```powershell
Get-Service Sense
```

Restart service:

```powershell
Restart-Service Sense
```

### Telemetry Tidak Masuk

Periksa:

- Defender Sensor Health.
- Endpoint Connectivity.
- Proxy Configuration.
- Security Event Logs.

### Device Muncul tetapi Inactive

Kemungkinan penyebab:

- Endpoint offline.
- Service Sense berhenti.
- Komunikasi ke cloud Microsoft terblokir.

## Best Practices Onboarding

- Gunakan Microsoft Intune untuk deployment skala besar.
- Uji onboarding pada kelompok kecil sebelum rollout massal.
- Pastikan service Sense berjalan pada seluruh endpoint.
- Monitor onboarding status melalui Microsoft Defender Portal.
- Gunakan Device Inventory untuk memverifikasi perangkat yang sudah onboard.
- Integrasikan dengan Defender XDR dan Microsoft Sentinel.
- Aktifkan Tamper Protection setelah onboarding berhasil.
- Terapkan EDR in Block Mode jika menggunakan antivirus pihak ketiga.

## Unboarding MDE

Unboarding adalah proses menghapus perangkat dari Microsoft Defender for Endpoint.

Alur:

```text
Settings
    ↓
Endpoints
    ↓
Device Management
    ↓
Offboarding
```

Microsoft menyediakan package offboarding yang dijalankan pada endpoint target.

## Ringkasan

Onboarding Microsoft Defender for Endpoint adalah proses mendaftarkan endpoint ke layanan MDE agar perangkat dapat mengirim telemetry keamanan dan memanfaatkan kemampuan EDR. Metode onboarding yang tersedia meliputi Local Script, Group Policy, Intune, Configuration Manager, dan VDI Deployment. Setelah onboarding berhasil, device akan muncul pada Microsoft Defender Portal dengan status Active dan mulai mengirim telemetry yang digunakan untuk deteksi, investigasi, dan respons terhadap ancaman.
