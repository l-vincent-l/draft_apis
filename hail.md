#Hail#

You need to make a *PUT* http request to create a hail, here are the parameters.

##Parameters##

Name              | Type   | Required | Example  | Description
------------------|--------|----------|----------|----------------
lon               | double | yes      | 47.99    | Longitude of the geographical position of the customer
lat               | double | yes      | 12.3     | Latitude of the geographical position of the customer
creation_datetime | int    | yes      | 11182888 | Creation datetime of the pickup.

##Response##


###Description hail###
 
Field           | Type   | Description
----------------|--------|-------------------------------------
self            | href   | A link to the newly created pickup
lon             | double | Longitude of the pickup position
lat             | double | Latitude of the pickup position
taxi            | taxi   | A taxi object 
status          | enum   | Status of the pickup
phone_number    | int    | Phone number to call to hail if it's pickable via phone
hailable_via    | enum   | Can be `API` or `phone`


###taxi object###

Field               | Type            | Description
--------------------|-----------------|-------------
lon                 | double          | Longitude
lat                 | double          | Latitude
direction           | double          | Angle in degree from the north
speed               | double          | Speed of the taxi in m/s
caracteristics      | list of strings | Special caracteristrics of the taxi
company_id          | string          | Company id
brand_id            | string          | Brand id
last_update         | int             | Unix timestamp of the last update
eta                 | int             | Estimated Time of arrival in seconds of the taxi
distance            | int             | Distance in meters of the taxi to the point
oncoming_fee        | double          | Oncoming fee in euros

