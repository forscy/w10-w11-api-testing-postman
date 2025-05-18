# API Testing dengan Postman

Oleh: Roy ([GitHub](https://github.com/royjtk/restful-booker-testing-postman))

Halo! Repo ini berisi dokumentasi dan laporan pengujian API menggunakan Postman yang saya kerjakan dalam mata kuliah Pengujian Perangkat Lunak. Di sini saya membahas pengalaman saya menguji RESTful Booker API serta pemahaman saya tentang API testing.

## Apa itu API Testing?

API (Application Programming Interface) adalah jembatan yang menghubungkan berbagai aplikasi dan layanan. Bayangkan API sebagai "pelayan restoran" yang menerima pesanan Anda (request), menyampaikannya ke dapur (server), dan membawakan makanan (response) kembali ke meja Anda!

API testing sangat penting karena:
- Memastikan data mengalir dengan benar antar sistem
- Mendeteksi bug sebelum sampai ke UI (lebih mudah diperbaiki!)
- Memvalidasi keamanan dan performa API
- Memastikan API memenuhi kebutuhan bisnis

## Jenis-jenis API Testing

Ada beberapa jenis pengujian API yang saya pelajari:

1. **Functional Testing** - Apakah API bekerja sesuai spesifikasi?
2. **Performance Testing** - Seberapa cepat respons API?
3. **Security Testing** - Apakah API aman dari ancaman?
4. **Reliability Testing** - Apakah API konsisten dalam berbagai kondisi?
5. **Load Testing** - Bisakah API menangani beban tinggi?

## Postman Sebagai Tool Pengujian

Postman adalah aplikasi super berguna yang memudahkan kita untuk:

- Membuat dan mengirim HTTP request dengan mudah
- Mengorganisir request dalam koleksi
- Menulis skrip pengujian untuk validasi otomatis
- Mengotomatisasi pengujian dengan Collection Runner
- Membuat dokumentasi API yang keren
- Memantau performa API secara real-time

## RESTful API Basics

REST API menggunakan protokol HTTP dengan beberapa metode utama:

- **GET** - Mengambil data (seperti melihat menu)
- **POST** - Mengirim data baru (seperti memesan makanan)
- **PUT** - Memperbarui data lengkap (seperti mengubah seluruh pesanan)
- **PATCH** - Memperbarui sebagian data (seperti menambah porsi)
- **DELETE** - Menghapus data (seperti membatalkan pesanan)

Status kode HTTP juga penting dipahami:
- 2xx = Sukses! (200 OK, 201 Created)
- 4xx = Kesalahan client (404 Not Found, 403 Forbidden)
- 5xx = Kesalahan server (500 Internal Server Error)

## RESTful Booker API

Untuk praktikum ini, saya menggunakan RESTful Booker API, platform booking hotel yang menyediakan endpoint:

- `/auth` - Untuk mendapatkan token autentikasi
- `/booking` - Untuk melihat dan membuat booking
- `/booking/{id}` - Untuk mengakses, mengubah, atau menghapus booking tertentu

## Koleksi Pengujian

Di repo ini, saya membuat beberapa koleksi pengujian:

1. **pengujian-restful-getbooking.json** - Menguji endpoint GET untuk mengambil informasi booking
2. **pengujian-restful-update-booking.json** - Menguji endpoint PUT untuk memperbarui booking

Setiap koleksi meliputi:
- Test script untuk validasi otomatis
- Penggunaan environment variables untuk token dan ID
- Pengujian case positif dan negatif

## Laporan Pengujian

Hasil pengujian dapat dilihat pada laporan HTML yang tersedia di folder `/reports/published/`:

- [Get Booking Report](./reports/published/get-booking-report.html)
- [Update Booking Report](./reports/published/update-booking-report.html)

Laporan ini menampilkan hasil pengujian secara detail dan memudahkan untuk melacak keberhasilan dan kegagalan test.

## Hal Yang Saya Pelajari

Selama praktikum ini, saya belajar:

1. **Penggunaan Test Script** - Mengotomatisasi validasi respons API
   ```javascript
   // Contoh test script
   pm.test("Status code is 200", function() {
       pm.response.to.have.status(200);
   });
   ```

2. **Environment Variables** - Menyimpan nilai dinamis seperti token dan ID
   ```
   {{base_url}}/booking/{{booking_id}}
   ```

3. **Collection Runner** - Menjalankan serangkaian request secara otomatis untuk pengujian menyeluruh

4. **JSON Schema Validation** - Memvalidasi struktur respons API sesuai dengan skema yang ditentukan

5. **Dokumentasi** - Pentingnya mendokumentasikan koleksi API untuk digunakan kembali

## Automation Testing

Automation testing merupakan aspek penting dalam pengembangan modern yang telah saya implementasikan dalam proyek ini. Dengan mengotomatisasi pengujian API, saya mendapatkan beberapa keuntungan:

### Apa yang saya implementasikan:

1. **Pengujian Terstruktur** - Saya membuat struktur pengujian yang mengikuti pola yang konsisten untuk memastikan semua aspek API diuji dengan benar.

2. **Test Case Otomatis** - Saya mengembangkan test case yang dapat dijalankan secara otomatis dan berulang. Ini memungkinkan pengujian regresi yang efisien untuk memastikan perubahan baru tidak merusak fungsionalitas yang sudah ada.

3. **Validasi Data Dinamis** - Implementasi validasi data yang dinamis menggunakan variabel environment Postman untuk memastikan data uji selalu konsisten dan valid.

4. **Laporan Otomatis** - Saya menghasilkan laporan pengujian HTML otomatis yang memberikan visibilitas cepat tentang hasil tes dan memudahkan identifikasi masalah.

### Manfaat yang saya peroleh:

1. **Efisiensi** - Mengurangi secara drastis waktu yang diperlukan untuk menjalankan tes berulang.

2. **Konsistensi** - Menghilangkan variasi manusia dalam pengujian dan memastikan setiap test case dijalankan dengan cara yang sama setiap kali.

3. **Cakupan yang Lebih Luas** - Mampu menguji banyak skenario dan kondisi batas yang sulit dilakukan secara manual.

4. **Deteksi Bug Lebih Awal** - Menemukan masalah lebih cepat dalam siklus pengembangan, mengurangi biaya perbaikan.

5. **Dokumentasi yang Lebih Baik** - Test case otomatis berfungsi sebagai dokumentasi yang hidup tentang bagaimana API seharusnya berperilaku.

Penerapan automation testing dengan Postman memungkinkan saya menjalankan pengujian secara konsisten dan berulang, sambil menghemat waktu dan meningkatkan kualitas pengujian secara keseluruhan.

## Kesimpulan

API testing merupakan komponen penting dalam pengembangan software modern. Dengan Postman, proses pengujian menjadi lebih mudah dan terotomatisasi. Memahami konsep dasar API, metode HTTP, dan teknik validasi respons sangat penting untuk memastikan aplikasi kita berkomunikasi dengan baik dan handal.

## Kontak

Jika Anda memiliki pertanyaan atau ingin berdiskusi tentang proyek ini, jangan ragu untuk menghubungi saya:

- **Nama:** Roy
- **GitHub:** [royjtk](https://github.com/royjtk)
- **Repository:** [restful-booker-testing-postman](https://github.com/royjtk/restful-booker-testing-postman)

---

**Tautan Berguna:**
- [Dokumentasi Postman](https://learning.postman.com/)
- [RESTful Booker API Docs](https://restful-booker.herokuapp.com/apidoc/index.html)
- [HTTP Status Codes](https://httpstatuses.com/)