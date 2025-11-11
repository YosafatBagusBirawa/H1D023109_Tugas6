## 🔄 Proses Passing Data

Aplikasi ini mendemonstrasikan cara mengirim data dari satu halaman ke halaman lain menggunakan Navigator.

### 1. Alur Umum

```
FormData (Halaman Input)
    ↓ (User klik Simpan)
Validasi & Ambil Data
    ↓
Navigator.push() + Constructor
    ↓
TampilData (Halaman Display)
    ↓ (Tampilkan Data)
```

### 2. Penjelasan Detail

#### Step 1: User Mengisi Form di FormData

Di file `lib/ui/form_data.dart`, user mengisi tiga TextField:

```dart
final _namaController = TextEditingController();
final _nimController = TextEditingController();
final _tahunController = TextEditingController();
```

- Nama: String (contoh: "cihuy")
- NIM: String (contoh: "H1D023109")
- Tahun Lahir: Integer (contoh: 2005)

#### Step 2: User Klik Tombol "Simpan"

Ketika tombol Simpan ditekan, method `_tombolSimpan()` dijalankan:

```dart
_tombolSimpan(){
  return ElevatedButton(
    onPressed: (){
      // Ambil data dari controller
      String nama = _namaController.text;
      String nim = _nimController.text;
      int tahun = int.parse(_tahunController.text);
      
      // Kirim data ke halaman berikutnya
      Navigator.of(context).push(MaterialPageRoute(
        builder: (context) => TampilData(
          nama: nama,
          nim: nim,
          tahun: tahun,
        )));
    },
    child: const Text("simpan")
  );
}
```

Penjelasan:
- `_namaController.text` → mengambil text yang diketik user
- `int.parse()` → mengkonversi string menjadi integer
- `Navigator.of(context).push()` → membuka halaman baru
- `MaterialPageRoute` → mendefinisikan rute/halaman yang ingin dibuka
- `TampilData(nama: nama, nim: nim, tahun: tahun)` → mengirim data via constructor

#### Step 3: Constructor TampilData Menerima Data

Di file `lib/ui/tampil_data.dart`, kita menerima data melalui constructor:

```dart
class TampilData extends StatelessWidget {
  final String nama;      // Menyimpan nama
  final String nim;       // Menyimpan NIM
  final int tahun;        // Menyimpan tahun lahir

  const TampilData({
    Key? key,
    required this.nama,    // Wajib dikirim
    required this.nim,     // Wajib dikirim
    required this.tahun,   // Wajib dikirim
  }) : super(key: key);
```

Penjelasan:
- `required` → parameter wajib dikirim saat membuat instance TampilData
- `final` → tidak bisa diubah setelah dibuat
- Data tersimpan di dalam instance widget

#### Step 4: Tampilkan Data di Halaman TampilData

Data ditampilkan di `build()` method:

```dart
@override
Widget build(BuildContext context) {
  final currentYear = DateTime.now().year;
  final umur = currentYear - tahun;  // Hitung umur dari tahun

  return Scaffold(
    appBar: AppBar(
      title: const Text('Tampil Data'),
    ),
    body: Center(
      child: Text(
        'Halo, nama saya $nama, saya memiliki nim $nim dan umur saya adalah $umur',
        style: Theme.of(context).textTheme.titleMedium,
        textAlign: TextAlign.center,
      ),
    ),
  );
}
```

Output contoh:
```
Halo, nama saya cihuy, saya memiliki nim H1D023109 dan umur saya adalah 20
```

### 5. Screenshot Aplikasi

#### FormData (Halaman Input)
![Form Data Screenshot](/Screenshot%202025-11-11%20224128.png)

Halaman pertama menampilkan:
- TextField untuk **Nama** (contoh: cihuy)
- TextField untuk **NIM** (contoh: h1d023109)
- TextField untuk **Tahun Lahir** (contoh: 2005)
- Tombol **Simpan** untuk mengirim data

#### TampilData (Halaman Display)
![Tampil Data Screenshot](/Screenshot%202025-11-11%20224227.png)

Halaman kedua menampilkan:
- Kalimat hasil gabungan data: "Halo, nama saya cihuy, saya memiliki nim h1d023109 dan umur saya adalah 20"
- Tombol Back untuk kembali ke halaman form
- Data umur dihitung otomatis dari tahun lahir (2025 - 2005 = 20)

## Getting Started

This project is a starting point for a Flutter application.

A few resources to get you started if this is your first Flutter project:

- [Lab: Write your first Flutter app](https://docs.flutter.dev/get-started/codelab)
- [Cookbook: Useful Flutter samples](https://docs.flutter.dev/cookbook)

For help getting started with Flutter development, view the
[online documentation](https://docs.flutter.dev/), which offers tutorials,
samples, guidance on mobile development, and a full API reference.
