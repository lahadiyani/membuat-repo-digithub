### Menghapus File Tertentu di Dalam Repository Git

1. **Masuk ke Direktori Repository**:
   Pertama, buka terminal dan navigasikan ke direktori repository Git yang ingin kamu ubah:

   ```bash
   cd path/to/your/repo
   ```

2. **Hapus File**:
   Gunakan perintah `git rm` diikuti dengan nama file yang ingin kamu hapus. Misalnya, jika kamu ingin menghapus file bernama `file_to_remove.txt`, gunakan perintah berikut:

   ```bash
   git rm file_to_remove.txt
   ```

   Jika kamu ingin menghapus file tanpa menghapusnya dari sistem file (misalnya, hanya dari repositori), gunakan opsi `--cached`:

   ```bash
   git rm --cached file_to_remove.txt
   ```

3. **Commit Perubahan**:
   Setelah menghapus file, kamu perlu melakukan commit untuk merekam perubahan tersebut dalam repository:

   ```bash
   git commit -m "Menghapus file_to_remove.txt"
   ```

4. **Push Perubahan ke Remote Repository**:
   Jika kamu bekerja dengan remote repository, seperti di GitHub, kamu perlu melakukan push untuk mengirim perubahan ke server:

   ```bash
   git push origin main
   ```

   Pastikan untuk mengganti `main` dengan nama cabang yang sesuai jika kamu menggunakan cabang yang berbeda.

### Menggunakan Command Line

Berikut adalah contoh lengkap perintah dalam format command line:

```bash
cd path/to/your/repo
git rm file_to_remove.txt
git commit -m "Menghapus file_to_remove.txt"
git push origin main
```

### Catatan

- **Menghapus Beberapa File**: Jika kamu ingin menghapus beberapa file sekaligus, cukup sebutkan nama file yang ingin dihapus, dipisahkan dengan spasi:

  ```bash
  git rm file1.txt file2.txt
  ```

- **Menghapus Seluruh Direktori**: Untuk menghapus seluruh direktori, gunakan perintah berikut:

  ```bash
  git rm -r directory_name
  ```

- **Undo Remove**: Jika kamu ingin membatalkan penghapusan file yang belum di-commit, gunakan:

  ```bash
  git checkout -- file_to_remove.txt
  ```
