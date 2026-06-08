# Laporan Praktikum Jaringan Komputer - Modul 4

## Domain Name System (DNS)

### Identitas Praktikan

| Item      | Keterangan |
| --------- | ---------- |
| Nama      | Syaraful   |
| Modul     | 4          |
| Praktikum | DNS        |

---

## 4.1 Tujuan Praktikum

1. Memahami cara kerja DNS.
2. Menggunakan perintah `nslookup`.
3. Menganalisis paket DNS menggunakan Wireshark.
4. Mengidentifikasi record DNS tipe A, NS, dan MX.

---

## 4.2 Konfigurasi Jaringan

Perintah:

```cmd
ipconfig
```

Alamat IPv4 yang digunakan:

```text
10.218.11.50
```

DNS Server:

```text
10.217.7.77
```

### Screenshot

![IPConfig](assets/ipconfig.png)

---

## 4.3 Analisis DNS Menggunakan Wireshark

Filter yang digunakan:

```text
dns
```

### DNS Request

| Parameter        | Nilai                               |
| ---------------- | ----------------------------------- |
| Source IP        | 10.218.11.50                        |
| Destination IP   | 10.217.7.77                         |
| Protocol         | UDP                                 |
| Source Port      | 52188                               |
| Destination Port | 53                                  |
| Query Type       | A                                   |
| Domain           | [www.ietf.org](http://www.ietf.org) |

### Screenshot

![DNS Request](assets/dns_request.png)

---

### DNS Response

| Parameter  | Nilai                               |
| ---------- | ----------------------------------- |
| Domain     | [www.ietf.org](http://www.ietf.org) |
| Answer RRs | 2                                   |
| Address 1  | 104.16.44.99                        |
| Address 2  | 104.16.45.99                        |

### Screenshot

![DNS Response](assets/dns_response.png)

---

## 4.4 Jawaban Pertanyaan Wireshark

### 1. Apakah DNS menggunakan UDP atau TCP?

DNS pada praktikum menggunakan:

```text
UDP
```

---

### 2. Berapa port tujuan DNS?

```text
Port Tujuan : 53
Port Sumber : 52188
```

---

### 3. Ke alamat IP mana DNS Request dikirim?

```text
10.217.7.77
```

Alamat tersebut merupakan DNS Server yang digunakan selama praktikum.

---

### 4. Apa jenis query DNS yang digunakan?

```text
Type A
```

Jumlah Answer pada DNS Request:

```text
0
```

---

### 5. Berapa jumlah jawaban pada DNS Response?

```text
2
```

Detail jawaban:

| Domain                              | Type | Address      |
| ----------------------------------- | ---- | ------------ |
| [www.ietf.org](http://www.ietf.org) | A    | 104.16.44.99 |
| [www.ietf.org](http://www.ietf.org) | A    | 104.16.45.99 |

---

### 6. Apakah paket TCP SYN dikirim ke alamat hasil DNS?

Ya.

Browser mengirim paket TCP SYN ke alamat IP yang diperoleh dari DNS Response.

---

### 7. Apakah browser selalu mengirim DNS Request saat membuka halaman yang sama?

Tidak.

Browser dan sistem operasi menyimpan hasil DNS dalam cache sehingga tidak perlu selalu melakukan query DNS baru.

---

# 4.5 Query DNS Menggunakan nslookup

## A Record

Perintah:

```cmd
nslookup www.kyoto-u.ac.jp 10.217.7.77
```

Hasil:

* Alias : [www.kyoto-u.ac.jp](http://www.kyoto-u.ac.jp)
* Canonical Name : pipe.pr.kyoto-u.ac.jp

IPv4:

```text
151.101.66.132
151.101.130.132
151.101.194.132
151.101.2.132
```

### Screenshot

![A Record](assets/kyoto_a_record.png)

---

## NS Record

Perintah:

```cmd
nslookup -type=NS ox.ac.uk 10.217.7.77
```

Name Server yang ditemukan:

* dns0.ox.ac.uk
* dns1.ox.ac.uk
* dns2.ox.ac.uk
* auth4.dns.ox.ac.uk
* auth5.dns.ox.ac.uk
* auth6.dns.ox.ac.uk

### Screenshot

![NS Record](assets/ox_ns_record.png)

---

## MX Record

Perintah:

```cmd
nslookup -type=MX yahoo.com 10.217.7.77
```

Mail Server:

* mta5.am0.yahoodns.net
* mta6.am0.yahoodns.net
* mta7.am0.yahoodns.net

### Screenshot

![MX Record](assets/yahoo_mx_record.png)

---

# 4.6 Kesimpulan

1. DNS berfungsi menerjemahkan nama domain menjadi alamat IP.
2. DNS menggunakan UDP port 53 untuk query standar.
3. Record A digunakan untuk memperoleh alamat IP host.
4. Record NS digunakan untuk memperoleh informasi Name Server suatu domain.
5. Record MX digunakan untuk memperoleh informasi Mail Server suatu domain.
6. Wireshark dapat digunakan untuk menganalisis proses DNS Request dan DNS Response secara detail.
