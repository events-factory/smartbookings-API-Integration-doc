# API Documentation

## Base URL

[https://smartbookings.rw](https://smartbookings.rw)

## Endpoints
----------------------------------------------------------------------------------------------------------------------------------------------------------
### Get filters

##### End Pont ------------------------------------------------------------------------->  `/Client-FiltersList`

##### HTTP Method -------------------------------------------------------------------------> `GET`

##### Response Body

The JSON response is a collection of objects, where each object represents a search filter category. Each object has two properties: "name" and "subCategory". The "name" property is a string that represents the name of the filter category, and the "subCategory" property is an array of objects, where each object represents a subcategory within the filter category.

```json
]
  "place": "Rwanda", // default search filters
  "bookingrange": "20/04/2023 - 21/04/2023", // default search filters
  "roomnum": 1, // default search filters
  "adult": 1, // default search filters
  "child": 0, // default search filters
	{
	    "name": "General Amenities", // name of the group
	    "subCategory": [ // filters in the group they are retiurned as array of objects
		{
		    "value": true, // value to be passed to the parametter when filtering
		    "searchID": "airconditioning", // parametter name to be passed when filtering
		    "name": "Air Conditioner" // nome to be displayed to the UI
		},
	    ]
	}
]

```

----------------------------------------------------------------------------------------------------------------------------------------------------------
### Get facilities

##### End Pont ------------------------------------------------------------------------->  `//Client-HotelsList/{{private_key_shared}}`

##### HTTP Method -------------------------------------------------------------------------> `GET`

##### Required parametters

`[place, bookingrange, roomnum, roomnum, adult, child]` 

Those parametters should be initially passed to the endpont in order to focus on the ares and limit the result default falues are returned in the filters API refer on the endpoint above

##### Response Body
```json
{
    "message": "Request successfull",
    "data": {
      "facilities": [ // return the array of object of all hotels
        {
          "hotelcode": "5e158144c15aa",
          "hotelname": "LEGEND HOTEL KIGALI",
          "banner": "https://smartbookings.rw/gallery/hotels/1661261031.jpeg",
          "star": "3",
          "address": "KN 8 Avenue, Kigali, Rwanda",
          "city": "Kigali, Rwanda",
          "country": "Rwanda",
          "minprice": "180",
          "currency": "USD ($)",
          "allroom": 5,
          "takeroom": 0,
          "requestedroom": "10",
          "available": 5,
          "summary": "Only 5 room available for this period",
          "category": "Boutique Hotel",
          "description": "Legend Hotel is one of Kigali's luxurious boutique hotels conveniently located in Kacyiru, Kigali City, situated next to the American Embassy with fantastic view of the surrounding hills. Legend Hotel offers you a confortable stay in a classy and relaxed atmosphere. the hotel is less than 20 minutes drive to Kigali International Airport and 10 minutes to the City Center.",
          "facilities": [ // facilities provided by the hotel
              "Languages: French, English, Swahili",
              "Breakfast: Free Continental, American, Buffet, A la carte, Vegetarian",
              "Internet: wireless in entire property (Free)",
              "Parking : Free, public, on site, does not require reservation",
              "Bar",
              "Air Conditioner (Free)",
              "Garden",
              "Terrace",
              "Non-smoking rooms",
              "Family rooms"
          ]
        }
      ]
    }
}
```

In the case of filteing by amenities the parametter should be passed in the url in the format of {{searchID}}={{value}}

```
{{host}}/Client-HotelsList/NjAzNjRkMTlkOTViOA/1/Find?{{searchID}}={{value}}&{{searchID}}={{value}}
```

The data passed should be encoded in URL format

The `{{searchID}}` and `{{value}}` are returned in the filter endpoint

Exceptions occur during the search process when filtering by date or price range. The date range is formatted as `MM/DD/YYYY - MM/DD/YYYY`, with both dates included in a single string. For the price range, the minimum and maximum amounts are separated by a semicolon, such as `1;100`, where the first value represents the minimum and the second value represents the maximum.

----------------------------------------------------------------------------------------------------------------------------------------------------------
### Get facilities

##### End Pont ------------------------------------------------------------------------->  `/Client-HotelDetail/{{private_key_shared}}`

##### HTTP Method -------------------------------------------------------------------------> `GET`

#####  Required parametters

`[adult,child,numberofroom,checkin,checkout]` these parametters are required to be passes in the url to determine price estimation and should be encoded as URL

Sample response

```json
  {
    "message": "Query successful",
    "hotel": {
        "id": "19",
        "name": "LEGEND HOTEL KIGALI",
        "code": "5e158144c15aa",
        "address": "KN 8 Avenue, Kigali, Rwanda",
        "description": "Legend Hotel is one of Kigali's luxurious boutique hotels conveniently located in Kacyiru, Kigali City, situated next to the American Embassy with fantastic view of the surrounding hills. Legend Hotel offers you a confortable stay in a classy and relaxed atmosphere. the hotel is less than 20 minutes drive to Kigali International Airport and 10 minutes to the City Center.",
        "country": "Rwanda",
        "star": "3",
        "city": "Kigali, Rwanda",
        "banner": "https://smartbookings.rw/gallery/hotels/1661261031.jpeg",
        "gallery": [
            "https://smartbookings.rw/gallery/hotels/1661261031.jpeg",
            "https://smartbookings.rw/gallery/hotels/1661261045.jpg",
            "https://smartbookings.rw/gallery/hotels/1661261052.jpeg",
            "https://smartbookings.rw/gallery/hotels/1661261059.jpeg",
            "https://smartbookings.rw/gallery/hotels/1661261067.jpeg"
        ]
    },
    "policies": {
        "checkin": "14:00",
        "checkout": "11:00",
        "cancelation-policy": [
            {
                "type": "Multiple Booking",
                "description": "For bookings of 10 rooms or more, the cancellation policy will be as follows: 19457 day(s) day(s) prior to arrival the cancelation is allowed,One night will be charged"
            },
            {
                "type": "Single Booking",
                "description": "For bookings of 1-9 rooms, the cancellation policy will be as follows: 19464 day(s) day(s) prior to arrival the cancelation is allowed,One night will be charged"
            }
        ],
        "children-policy": "Children are allowed",
        "pets-policy": "Pets are allowed"
    },
    "payment": [
        "MasterCard",
        "Visa Card",
        "Onsite Payement"
    ],
    "facilities": [
        "Languages: French, English, Swahili",
        "Breakfast: Free Continental, American, Buffet, A la carte, Vegetarian",
        "Internet: wireless in entire property (Free)",
        "Parking : Free, public, on site, does not require reservation",
        "Bar",
        "Air Conditioner (Free)",
        "Garden",
        "Terrace",
        "Non-smoking rooms",
        "Family rooms"
    ],
    "extrabed": {
        "extrabed": "yes",
        "numberofextrabed": "1",
        "extrabedchildprice": [
            {
                "type": "Children up to 2 years old in cribs",
                "allowed": "yes",
                "age": "0-2",
                "price": "30"
            },
            {
                "type": "Young children",
                "allowed": "yes",
                "age": "Up to 12 years old",
                "price": "40"
            },
            {
                "type": "Adults",
                "allowed": "yes",
                "age": "Above 12 years old",
                "price": "50"
            }
        ]
    },
    "rooms": [
        {
            "roomcode": "5e158d07410af",
            "roomname": "Deluxe Double Room",
            "othername": "Deluxe Room",
            "roomtype": "Double",
            "roomsize": "30",
            "unitmesure": "square meters",
            "roomprice": "180",
            "currencyunit": "USD ($)",
            "available": 0,
            "summury": "This room can only take 1 people, you requested 2 adults and 0 children",
            "capacity": 1,
            "bedrooms": {
                "id": "22",
                "bedtypeone": "King bed(s) 181-210 cm wide",
                "numberone": "1",
                "bedtypetwo": "Twin bed(s) 90-130 cm wide",
                "numbertwo": "0",
                "bedtypethree": "",
                "numberthree": "0",
                "totalpeopleinbedroom": "2",
                "roomcode": "5e158d07410af",
                "doneOn": "08 January 2020",
                "doneBy": "23"
            },
            "numberofbedroom": "1 bedroom",
            "numberofbathroom": "1 bathroom",
            "livingroom": "1 Living room",
            "amenties": []
        }
    ]
}
```

----------------------------------------------------------------------------------------------------------------------------------------------------------
### Post Booking

##### End Pont ------------------------------------------------------------------------->  `/Client-BookingForm`

##### HTTP Method -------------------------------------------------------------------------> `POST`

##### Headers

The authorisation header should be passed in the header request Authorization : {{shared_key}}

#####  Request body

```json
{
  "title": "MR",
  "firs_tname": "Aime",
  "last_name": "Moulin",
  "email": "aimemalaika1995@gmail.com",
  "booking_for": "myself",
  "beneficiername": "",
  "beneficieremail": "",
  "number_of_room": 1,
  "askquestion": "test question",
  "coming_on": "2019-01-01 00:00:00",
  "country": "France",
  "phone": "0600000000",
  "payment_method": "MasterCard", 
  "reason":  "Business",
  "hotel_code": "605849ad13851",
  "room_code": "60584d7ab66f8",
  "book_from": 1655589600,
  "book_to": 1656108000,
  "adult": 1,
  "child": 0,
  "token": "tokenuniqueme"
}
```

NB: 

The "book_from" and "book_to" should be in time stamp foprmat

###### Response format

```json
{
    "reponse": 1,
    "message": "Booking done successfully check your email for confirmation",
    "token": "2af44637a7e5de48c148daf771efb2c4c9800a3c"
}

```


