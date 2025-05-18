# Penggunaan Postman untuk Pengujian API

## Daftar Isi
1. [Pendahuluan](#pendahuluan)
2. [Instalasi Postman](#instalasi-postman)
3. [Setup Environment](#setup-environment)
4. [Membuat Collection](#membuat-collection)
5. [Pengujian GET Endpoint](#pengujian-get-endpoint)
6. [Pengujian PUT Endpoint](#pengujian-put-endpoint)
7. [Menggunakan Test Scripts](#menggunakan-test-scripts)
8. [Menjalankan Collection Runner](#menjalankan-collection-runner)
9. [Menghasilkan Laporan HTML dengan Newman](#menghasilkan-laporan-html-dengan-newman)
10. [Kesimpulan](#kesimpulan)

## Pendahuluan

Dokumen ini menjelaskan langkah-langkah penggunaan Postman untuk pengujian API RESTful Booker. Pengujian ini dilakukan sebagai bagian dari praktikum Pengujian Perangkat Lunak untuk memahami konsep API testing dan implementasinya menggunakan Postman.

## Instalasi Postman

### Langkah Instalasi
1. Download Postman dari situs resmi [https://www.postman.com/downloads/](https://www.postman.com/downloads/)
2. Install aplikasi sesuai dengan sistem operasi yang digunakan
3. Buka aplikasi Postman

**Screenshot Postman setelah instalasi:**

[SCREENSHOT 1: Tampilan awal Postman]

## Setup Environment

Environment Postman memungkinkan kita untuk menyimpan variabel yang dapat digunakan di berbagai request, memudahkan pengujian dengan parameter yang berbeda-beda.

### Langkah Pembuatan Environment
1. Klik tombol "Environments" di sidebar kiri
2. Klik tombol "+" untuk membuat environment baru
3. Beri nama "RESTful Booker Environment"
4. Tambahkan variable-variable berikut:
   - `baseUrl` : https://restful-booker.herokuapp.com
   - `authToken` : (akan diisi nanti melalui script)
   - `validBookingId` : (akan diisi nanti melalui script)
   - `updateBookingId` : (akan diisi nanti melalui script)
5. Klik "Save"

**Screenshot Setup Environment:**

[SCREENSHOT 2: Pembuatan environment di Postman]

## Membuat Collection

Collection memungkinkan kita mengelompokkan request terkait menjadi satu grup.

### Langkah Pembuatan Collection
1. Klik tombol "Collections" di sidebar kiri
2. Klik tombol "+" untuk membuat collection baru
3. Beri nama "RESTful Booker API Testing"
4. Tambahkan deskripsi singkat tentang collection
5. Klik "Create"

**Screenshot Pembuatan Collection:**

[SCREENSHOT 3: Pembuatan collection di Postman]

## Pengujian GET Endpoint

Pengujian GET endpoint dilakukan untuk memverifikasi bahwa API dapat mengembalikan data booking dengan benar.

### Langkah Pengujian GET Endpoint
1. Pada collection yang telah dibuat, klik "Add Request"
2. Beri nama "Get Booking"
3. Pilih metode GET
4. Masukkan URL `{{baseUrl}}/booking/1` (menggunakan variabel environment)
5. Tambahkan header Accept: application/json
6. Klik "Send" untuk mengirim request

**Screenshot GET Request:**

[SCREENSHOT 4: Setup dan hasil GET request]

### Pengujian GET dengan Parameter Invalid
1. Buat request GET baru dengan nama "Get Booking - Invalid ID"
2. Masukkan URL dengan ID yang tidak valid: `{{baseUrl}}/booking/999999`
3. Klik "Send" dan verifikasi bahwa response menunjukkan error atau Not Found

**Screenshot GET Request dengan ID Invalid:**

[SCREENSHOT 5: Hasil GET request dengan ID yang tidak valid]

## Pengujian PUT Endpoint

Pengujian PUT endpoint dilakukan untuk memverifikasi bahwa API dapat memperbarui data booking dengan benar.

### Langkah Autentikasi
1. Buat request baru dengan nama "Create Token"
2. Pilih metode POST
3. Masukkan URL `{{baseUrl}}/auth`
4. Tambahkan header Content-Type: application/json
5. Pada tab Body, pilih raw dan format JSON
6. Masukkan body berikut:
```json
{
    "username": "admin",
    "password": "password123"
}
```
7. Klik "Send" untuk mendapatkan token autentikasi

**Screenshot Autentikasi:**

[SCREENSHOT 6: Proses autentikasi dan mendapatkan token]

### Langkah Pengujian PUT Endpoint
1. Buat request baru dengan nama "Update Booking"
2. Pilih metode PUT
3. Masukkan URL `{{baseUrl}}/booking/1`
4. Tambahkan headers:
   - Content-Type: application/json 
   - Accept: application/json
   - Cookie: token={{token}}
5. Pada tab Body, masukkan:
```json
{
    "firstname": "James",
    "lastname": "Brown",
    "totalprice": 150,
    "depositpaid": true,
    "bookingdates": {
        "checkin": "2023-06-01",
        "checkout": "2023-06-10"
    },
    "additionalneeds": "Breakfast and Dinner"
}
```
6. Klik "Send" untuk mengirim request

**Screenshot PUT Request:**

[SCREENSHOT 7: Setup dan hasil PUT request]

### Pengujian PUT dengan Data Invalid
1. Buat request PUT baru dengan nama "Update Booking - Invalid Data"
2. Gunakan URL yang sama tetapi dengan body yang tidak sesuai format
3. Klik "Send" dan verifikasi response error

**Screenshot PUT Request dengan Data Invalid:**

[SCREENSHOT 8: Hasil PUT request dengan data yang tidak valid]

## Menggunakan Test Scripts

Test scripts memungkinkan kita melakukan validasi otomatis terhadap response dari API.

### Contoh Test Script untuk GET Endpoint
1. Pada request "Get Booking", buka tab "Script" dan pilih Post Response
2. Tambahkan script berikut:

```javascript
// Verifikasi status code
pm.test("Status code is 200 OK", function() {
    pm.response.to.have.status(200);
});

// Verifikasi struktur response
pm.test("Response has correct structure", function() {
    const responseJson = pm.response.json();
    
    pm.expect(responseJson).to.have.property("firstname");
    pm.expect(responseJson).to.have.property("lastname");
    pm.expect(responseJson).to.have.property("totalprice");
    pm.expect(responseJson).to.have.property("bookingdates");
    pm.expect(responseJson.bookingdates).to.have.property("checkin");
    pm.expect(responseJson.bookingdates).to.have.property("checkout");
});

// Verifikasi tipe data
pm.test("Data types are correct", function() {
    const responseJson = pm.response.json();
    
    pm.expect(responseJson.firstname).to.be.a("string");
    pm.expect(responseJson.totalprice).to.be.a("number");
    pm.expect(responseJson.depositpaid).to.be.a("boolean");
});
```

**Screenshot Test Script untuk GET:**

[SCREENSHOT 9: Penulisan test script untuk GET request]

### Contoh Test Script untuk PUT Endpoint
1. Pada request "Update Booking", buka tab "Script" dan pilih Post Response
2. Tambahkan script berikut:

```javascript
// Verifikasi status code
pm.test("Status code is 200 OK", function() {
    pm.response.to.have.status(200);
});

// Verifikasi data telah berubah
pm.test("Data has been updated correctly", function() {
    const responseJson = pm.response.json();
    
    pm.expect(responseJson.firstname).to.eql("James");
    pm.expect(responseJson.lastname).to.eql("Brown");
    pm.expect(responseJson.totalprice).to.eql(150);
    pm.expect(responseJson.bookingdates.checkin).to.eql("2023-06-01");
});

// Menyimpan ID booking untuk digunakan dalam test selanjutnya
if (pm.response.code === 200) {
    pm.environment.set("last_updated_name", pm.response.json().firstname);
}
```

**Screenshot Test Script untuk PUT:**

[SCREENSHOT 10: Penulisan test script untuk PUT request]

## Menjalankan Collection Runner

Collection Runner memungkinkan kita menjalankan seluruh test case dalam satu collection secara bersamaan.

### Langkah Menjalankan Collection Runner
1. Klik kanan pada collection "RESTful Booker API Testing"
2. Pilih "Run collection"
3. Pilih environment "RESTful Booker Environment"
4. Atur urutan request yang sesuai (autentikasi terlebih dahulu)
5. Klik "Run" untuk menjalankan semua request dalam collection

**Screenshot Collection Runner:**

[SCREENSHOT 11: Setup Collection Runner]
[SCREENSHOT 12: Hasil dari Collection Runner]

## Menghasilkan Laporan HTML dengan Newman

Untuk menghasilkan laporan pengujian yang lebih terstruktur dan dapat diakses, saya menggunakan Newman, command-line runner untuk Postman. Newman memungkinkan menjalankan dan menghasilkan laporan HTML dari collection Postman melalui terminal.

### Langkah Instalasi Newman
1. Pastikan Node.js sudah terinstal di komputer
2. Install Newman menggunakan npm dengan perintah:
   ```
   npm install -g newman
   ```
3. Install reporter HTML dengan perintah:
   ```
   npm install -g newman-reporter-htmlextra
   ```

### Langkah Menghasilkan Laporan
1. Export collection dari Postman (klik kanan pada collection > Export)
2. Simpan collection dalam format JSON
3. Export environment juga dari Postman jika diperlukan
4. Jalankan perintah Newman dengan reporter HTML:
   ```
   newman run pengujian-restful-getbooking.json -e Restful_Booker_Environment.json -r htmlextra --reporter-htmlextra-export ./reports/published/get-booking-report.html
   ```
5. Laporan HTML akan dihasilkan di folder yang ditentukan

**Screenshot Laporan HTML GET Endpoint:**

[SCREENSHOT 13: Contoh laporan HTML untuk pengujian GET endpoint]

Untuk menghasilkan laporan pengujian PUT endpoint, perintah yang serupa digunakan:

```
newman run pengujian-restful-update-booking.json -e Restful_Booker_Environment.json -r htmlextra --reporter-htmlextra-export ./reports/published/update-booking-report.html
```

**Screenshot Laporan HTML PUT Endpoint:**

[SCREENSHOT 14: Contoh laporan HTML untuk pengujian PUT endpoint]

### Keunggulan Menggunakan Newman

1. **Integrasi CI/CD** - Newman dapat diintegrasikan dengan pipeline CI/CD untuk otomatisasi lengkap
2. **Format Laporan yang Kustomisasi** - Reporter htmlextra memberikan tampilan yang lebih informatif dibandingkan reporter bawaan Postman
3. **Kemampuan Command Line** - Memungkinkan pengujian API tanpa perlu membuka aplikasi Postman
4. **Batch Execution** - Dapat menjalankan multiple collection dalam satu perintah

## Kesimpulan

Pengujian API menggunakan Postman memungkinkan kita untuk memverifikasi berbagai aspek dari RESTful API seperti RESTful Booker. Melalui praktikum ini, saya telah berhasil mengimplementasikan pengujian untuk endpoint GET dan PUT dengan berbagai skenario, termasuk pengujian positif dan negatif.

Penggunaan fitur-fitur Postman seperti environment variables dan test scripts sangat memudahkan proses pengujian dan memastikan API bekerja sesuai dengan yang diharapkan. Penambahan Newman sebagai command-line runner memberikan fleksibilitas lebih dalam mengotomatiskan pengujian dan menghasilkan laporan yang komprehensif.

Kombinasi Postman untuk desain pengujian dan Newman untuk eksekusi dan pelaporan membentuk alur kerja yang efisien dan profesional dalam pengujian API. Laporan HTML yang dihasilkan Newman menyajikan hasil pengujian dalam format yang mudah dibaca dan dapat dibagikan kepada tim pengembangan atau stakeholder lainnya.