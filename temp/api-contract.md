Booking - DeleteBooking
Returns the ids of all the bookings that exist within the API. Can take optional query strings to search and return a subset of booking ids.

delete
https://restful-booker.herokuapp.com/booking/1
Example 1 (Cookie):
Example 2 (Basic auth):
curl -X DELETE \
  https://restful-booker.herokuapp.com/booking/1 \
  -H 'Content-Type: application/json' \
  -H 'Cookie: token=abc123'
curl -X DELETE \
  https://restful-booker.herokuapp.com/booking/1 \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Basic YWRtaW46cGFzc3dvcmQxMjM='
Header
Field	Type	Description
Cookieoptional	string	
Sets an authorization token to access the DELETE endpoint, can be used as an alternative to the Authorization

Default value: token=<token_value>

Authorizationoptional	string	
Basic authorization header to access the DELETE endpoint, can be used as an alternative to the Cookie header

Default value: Basic YWRtaW46cGFzc3dvcmQxMjM=

Url Parameter
Field	Type	Description
id	Number	
ID for the booking you want to update

Success 200
Field	Type	Description
OK	String	
Default HTTP 201 response

Response:
HTTP/1.1 201 Created



=================================
Booking - CreateBooking
Creates a new booking in the API

post
https://restful-booker.herokuapp.com/booking
JSON example usage:
curl -X POST \
  https://restful-booker.herokuapp.com/booking \
  -H 'Content-Type: application/json' \
  -d '{
    "firstname" : "Jim",
    "lastname" : "Brown",
    "totalprice" : 111,
    "depositpaid" : true,
    "bookingdates" : {
        "checkin" : "2018-01-01",
        "checkout" : "2019-01-01"
    },
    "additionalneeds" : "Breakfast"
}'
Header
Field	Type	Description
Content-Type	string	
Sets the format of payload you are sending. Can be application/json

Default value: application/json

Accept	string	
Sets what format the response body is returned in. Can be application/json

Default value: application/json

Request body
Field	Type	Description
firstname	String	
Firstname for the guest who made the booking

lastname	String	
Lastname for the guest who made the booking

totalprice	Number	
The total price for the booking

depositpaid	Boolean	
Whether the deposit has been paid or not

  checkin	Date	
Date the guest is checking in

  checkout	Date	
Date the guest is checking out

additionalneeds	String	
Any other needs the guest has

Success 200
Field	Type	Description
bookingid	Number	
ID for newly created booking

booking	Object	
Object that contains

  firstname	String	
Firstname for the guest who made the booking

  lastname	String	
Lastname for the guest who made the booking

  totalprice	Number	
The total price for the booking

  depositpaid	Boolean	
Whether the deposit has been paid or not

  bookingdates	Object	
Sub-object that contains the checkin and checkout dates

    checkin	Date	
Date the guest is checking in

    checkout	Date	
Date the guest is checking out

  additionalneeds	String	
Any other needs the guest has

JSON Response:
URL Response:
HTTP/1.1 200 OK

{
    "bookingid": 1,
    "booking": {
        "firstname": "Jim",
        "lastname": "Brown",
        "totalprice": 111,
        "depositpaid": true,
        "bookingdates": {
            "checkin": "2018-01-01",
            "checkout": "2019-01-01"
        },
        "additionalneeds": "Breakfast"
    }
}