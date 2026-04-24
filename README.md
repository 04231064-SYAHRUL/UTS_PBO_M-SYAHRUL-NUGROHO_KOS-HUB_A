# 🏢 Kost-Hub — Sistem Manajemen Kos Mahasiswa
![Kotlin]([https://img.shields.io/badge/Kotlin-7F52FF?style=for-the-badge&logo=kotlin&logoColor=white](https://pl.kotl.in/04V21L09F))
![OOP](https://img.shields.io/badge/Paradigma-OOP-blue?style=for-the-badge)
![Status](https://img.shields.io/badge/Status-Selesai-success?style=for-the-badge)
![ITK](https://img.shields.io/badge/Institut-Teknologi%20Kalimantan-orange?style=for-the-badge)

> **Proyek UTS Pemrograman Berorientasi Objek** > Mengintegrasikan keamanan data dengan prinsip Enkapsulasi dalam manajemen hunian digital.

---

## 👤 Identitas Pengembang
| Keterangan | Detail |
| :--- | :--- |
| **Nama** | M. Syahrul Nugroho |
| **NIM** | 04231064 |
| **Prodi** | Teknik Elektro |
| **Instansi** | Institut Teknologi Kalimantan |

---

## 📋 Ikhtisar Proyek
**Kost-Hub** bukan sekadar aplikasi pencatatan, melainkan simulasi kontrol akses data. Masalah utama dalam sistem manajemen tradisional adalah kerentanan manipulasi saldo dan status aset. Proyek ini hadir untuk mendemonstrasikan bagaimana **Object-Oriented Programming (OOP)** menyelesaikan masalah tersebut melalui:

* **Integritas Data**: Saldo tidak bisa dikurangi tanpa transaksi yang valid.
* **Keamanan Status**: Kamar tidak bisa dipesan ganda (*race condition avoidance*).
* **Transparansi Finansial**: Pendapatan pemilik terkunci secara privat dan hanya bertambah melalui sistem.

---

## 🏗️ Arsitektur Sistem & Struktur Kelas
Sistem dirancang dengan pemisahan tanggung jawab (*Separation of Concerns*) yang jelas.

```mermaid
classDiagram
    direction LR
    class TransaksiKos {
        <<Controller>>
        +pesanKamar(p: Penyewa, k: Kamar)
        +bayarTagihan(p: Penyewa, b: BapakKos, k: Kamar)
    }
    class Penyewa {
        <<Entity>>
        -saldo: Int
        +bayar(jumlah: Int) Boolean
    }
    class Kamar {
        <<Entity>>
        -status: StatusKamar
        +pesan() Boolean
    }
    class BapakKos {
        <<Entity>>
        -pendapatan: Int
        +tambahPendapatan(jumlah: Int)
    }

    TransaksiKos ..> Penyewa : Mengelola Saldo
    TransaksiKos ..> Kamar : Memvalidasi Status
    TransaksiKos ..> BapakKos : Mengirim Pendapatan
