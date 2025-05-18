# Praktikum API Testing dengan Postman

## Ringkasan

Praktikum ini memperkenalkan konsep API Testing menggunakan Postman. Anda akan belajar cara menguji dan memvalidasi API menggunakan Postman, memahami konsep RESTful API, dan mempraktikkan berbagai metode HTTP request.

## Jadwal Praktikum

| Pertemuan | Tanggal | Materi |
|-----------|---------|--------|
| 10 | Minggu ke-10 | Pengenalan API Testing dan Instalasi Postman |
| 11 | Minggu ke-11 | Praktik API Testing dengan Postman dan RESTful Booker API |

## Persiapan Praktikum

### Alat yang Dibutuhkan
1. **Postman** - Unduh dan instal dari [situs resmi Postman](https://www.postman.com/downloads/)
2. **Akun Postman** (opsional) - Untuk menyimpan koleksi di cloud
3. **Web browser**
4. **Koneksi internet**

### Pengetahuan Prasyarat
1. Pemahaman dasar tentang HTTP dan REST API
2. Pemahaman dasar format data JSON

## Materi Praktikum

### 1. Pengenalan API Testing

#### Apa itu API?
API (Application Programming Interface) adalah sekumpulan aturan dan protokol yang memungkinkan aplikasi atau komponen perangkat lunak berkomunikasi satu sama lain. API adalah cara aplikasi berinteraksi dengan sistem lain untuk mengakses data atau layanan.

#### Kenapa API Testing Penting?
- Menguji alur data dan respons dari API
- Memastikan komunikasi antar sistem berjalan dengan benar
- Memvalidasi keamanan API
- Memastikan API memenuhi persyaratan bisnis dan teknis
- Mendeteksi error sebelum sampai ke UI

#### Jenis-jenis API Testing
1. **Functional Testing** - Menguji fungsi API bekerja sesuai spesifikasi
2. **Performance Testing** - Menguji kecepatan respons dan throughput API
3. **Security Testing** - Menguji keamanan dan otorisasi API
4. **Reliability Testing** - Menguji konsistensi API di berbagai kondisi
5. **Load Testing** - Menguji kemampuan API menangani beban tinggi

### 2. Pengenalan Postman

#### Apa itu Postman?
Postman adalah aplikasi yang memungkinkan pengguna untuk menguji, membangun, mendokumentasikan, dan memonitoring API dengan antarmuka yang mudah digunakan.

#### Fitur Utama Postman
1. **HTTP Request Builder** - Membuat dan mengirim HTTP request
2. **Collections** - Mengorganisir request dalam grup
3. **Environments** - Mengelola variabel dan konfigurasi berbeda
4. **Testing Scripts** - Menulis skrip pengujian untuk memvalidasi respons
5. **Automation** - Mengotomasi pengujian dengan Collection Runner
6. **Documentation** - Membuat dokumentasi API
7. **Monitoring** - Memantau performa API

### 3. REST API Basics

#### Protokol HTTP
HTTP (Hypertext Transfer Protocol) adalah protokol yang digunakan untuk mengirim permintaan dan menerima respons di internet.

#### Metode HTTP
- **GET** - Mengambil data dari server
- **POST** - Mengirim data baru ke server
- **PUT** - Memperbarui data yang sudah ada di server
- **PATCH** - Memperbarui sebagian data di server
- **DELETE** - Menghapus data dari server

#### Format Response
- **JSON** (JavaScript Object Notation)
- **XML** (eXtensible Markup Language)
- **HTML** (Hypertext Markup Language)
- **Plain Text**

#### HTTP Status Codes
- **1xx** - Informational
- **2xx** - Success (200 OK, 201 Created, dll)
- **3xx** - Redirection
- **4xx** - Client Error (404 Not Found, 403 Forbidden, dll)
- **5xx** - Server Error (500 Internal Server Error, dll)

### 4. Praktikum dengan RESTful Booker API

RESTful Booker adalah aplikasi API publik yang menyediakan endpoint untuk booking hotel, yang ideal untuk belajar API testing.

#### Endpoint RESTful Booker API
Base URL: [https://restful-booker.herokuapp.com](https://restful-booker.herokuapp.com/apidoc/index.html)

| Endpoint | Metode | Deskripsi |
|----------|--------|-----------|
| `/auth` | POST | Membuat token autentikasi |
| `/booking` | GET | Mendapatkan semua ID booking |
| `/booking` | POST | Membuat booking baru |
| `/booking/{id}` | GET | Mendapatkan detail booking |
| `/booking/{id}` | PUT | Memperbarui booking (memerlukan auth) |
| `/booking/{id}` | PATCH | Memperbarui sebagian booking (memerlukan auth) |
| `/booking/{id}` | DELETE | Menghapus booking (memerlukan auth) |

### 5. Tutorial API Testing dengan Postman

#### Langkah 1: Instalasi Postman
- Unduh Postman dari [situs resmi](https://www.postman.com/downloads/)
- Instal aplikasi di komputer Anda
- Buat akun atau gunakan tanpa login

#### Langkah 2: Membuat Collection
1. Klik tombol "New" di Postman
2. Pilih "Collection"
3. Beri nama "RESTful Booker API Testing"
4. Klik "Create"

#### Langkah 3: Autentikasi
1. Tambahkan request baru ke collection
2. Nama: "Create Token"
3. Metode: POST
4. URL: `https://restful-booker.herokuapp.com/auth`
5. Headers: `Content-Type: application/json`
6. Body (raw JSON):
```json
{
    "username": "admin",
    "password": "password123"
}
```
7. Kirim request dan verifikasi respons 200 OK dengan token

#### Langkah 4: Membuat Booking Baru
1. Tambahkan request baru ke collection
2. Nama: "Create Booking"
3. Metode: POST
4. URL: `https://restful-booker.herokuapp.com/booking`
5. Headers: `Content-Type: application/json`
6. Body (raw JSON):
```json
{
    "firstname": "Jim",
    "lastname": "Brown",
    "totalprice": 111,
    "depositpaid": true,
    "bookingdates": {
        "checkin": "2023-05-01",
        "checkout": "2023-05-10"
    },
    "additionalneeds": "Breakfast"
}
```
7. Kirim request dan verifikasi respons 200 OK dengan ID booking

#### Langkah 5: Mendapatkan Detail Booking
1. Tambahkan request baru ke collection
2. Nama: "Get Booking"
3. Metode: GET
4. URL: `https://restful-booker.herokuapp.com/booking/{id}` (ganti {id} dengan ID dari langkah 4)
5. Kirim request dan verifikasi detailnya sesuai dengan yang dibuat

#### Langkah 6: Memperbarui Booking
1. Tambahkan request baru ke collection
2. Nama: "Update Booking"
3. Metode: PUT
4. URL: `https://restful-booker.herokuapp.com/booking/{id}`
5. Headers:
   - `Content-Type: application/json`
   - `Cookie: token={token}` (ganti {token} dengan token dari langkah 3)
6. Body (raw JSON):
```json
{
    "firstname": "James",
    "lastname": "Brown",
    "totalprice": 150,
    "depositpaid": true,
    "bookingdates": {
        "checkin": "2023-05-01",
        "checkout": "2023-05-15"
    },
    "additionalneeds": "Breakfast and Dinner"
}
```
7. Kirim request dan verifikasi perubahan

#### Langkah 7: Menghapus Booking
1. Tambahkan request baru ke collection
2. Nama: "Delete Booking"
3. Metode: DELETE
4. URL: `https://restful-booker.herokuapp.com/booking/{id}`
5. Headers:
   - `Cookie: token={token}` (ganti {token} dengan token dari langkah 3)
6. Kirim request dan verifikasi respons 201 Created

### 6. Test Script di Postman

Postman memungkinkan penulisan skrip pengujian untuk memverifikasi respons API secara otomatis.

#### Contoh Skrip Test untuk Membuat Token

```javascript
// Verify status code
pm.test("Status code is 200", function() {
    pm.response.to.have.status(200);
});

// Verify response has token
pm.test("Response has token", function() {
    var jsonData = pm.response.json();
    pm.expect(jsonData.token).to.exist;
});

// Save token to environment variable
if (pm.response.json().token) {
    pm.environment.set("auth_token", pm.response.json().token);
}
```

#### Contoh Skrip Test untuk Membuat Booking

```javascript
// Verify status code
pm.test("Status code is 200", function() {
    pm.response.to.have.status(200);
});

// Verify response structure
pm.test("Response has booking details", function() {
    var jsonData = pm.response.json();
    pm.expect(jsonData.booking).to.exist;
    pm.expect(jsonData.bookingid).to.exist;
});

// Save booking ID for later use
if (pm.response.json().bookingid) {
    pm.environment.set("booking_id", pm.response.json().bookingid);
}
```

### 7. Environment Variables

Environment variables memungkinkan Anda menyimpan dan menggunakan nilai di seluruh koleksi.

#### Cara Membuat Environment
1. Klik tombol "Environments" di sidebar
2. Klik "+" untuk membuat environment baru
3. Beri nama "RESTful Booker"
4. Tambahkan variabel yang diperlukan:
   - `base_url`: `https://restful-booker.herokuapp.com`
   - `auth_token`: (akan diisi oleh test script)
   - `booking_id`: (akan diisi oleh test script)

#### Cara Menggunakan Environment Variables
- URL: `{{base_url}}/booking/{{booking_id}}`
- Headers: `Cookie: token={{auth_token}}`

### 8. Collection Runner

Collection Runner memungkinkan Anda menjalankan serangkaian request secara otomatis.

#### Langkah Menjalankan Collection
1. Klik kanan pada collection dan pilih "Run collection"
2. Pilih environment "RESTful Booker"
3. Atur urutan request: Auth > Create Booking > Get Booking > Update Booking > Delete Booking
4. Klik "Run"
5. Periksa hasil pengujian

## Tugas Praktikum

1. Buat collection Postman untuk RESTful Booker API
2. Implementasikan request untuk semua endpoint dasar (auth, booking, dll)
3. Tambahkan test script untuk setiap request untuk memverifikasi respons
4. Gunakan environment variables untuk menyimpan token dan ID booking
5. Dokumentasikan collection dengan deskripsi dan comments
6. Jalankan collection menggunakan Collection Runner
7. Buatlah laporan hasil pengujian (screenshot hasil pengujian)

## Kontak dan Bantuan

- Tutorial Postman: [https://toolsqa.com/postman/postman-tutorial/](https://toolsqa.com/postman/postman-tutorial/)
- Playlist Tutorial: [YouTube Playlist](https://www.youtube.com/playlist?list=PLbwZ_0ncMaxgiLi_hiRJS2z9MApGkeYnZ)
- Dokumentasi RESTful Booker: [https://restful-booker.herokuapp.com/apidoc/index.html](https://restful-booker.herokuapp.com/apidoc/index.html)

## Kriteria Penilaian

| Aspek | Bobot |
|-------|-------|
| Kelengkapan implementasi endpoint | 30% |
| Penggunaan test scripts | 25% |
| Penggunaan environment variables | 15% |
| Dokumentasi collection | 15% |
| Laporan hasil pengujian | 15% |

## Referensi Tambahan

1. [REST API Tutorial](https://www.restapitutorial.com/)
2. [Postman Learning Center](https://learning.postman.com/)
3. [JSON Schema Validation](https://json-schema.org/)
4. [HTTP Status Codes](https://httpstatuses.com/)