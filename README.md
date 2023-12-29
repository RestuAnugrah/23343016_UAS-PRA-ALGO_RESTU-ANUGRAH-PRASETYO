# 23343016_UAS-PRA-ALGO_RESTU-ANUGRAH-PRASETYO

#include <iostream>
#include <string>
#define MAX_SISWA 100

struct Siswa {
    std::string nama;
    std::string alamat;
    int nis;
    float nilaiMatematika;
    float nilaiIPA;
    float nilaiBahasaIndonesia;
    float nilai;
    bool diproses;
};

Siswa daftarSiswa[MAX_SISWA];
int jumlahSiswa = 0;
const int kuota = 50;

void inputNilaiSiswa(int nis) {
	bool found = false;
    for (int i = 0; i < jumlahSiswa; i++) {
        if (daftarSiswa[i].nis == nis) {
        	found = true;
            std::cout << "Masukkan nilai Matematika: ";
            std::cin >> daftarSiswa[i].nilaiMatematika;
            std::cout << "Masukkan nilai IPA: ";
            std::cin >> daftarSiswa[i].nilaiIPA;
            std::cout << "Masukkan nilai Bahasa Indonesia: ";
            std::cin >> daftarSiswa[i].nilaiBahasaIndonesia;
            return;
        }
    }
    if (!found){
    std::cout << "NIS tidak ditemukan." << std::endl;
   }
}

void inputDataSiswa() {
    if (jumlahSiswa < MAX_SISWA) {
        std::cout << "Masukkan nama siswa: ";
        std::cin >> daftarSiswa[jumlahSiswa].nama;
        std::cout << "Masukkan alamat siswa: ";
        std::cin >> daftarSiswa[jumlahSiswa].alamat;
        
        bool validNIS = false;
        do {
            std::cout << "Masukkan NIS siswa (harus unik): ";
            std::cin >> daftarSiswa[jumlahSiswa].nis;
            
            validNIS = true;
            for (int i = 0; i < jumlahSiswa; i++) {
                if (daftarSiswa[i].nis == daftarSiswa[jumlahSiswa].nis) {
                    std::cout << "NIS sudah digunakan. Masukkan NIS lain." << std::endl;
                    validNIS = false;
                    break;
                }
            }
        } while (!validNIS);
        
        std::cout << "Nilai siswa: ";
        std::cin >> daftarSiswa[jumlahSiswa].nilai;
        daftarSiswa[jumlahSiswa].diproses = false;
        jumlahSiswa++;
    } else {
        std::cout << "Kuota siswa penuh" << std::endl;
    }
}

void hitungRataRata() {
    float totalNilai = 0;
    for (int i = 0; i < jumlahSiswa; i++) {
        totalNilai += daftarSiswa[i].nilai;
    }
    float rataRata = totalNilai / jumlahSiswa;
    std::cout << "Rata-rata nilai siswa: " << rataRata << std::endl;
}

void tampilkanKuotaTersisa() {
    int siswaLulus = 0;
    for (int i = 0; i < jumlahSiswa; i++) {
        if (daftarSiswa[i].diproses) {
            siswaLulus++;
        }
    }
    int kuotaTersisa = kuota - siswaLulus;
    std::cout << "Jumlah kuota siswa yang dapat lulus yang tersisa: " << kuotaTersisa << std::endl;
}

void tampilkanSiswaBelumDiproses() {
    std::cout << "Data siswa yang belum diproses: " << std::endl;
    for (int i = 0; i < jumlahSiswa; i++) {
        if (!daftarSiswa[i].diproses) {
            std::cout << "Nama: " << daftarSiswa[i].nama << ", Alamat: " << daftarSiswa[i].alamat << ", NIS: " << daftarSiswa[i].nis << std::endl;
        }
    }
}

void tandaiSelesaiProses(int nis) {
    for (int i = 0; i < jumlahSiswa; i++) {
        if (daftarSiswa[i].nis == nis) {
            daftarSiswa[i].diproses = true;
            std::cout << "Data siswa dengan NIS " << nis << " telah ditandai sebagai selesai diproses." << std::endl;
            return;
        }
    }
    std::cout << "NIS tidak ditemukan." << std::endl;
}

void tampilkanSiswaSudahDiproses() {
    std::cout << "Data siswa yang sudah diproses: " << std::endl;
    for (int i = 0; i < jumlahSiswa; i++) {
        if (daftarSiswa[i].diproses) {
            std::cout << "Nama: " << daftarSiswa[i].nama << ", Alamat: " << daftarSiswa[i].alamat << ", NIS: " << daftarSiswa[i].nis << std::endl;
        }
    }
}

int main() {
    int pilihan;
    do {
        std::cout << "\nMenu:\n1. Input data siswa\n2. Input nilai siswa\n3. Hitung Rata Rata Nilai Siswa\n4. Tampilkan Kuota Siswa Yang Tersisa\n5. Tampilkan Siswa Yang Belum Diproses\n6. Tandai Data Siswa Yang Sudah Diproses\n7. Tampilkan Siswa Yang Sudah Diproses\n8. Keluar\nPilih menu: ";
        std::cin >> pilihan;

        switch (pilihan) {
            case 1:
                inputDataSiswa();
                break;
                case 2:
    int inputNIS;
    std::cout << "Masukkan NIS siswa untuk mengimputkan nilai: ";
    std::cin >> inputNIS;
    inputNilaiSiswa(inputNIS);
    break;

            case 3:
                hitungRataRata();
                break;
            case 4:
                tampilkanKuotaTersisa();
                break;
            case 5:
                tampilkanSiswaBelumDiproses();
                break;
            case 6:
                int nis;
                std::cout << "Masukkan NIS siswa yang sudah selesai diproses: ";
                std::cin >> nis;
                tandaiSelesaiProses(nis);
                break;
            case 7:
                tampilkanSiswaSudahDiproses();
                break;
            case 8:
                std::cout << "Program selesai.";
                break;
            default:
                std::cout << "Pilihan tidak valid. Silakan pilih lagi." << std::endl;
        }
    } while (pilihan != 8);

    return 0;
}
