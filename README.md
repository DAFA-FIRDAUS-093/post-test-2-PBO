-------------------------SISTEM TRAVEL MOBIL ANTAR KOTA KALTIM------------------------------

Deskripsi Singkat

Program ini merupakan aplikasi sederhana berbasis Java Console yang digunakan untuk mengelola data travel mobil antar kota di Kalimantan Timur.
Fitur yang tersedia meliputi:

1.Menambah data travel

2.Melihat semua data travel

3.Mengubah data travel

4.Menghapus data travel

Program ini dibuat dengan konsep OOP menggunakan beberapa class dan package (model, service, dan main).


Alur Program 

1. Saat dijalankan, program menampilkan menu utama:

1 Tambah Data Travel

2 Lihat Semua Data Travel

3 Update Data Travel

4 Hapus Data Travel

5 Keluar

Dokumentasi menu:

<img width="491" height="124" alt="image" src="https://github.com/user-attachments/assets/95852926-62dc-4a1a-8e68-aa209a40d62b" />


2. User memilih menu dengan memasukkan angka.

   1.Jika user memasukan angka 1 maka user menambahkan data untuk travel.

   <img width="358" height="205" alt="image" src="https://github.com/user-attachments/assets/026f5ac7-21c2-4244-bb54-3a5a41c34b73" />

   2.Jika user memasukan angka 2 maka user akan melihat semua data untuk travel.

   <img width="628" height="204" alt="image" src="https://github.com/user-attachments/assets/46ad78d9-3f28-413e-ab1e-caf7e9ce464a" />

   3.Jika user memilih angka tiga maka akan mengupdate data untuk travel.

   <img width="462" height="221" alt="image" src="https://github.com/user-attachments/assets/4ac5b837-be31-4b28-859f-0e65397a6944" />

3. Program akan menjalankan logika sesuai pilihan user:

  1. Tambah Data → User mengisi sopir, asal, tujuan, dan tipe mobil, lalu data disimpan ke ArrayList.

  2. Lihat Data → Program menampilkan semua data yang tersimpan.

  3. Update Data → User memilih data berdasarkan nomor, lalu mengisi data baru untuk mengganti.

  4. Hapus Data → User memilih data berdasarkan nomor, lalu data akan dihapus dari ArrayList.

  5. Keluar → Program berhenti.

4. Program akan terus berjalan dalam perulangan hingga user memilih menu keluar.


5. Kode Program


   1. Kode Program untuk packages main:

      
import java.util.Scanner;
import model.Travel;
import service.service;

public class main {
    public static void main(String[] args) {
        Scanner input = new Scanner(System.in);
        service service = new service();
        boolean jalan = true;

        while (jalan) {
            System.out.println("SISTEM TRAVEL MOBIL ANTAR KOTA KALTIM");
            System.out.println("1. Tambah Data Travel");
            System.out.println("2. Lihat Semua Data Travel");
            System.out.println("3. Update Data Travel");
            System.out.println("4. Hapus Data Travel");
            System.out.println("5. Keluar");
            System.out.print("Pilih menu: ");
            int pilih = input.nextInt();
            input.nextLine(); // clear buffer

            switch (pilih) {
                case 1:
                    System.out.print("Nama Sopir: ");
                    String sopir = input.nextLine();
                    if (sopir.isEmpty()) {
                        System.out.println("Nama sopir tidak boleh kosong!");
                        break; // balik ke menu utama
                    }

                    System.out.print("Sedang diKota Mana: ");
                    String asal = input.nextLine();
                    if (asal.isEmpty()) {
                        System.out.println("Asal tidak boleh kosong!");
                        break;
                    }

                    System.out.print("Kota Tujuan: ");
                    String tujuan = input.nextLine();
                    if (tujuan.isEmpty()) {
                        System.out.println("Tujuan tidak boleh kosong!");
                        break;
                    }

                    System.out.print("Tipe Mobil: ");
                    String tipe = input.nextLine();
                    if (tipe.isEmpty()) {
                        System.out.println("Tipe mobil tidak boleh kosong!");
                        break;
                    }

                    Travel t = new Travel(sopir, asal, tujuan, tipe);
                    service.tambahTravel(t);
                    break;

                case 2:
                    service.lihatTravel();
                    break;

                case 3:
                    service.lihatTravel();
                    System.out.print("Pilih nomor data yang ingin diupdate: ");
                    int idxUpdate = input.nextInt() - 1;
                    input.nextLine();

                    System.out.print("Nama Sopir baru: ");
                    sopir = input.nextLine();
                    System.out.print("Sedang diKota Mana: ");
                    asal = input.nextLine();
                    System.out.print("Kota Tujuan baru: ");
                    tujuan = input.nextLine();
                    System.out.print("Tipe Mobil baru: ");
                    tipe = input.nextLine();

                    Travel travelBaru = new Travel(sopir, asal, tujuan, tipe);
                    service.updateTravel(idxUpdate, travelBaru);
                    break;

                case 4:
                    service.lihatTravel();
                    System.out.print("Pilih nomor data yang ingin dihapus: ");
                    int idxHapus = input.nextInt() - 1;
                    input.nextLine();
                    service.hapusTravel(idxHapus);
                    break;

                case 5:
                    jalan = false;
                    System.out.println("Terima kasih!");
                    break;

                default:
                    System.out.println("Pilihan tidak valid!");
            }
        }
    }
}

  2. Kode program untuk packages service:



   import java.util.ArrayList;
import model.Travel;

public class service {
    private ArrayList<Travel> daftarTravel = new ArrayList<>();

    public void tambahTravel(Travel travel) {
        daftarTravel.add(travel);
        System.out.println("Data berhasil ditambahkan!");
    }

    public void lihatTravel() {
        if (daftarTravel.isEmpty()) {
            System.out.println("Belum ada data travel.");
        } else {
            System.out.println("DAFTAR TRAVEL:");
            for (int i = 0; i < daftarTravel.size(); i++) {
                System.out.println((i + 1) + ". " + daftarTravel.get(i));
            }
        }
    }

    public void updateTravel(int index, Travel travelBaru) {
        if (index >= 0 && index < daftarTravel.size()) {
            daftarTravel.set(index, travelBaru);
            System.out.println("Data berhasil diupdate!");
        } else {
            System.out.println("Data tidak ditemukan.");
        }
    }

    public void hapusTravel(int index) {
        if (index >= 0 && index < daftarTravel.size()) {
            daftarTravel.remove(index);
            System.out.println("Data berhasil dihapus!");
        } else {
            System.out.println("Data tidak ditemukan.");
        }
    }
}
   

  3. Kode Program untuk packages 


  public class Travel {
    private String sopir;
    private String asal;
    private String tujuan;
    private String tipeMobil;

    // Constructor
    public Travel(String sopir, String asal, String tujuan, String tipeMobil) {
        this.sopir = sopir;
        this.asal = asal;
        this.tujuan = tujuan;
        this.tipeMobil = tipeMobil;
    }

    // Getter & Setter
    public String getSopir() {
        return sopir;
    }

    public void setSopir(String sopir) {
        this.sopir = sopir;
    }

    public String getAsal() {
        return asal;
    }

    public void setAsal(String asal) {
        this.asal = asal;
    }

    public String getTujuan() {
        return tujuan;
    }

    public void setTujuan(String tujuan) {
        this.tujuan = tujuan;
    }

    public String getTipeMobil() {
        return tipeMobil;
    }

    public void setTipeMobil(String tipeMobil) {
        this.tipeMobil = tipeMobil;
    }

    @Override
    public String toString() {
        return "Sopir: " + sopir + ", Asal: " + asal + ", Tujuan: " + tujuan + ", Tipe Mobil: " + tipeMobil;
    }
}



6. Untuk tampilan di Source Packages untuk ketiga packages tersebut:


   <img width="406" height="185" alt="image" src="https://github.com/user-attachments/assets/426a90c7-7a0f-4e84-9b24-a6a08d0ab69c" />

7. Disini saya memasangkan invalid input, jadi jika user tidak memasukan data maka akan muncul notifikasi "Nama sopir tidak boleh kosong!".

   contoh jika user tidak memasukan data :

   <img width="326" height="156" alt="image" src="https://github.com/user-attachments/assets/90ce120b-62a3-4f9e-8ca4-995ae5da4633" />


   
