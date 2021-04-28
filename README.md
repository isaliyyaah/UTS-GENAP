package com.company;

import java.util.ArrayList;
import java.util.List;
import java.util.Scanner;

public class Main
{
    public static void main(String[] args)
    {
        int cho;
        String Uname, unameIn, passIn;
        String Pass;
        ArrayList<Tilang> List = new ArrayList<>();
        Scanner put = new Scanner(System.in);

        Uname = "hayput";
        Pass = "12345";

        do{
            System.out.println("L O G I N");
            Scanner put1 = new Scanner(System.in);
            System.out.println("Input Username : ");
            unameIn = put1.nextLine();

            System.out.println("Input Password : ");
            passIn = put1.nextLine();
        } while (!unameIn.equals(Uname) && !passIn.equals(Pass));

        do{
            System.out.println("===============================");
            System.out.println("E-TILANG : KOTA WARNA WARNI     ");
            System.out.println("===============================");
            System.out.println("1. Pendataan Pelanggar");
            System.out.println("2. Melihat Data Pelanggar");
            System.out.println("3. Menampilkan Surat Tilang ");
            System.out.println("4. Logout");
            System.out.println("===============================");
            System.out.println("Pilihan : ");
            cho = put.nextInt();
            switch (cho) {
                case 1:
                    Pelanggaran(List);
                    break;
                case 2:
                    Data(List);
                    break;
                case 3 :
                    Surat(List);
            }
        } while (cho != 4);
    }
    
      private static void Pelanggaran(ArrayList<Tilang> List)
      {
        String nama, alamat, nik, jeniskendaraan, tipekendaraan, choice, nomortelpon, email;
        int jenispelanggaran ;
        List<JenisPelanggaran> jenis = new ArrayList<>();
        Scanner add = new Scanner(System.in);

        System.out.print("Masukan Nama : ");
        nama = add.nextLine();
        System.out.print("Masukan Alamat : ");
        alamat = add.nextLine();
        System.out.print("Masukan NIK : ");
        nik = add.nextLine();

        System.out.println("Jenis Kendaraan ");
        System.out.println("1. Roda Dua");
        System.out.println("2. Roda Empat/Lebih");
        System.out.println("Masukkan Nomor :");
        jeniskendaraan = add.nextLine();

        System.out.println("Tipe Kendaraan ");
        System.out.println("1. Motor");
        System.out.println("2. Mobil");
        System.out.println("3. Bis");
        System.out.println("4. Truk/Tronton");
        System.out.println("Masukkan  Tipe Kendaraan :");
        tipekendaraan = add.nextLine();

        System.out.print("Masukan No.Telpon : ");
        nomortelpon = add.nextLine();
        System.out.print("Masukan E-mail : ");
        email = add.nextLine();

        do{
            System.out.println("Jenis Pelanggaran ");
            System.out.println("1. Menggunakan Gawai / Handphone saat berkendara");
            System.out.println("2. Tidak memakai helm");
            System.out.println("3. Tidak memakai sabuk pengaman");
            System.out.println("4. Melanggar rambu lalu lintas dan marka jalan");
            System.out.println("5. Memakai plat nomor palsu");
            System.out.println("Masukkan  Jenis Pelanggaran :");
            jenispelanggaran = add.nextInt();
            add.nextLine();
            if (jenispelanggaran > 5) {
                choice = "no";
            } else {
                jenis.add(new JenisPelanggaran(jenispelanggaran));
                System.out.println("Adakah pelanggaran lain? (yes/no)");
                choice = add.nextLine();
            }
        } while (choice.equals("yes"));

        List.add(new Tilang(nama, alamat, nik, jeniskendaraan, tipekendaraan, nomortelpon, email, jenis ));
    }
    
    private static void Data(ArrayList<Tilang> List)
    {
        if (List != null) {
            for (int i = 0; i < List.size(); i++) {
                System.out.println("====================================");
                System.out.println("Nama : " + List.get(i).getNama());
                System.out.println("Alamat : " + List.get(i).getAlamat());
                System.out.println("NIK : " + List.get(i).getNik());
                System.out.println("jenis kendaraan : " + List.get(i).getJeniskendaraan());
                System.out.println("tipe kendaraan : " + List.get(i).getTipekendaraan());
                System.out.println("notelpon : " + List.get(i).getNomortelpon());
                System.out.println("email : " + List.get(i).getEmail());
                System.out.println("tipe pelanggaran : ");
                for (int a = 0; a < List.get(i).getJp().size(); a++) {
                    System.out.println((a + 1) + " = " + List.get(i).getJp().get(a).number);
                }
            }
        } else {
            System.out.println("Try again!");
        }
    }
    
    private static void Surat(ArrayList<Tilang> List)
    {
        int tilang, total = 0;
        Scanner surat = new Scanner(System.in);
        String[] jenispel = {
                "Menggunakan Gawai / Handphone saat berkendara",
                "Tidak memakai helm",
                "Tidak memakai sabuk pengaman",
                "Melanggar rambu lalu lintas dan marka jalan",
                "Memakai plat nomor palsu",
        };
        int[] harga = {
                750000,
                250000,
                250000,
                500000,
                500000,
        };

        Data(List);
        System.out.println("Pilih ID Tilang : ");
        tilang = surat.nextInt() - 1;
        Tilang t = List.get(tilang);
        System.out.println("Nama : " + t.getNama());
        System.out.println("Alamat : " + t.getAlamat());
        System.out.println("NIK : " + t.getNik());
        System.out.println("jenis kendaraan : " + t.getJeniskendaraan());
        System.out.println("tipe kendaraan : " + t.getTipekendaraan());
        System.out.println("notelp : " + t.getNomortelpon());
        System.out.println("email : " + t.getEmail());
        System.out.println("tipe pelanggaran : ");
        for (int a = 0; a < t.getJp().size(); a++) {
            System.out.println("pelanggaran ke " + (a + 1) + " = " + jenispel[a]);
            System.out.println("biaya denda " + (a + 1) + " = " + harga[a]);
            System.out.println("=============================================");
            total = total + harga[a];
        }
        System.out.println("total denda : " + total);
    }
}

class JenisPelanggaran
{
    int number;

    public JenisPelanggaran(int noJenis) {
        this.number = noJenis;
    }

    public int getNoJenis() {
        return number;
    }

    public void setNoJenis(int noJenis) {
        this.number = noJenis;
    }
}

class Tilang
{
    String nama, alamat, nik, jeniskendaraan, tipekendaraan, nomortelpon, email;
    List<JenisPelanggaran> jp;

    public Tilang(String nama, String alamat, String nik, String jeniskendaraan, String tipekendaraan,  String nomortelpon, String email, List<JenisPelanggaran> jp)
    {
        this.nama = nama;
        this.alamat = alamat;
        this.nik = nik;
        this.jeniskendaraan = jeniskendaraan;
        this.tipekendaraan = tipekendaraan;
        this.nomortelpon = nomortelpon;
        this.email = email;
        this.jp = jp;
    }

    public List<JenisPelanggaran> getJp()
    {
        return jp;
    }

    public void setJp(List<JenisPelanggaran> jp)
    {
        this.jp = jp;
    }

    public String getJeniskendaraan()
    {
        return jeniskendaraan;
    }

    public void setJeniskendaraan(String jeniskendaraan)
    {
        this.jeniskendaraan = jeniskendaraan;
    }

    public String getNama()
    {
        return nama;
    }

    public void setNama(String nama)
    {
        this.nama = nama;
    }

    public String getAlamat()
    {
        return alamat;
    }

    public void setAlamat(String alamat)
    {
        this.alamat = alamat;
    }

    public String getNik()
    {
        return nik;
    }

    public void setNik(String nik)
    {
        this.nik = nik;
    }

    public String getTipekendaraan()
    {
        return tipekendaraan;
    }

    public void setTipekendaraan(String tipekendaraan)
    {
        this.tipekendaraan = tipekendaraan;
    }

    public String getNomortelpon()
    {
        return nomortelpon;
    }

    public void setNomortelpon(String nomortelpon)
    {
        this.nomortelpon = nomortelpon;
    }

    public String getEmail()
    {
        return email;
    }

    public void setEmail(String email)
    {
        this.email = email;
    }
}
