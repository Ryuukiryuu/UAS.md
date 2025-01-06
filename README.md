# UAS BAHASA PEMROGRAMAN

class StudentData:
    """Class untuk menyimpan data mahasiswa."""
    def __init__(self, nama, nim, prodi, kelas, nilai_tugas, nilai_uts):
        self.nama = nama
        self.nim = nim
        self.prodi = prodi
        self.kelas = kelas
        self.nilai_tugas = nilai_tugas
        self.nilai_uts = nilai_uts

class StudentView:
    """Class untuk menampilkan data mahasiswa."""
    @staticmethod
    def display_students(students):
        print("\nData Mahasiswa:")
        print("+------+--------------------+-----------+-------+------------+----------+")
        print("| NIM  | Nama               | Prodi     | Kelas | Nilai Tugas | Nilai UTS|")
        print("+------+--------------------+-----------+-------+------------+----------+")
        for student in students:
            print(f"| {student.nim:<4} | {student.nama:<18} | {student.prodi:<9} | {student.kelas:<5} | {student.nilai_tugas:<10} | {student.nilai_uts:<8}|")
        print("+------+--------------------+-----------+-------+------------+----------+")

class StudentProcess:
    """Class untuk memproses data mahasiswa."""
    def __init__(self):
        self.students = []

    def add_student(self):
        try:
            nama = input("Masukkan Nama: ").strip()
            nim = input("Masukkan NIM: ").strip()
            prodi = input("Masukkan Prodi: ").strip()
            kelas = input("Masukkan Kelas: ").strip()
            nilai_tugas = float(input("Masukkan Nilai Tugas: ").strip())
            nilai_uts = float(input("Masukkan Nilai UTS: ").strip())

            if not nama or not nim or not prodi or not kelas:
                raise ValueError("Data tidak boleh kosong!")
            if nilai_tugas < 0 or nilai_tugas > 100 or nilai_uts < 0 or nilai_uts > 100:
                raise ValueError("Nilai harus di antara 0-100!")

            student = StudentData(nama, nim, prodi, kelas, nilai_tugas, nilai_uts)
            self.students.append(student)
            print("Data mahasiswa berhasil ditambahkan!\n")

        except ValueError as ve:
            print(f"Error: {ve}\n")
        except Exception as e:
            print(f"Error tidak terduga: {e}\n")

# Main Program
def main():
    process = StudentProcess()
    view = StudentView()

    while True:
        print("\n=== Program Data Mahasiswa ===")
        print("1. Tambah Data Mahasiswa")
        print("2. Tampilkan Data Mahasiswa")
        print("3. Keluar")

        try:
            choice = int(input("Pilih menu: "))
            if choice == 1:
                process.add_student()
            elif choice == 2:
                view.display_students(process.students)
            elif choice == 3:
                print("Keluar dari program.")
                break
            else:
                print("Pilihan tidak valid. Coba lagi!\n")

        except ValueError:
            print("Input harus berupa angka!\n")

if __name__ == "__main__":
    main()

### **1. Kelas `StudentData`**
Kelas `StudentData` digunakan untuk merepresentasikan data mahasiswa dalam program. Kelas ini memiliki enam atribut: `nama`, `nim`, `prodi`, `kelas`, `nilai_tugas`, dan `nilai_uts`, yang diinisialisasi melalui metode `__init__`. Setiap atribut menyimpan informasi penting tentang mahasiswa, seperti identitas dan nilai akademiknya. Objek dari kelas ini berfungsi sebagai entitas individu untuk setiap mahasiswa yang datanya diolah dan ditampilkan dalam program.

---

### **2. Kelas `StudentView`**
Kelas `StudentView` bertanggung jawab untuk menampilkan data mahasiswa dalam bentuk tabel yang rapi dan terstruktur. Metode `display_students` digunakan untuk mencetak daftar mahasiswa, dengan format kolom yang diratakan menggunakan f-string untuk menjaga estetika. Karena metode ini bersifat statis (`@staticmethod`), penggunaannya tidak memerlukan instansiasi kelas, cukup dipanggil langsung. Kelas ini memastikan bahwa data mahasiswa yang tersimpan dapat dilihat pengguna dengan cara yang mudah dibaca.

---

### **3. Kelas `StudentProcess`**
Kelas `StudentProcess` menangani proses penambahan data mahasiswa ke dalam daftar. Atribut `students` adalah list yang menyimpan objek-objek mahasiswa. Metode `add_student` meminta pengguna memasukkan data melalui input keyboard, dengan validasi untuk memastikan data tidak kosong dan nilai berada dalam rentang 0-100. Jika validasi gagal, kesalahan akan ditangkap dan pesan yang relevan ditampilkan. Setelah validasi berhasil, data mahasiswa baru ditambahkan ke list `students`, yang nantinya dapat ditampilkan oleh `StudentView`.

---

### **4. Program Utama (`main`)**
Program utama (`main`) adalah pusat kontrol program, memberikan antarmuka menu kepada pengguna. Menu ini memiliki tiga opsi: menambah data mahasiswa, menampilkan data mahasiswa, atau keluar dari program. Pilihan diambil melalui input angka, dan validasi dilakukan untuk memastikan hanya angka yang diterima. Dengan menggunakan loop `while True`, program tetap berjalan hingga pengguna memilih untuk keluar. Program utama memanfaatkan kelas `StudentProcess` untuk menambah data dan `StudentView` untuk menampilkan data.

---

### **5. Blok Eksekusi (`if __name__ == "__main__"`)**
Blok ini memastikan bahwa program hanya dijalankan jika file ini dieksekusi langsung, bukan diimpor sebagai modul ke program lain. Ketika file ini dijalankan, fungsi `main` akan dipanggil, memulai program dan menampilkan menu utama. Pendekatan ini menjaga modularitas program, memungkinkan kode digunakan ulang atau diuji dalam konteks lain tanpa memicu eksekusi langsung.

**Konsep modular** Dalam program yang saya buat, diterapkan dengan membagi program ke dalam beberapa **kelas** dan **metode**, masing-masing memiliki tanggung jawab spesifik.

### **1. Pemisahan Tanggung Jawab dengan Kelas**
Program dibagi menjadi tiga kelas utama:
1. **`StudentData`**: Bertanggung jawab untuk merepresentasikan data mahasiswa (sebagai model). Kelas ini hanya berisi atribut dan menyimpan informasi mahasiswa seperti nama, NIM, program studi, kelas, nilai tugas, dan nilai UTS.
   - Contoh modularitas: Semua data terkait mahasiswa dikelola di kelas ini, membuat data lebih terstruktur.

2. **`StudentView`**: Bertugas menampilkan data mahasiswa dalam bentuk tabel. Kelas ini hanya berfokus pada logika tampilan tanpa mencampuri cara data dikumpulkan atau diolah.
   - Contoh modularitas: Jika format tampilan data ingin diubah (misalnya menjadi file JSON atau CSV), Anda cukup memodifikasi kelas ini tanpa memengaruhi logika input atau pengolahan data.

3. **`StudentProcess`**: Menangani proses input data mahasiswa dari pengguna, validasi, dan penyimpanan ke dalam list. Modul ini bertindak sebagai "pengelola data" dan memastikan data yang dimasukkan valid sebelum ditambahkan ke sistem.
   - Contoh modularitas: Proses validasi atau manipulasi data mahasiswa sepenuhnya dilakukan di kelas ini, tanpa memengaruhi cara data ditampilkan atau disimpan.

---

### **2. Penggunaan Metode dengan Tanggung Jawab Tunggal**
Setiap metode memiliki tanggung jawab spesifik:
- **`add_student` (di `StudentProcess`)**:
  - Meminta input data mahasiswa dari pengguna, memvalidasinya, dan menyimpannya dalam list.
  - Modularitas: Semua logika terkait input dan validasi ditempatkan di satu metode, sehingga mudah dipahami dan dirawat.
  
- **`display_students` (di `StudentView`)**:
  - Menampilkan data mahasiswa yang tersimpan dalam list dengan format tabel.
  - Modularitas: Logika tampilan tidak bercampur dengan logika validasi atau penyimpanan data.

---

### **3. Pemisahan Logika dalam Program Utama**
Program utama (`main`) bertindak sebagai pengontrol, yang hanya mengarahkan logika berdasarkan pilihan pengguna:
- Menggunakan objek dari kelas `StudentProcess` untuk menambahkan data mahasiswa.
- Menggunakan objek dari kelas `StudentView` untuk menampilkan data.
- Modularitas: Program utama tidak mengandung detail implementasi seperti cara data disimpan, divalidasi, atau ditampilkan. Tugas-tugas tersebut didelegasikan ke modul masing-masing.

---

### **4. Modularitas dengan Blok Eksekusi**
Blok eksekusi:
```python
if __name__ == "__main__":
    main()
```
Memastikan bahwa kode hanya dieksekusi jika file ini dijalankan secara langsung, bukan diimpor sebagai modul oleh program lain. Modularitas di sini memungkinkan kode (terutama kelas `StudentData`, `StudentView`, dan `StudentProcess`) digunakan kembali di proyek lain tanpa menjalankan program utama.

---

### **Keuntungan Modularitas dalam Codingan**
1. **Keterpisahan Tanggung Jawab**: 
   - Kode dibagi berdasarkan fungsinya (model, view, dan process).
   - Perubahan pada satu bagian (misalnya, tampilan data) tidak memengaruhi bagian lain (misalnya, logika input).

2. **Reusabilitas**:
   - Kelas dan metode dapat digunakan kembali di program lain tanpa modifikasi besar.

3. **Fleksibilitas dan Skalabilitas**:
   - Jika ingin menambahkan fitur baru, seperti menghitung nilai rata-rata atau menyimpan data ke file, Anda bisa melakukannya dengan menambahkan modul baru tanpa merombak struktur yang ada.

4. **Kemudahan Pemeliharaan**:
   - Karena setiap modul independen, debugging dan pengembangan program menjadi lebih mudah.
Konsep modular dalam codingan ini diterapkan dengan baik melalui pemisahan program menjadi tiga kelas (`StudentData`, `StudentView`, dan `StudentProcess`), penggunaan metode dengan tanggung jawab tunggal, serta struktur program utama yang hanya bertugas mengatur alur logika. Modularitas ini membuat program lebih bersih, terorganisir, dan mudah dikembangkan.
