
## Matriks Pengujian API - Delete Booking

| ID | Class | Break down class | Kombinasi Data (berada dalam range/ pada tepi batas/ tepi batas +1 / tepi batas -1) | Type Testing | Expectation Result (Respon dari Sistem) |||
|--|--|--|--|--|--|--|--|
| | | | | | Respon Body | Message Status | Database Condition |
| 1 | Autentikasi | Autentikasi Valid (Cookie) | Token autentikasi benar via Cookie | Positive | Tidak ada body | 201 Created | Booking berhasil dihapus |
| 2 | Autentikasi | Autentikasi Valid (Basic Auth) | Username dan password benar via Basic Auth | Positive | Tidak ada body | 201 Created | Booking berhasil dihapus |
| 3 | Autentikasi | Autentikasi Invalid | Token salah atau kadaluarsa | Negative | Error object | 403 Forbidden | Tidak ada perubahan |
| 4 | Autentikasi | Autentikasi Invalid | Header autentikasi tidak disertakan | Negative | Error object | 403 Forbidden | Tidak ada perubahan |
| 5 | Penghapusan Booking | Penghapusan Booking Valid | ID booking valid (berada dalam range) | Positive | Tidak ada body | 201 Created | Booking berhasil dihapus |
| 6 | Penghapusan Booking | Penghapusan Booking Invalid | ID booking tidak ada | Negative | Error object | 404 Not Found | Tidak ada perubahan |
| 7 | Penghapusan Booking | Penghapusan Booking Invalid | ID booking = 0 (pada tepi batas) | Negative | Error object | 404 Not Found | Tidak ada perubahan |
| 8 | Penghapusan Booking | Penghapusan Booking Invalid | ID booking = -1 (di bawah batas) | Negative | Error object | 404 Not Found | Tidak ada perubahan |
| 9 | Penghapusan Booking | Penghapusan Booking Invalid | ID booking menggunakan huruf/karakter khusus | Negative | Error object | 404 Not Found | Tidak ada perubahan |
| 10 | Header | Content Type Valid | Content-Type: application/json | Positive | Tidak ada body | 201 Created | Booking berhasil dihapus |
| 11 | Header | Cookie Valid | Cookie: token=abc123 | Positive | Tidak ada body | 201 Created | Booking berhasil dihapus |
| 12 | Header | Basic Auth Valid | Authorization: Basic YWRtaW46cGFzc3dvcmQxMjM= | Positive | Tidak ada body | 201 Created | Booking berhasil dihapus |
| 13 | Header | Cookie Invalid | Cookie: token= (kosong) | Negative | Error object | 403 Forbidden | Tidak ada perubahan |
| 14 | Header | Basic Auth Invalid | Authorization format salah | Negative | Error object | 403 Forbidden | Tidak ada perubahan |
s