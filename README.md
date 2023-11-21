## **Langkah-langkah Praktikum**

1. Install XAMPP
   Unduh XAMPP dari https://www.apachefriends.org/download.html dan pilih versi
   portable untuk memudahkan proses installasi. Kemudian extract file tersebut, seusikan
   direktorinya (misal: d:\xampp).

2. Memulai PHP
   Buat folder lab7_php_dasar pada root directory web server (d:\xampp\htdocs)

3. PHP Dasar
   Buat file baru dengan nama php_dasar.php pada directory tersebut. Kemudian buat
   kode seperti berikut.

    ```php
        <!DOCTYPE html>
        <html lang="en">
            <head>
                <meta charset="UTF-8">
                <title>PHP Dasar</title>
            </head>
            <body>
                <h1>Belajar PHP Dasar</h1>
                <?php
                echo "Hello World";
                ?>
            </body>
        </html>

    ```

    ![img](img/gambar1.png)

4. Variable PHP

    ```php
        <?php
        $nim = "0411500400";
        $nama = 'Abdullah';
        echo "NIM : " . $nim . "<br>";
        echo "Nama : $nama";
        ?>
    ```

    ![img](img/gambar2.png)

5. Predefine Variable $_GET

    ```php
        <?php
        echo 'Selamat Datang ' . $_GET['nama'];
        ?>

    ```

    ![img](img/gambar3.png)

6. Membuat Form

    ```php
        <!DOCTYPE html>
        <html lang="en">
            <head>
                <meta charset="UTF-8">
                <title>PHP Dasar</title>
            </head>
            <body>
                <h2>Form Input</h2>
                <form method="post">
                    <label>Nama: </label>
                    <input type="text" name="nama">
                    <input type="submit" value="Kirim">
                </form>
                <?php
                echo 'Selamat Datang ' . $_POST['nama'];
                ?>
            </body>
        </html>

    ```

    ![img](img/gambar4.png)

7. Operator

    ```php
        <?php
        $gaji = 1000000;
        $pajak = 0.1;
        $thp = $gaji - ($gaji*$pajak);
        echo "Gaji sebelum pajak = Rp. $gaji <br>";
        echo "Gaji yang dibawa pulang = Rp. $thp";
        ?>

    ```

    ![img](img/operator.png)

8. Kondisi IF

    ```php
        <?php
        $nama_hari = date("l");
        if ($nama_hari == "Sunday") {
            echo "Minggu";
        } elseif ($nama_hari == "Monday") {
            echo "Senin";
        } else {
            echo "Selasa";
        }
        ?>
    ```

    ![img](img/if.png)

9. Kondisi Switch

    ```php
        <?php
        $nama_hari = date("l");
        switch ($nama_hari) {
        case "Sunday":
            echo "Minggu";
            break;
        case "Monday":
            echo "Senin";
            break;
        case "Tuesday":
            echo "Selasa";
            break;
        default:
            echo "Sabtu";
        ?>
    ```

    ![img](img/swicth.png)

10. Perulangan for

    ```php
        <?php
        echo "Perulangan 1 sampai 10 <br />";
        for ($i=1; $i<=10; $i++) {
            echo "Perulangan ke: " . $i . '<br />';
        }
        echo "Perulangan Menurun dari 10 ke 1 <br />";
        for ($i=10; $i>=1; $i--) {
            echo "Perulangan ke: " . $i . '<br />';
        }
        ?>
    ```

    ![img](img/gambar5.png)

11. Perulangan while

    ```php
        <?php
        echo "Perulangan 1 sampai 10 <br />";
        $i=1;
        while ($i<=10) {
            echo "Perulangan ke: " . $i . '<br />';
            $i++;
        }
        ?>
    ```

    ![img](img/gambar6.png)

12. Perulangan dowhile

    ```php
        <?php
        echo "Perulangan 1 sampai 10 <br />";
        $i=1;
        do {
            echo "Perulangan ke: " . $i . '<br />';
            $i++;
        } while ($i<=10);
        ?>
    ```

    ![img](img/gambar7.png)

## Pertanyaan dan Tugas
Buatlah program PHP sederhana dengan menggunakan form input yang menampilkan 
nama, tanggal lahir dan pekerjaan. Kemudian tampilkan outputnya dengan menghitung 
umur berdasarkan inputan tanggal lahir. Dan pilihan pekerjaan dengan gaji yang 
berbeda-beda sesuai pilihan pekerjaan.
```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Form Input PHP</title>
    <link rel="stylesheet" href="styles.css">
</head>
<body>
```
```php
<?php
// Fungsi untuk menghitung umur berdasarkan tanggal lahir
function hitungUmur($tanggal_lahir) {
    $today = new DateTime();
    $tanggal_lahir = new DateTime($tanggal_lahir);
    $umur = $today->diff($tanggal_lahir);
    return $umur->y;
}

// Daftar pekerjaan beserta gaji
$pekerjaan_gaji = array(
    'Programmer' => 5000000,
    'Designer' => 4500000,
    'Analyst' => 4800000
);

// Memproses form jika sudah disubmit
if ($_SERVER["REQUEST_METHOD"] == "POST") {
    // Mengambil data dari form
    $nama = $_POST["nama"];
    $tanggal_lahir = $_POST["tanggal_lahir"];
    $pekerjaan = $_POST["pekerjaan"];

    // Validasi data
    if (empty($nama) || empty($tanggal_lahir) || empty($pekerjaan)) {
        echo "Harap lengkapi semua field!";
    } else {
        // Menghitung umur
        $umur = hitungUmur($tanggal_lahir);

        // Menampilkan output
        echo "<h2>Hasil Input</h2>";
        echo "<p><span>Nama         :</span> $nama</p>";
        echo "<p><span>Tanggal Lahir:</span> $tanggal_lahir</p>";
        echo "<p><span>Pekerjaan    :</span> $pekerjaan</p>";
        echo "<p><span>Umur         :</span> $umur tahun</p>";
        echo "<p><span>Gaji         :</span> " . number_format($pekerjaan_gaji[$pekerjaan]) . "</p>";
    }
}
?>
```
```html
<h2 class="form">Form Input</h2>
<div class="container">
    <form method="post" action="<?php echo htmlspecialchars($_SERVER["PHP_SELF"]);?>">
        <div class="input-group">
            <label for="nama">Nama </label>
            <input type="text" name="nama">
        </div>
        <div class="input-group">
            <label for="tanggal_lahir">Tanggal Lahir </label>
            <input type="date" name="tanggal_lahir">
        </div>
        <div class="input-group">
            <label for="pekerjaan">Pekerjaan </label>
            <select name="pekerjaan">
                <option value="Programmer">Programmer</option>
                <option value="Designer">Designer</option>
                <option value="Analyst">Analyst</option>
            </select>
        </div>
        
        <input type="submit" name="submit" value="Submit" class="btn">
    </form>
</div>

</body>
</html>

```
