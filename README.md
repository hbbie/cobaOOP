# cobaOOP
## Nama    : Dhani Naufal Habibie
## Kelas   : TI.24.A4
## NIM     : 312410300
## Matkul  : Bahasa Pemrograman
## Dosen Pengampu: Agung Nugroho, S.Kom., M.Kom.


# Latihan 1

![Screenshot 2024-12-10 185634](https://github.com/user-attachments/assets/6b28317a-58a9-4786-94ba-2d0bf4a5ee20)

You said:
tolong kerjakan dan jelaskan
ChatGPT said:
ChatGPT

Baik, berikut adalah penjelasan dan implementasi dari struktur program sesuai gambar.
# Struktur Program
# data/mahasiswa.py:
Berisi class Mahasiswa (sebagai model untuk data mahasiswa).
Berisi class DataMahasiswa (sebagai pengelola data mahasiswa, seperti tambah, ubah, hapus, dan cari data).

# view/input_form.py:
Berisi class untuk membuat form input data mahasiswa.

# view/mahasiswa.py:
Berisi class untuk menampilkan data mahasiswa dalam bentuk daftar atau detail.

# main.py:
Berisi program utama untuk menjalankan menu aplikasi.

Implementasi/Kode
# 1. File data/mahasiswa.py
```python
class Mahasiswa:
    def __init__(self, nim, nama, jurusan):
        self.nim = nim
        self.nama = nama
        self.jurusan = jurusan

    def __str__(self):
        return f"NIM: {self.nim}, Nama: {self.nama}, Jurusan: {self.jurusan}"

class DataMahasiswa:
    def __init__(self):
        self.data = []

    def tambah_mahasiswa(self, mahasiswa):
        self.data.append(mahasiswa)

    def hapus_mahasiswa(self, nim):
        self.data = [m for m in self.data if m.nim != nim]

    def cari_mahasiswa(self, nim):
        for m in self.data:
            if m.nim == nim:
                return m
        return None

    def ubah_mahasiswa(self, nim, nama_baru, jurusan_baru):
        mahasiswa = self.cari_mahasiswa(nim)
        if mahasiswa:
            mahasiswa.nama = nama_baru
            mahasiswa.jurusan = jurusan_baru
````
            
# 2. File view/input_form.py
```python
class InputForm:
    @staticmethod
    def input_data():
        nim = input("Masukkan NIM: ")
        nama = input("Masukkan Nama: ")
        jurusan = input("Masukkan Jurusan: ")
        return nim, nama, jurusan
  ````
        
# 3. File view/mahasiswa.py
```python
class ViewMahasiswa:
    @staticmethod
    def tampilkan_daftar(data):
        print("Daftar Mahasiswa:")
        for m in data:
            print(m)

    @staticmethod
    def tampilkan_detail(mahasiswa):
        if mahasiswa:
            print("Detail Mahasiswa:")
            print(mahasiswa)
        else:
            print("Mahasiswa tidak ditemukan.")
````

# 4. File main.py
```python
from data.mahasiswa import Mahasiswa, DataMahasiswa
from view.input_form import InputForm
from view.mahasiswa import ViewMahasiswa

def main():
    data_mahasiswa = DataMahasiswa()

    while True:
        print("\nMenu:")
        print("1. Tambah Mahasiswa")
        print("2. Tampilkan Semua Mahasiswa")
        print("3. Cari Mahasiswa")
        print("4. Hapus Mahasiswa")
        print("5. Ubah Mahasiswa")
        print("6. Keluar")

        pilihan = input("Pilih menu: ")
        if pilihan == "1":
            nim, nama, jurusan = InputForm.input_data()
            mahasiswa = Mahasiswa(nim, nama, jurusan)
            data_mahasiswa.tambah_mahasiswa(mahasiswa)
            print("Mahasiswa berhasil ditambahkan.")
        elif pilihan == "2":
            ViewMahasiswa.tampilkan_daftar(data_mahasiswa.data)
        elif pilihan == "3":
            nim = input("Masukkan NIM yang dicari: ")
            mahasiswa = data_mahasiswa.cari_mahasiswa(nim)
            ViewMahasiswa.tampilkan_detail(mahasiswa)
        elif pilihan == "4":
            nim = input("Masukkan NIM yang akan dihapus: ")
            data_mahasiswa.hapus_mahasiswa(nim)
            print("Mahasiswa berhasil dihapus.")
        elif pilihan == "5":
            nim = input("Masukkan NIM yang akan diubah: ")
            nama_baru = input("Masukkan Nama baru: ")
            jurusan_baru = input("Masukkan Jurusan baru: ")
            data_mahasiswa.ubah_mahasiswa(nim, nama_baru, jurusan_baru)
            print("Data mahasiswa berhasil diubah.")
        elif pilihan == "6":
            print("Keluar dari program.")
            break
        else:
            print("Pilihan tidak valid.")

if __name__ == "__main__":
    main()
````

# penjelasan
    Package data: Menangani data dan logika manajemen mahasiswa.
    Package view: Menangani interaksi dengan pengguna (input/output).
    File main.py: Menjalankan aplikasi dan mengintegrasikan modul yang dibuat.

Dalam Python, file __init__.py adalah file khusus yang digunakan untuk menunjukkan bahwa direktori tertentu adalah sebuah package. Ada beberapa alasan mengapa file __init__.py sering dibiarkan kosong, terutama dalam konteks seperti contoh di atas:
1. Tidak Ada Logika yang Dibutuhkan di __init__.py

    Dalam struktur proyek tersebut, file __init__.py tidak memerlukan logika tambahan karena semua kode dan fungsionalitas sudah didefinisikan di modul lain (misalnya
```python
mahasiswa.py, input_form.py).
    Tujuannya hanyalah untuk menunjukkan bahwa direktori data dan view adalah package Python yang valid.
````
3. Menggunakan __init__.py Sebagai Indikator Package

    Secara teknis, sejak Python 3.3, file __init__.py tidak lagi diwajibkan untuk mendeklarasikan package. Namun, tetap disarankan untuk menyertakan file ini, meskipun kosong, agar kompatibel dengan versi Python yang lebih lama atau untuk menambah kejelasan struktur proyek.

4. Kapan __init__.py Tidak Kosong?

Ada beberapa skenario di mana Anda mungkin menambahkan kode ke dalam __init__.py:

    Ekspor Simbol: Untuk menentukan apa yang akan diimpor saat menggunakan from package import *.

from .mahasiswa import Mahasiswa, DataMahasiswa

Logika Inisialisasi Package: Jika package membutuhkan konfigurasi awal.
Shortcut Import: Untuk mempermudah impor modul dengan menyediakannya langsung di level package. Misalnya:
```python
    # __init__.py di folder view
    from .input_form import InputForm
    from .mahasiswa import ViewMahasiswa
````
Kesimpulan

Dalam contoh yang Anda berikan, __init__.py dibiarkan kosong karena tidak ada kebutuhan khusus untuk logika tambahan di dalam file tersebut. Semua fungsionalitas sudah didefinisikan dalam modul-modul terkait (mahasiswa.py, input_form.py). Ini adalah praktik yang umum dan sederhana.

# Hasil Program
![image](https://github.com/user-attachments/assets/6394778e-2d89-41f9-85b5-af24355d333c)

![image](https://github.com/user-attachments/assets/00173cbb-0f10-4910-97f4-572561197385)

![image](https://github.com/user-attachments/assets/fe8e03c0-65c7-42c4-a7af-7670d2cc90ea)




