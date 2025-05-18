## Matriks Pengujian API - Create Booking

| ID | Class | Break down class | Kombinasi Data (berada dalam range/ pada tepi batas/ tepi batas +1 / tepi batas -1) | Type Testing | Expectation Result (Respon dari Sistem) |||
|--|--|--|--|--|--|--|--|
| | | | | | Respon Body | Message Status | Database Condition |
| 1 | Header | Content Type Valid | Content-Type: application/json | Positive | Booking ID & detail booking | 200 OK | Booking baru ditambahkan |
| 2 | Header | Accept Valid | Accept: application/json | Positive | Booking ID & detail booking | 200 OK | Booking baru ditambahkan |
| 3 | Header | Content Type Invalid | Content-Type: text/plain | Negative | Error object | 415 Unsupported Media Type | Tidak ada perubahan |
| 4 | Header | Accept Invalid | Accept: application/xml | Negative | Error object (atau format xml) | 406 Not Acceptable | Tidak ada perubahan |
| 5 | Data Tamu | Nama Depan Valid | firstname dengan karakter alfabet | Positive | Booking ID & detail booking | 200 OK | Booking baru ditambahkan |
| 6 | Data Tamu | Nama Depan Invalid | firstname kosong | Negative | Error object | 400 Bad Request | Tidak ada perubahan |
| 7 | Data Tamu | Nama Belakang Valid | lastname dengan karakter alfabet | Positive | Booking ID & detail booking | 200 OK | Booking baru ditambahkan |
| 8 | Data Tamu | Nama Belakang Invalid | lastname kosong | Negative | Error object | 400 Bad Request | Tidak ada perubahan |
| 9 | Harga | Harga Total Valid | totalprice positif (dalam range) | Positive | Booking ID & detail booking | 200 OK | Booking baru ditambahkan |
| 10 | Harga | Harga Total Valid | totalprice = 0 (pada tepi batas) | Positive | Booking ID & detail booking | 200 OK | Booking baru ditambahkan |
| 11 | Harga | Harga Total Invalid | totalprice = -1 (di bawah batas) | Negative | Error object | 400 Bad Request | Tidak ada perubahan |
| 12 | Harga | Harga Total Invalid | totalprice = "abc" (tipe data salah) | Negative | Error object | 400 Bad Request | Tidak ada perubahan |
| 13 | Status Deposit | Deposit Valid | depositpaid = true | Positive | Booking ID & detail booking | 200 OK | Booking baru ditambahkan |
| 14 | Status Deposit | Deposit Valid | depositpaid = false | Positive | Booking ID & detail booking | 200 OK | Booking baru ditambahkan |
| 15 | Status Deposit | Deposit Invalid | depositpaid = "string" (tipe data salah) | Negative | Error object | 400 Bad Request | Tidak ada perubahan |
| 16 | Status Deposit | Deposit Invalid | depositpaid kosong | Negative | Error object | 400 Bad Request | Tidak ada perubahan |
| 17 | Tanggal | Tanggal Checkin Valid | Format tanggal valid "YYYY-MM-DD" | Positive | Booking ID & detail booking | 200 OK | Booking baru ditambahkan |
| 18 | Tanggal | Tanggal Checkout Valid | Format tanggal valid "YYYY-MM-DD" | Positive | Booking ID & detail booking | 200 OK | Booking baru ditambahkan |
| 19 | Tanggal | Tanggal Checkin Invalid | Format tanggal tidak valid | Negative | Error object | 400 Bad Request | Tidak ada perubahan |
| 20 | Tanggal | Tanggal Checkout Invalid | Format tanggal tidak valid | Negative | Error object | 400 Bad Request | Tidak ada perubahan |
| 21 | Tanggal | Range Tanggal Valid | checkout > checkin | Positive | Booking ID & detail booking | 200 OK | Booking baru ditambahkan |
| 22 | Tanggal | Range Tanggal Valid | checkout = checkin (pada tepi batas) | Positive | Booking ID & detail booking | 200 OK | Booking baru ditambahkan |
| 23 | Tanggal | Range Tanggal Invalid | checkout < checkin (di bawah batas) | Negative | Error object | 400 Bad Request | Tidak ada perubahan |
| 24 | Tanggal | Tanggal Kosong | bookingdates kosong | Negative | Error object | 400 Bad Request | Tidak ada perubahan |
| 25 | Kebutuhan Tambahan | Kebutuhan Valid | additionalneeds dengan teks | Positive | Booking ID & detail booking | 200 OK | Booking baru ditambahkan |
| 26 | Kebutuhan Tambahan | Kebutuhan Kosong | additionalneeds kosong | Positive | Booking ID & detail booking (tanpa additionalneeds) | 200 OK | Booking baru ditambahkan |
| 27 | Body Request | Request Valid | Semua field wajib valid | Positive | Booking ID & detail booking | 200 OK | Booking baru ditambahkan |
| 28 | Body Request | Request Invalid | Body JSON malformed | Negative | Error object | 400 Bad Request | Tidak ada perubahan |
| 29 | Body Request | Request Invalid | Body kosong | Negative | Error object | 400 Bad Request | Tidak ada perubahan |
| 30 | Respons | Respons Valid | Sukses | Positive | Object dengan bookingid dan booking object | 200 OK | Booking baru ditambahkan |
