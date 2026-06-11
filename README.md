# 🔐 Panduan GPG — Install & Membuka File GPG

GPG (GNU Privacy Guard) adalah alat enkripsi open-source untuk mengamankan file dan komunikasi. Panduan ini mencakup instalasi **Gpg4win** (Windows) dan cara membuka/mendekripsi file `.gpg`.

---

## 📥 Instalasi Gpg4win (Windows)

### Langkah 1 — Unduh Installer

1. Buka browser dan kunjungi: **https://gpg4win.org/download.html**
2. Klik tombol **"Download Gpg4win"**
3. Simpan file installer (contoh: `gpg4win-4.x.x.exe`)

### Langkah 2 — Jalankan Installer

1. Double-click file installer yang sudah diunduh
2. Jika muncul peringatan UAC (User Account Control), klik **"Yes"**
3. Pilih bahasa instalasi → klik **"OK"**

### Langkah 3 — Pilih Komponen

Di layar pemilihan komponen, centang yang dibutuhkan:

| Komponen | Fungsi | Rekomendasi |
|---|---|---|
| **GnuPG** | Inti enkripsi GPG | ✅ Wajib |
| **Kleopatra** | Antarmuka GUI untuk GPG | ✅ Disarankan |
| **GpgOL** | Integrasi Outlook | Opsional |
| **GpgEX** | Integrasi Windows Explorer | ✅ Disarankan |

Klik **"Next"** → **"Install"** → tunggu hingga selesai → klik **"Finish"**

### Langkah 4 — Verifikasi Instalasi

Buka **Command Prompt** atau **PowerShell**, lalu jalankan:

```bash
gpg --version
```

Output yang diharapkan:
```
gpg (GnuPG) 2.x.x
...
```

---

## 📂 Membuka / Mendekripsi File GPG

### Metode 1 — Menggunakan Kleopatra (GUI)

1. Buka aplikasi **Kleopatra**
2. Klik menu **"Decrypt/Verify Files"** atau tekan `Ctrl+D`
3. Pilih file `.gpg` yang ingin dibuka
4. Klik **"Decrypt/Verify"**
5. Masukkan **passphrase** jika diminta
6. File hasil dekripsi akan tersimpan di folder yang sama

> **Alternatif:** Klik kanan file `.gpg` di Windows Explorer → **"More GpgEX options"** → **"Decrypt"**

---

### Metode 2 — Menggunakan Command Line

#### Dekripsi file terenkripsi simetris (password)

```bash
gpg --output nama_output.txt --decrypt nama_file.gpg
```

#### Dekripsi file terenkripsi dengan kunci publik/privat

```bash
gpg --output nama_output.txt --decrypt nama_file.gpg
```

> GPG akan otomatis menggunakan private key yang sesuai dari keyring Anda.

#### Contoh nyata

```bash
# Dekripsi file "dokumen.pdf.gpg" menjadi "dokumen.pdf"
gpg --output dokumen.pdf --decrypt dokumen.pdf.gpg
```

---

## 🔑 Import Kunci GPG (Jika Diperlukan)

Jika file GPG dienkripsi dengan kunci orang lain, Anda perlu mengimport private key terlebih dahulu:

```bash
# Import private key dari file
gpg --import private_key.asc

# Verifikasi kunci sudah masuk
gpg --list-secret-keys
```

---

## ❓ Troubleshooting Umum

| Masalah | Solusi |
|---|---|
| `No secret key` | Import private key yang sesuai dengan `gpg --import` |
| `Bad passphrase` | Pastikan passphrase yang dimasukkan benar |
| `gpg` tidak dikenali di CMD | Tambahkan path GnuPG ke variabel `PATH` sistem |
| File tidak bisa dibuka di Kleopatra | Coba via command line untuk melihat pesan error |

---

## 📌 Catatan

- File GPG biasanya berekstensi `.gpg` atau `.asc`
- Simpan **private key** dan **passphrase** dengan aman — jika hilang, file tidak dapat didekripsi
- Untuk keamanan lebih, gunakan **kunci publik/privat** daripada enkripsi simetris

---

*Panduan ini mengacu pada Gpg4win versi terbaru. Tampilan antarmuka mungkin sedikit berbeda antar versi.*
