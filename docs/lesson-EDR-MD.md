# Microsoft Defender for Endpoint (MDE) - Endpoint Detection and Response (EDR)

## Overview

Microsoft Defender for Endpoint (MDE) adalah solusi keamanan endpoint berbasis cloud dari Microsoft yang menyediakan kemampuan threat prevention, threat detection, threat investigation, threat response, dan threat hunting. MDE merupakan bagian dari Microsoft Defender XDR yang mengkorelasikan sinyal keamanan dari endpoint, identitas, email, aplikasi, dan cloud untuk memberikan visibilitas ancaman yang lebih luas.

## Apa itu EDR?

Endpoint Detection and Response (EDR) adalah teknologi keamanan yang dirancang untuk:

- Mengumpulkan telemetry endpoint secara kontinu.
- Mendeteksi aktivitas mencurigakan dan berbahaya.
- Menyelidiki ancaman secara otomatis maupun manual.
- Memberikan kemampuan containment dan remediation.

EDR berfokus pada aktivitas setelah ancaman berhasil masuk ke endpoint (post-breach detection and response).

## Komponen Utama MDE EDR

### Behavioral Monitoring

Microsoft Defender for Endpoint memonitor aktivitas sistem secara real-time seperti:

- Process Creation
- Process Termination
- DLL Loading
- Registry Modification
- Scheduled Task Creation
- Service Creation
- Network Connection
- User Logon Activity

Tujuannya adalah mendeteksi perilaku berbahaya yang tidak dapat dikenali hanya dengan signature antivirus.

### Telemetry Collection

MDE mengumpulkan berbagai jenis telemetry:

- Process Events
- Network Events
- File Events
- Registry Events
- Logon Events
- Device Information

Data telemetry dikirim ke cloud Microsoft untuk dianalisis menggunakan Machine Learning dan Threat Intelligence.

### Threat Detection

MDE menggunakan beberapa metode deteksi:

- Behavioral Analytics
- Machine Learning
- Threat Intelligence
- Indicators of Compromise (IOC)
- Attack Technique Detection

Jenis ancaman yang dapat dideteksi:

- Malware
- Ransomware
- Credential Theft
- Persistence Mechanisms
- Living Off The Land Attacks (LOLBins)
- Lateral Movement
- Command and Control Activity

### Automated Investigation and Remediation (AIR)

AIR memungkinkan investigasi otomatis terhadap alert yang muncul.

Kemampuan AIR:

- Mengidentifikasi root cause
- Menghubungkan aktivitas terkait
- Menentukan verdict
- Menjalankan remediation otomatis

Contoh tindakan otomatis:

- Quarantine File
- Stop Process
- Remove Registry Persistence
- Remove Scheduled Task
- Isolate Device

## EDR in Block Mode

### Definisi

EDR in Block Mode memungkinkan Microsoft Defender for Endpoint melakukan pemblokiran ancaman meskipun perangkat menggunakan antivirus pihak ketiga sebagai antivirus utama.

### Fungsi

- Memberikan proteksi tambahan.
- Memblokir artefak berbahaya yang ditemukan EDR.
- Melakukan remediation walaupun Microsoft Defender Antivirus berjalan dalam mode pasif.

### Use Case

- Organisasi menggunakan antivirus non-Microsoft.
- Organisasi tetap ingin memanfaatkan kemampuan deteksi dan remediation dari MDE.

## Detection Pipeline

### Tahap 1 - Event Collection

Endpoint menghasilkan event seperti:

- Process Start
- File Creation
- Registry Modification
- Network Connection

### Tahap 2 - Cloud Analysis

Data dianalisis menggunakan:

- Machine Learning
- Threat Intelligence
- Behavioral Analytics

### Tahap 3 - Alert Generation

```text
Event → Detection Logic → Alert
```

### Tahap 4 - Incident Correlation

Beberapa alert dapat dikorelasikan menjadi satu incident.

Contoh:

- Suspicious PowerShell
- Credential Dumping
- Remote Access Activity

Menjadi:

```text
Incident: Potential Human-Operated Ransomware
```

## Device Timeline

Device Timeline menampilkan seluruh aktivitas endpoint secara kronologis.

Informasi yang tersedia:

- Process Execution
- Network Communication
- File Changes
- Registry Changes
- Logon Activity

Timeline digunakan untuk investigative analysis dan forensic investigation.

## Advanced Hunting

### Definisi

Advanced Hunting adalah fitur pencarian ancaman menggunakan Kusto Query Language (KQL).

Digunakan untuk:

- Threat Hunting
- Root Cause Analysis
- IOC Search
- Incident Investigation
- Detection Validation

### Tabel Penting pada Advanced Hunting

#### DeviceProcessEvents

Menyimpan aktivitas proses.

```kql
DeviceProcessEvents
| where FileName == "powershell.exe"
```

#### DeviceNetworkEvents

Menyimpan aktivitas jaringan.

```kql
DeviceNetworkEvents
| where RemotePort == 3389
```

#### DeviceFileEvents

Menyimpan aktivitas file.

```kql
DeviceFileEvents
| where ActionType == "FileCreated"
```

#### DeviceRegistryEvents

Menyimpan aktivitas registry.

```kql
DeviceRegistryEvents
| where RegistryValueName contains "Run"
```

#### DeviceLogonEvents

Menyimpan aktivitas autentikasi.

```kql
DeviceLogonEvents
```

## Alert Severity

### Informational

Aktivitas tidak menunjukkan ancaman aktif.

### Low

Indikasi aktivitas mencurigakan ringan yang memerlukan monitoring.

### Medium

Aktivitas yang membutuhkan investigasi lebih lanjut.

### High

Kemungkinan besar merupakan aktivitas berbahaya.

### Critical

Ancaman aktif dengan dampak tinggi terhadap organisasi.

## Incident Management

### Alert

Notifikasi yang dihasilkan dari deteksi ancaman.

### Incident

Kumpulan alert yang memiliki keterkaitan aktivitas atau entitas.

### Entity

Objek yang terlibat dalam insiden.

Contoh entity:

- User
- Device
- IP Address
- File
- Process
- Domain
- URL

### Incident Timeline

Menampilkan kronologi aktivitas yang berhubungan dengan insiden.

Contoh:

1. User Login
2. PowerShell Execution
3. Credential Dumping
4. Lateral Movement
5. Ransomware Execution

## Response Actions

### Isolate Device

Mengisolasi endpoint dari jaringan.

Jenis isolasi:

- Full Isolation
- Selective Isolation

### Run Antivirus Scan

Menjalankan Microsoft Defender Antivirus Scan pada endpoint.

### Collect Investigation Package

Mengumpulkan artefak forensik untuk kebutuhan investigasi.

Artefak yang dikumpulkan:

- Running Processes
- Event Logs
- Autoruns
- Network Configuration
- Scheduled Tasks
- Security Information

### Restrict App Execution

Membatasi aplikasi tertentu agar tidak bisa dijalankan pada endpoint.

### Live Response

Remote shell yang memungkinkan investigator melakukan pengumpulan data dan investigasi secara langsung pada endpoint.

Contoh command:

```text
processes
services
dir
cd
getfile
putfile
```

## Attack Techniques yang Sering Dideteksi

### Credential Dumping

Tools yang umum digunakan:

- Mimikatz
- ProcDump

MITRE ATT&CK:

```text
T1003
```

### PowerShell Abuse

Penggunaan PowerShell untuk aktivitas mencurigakan atau berbahaya.

MITRE ATT&CK:

```text
T1059.001
```

### Lateral Movement

Perpindahan ancaman dari satu endpoint ke endpoint lain.

Contoh:

- PsExec
- SMB
- RDP

MITRE ATT&CK:

```text
T1021
```

### Persistence

Teknik mempertahankan akses pada sistem yang telah terkompromi.

Contoh:

- Registry Run Keys
- Scheduled Tasks
- Services

MITRE ATT&CK:

```text
T1547
```

### Defense Evasion

Upaya pelaku ancaman untuk menghindari deteksi.

Contoh:

- Obfuscated PowerShell
- AMSI Bypass
- Security Tool Disablement

MITRE ATT&CK:

```text
T1562
```

## MITRE ATT&CK Mapping

| Technique | MITRE ID |
|------------|-----------|
| PowerShell Execution | T1059.001 |
| Credential Dumping | T1003 |
| Remote Services | T1021 |
| Registry Persistence | T1547 |
| Defense Evasion | T1562 |
| Command and Scripting Interpreter | T1059 |
| Scheduled Task Persistence | T1053 |
| Service Creation | T1543 |

## Device Risk Levels

### Low

Risiko rendah dan tidak menunjukkan ancaman aktif.

### Medium

Terdapat indikasi ancaman atau kerentanan yang perlu diperhatikan.

### High

Ancaman aktif atau tingkat eksposur yang signifikan terhadap endpoint.

## Common SOC Workflow

### 1. Alert Received

SOC menerima alert dari Microsoft Defender for Endpoint.

### 2. Triage

Analis mengevaluasi:

- Severity
- Impact
- Scope
- Confidence

### 3. Investigation

Menggunakan:

- Device Timeline
- Incident Timeline
- Advanced Hunting
- Live Response
- Entity Analysis

### 4. Containment

Melakukan:

- Device Isolation
- File Quarantine
- User Restriction

### 5. Remediation

Menghapus malware dan persistence yang ditemukan.

### 6. Recovery

Mengembalikan endpoint ke kondisi operasional normal.

### 7. Lessons Learned

Melakukan evaluasi dan peningkatan kontrol keamanan.

## Best Practices

- Aktifkan EDR in Block Mode.
- Aktifkan Automated Investigation and Remediation.
- Integrasikan dengan Microsoft Defender XDR.
- Integrasikan dengan Microsoft Sentinel.
- Review incident High dan Critical setiap hari.
- Implementasikan Custom Detection Rules.
- Lakukan Threat Hunting secara berkala.
- Aktifkan Tamper Protection.
- Aktifkan Attack Surface Reduction Rules.
- Monitor Device Exposure Score.
- Monitor Secure Score secara berkala.
- Lakukan tuning alert untuk mengurangi false positive.

## Istilah Penting

### Alert

Notifikasi hasil deteksi ancaman.

### Incident

Sekumpulan alert yang berhubungan.

### Entity

Objek yang terlibat dalam insiden.

### EDR

Endpoint Detection and Response.

### AIR

Automated Investigation and Remediation.

### IOC

Indicator of Compromise.

### IOA

Indicator of Attack.

### KQL

Kusto Query Language.

### TVM

Threat and Vulnerability Management.

### Live Response

Remote command shell untuk investigasi endpoint.

### Advanced Hunting

Kemampuan pencarian ancaman menggunakan KQL.

### Device Timeline

Riwayat aktivitas endpoint secara detail.

### Threat Hunting

Aktivitas pencarian ancaman secara proaktif.

### Tamper Protection

Fitur untuk mencegah perubahan tidak sah terhadap konfigurasi keamanan Microsoft Defender.

### Attack Surface Reduction (ASR)

Kumpulan aturan untuk mengurangi peluang eksploitasi endpoint.

## Ringkasan

Microsoft Defender for Endpoint (MDE) EDR adalah solusi Endpoint Detection and Response yang menyediakan kemampuan deteksi, investigasi, dan respons ancaman berbasis cloud. Platform ini memanfaatkan telemetry endpoint, Machine Learning, Behavioral Analytics, Threat Intelligence, Automated Investigation and Remediation, serta Threat Hunting untuk mendeteksi dan menangani ancaman secara efektif.

Fitur utama yang menjadi fondasi MDE EDR meliputi:

- Behavioral Monitoring
- Threat Detection
- EDR in Block Mode
- Advanced Hunting
- Device Timeline
- Incident Correlation
- Live Response
- Automated Investigation and Remediation (AIR)
- Device Isolation
- Microsoft Defender XDR Integration
- Microsoft Sentinel Integration

MDE membantu Security Operations Center (SOC) mengidentifikasi, menyelidiki, mengendalikan, dan menghapus ancaman dengan lebih cepat sehingga mengurangi risiko kompromi terhadap perangkat dan lingkungan organisasi.
