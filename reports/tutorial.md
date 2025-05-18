# Buat folder untuk report
New-Item -Path "d:\semester6\ppl\w10-w11-api-testing-postman\reports\published" -ItemType Directory -Force

# Jalankan newman dengan HTML reporter untuk Update Booking
newman run "d:\semester6\ppl\w10-w11-api-testing-postman\pengujian-restful-update-booking.json" -e "d:\semester6\ppl\w10-w11-api-testing-postman\Restful_Booker_Environment.json" -r htmlextra --reporter-htmlextra-export "d:\semester6\ppl\w10-w11-api-testing-postman\reports\published\update-booking-report.html"

# Jalankan untuk Get Booking
newman run "d:\semester6\ppl\w10-w11-api-testing-postman\pengujian-restful-getbooking.json" -e "d:\semester6\ppl\w10-w11-api-testing-postman\Restful_Booker_Environment.json" -r htmlextra --reporter-htmlextra-export "d:\semester6\ppl\w10-w11-api-testing-postman\reports\published\get-booking-report.html"