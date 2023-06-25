# studykasus pertemuan 13 - 14
```
Nama : Sahrul Ridwansyah 
Kelas: TI.22.A2
Nim  : 312210063
```

# create table

```
create table perusahaan (
    id_p varchar (10) primary key,
    nama varchar (50),
    alamat varchar (50));
```
```
create table dapartement (
    id_dept varchar (10) primary key,
    nama varchar (50),
    id_p varchar (10),
    manager_nik varchar (10));
```
```
create table karyawan (
   nik varchar (10) primary key,
   nama varchar (50),
   id_dept varchar (10),
   sup_nik varchar (10));
```
```
create table project (
    id_project varchar (10) primary key,
    nama varchar (50),
    tgl_mulai datetime,
    tgl_selesai datetime,
    status tinyint(1));
```
```
create table project_detail (
    id_project varchar (10),
    nik varchar (10));
```

# insert into
```
insert into perusahaan (id_p, nama, alamat)
    -> values
    -> ('p01', 'kantor pusat', 'null'),
    -> ('p02', 'cabang bekasi', 'null');
```
```
insert into dapartement (id_dept, nama, id_p, manager_nik)
    -> values
    -> ('d01', 'produksi', 'p02', 'n01'),
    -> ('d02', 'marketing', 'p01', 'n03'),
    -> ('d03', 'Rnd', 'p02', 'null'),
    -> ('d04', 'logistik', 'p02', 'null');
```
```
insert into karyawan (nik, nama, id_dept, sup_nik)
    -> values
    -> ('n01', 'ari', 'd01', 'null'),
    -> ('n02', 'dina', 'd01', 'null'),
    -> ('n03', 'rika', 'd03', 'null'),
    -> ('n04', 'ratih', 'd01', 'n01'),
    -> ('n05', 'riko', 'd01', 'n01'),
    -> ('n06', 'dani', 'd02', 'null'),
    -> ('n07', 'anis', 'd02', 'n06'),
    -> ('n08', 'dika', 'd02', 'n06');
```
```
insert into project (id_project, nama, tgl_mulai, tgl_selesai, status)
    -> values
    -> ('pj01', 'A', '2019-01-10', '2019-03-10', '1'),
    -> ('pj02', 'B', '2019-02-15', '2019-04-10', '1'),
    -> ('pj03', 'C', '2019-03-21', '2019-05-10', '1');
```
```
insert into project_detail (id_project, nik)
    -> values
    -> ('pj01', 'n01'),
    -> ('pj01', 'n02'),
    -> ('pj01', 'n03'),
    -> ('pj01', 'n04'),
    -> ('pj01', 'n05'),
    -> ('pj01', 'n07'),
    -> ('pj01', 'n08'),
    -> ('pj02', 'n01'),
    -> ('pj02', 'n03'),
    -> ('pj02', 'n05'),
    -> ('pj03', 'n03'),
    -> ('pj03', 'n07'),
    -> ('pj03', 'n08');
```

![image](https://github.com/sahrul180304/studykasus/assets/115526901/88029e44-46ef-4aec-83e0-7e7f412a0b4c)

![image](https://github.com/sahrul180304/studykasus/assets/115526901/0075c511-e658-4817-b80e-d00cbff7d205)

![image](https://github.com/sahrul180304/studykasus/assets/115526901/09376a68-2dad-4359-859f-7eb513ce7fa4)


# join table
```
SELECT d.nama AS dapartement, k.nama AS manager
    -> FROM dapartement d
    -> LEFT JOIN karyawan k ON d.manager_nik = k.nik;
```
```
SELECT k.nik, k.nama, d.nama dapartement, s.nama supervisor
    -> FROM karyawan k
    -> LEFT JOIN karyawan s ON s.nik = k.sup_nik
    -> LEFT JOIN dapartement d ON d.id_dept = k.id_dept;
```
```
SELECT k.nik, k.nama
    FROM karyawan k
    JOIN project_detail pj_d ON pj_d.nik = k.nik
    JOIN project pj ON pj.id_project = pj_d.id_project
    WHERE pj.nama = 'A';
```

![image](https://github.com/sahrul180304/studykasus/assets/115526901/2834824a-0119-4c6a-a341-c3e0eb3b859e)

![image](https://github.com/sahrul180304/studykasus/assets/115526901/be847dd1-5d87-45ca-8769-97be7ea2a872)

# latihan praktikum
```
SELECT p.nama AS project, d.nama AS departemen
FROM project p
INNER JOIN project_detail pd ON p.id_project = pd.id_project
INNER JOIN karyawan k ON pd.nik = k.nik
INNER JOIN dapartement d ON k.id_dept = d.id_dept
ORDER BY p.nama, d.nama;
```
```
SELECT p.nama AS project, d.nama AS dapartement, COUNT(k.nik) AS jumlah_karyawan
FROM project p
INNER JOIN project_detail pd ON p.id_project = pd.id_project
INNER JOIN karyawan k ON pd.nik = k.nik
INNER JOIN dapartement d ON k.id_dept = d.id_dept
GROUP BY p.nama, d.nama
ORDER BY p.nama, d.nama;
```
```
SELECT COUNT(p.id_project) AS jumlah_proyek
    FROM project p
    INNER JOIN project_detail pd ON p.id_project = pd.id_project
    INNER JOIN karyawan k ON pd.nik = k.nik
    INNER JOIN dapartement d ON k.id_dept = d.id_dept
    WHERE d.nama = 'RnD' AND p.status = 1;
```
```
SELECT COUNT(p.id_project) AS jumlah_proyek
    FROM project p
    INNER JOIN project_detail pd ON p.id_project = pd.id_project
    INNER JOIN karyawan k ON pd.nik = k.nik
    WHERE k.nama = 'Ari';
```
```
SELECT k.nama AS nama_karyawan
    FROM karyawan k
    INNER JOIN project_detail pd ON k.nik = pd.nik
    INNER JOIN project p ON pd.id_project = p.id_project
    WHERE p.nama = 'B';
```

![image](https://github.com/sahrul180304/studykasus/assets/115526901/54958752-3605-4966-b175-2500ad9c323f)

    
![image](https://github.com/sahrul180304/studykasus/assets/115526901/3a7e51cf-430e-4b1e-91da-8d3dad561814)


![image](https://github.com/sahrul180304/studykasus/assets/115526901/00b49518-15c6-4063-aa06-96e555850a9b)


![image](https://github.com/sahrul180304/studykasus/assets/115526901/9a33c516-0dc2-4a7e-9e12-b60929f544ec)


![image](https://github.com/sahrul180304/studykasus/assets/115526901/bd5c7c91-48e3-4cd2-be87-3986b9cb57e0)















