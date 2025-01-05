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
