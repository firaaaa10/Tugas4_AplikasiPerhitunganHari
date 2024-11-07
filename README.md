# AplikasiPerhitunganHari
 Tugas 4 - Siti Safira 2210010336

# 1. Deskripsi Program
Aplikasi ini menghitung jumlah hari dalam bulan tertentu pada tahun tertentu yang dipilih oleh pengguna.

- Input: Pengguna memilih bulan dari JComboBox dan memasukkan tahun menggunakan JSpinner.
- Penggunaan JCalendar: Untuk mempermudah pengguna memilih bulan dan tahun.
- Output: Setelah tombol ditekan, aplikasi menampilkan jumlah hari dalam bulan yang dipilih.
  
# 2. Komponen GUI: 
JFrame, JPanel, JLabel, JComboBox, JSpinner, JButton, JCalendar
- JPanel: Untuk menampung komponen lain.
- JLabel: Berfungsi sebagai label untuk elemen input dan output.
- JComboBox: Untuk memilih bulan.
- JSpinner: Untuk memasukkan tahun.
- JCalendar: Untuk mempermudah pengguna memilih bulan dan tahun secara visual.
- JButton: Tombol untuk menghitung jumlah hari, menghitung selisih hari, hapus dan keluar

- Button Hitung
```
private void btnHitungActionPerformed(java.awt.event.ActionEvent evt) {                                          
    btnHitung.addActionListener((ActionEvent e) -> {
        kalkulatorhari();
    });
    }  
```
- Button Hitung Selisih Hari
```
private void calculateDifferenceButtonActionPerformed(java.awt.event.ActionEvent evt) {                                                          
    // Event listener untuk tombol "Hitung Selisih Hari"
        calculateDifferenceButton.addActionListener((ActionEvent e) -> {
            calculateDateDifference();
        });
    
    }      
```
- Button Hapus
```
private void btnHapusActionPerformed(java.awt.event.ActionEvent evt) {                                         
    // Event listener untuk tombol "Hapus"
        btnHapus.addActionListener((ActionEvent e) -> {
            hapusinput();
        });
    
    }      
```
Metode hapusinput() di panggil
```
// Metode untuk menghapus atau mereset pilihan
    private void hapusinput() {
        // Reset bulan ke Januari
        cmbBoxBulan.setSelectedIndex(0);

        // Reset tahun ke tahun default (misalnya 2023)
        SpinnerTahun.setValue(2023);

        // Reset JCalendar ke tanggal hari ini
        JKalender.setCalendar(Calendar.getInstance());

        // Kosongkan hasil pada JLabel
        lblHasil.setText("Jumlah hari: ");
    }
```
- Button Keluar
```
   private void jButton1ActionPerformed(java.awt.event.ActionEvent evt) {                                         
    System.exit(0);       
    } 
```
# 3. Logika Program: 
Penggunaan API tanggal (LocalDate), Perhitungan hari dalam bulan, Perhitungan tahun kabisat

# 4. Events:
• ActionListener untuk tombol Hitung
```
 private void btnHitungActionPerformed(java.awt.event.ActionEvent evt) {                                          
    btnHitung.addActionListener((ActionEvent e) -> {
        kalkulatorhari();
    });
    }
```
Penjelasan Kode :
ActionListener pada buttonHitung Saat tombol ditekan, metode kalkulatorhari() akan dipanggil.
```
 private void kalkulatorhari() {
        //Mengambil nilai bulan dari JComboBox
        int month = cmbBoxBulan.getSelectedIndex() + 1; // ComboBox menggunakan indeks dari 0, jadi ditambah 1
        // Mengambil nilai tahun dari JSpinner
        int year = (int) SpinnerTahun.getValue();

        // Juga mengatur tanggal JCalendar sesuai dengan bulan dan tahun yang dipilih
        Calendar selectedDate = JKalender.getCalendar();
        selectedDate.set(Calendar.MONTH, month - 1); // Calendar.MONTH menggunakan indeks dari 0
        selectedDate.set(Calendar.YEAR, year);
        JKalender.setCalendar(selectedDate); // Menampilkan bulan dan tahun yang dipilih di JCalendar

        // Membuat objek YearMonth berdasarkan bulan dan tahun yang dipilih
        YearMonth yearMonth = YearMonth.of(year, month);

        // Menghitung jumlah hari dalam bulan tersebut
        int daysInMonth = yearMonth.lengthOfMonth();

        // Mendapatkan hari pertama dan hari terakhir dalam bulan tersebut
        LocalDate firstDay = yearMonth.atDay(1);
        LocalDate lastDay = yearMonth.atEndOfMonth();

        // Menampilkan hasil jumlah hari, hari pertama, dan hari terakhir pada JLabel
        lblHasil.setText(String.format(
            "Jumlah hari: %d, Hari pertama: %s, Hari terakhir: %s", 
            daysInMonth, firstDay.getDayOfWeek(), lastDay.getDayOfWeek()
        ));
     
    }

```
Metode hitungHari():
- comboBoxBulan.getSelectedIndex() mendapatkan indeks bulan yang dipilih (dengan Januari sebagai indeks 0), lalu menambahkan 1 agar sesuai dengan bulan kalender (Januari = 1).
- spinnerTahun.getValue() mengambil nilai tahun yang dipilih.
- Menghitung jumlah hari: YearMonth.of(tahun, bulan) membuat objek YearMonth untuk bulan dan tahun yang dipilih. Metode lengthOfMonth() kemudian digunakan untuk mendapatkan jumlah hari pada bulan tersebut.
- Hasil jumlah hari ditampilkan di labelHasil.
  
• ChangeListener pada JSpinner untuk input tahun
```
private void SpinnerTahunStateChanged(javax.swing.event.ChangeEvent evt) {                                          
    SpinnerTahun.addChangeListener((ChangeEvent e) -> {
        pembaruankalender();
    });
    }   
```
Listener untuk mengubah bulan dan tahun pada JCalendar saat ComboBox atau Spinner berubah
```
private void cmbBoxBulanItemStateChanged(java.awt.event.ItemEvent evt) {                                             
        cmbBoxBulan.addItemListener((ItemEvent e) -> {
            pembaruankalender();
        });
    }    
```
Metode pembaruankalender() akan di panggil
```
// Metode untuk memperbarui JCalendar sesuai pilihan bulan dan tahun
    private void pembaruankalender() {
        int month = cmbBoxBulan.getSelectedIndex(); // Indeks bulan ComboBox mulai dari 0
        int year = (int) SpinnerTahun.getValue();

        // Mengatur JCalendar untuk bulan dan tahun yang dipilih
        Calendar selectedDate = Calendar.getInstance();
        selectedDate.set(Calendar.YEAR, year);
        selectedDate.set(Calendar.MONTH, month); // Calendar.MONTH juga mulai dari 0
        selectedDate.set(Calendar.DAY_OF_MONTH, 1);
        JKalender.setCalendar(selectedDate); // Memperbarui tampilan JCalendar
    }
```
# 5. Variasi:
• Tampilkan informasi tambahan seperti hari pertama dan terakhir dalam bulan tersebut
```
// Mendapatkan hari pertama dan hari terakhir dalam bulan tersebut
        LocalDate firstDay = yearMonth.atDay(1);
        LocalDate lastDay = yearMonth.atEndOfMonth();
```
• Integrasikan fitur untuk menghitung selisih hari antara dua tanggal
```
 private void calculateDifferenceButtonActionPerformed(java.awt.event.ActionEvent evt) {                                                          
    // Event listener untuk tombol "Hitung Selisih Hari"
        calculateDifferenceButton.addActionListener((ActionEvent e) -> {
            calculateDateDifference();
        });
    
    }
```
Metode calculateDateDifference() akan di panggil
```
// Metode untuk menghitung selisih hari antara dua tanggal
    private void calculateDateDifference() {
        // Mendapatkan tanggal awal dan akhir dari JCalendar
        Calendar startCal = startCalendar.getCalendar();
        Calendar endCal = endCalendar.getCalendar();

        // Konversi Calendar ke LocalDate
        LocalDate startDate = startCal.toInstant().atZone(ZoneId.systemDefault()).toLocalDate();
        LocalDate endDate = endCal.toInstant().atZone(ZoneId.systemDefault()).toLocalDate();

        // Menghitung selisih hari menggunakan ChronoUnit.DAYS
        long daysBetween = ChronoUnit.DAYS.between(startDate, endDate);

        // Menampilkan hasil selisih hari pada JLabel
        differenceLabel.setText("Selisih hari antara dua tanggal: " + daysBetween + " hari");
    }
    
```
# Hasil Gambar Project Ketika di Run
![](https://github.com/firaaaa10/Tugas4_AplikasiPerhitunganHari/blob/main/Cuplikan%20layar%202024-11-07%20153306.png).
## Indikator Penilaian:

| No  | Komponen         |  Persentase  |
| :-: | --------------   |   :-----:    |
|  1  | Komponen GUI     |    10    |
|  2  | Logika Program   |    20    |
|  3  | Kesesuaian UI    |    15    |
|  4  | Constructor      |    15    |
|  5  | Memenuhi Variasi |    40    |
|     | TOTAL        | 100 |

## Pembuat

Nama  : Siti Safira
NPM   : 2210010336
