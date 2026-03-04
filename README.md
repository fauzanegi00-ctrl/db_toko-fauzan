# toko_fauzan
Apa Itu JOIN?

JOIN adalah perintah di SQL yang digunakan untuk menggabungkan data dari dua atau lebih tabel berdasarkan kolom yang saling berhubungan (biasanya primary key dan foreign key).

Tujuan JOIN:
Agar kita bisa menampilkan data yang tersebar di beberapa tabel menjadi satu hasil.

Contoh:

Tabel pelanggan

Tabel pesan

Kalau mau menampilkan nama siswa beserta nama kelasnya → harus pakai JOIN.
1. INNER JOIN

INNER JOIN menampilkan hanya data yang memiliki hubungan di kedua tabel.

Jika tidak ada pasangan data, maka tidak ditampilkan.

2. LEFT JOIN (LEFT OUTER JOIN)

LEFT JOIN menampilkan semua data dari tabel kiri, walaupun tidak ada pasangan di tabel kanan.

Jika tidak ada pasangan, maka akan muncul NULL.

3. RIGHT JOIN (RIGHT OUTER JOIN)

RIGHT JOIN kebalikan dari LEFT JOIN.
Menampilkan semua data dari tabel kanan, walaupun tidak ada pasangan di tabel kiri.

sql
Setting environment for using XAMPP for Windows.
LENOVO@LAPTOP-PDKLLKHP c:\xampp
# mysql -u root
Welcome to the MariaDB monitor.  Commands end with ; or \g.
Your MariaDB connection id is 17
Server version: 10.4.32-MariaDB mariadb.org binary distribution

Copyright (c) 2000, 2018, Oracle, MariaDB Corporation Ab and others.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

MariaDB [(none)]> create database toko;
Query OK, 1 row affected (0.002 sec)

MariaDB [(none)]> use toko;
Database changed
MariaDB [toko]> create table pelanggan(
    ->  id_pelanggan int primary key,
    -> nama varchar(50));
Query OK, 0 rows affected (0.024 sec)

MariaDB [toko]> insert into pelanggan
    -> (id_pelanggan, nama) values
    -> (1,'Andi'),
    -> (2,'Budi'),
    -> (3,'Sari');
Query OK, 3 rows affected (0.010 sec)
Records: 3  Duplicates: 0  Warnings: 0

MariaDB [toko]> select * from pelanggan;
+--------------+------+
| id_pelanggan | nama |
+--------------+------+
|            1 | Andi |
|            2 | Budi |
|            3 | Sari |
+--------------+------+
3 rows in set (0.001 sec)

MariaDB [toko]> create table pesanan(
    -> id_pesanan int primary key,
    -> id_pelanggan int,
    -> produk varchar(50));
Query OK, 0 rows affected (0.023 sec)

MariaDB [toko]> insert into pesanan
    -> (id_pesanan, id_pelanggan, produk) values
    -> (101,1,'Laptop'),
    -> (102,2,'Smartphone'),
    -> (103,1,'Headset');
Query OK, 3 rows affected (0.005 sec)
Records: 3  Duplicates: 0  Warnings: 0

MariaDB [toko]>  select * from pesanan;
+------------+--------------+------------+
| id_pesanan | id_pelanggan | produk     |
+------------+--------------+------------+
|        101 |            1 | Laptop     |
|        102 |            2 | Smartphone |
|        103 |            1 | Headset    |
+------------+--------------+------------+
3 rows in set (0.000 sec)

MariaDB [toko]>  select pelanggan.nama, pesanan.produk
    -> from pelanggan
    -> left join pesanan on pelanggan.id_pelanggan = pesanan.id_pelanggan;
+------+------------+
| nama | produk     |
+------+------------+
| Andi | Laptop     |
| Budi | Smartphone |
| Andi | Headset    |
| Sari | NULL       |
+------+------------+
4 rows in set (0.006 sec)

MariaDB [toko]>  select pelanggan.nama, pesanan.produk
    ->  from pelanggan
    ->  right join pesanan on pelanggan.id_pelanggan = pesanan.id_pelanggan;
+------+------------+
| nama | produk     |
+------+------------+
| Andi | Laptop     |
| Budi | Smartphone |
| Andi | Headset    |
+------+------------+
3 rows in set (0.005 sec)

MariaDB [toko]>
