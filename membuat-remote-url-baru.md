# Mengganti Nama Repository GitHub

## 1. Mengganti Nama Repository di GitHub

### 1.1 Masuk ke Akun GitHub
1. Buka [GitHub](https://github.com/) dan masuk ke akun kamu.

### 1.2 Akses Repository
1. Klik pada nama repository yang ingin kamu ganti namanya.

### 1.3 Masuk ke Pengaturan Repository
1. Klik tab **"Settings"** yang ada di bagian kanan atas halaman repository.

### 1.4 Mengganti Nama Repository
1. Di bagian **"Repository name"**, ubah nama repository sesuai keinginan.
2. Klik tombol **"Rename"** untuk menyimpan perubahan.

## 2. Mengupdate Remote Repository di Local

Setelah mengganti nama repository di GitHub, kamu perlu memperbarui URL remote di repository lokal agar sesuai dengan nama baru.

### 2.1 Cek Remote Repository
Periksa remote repository yang terhubung dengan perintah:

```bash
git remote -v
```

### 2.2 Mengganti URL Remote
Jika nama repository di GitHub berubah, update URL remote dengan perintah berikut:

```bash
git remote set-url origin git@github.com:username/nama-repo-baru.git
```

Gantilah `username` dengan nama pengguna GitHub kamu dan `nama-repo-baru` dengan nama baru repository yang telah kamu ubah.

## 3. Verifikasi Perubahan

Setelah memperbarui URL remote, verifikasi apakah perubahan berhasil dengan perintah:

```bash
git remote -v
```

Kamu harus melihat URL baru untuk remote `origin`.

## 4. Melakukan Push

Setelah mengganti nama repository dan memperbarui remote, kamu bisa melakukan push seperti biasa:

```bash
git push origin main
```
