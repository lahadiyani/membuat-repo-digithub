Baik, berikut adalah dokumentasi lengkap yang hanya berisi kode dalam format Markdown:

```markdown
# Dokumentasi Penggunaan Git dan GitHub

## 1. Pembuatan Repository Pertama

### 1.1 Buat Repository di GitHub
1. Masuk ke akun GitHub kamu.
2. Klik tombol **"New"** di bagian kiri atas untuk membuat repository baru.
3. Isi nama repository, misalnya `test-repo`.
4. Pilih visibilitas repository (Public atau Private).
5. Klik **"Create repository"**.

### 1.2 Membuat Kunci SSH
Jika kamu belum memiliki kunci SSH, kamu bisa membuatnya dengan langkah berikut:

```bash
ssh-keygen -t rsa -b 4096 -C "youremail@example.com"
```

### 1.3 Menambahkan Kunci SSH ke GitHub
1. Salin kunci publik ke clipboard:

   ```bash
   cat ~/.ssh/id_rsa.pub
   ```

2. Masuk ke GitHub, buka **Settings** > **SSH and GPG keys**.
3. Klik **"New SSH key"**.
4. Tempel kunci publik yang sudah disalin, beri judul, lalu klik **"Add SSH key"**.

## 2. Konfigurasi Nama dan Email

Setelah menambahkan kunci SSH, kamu perlu mengkonfigurasi nama dan email untuk Git:

```bash
git config --global user.name "Nama Kamu"
git config --global user.email "youremail@example.com"
```

## 3. Memulai Repository Lokal

### 3.1 Inisialisasi Repository
Navigasi ke direktori di mana kamu ingin membuat proyek dan jalankan:

```bash
git init
```

### 3.2 Menambahkan File
Buat file baru, misalnya `README.md`, dan tambahkan konten:

```bash
echo "# Ini adalah test" >> README.md
```

Kemudian, tambahkan file ke staging area:

```bash
git add README.md
```

### 3.3 Melakukan Commit
Setelah menambahkan file, lakukan commit untuk menyimpan perubahan:

```bash
git commit -m "Initial commit"
```

## 4. Mengelola Branch

### 4.1 Membuat dan Beralih ke Branch Utama
Jika kamu ingin mengganti nama branch utama menjadi `main`, gunakan perintah berikut:

```bash
git branch -M main
```

## 5. Menambahkan Remote Repository

### 5.1 Menambahkan Remote Origin
Setelah repository lokal siap, tambahkan remote repository ke GitHub:

```bash
git remote add origin git@github.com:username/test-repo.git
```

## 6. Mengirim Perubahan ke Remote

### 6.1 Melakukan Push ke GitHub
Untuk mengirim commit ke GitHub, jalankan:

```bash
git push -u origin main
```

## 7. Troubleshooting

### 7.1 Jika Mendapatkan Error
- **Error: "Permission denied (publickey)"**
- **Error: "Repository not found"**

### 7.2 Jika Push Ditolak
Jika kamu menerima pesan error bahwa push ditolak karena ada perubahan di remote, gunakan:

```bash
git pull origin main --rebase
```
```
