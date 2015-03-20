API Taxis
=========

Retrives taxi around coordinates.

Parameters
----------

Name               | Type   |  Required | Example       |   Comment
-------------------|--------|-----------|---------------|-----------
lon                | double |  Yes      | 45.666        | Longitude of the position of the taxi
lat                | double |  Yes      | -77.88        | Latitude of the position of the taxi
company_id         | string |  No       |  company:1    | Only returns taxis of this company
has_caracteristic  | string |  No       |  dog_accepted | Only returns taxis with the given caracteristic
pickable_via_api   | bool   |  No       |  true         | Filter taxis pickable or not via API
pickable_via_phone | bool   |  No       |  false        | Filter taxis pickable or not via phone
min_seats          | int    |  No       |  4            | Only returns cars with this number of seats or higher
destination_lon    | double |  No       |  46.777       | The API will retrieve estimated distance to the arrival to 
destination_lat    | double |  No       |  34.4         | The destination when it's filled up.


Response
--------

If the HTTP response code is 200, the response is compouned of a dictionnary 
of taxis, a dictionnary of companies, a dictionnary of car brands, and a
destination object.

Description of a taxi object
*****************************

Field               | Type            | Description
--------------------|-----------------|------------------------------------------
lon                 | double          | Longitude
lat                 | double          | Latitude
direction           | double          | Angle in degree from the north
speed               | double          | Speed of the taxi in m/s
caracteristics      | list of strings | Special caracteristrics of the taxi
company_id          | string          | Company id
brand_id            | string          | Brand id
pickup              | href            | Link to a pickup to this taxi
pickable_by_phone   | bool            | Is the taxi pickable via API
pickable_by_api     | bool            | Is the taxi pickable via phone
last_update         | int             | Unix timestamp of the last update
eta                 | int             | Estimated Time of arrival in seconds of the taxi
distance            | int             | Distance in meters of the taxi to the point
oncoming_fee        | double          | Oncoming fee in euros


Description of a company
************************

Field | Type            | Description
------|-----------------|------------------------------------------
name  | string          | Company name 


Description of a car
********************

Field  | Type     | Description
-------|----------|------------------------------------------
brand  | string   | Brand of the car
model  | string   | Model of the car
seats  | int      | Number of available seats in the car

Destination
***********

Field    | Type     | Description
---------|----------|--------------------------------------------------
distance |  int     | Estimated distance to the destination in meters
price    |  double  | Estimated price, without oncoming fees in euros

Example
-------

Request: `https://api.openmaraude.fr/v1/taxis?lon=47.88&lat=12.33&destination_lon=47.92&destination_lat=13.3`

```
{
    "taxis": {
        "taxi1": {
             "lon": 47.3
             "lat": 12.3,
             "direction": -12,
             "speed": 1.2,
             "caracteristics": ["dog_accepted"],
             "company_id": "company1",
             "car_id": "car:1",
             "pickup": "https://api.openmaraude.fr/v1/taxi/taxi1/pickup?lon=47.88&lat=12.33&creation_datetime=12331221",
             "pickable_by_phone": true 
             "pickable_by_api": false,
             "last_update": 11229339,
             "eta": 180,
             "distance": 200,
             "oncoming_fee": 2.4
        }
    },
    "companies": {
        "company:1": {
            "name": "Super Taxi"
        }
    },
    "cars": {
        "car:1": {
            "brand": "renault",
            "model": "velstatis",
            "seats": 3
        }
    }
    "destination": {
        "distance": 5789,
        "price": 15.4
    }
}
```
