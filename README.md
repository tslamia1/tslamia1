56274190import java.util.ArrayList;
import java.util.Scanner;

class MahasiswaTest {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        System.out.println("Selamat Datang");
        System.out.print("Masukkan Nama : ");
        String nama = scanner.nextLine();
        System.out.print("Masukkan NPM : ");
        String npm = scanner.nextLine();
        System.out.print("Jumlah Matakuliah : ");
        int jumlahMatakuliah = scanner.nextInt();

        Mahasiswa mahasiswa = new Mahasiswa(nama, npm, jumlahMatakuliah);

        mahasiswa.cetakData();
    }
}

class Mahasiswa {
    private String nama;
    private String npm;
    private KHS khs;

    public Mahasiswa(String nama, String npm, int jumlahMatakuliah) {
        this.nama = nama;
        this.npm = npm;
        this.khs = new KHS();
        setDataMatakuliah(jumlahMatakuliah);
    }

    public String getNama() {
        return nama;
    }

    public void setNama(String nama) {
        this.nama = nama;
    }

    public String getNpm() {
        return npm;
    }

    public void setNpm(String npm) {
        this.npm = npm;
    }

    public KHS getKhs() {
        return khs;
    }

    private void setDataMatakuliah(int jumlahMatakuliah) {
        for (int i = 0; i < jumlahMatakuliah; i++) {
            Scanner scanner = new Scanner(System.in);

            System.out.print("Nama Matakuliah : ");
            String namaMatkul = scanner.nextLine();
            System.out.print("SKS : ");
            int sks = scanner.nextInt();
            System.out.print("Grade : ");
            char grade = scanner.next().charAt(0);

            NilaiPBO nilaiPBO = new NilaiPBO();
            nilaiPBO.setData(namaMatkul, sks, grade);
            khs.addMatakuliah(nilaiPBO);
        }
    }

    public void cetakData() {
        System.out.println("Nama : " + nama);
        System.out.println("NPM : " + npm);
        System.out.println("IPK : " + khs.getIPK());
    }
}

class NilaiPBO {
    private String matkul;
    private int sks;
    private char grade;

    public void setData(String matkul, int sks, char grade) {
        this.matkul = matkul;
        this.sks = sks;
        this.grade = grade;
    }

    public String getMatkul() {
        return matkul;
    }

    public int getSks() {
        return sks;
    }

    public char getGrade() {
        return grade;
    }

    public int getPoin() {
        int poin = 0;
        switch (grade) {
            case 'A':
                poin = 4;
                break;
            case 'B':
                poin = 3;
                break;
            case 'C':
                poin = 2;
                break;
            case 'D':
                poin = 1;
                break;
            case 'E':
                poin = 0;
                break;
        }
        return poin;
    }
}

class KHS {
    private ArrayList<NilaiPBO> matakuliahList;

    public KHS() {
        matakuliahList = new ArrayList<>();
    }

    public void addMatakuliah(NilaiPBO nilaiPBO) {
        matakuliahList.add(nilaiPBO);
    }

    public void cetakKHS() {
        for (NilaiPBO nilaiPBO : matakuliahList) {
            System.out.println("Matakuliah: " + nilaiPBO.getMatkul());
            System.out.println("SKS: " + nilaiPBO.getSks());
            System.out.println("Grade: " + nilaiPBO.getGrade());
            System.out.println();
        }
    }

    public double getIPK() {
        int totalPoin = 0;
        int totalSks = 0;

        for (NilaiPBO nilaiPBO : matakuliahList) {
            totalPoin += nilaiPBO.getPoin() * nilaiPBO.getSks();
            totalSks += nilaiPBO.getSks();
        }

        if (totalSks == 0) {
            return 0.0;
        }

        return (double) totalPoin / totalSks;
    }
}

