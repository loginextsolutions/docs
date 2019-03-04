---
title: LogiNext API

language_tabs:
  - Sample Requests and Responses

toc_footers:
  - <a href='#'>Sign Up for a Developer Key</a>
  - <a href='https://github.com/tripit/slate'>Documentation Powered by Slate</a>

search: true
---

# Introduction


## LogiNext Terminology

LogiNext welcomes you to the world of organised logistics.

In this section we'll go over the elements that make up the LogiNext system, and how you can start integrating with the LogiNext API.

###Delivery Associate 
A Delivery Associate carries out the Pick-up or Delivery of Orders. Delivery Associates can be
maintainence men, repair men, or delivery boys.

When a Delivery Associate is created in LogiNext, Login credentails are generated, using which the Delivery Associate can Sign-in to the TrackNext app.

###Vehicle
Vehicles can be used to Pick-up and Deliver Orders that are part of the Trip. A Vehicle could be a bike, car, truck, van and more. 

###Driver 
Driver is responsible for driving/riding the Delivery Vehicle.

###Branch 
A Branch could be the fulfillment center or warehouse where Orders are either Delivered or Pickedup from. 

###Service Time 
Service Time is the time it takes to service an Order at a particular location. For example - If an Order is to be delivered at a Customer's Home address, the Service time would include the time for parking the Vehicle and accounting for security checks at the location if any. Similarly, if an Order is to be delivered at a warehouse, Service Time will account for parking, loading and unloading at the delivery location.

Depending on the kind of business, the Driver and Delivery Associate could be the same person. In some cases they are different where in addition to a Driver, there is a Delivery Associate delivering the shipments home.


### Orders

An Order has details of shipment you want to pickup from your merchant or deliver to your customer. Pick Up and Delivery could be different depending on the industry you are in. For example, in the Courier Industry, Pick Up and Delivery can be for Customers.

Orders can be be labeled differently, according to your industry and needs. For example, one customer has named it shipment.

### Trips
Trips are defined as a group of orders that a delivery associate must fulfill as part of a single assignment. One trip can consist of multiple orders to be delivered by a delivery associate.

## Integration Details

Using the LogiNext API, you can integrate all the segments of your logistics and supply chain network into our product platform to create a seamless experience for your operations and executive team.

The LogiNext API is designed to allow our client partners to add delivery associates(resources), orders, plan a route, start the trip, track and follow the updates till the trip is completed and shipment is pickedup/delivered at the desired location.

Below are few important steps that would explain what it takes for you, as our Client partner, to link your system with LogiNext’s.

<b><u>Step 1</u></b> –  Please read carefully the Request, Responses and Authentication section so that you can configure things on your end to integrate with LogiNext APIs.

<b><u>Step 2</u></b> – You will need to get the username and password which will be provided to you either by our system (in case of auto sign-up) or by our assigned CSAs(Customer Service Associate).

<b><u>Step 3</u></b> – (Optional) If you are planning to consume any of the LogiNext notifications, you will need to share the end-point URL on your system to consume the Webhook.

<br> In case of any queries during the integration process, please reach out to us at
<a href="mailto:support@loginextsolutions.com?Subject=Integration%20Queries" target="_top">support@loginextsolutions.com</a> 


# Requests

The base URL for all requests to the LogiNext API is:

https://api.loginextsolutions.com/

Our API is REST-based. This means:

1. It make use of standard HTTP verbs like GET, POST, DELETE.

2. The API uses standard HTTP error responses(status codes) to indicate status of your requests – success and error codes.

3. Authentication is specified with HTTP Basic Authentication.

Also,the input dates like 2016-07-01T11:18:00.000Z are accepted in Coordinated Universal Time (UTC) format.

### Request Headers

Header | Sample Value | Description
--------- | ------- | -------------
Content-Type | application/json | JSON request
WWW-Authenticate | BASIC 51bbe3f7-1671-476c-818a-e7fbbca10202 | Authentication token

### Versioning

Versioning allows us to provide developers a consistent experience. All endpoints are prefixed with a version such as /v1, v2 etc. This version refers to the overall layout of the endpoints and response standards.

# Responses

The LogiNext API uses HTTP status codes to indicate the status of your requests. This includes Success and Error codes.

Dates in API responses like 2016-07-01T11:18:00.000Z are sent in Coordinated Universal Time (UTC) format.

Code | Message | Description
---------- | ------- | -------
200 | Success | This message means that the request is successfully processed.
201 | Created  | This message means that the resource is successfully created.
202 | Acknowledged | This status code indicates that a request has been received and taken up for processing. It may take some time to complete processing this kind of request, and LogiNext will typically send a webhook notification with the results of the response once the request has been csuccessfully completed.
400 | Bad Request  | This message means that the request is syntactically incorrect. You will receive this med=ssage in a case where the request body sent is not a standard JSON or array object as is expected by LogiNext.
401 | Invalid username or password  | This message means that invalid credentials are passed.
404 | Not Found  | This message means that the resource could not be found.
405 | Method Not Allowed  | This message means that the method used to access the resource is invalid.
409 | Request Error  | This message means that there is a validation error in the data sent in the request body. This could either be missing out a mandatory field in the API or sending an incrrect branch name in the request body.
415 | Unsupported Media Type  |  This message means that the request is not in the format accepted by this method of target resource.
429 | Too Many Requests  |  This message means that too many resources are requested.
500 | Internal Server Error  | This message means that there is an issue with the LogiNext server.Please try accessing the request later.
503 | Service Unavailable  | This message means that the LogiNext applications are down for scheduled maintanance. Please try accessing the request later.

# Authentication

##Authenticate

LogiNext API uses Basic Authentication to provide you an authorized access. Please use the the below URL Endpoint to authenticate yourself as a user of this API.

You will have to pass the username and password which is provided to you either by our system (in case of auto sign-up) or by our assigned CSAs(Customer Service Associate).

The response will contain a session token, which is unique in relation to every specific customer.

If you want session to be valid for 1 Hour, then the "sessionExpiryTimeout" should be 1.<br>
Similarly for - <br>
24 Hours, it should be 24 <br>
6 months, it should be  180* 24 = 4320<br>
12 Months, it should be 365*24= 8760<br>
5 Years, it should be 365*5*24 = 43800<br>
10 Years, it should be 365*10*24= 87600<br>

<b><u>If you do not provide 'sessionExpiryTimeout', the validity of this session token will be 1 day (24 hours).</u></b>

Please ensure that you add the token as part of every Loginext API call.

> Definition

```json
https://api.loginextsolutions.com/LoginApp/login/authenticate
```
> Request Body

```json
{
        "userName":"demouser",
        "password":"Admin#1!",
        "sessionExpiryTimeout": 87600
}  
```

> Response

```json
{
  "status": 200,
  "message": "success",
  "data": null,
  "hasError": false
}
```

#### Request

<span class="post">POST</span>`https://api.loginextsolutions.com/LoginApp/login/authenticate`

#### Request Headers

Header | Sample Value | Description
--------- | ------- | -------------
Content-Type | application/json | JSON request

#### Request Parameters

Parameter | DataType | Length | Required | Description
-----------|-------|---|---------------|--------
userName | String | 255 | Mandatory | Username provided by LogiNext
password | String | 255 | Mandatory | Password provided by LogiNext
sessionExpiryTimeout | Integer | 10 | Optional | Number of hours till which you want the session to be valid

#### Response
The response will consist of parameters as mentioned in the "Responses" section based on the request parameters passed.For example,the response can contain 200 - Success or 401 - Invalid username or password, etc.

#### Response Headers

The response header will consist of Authentication Token. Please note that the validity of this token by default is 24 hours only.

Header | Sample Value
--------- | -------
WWW-Authenticate | BASIC 075b8961-bd02-454c-83eb-259f965f313f


## Authenticate Delivery Associate

Call the mobile authenticate API to obtain the token and key for a Delivery Associate.

You will have to pass the username and password entered at the time of creating the Delivery Associate in the LogiNext system in the request body.

The response will contain a session token, which is unique in relation to every specific customer. This token will have a validaity of 4 years from the time of creation.



> Definition

```json
  https://api.loginextsolutions.com/LoginApp/login/mobile/auth
```
> Request Body

```json
{
  "userName": "mi4",
  "password": "admin",
  "imei":"12345",
  "latitude": 19.1114131,
  "longitude": 72.9094666,
  "androidId": "ce6448cf20b78483",
  "androidTime": "2017-04-21T05:53:47Z"
}  
```

> Response

```json
{
    "status": 200,
    "message": "Login successfully.",
    "hasError": false
}
```

#### Request

<span class="post">POST</span>`https://api.loginextsolutions.com/LoginApp/login/mobile/auth`

#### Request Headers

Header | Sample Value | Description
--------- | ------- | -------------
Content-Type | application/json | JSON request


#### Request Parameters

Parameter | DataType | Length | Required | Description
-----------|-------|---|---------------|--------
userName | String | 255 | Mandatory | Username provided by LogiNext
password | String | 255 | Mandatory | Password provided by LogiNext
imei | String | 50 | Mandatory | IMEI Number of the Delivery Associate's phone
latitude | Double | | Optional | Geolocation(latitude) coordinate of the Delivery Associate
longitude | Double | | Optional | Geolocation(longitude) coordinate of the Delivery Associate
androidId | String | 10 | Optional | Device ID of the Delivery Associate
androidTime | Date | | Optional | Current Date and Time in UTC and the mentioned Format. Sample Value - 2017-12-11T07:21:39Z


#### Response
The response will consist of parameters as mentioned in the "Responses" section based on the request parameters passed.For example,the response can contain 200 - Success or 401 - Invalid username or password, etc.

#### Response Headers

The response header will consist of Authentication Token and Client Secret Key. Please note that the validity of this token and key is 24 hours only.

Header | Sample Value
--------- | -------
WWW-Authenticate | BASIC 075b8961-bd02-454c-83eb-259f965f313f


##Invalidate

You can fetch a fresh session token by calling the below API. This call will invalidate the existing token  and then you will be provided with a new token which you will have to pass everytime in every other API call.

> Definition

```json
https://api.loginextsolutions.com/LoginApp/login/token/refresh
```

> Response

```json
{
  "status": 200,
  "message": "success",
  "data": null,
  "hasError": false
}
```

This endpoint invalidates a user.

#### Request

<span class="post">GET</span>`https://api.loginextsolutions.com/LoginApp/login/token/refresh`


#### Request Headers

Header | Sample Value
--------- | ------- | -------------
Content-Type | application/json | Json request
WWW-Authenticate | BASIC 8bce7b1b-9762-4de7-b9cd-976ecf38b6a0 | Authentication token

#### Response Headers

Header | Sample Value
--------- | -------
WWW-Authenticate | BASIC 075b8961-bd02-454c-83eb-259f965f313f


# Limits


LogiNext API defines Rate Limits based on the API being called. Different APIs have different Rate Limits depending on the use case and request body of the API.

To create Orders, you can call the LogiNext API with a call rate of 1 request/second.

The LogiNext Orders API accept upto 20 records per request. For eg - If you call the Create Order API, you can create upto 20 Orders per second, with a single call of this API.


This means - 

1n 1 second you can create 20 Orders in LogiNext.<br>
In 1 minute you can create - 20*60 = 1200 Orders in LogiNext.<br>
In 1 hour you can create - 20*60*60 = 72000 Orders in LogiNext.<br>

The Get Location Serviceability API has a Rate Limit of 20 requests/second. You can make 20 calls for this API every second, as one call for this API returns a signle address per call.

Going beyond your rate limit will cause you to receive a temporary ban. You will receive a 429 'Max Request Limit Reached' error  to your API calls if you go beyond this limit.

## Batching
The LogiNext API support multiple records per request. For eg - You can send upto 20 Orders to be created in a single call of the Create Order API. 

APIs that support batching have a rate limit of 1 request per second and accept upto 20 records per request. 

If you are pushing more than 20 Orders to LogiNext, you will need to create a queuing mechanism that will push 20 Orders  in each request of the Create Order API per second. The next set of Orders can be sent in the next request after a 1 second delay. 

We recommend implementing retry mechanism at your end in case of the following error responses received from the LogiNext API - 429, 500



# LogiNext Haul <sup>TM</sup>


1. Once the resources are created, then you can create trips by calling Create Trips API. You need to provide the Unique trip name along with the Origin and Destination Address details and the Journey date. The acknowledgement consists of the Reference ID for each of the trips created which needs to be stored in your system for future references.
Please check with our assigned CSAs on the address format based on the model type configured for you as either the Pin Code or Hub to Hub.

2. Further you can mark the trip as started by calling the Start Trip API and mark the same trip as stopped by calling Stop Trip API. In both these API you will have to pass the trip reference ID.

3. Finally you can track your vehicle in transit through the Track Last Location API. in this case also you need to pass the Trip Reference ID.

## Vehicle
### Create

For Haul and Mile products, you can create and maintain details of the vehicles in the LogiNext system using Create Vehicle API. This API requires vehicle’s primary information (mandatory - Vehicle Number) and returns a "Reference Id" which you need to store in order to update the vehicle information in future.

> Definition

```json
https://api.loginextsolutions.com/VehicleApp/haul/v1/create
```


> Request Body

```json
[
  {
        "vehicleNumber":"MH-111",
        "vehicleMake":"2015",
        "vehicleModel":"OMNI",
        "typeOfBody":"Flat Bed",
        "unladdenWeight":10,
        "capacityInWeight":10,
        "capacityInUnits":10,
        "capacityInVolume":10,
        "chasisNumber":"CHASIS-123",
        "engineNumber":"A-12353-D1234",
        "markerName":"Marker-1",
        "registrationNumber":"",
        "pucValidity":"2016-07-01T11:18:00.000Z",
        "insuranceValidity":"2016-07-01T11:18:00.000Z",
        "vehiclePermit":"New York, NY",
        "ownership":"company",
        "ownerName":"Mathew Richardson",
        "transporter":"",
        "financer":"",
        "accidentHistory":"",
        "rentStartDate":null,
        "rentEndDate":null,
        "deviceId":{
            "barcode":"LN12345678"
        }
    }
]  
```

> Response

```json
{
  "status": 200,
  "message": "success",
  "data": [
      {
        "vehicleNumber":"1ABC234",
        "referenceId":"a9be39b9347911e6829f000d3aa04450"
      }
     ],
  "hasError": false
}
```

Create a new vehicle by passing form data through json.

The acknowledgement will provide the vehicle number and reference ID.

#### Request

<span class="post">POST</span>`https://api.loginextsolutions.com/VehicleApp/haul/v1/create`


#### Request Parameters

Parameter | DataType |  Length | Required | Description
-----------|-------|-------|-------------|----------
vehicleNumber | String | 255 | Mandatory | Unique name to identify the vehicle
vehicleMake | String | 255 | Optional | Make of the vehicle like Mazda, Volvo, etc.
vehicleModel | String | 40 | Optional | Model of the vehicle as specified by manufacturer like FH series, MethaneDiesel, etc.
typeOfBody | String | 40 | Optional | Body Type of the vehicle. This is static field and can have only one of the below values - 4 wheeler, 2 wheeler, 24FT, 20FT, 32FT, 19FT, TATA 407, 14 FT CANTER, 17FT, TRLR, TRUCK
unladdenWeight | Integer | 10 | Optional | Unladen weight of the vehicle in Kg.
capacityInWeight | Integer | 10 | Optional | Capacity of vehicle in Kg.
capacityInUnits | Integer | 10 | Optional | Capacity of the vehicle in Units
capacityInVolume | Integer | 10 | Optional | Capacity of the vehicle on cubic centimeters
chasisNumber | String | 255 | Optional | Chassis / VIN number of the vehicle
engineNumber | String | 255 | Optional | Engine Number of the vehicle
markerName | String | 255 | Optional | Name of the Sub-ordinate who is driving along with the driver
registrationNumber | String | 255 | Optional | Registered Number provided by the local transportation authority
pucValidity | Date |  | Optional | Date till which PUC certificate is valid.Format - YYYY-MM-DDTHH:MM:SS.SSSZ e.g. : 2016-07-01T11:18:00.000Z. This date always needs to be later than the current date.
insuranceValidity | Date |  | Optional | Date till which insurance of the vehicle is valid. Format - YYYY-MM-DDTHH:MM:SS.000Z e.g. : 2016-07-01T11:18:00.SSSZ.This date always needs to be later than the current date.
vehiclePermit | String | 40 | Optional | Full name of the states of India in which the vehicle is permitted to travel
ownership | String | 50 | Optional | Entity that owns the vehicle. This field can have only below two values - Company , Vendor
ownerName | String | 255 | Optional | Name of the Company / Vendor who owns the vehicle
transporter | String | 40 | Optional | Name of the transporter / carrier / 3PL provider responsible for the delivery.
financer | String | 40 | Optional | If the vehicle is on loan, then name of the financer
accidentHistory | String | 160 | Optional | If vehicle has any accident records against it, then please document the details through this field
rentStartDate | Date |  | Optional | This input is valid only if the vehicle’s owner is a vendor. Format - YYYY-MM-DDTHH:MM:SS.000Z e.g. : 2016-07-01T11:18:00.SSSZ. Rent start Date should be earlier than the Rent End Date.
rentEndDate  | Date |  | Optional | This input is valid only if the vehicle’s owner is a vendor. Format - YYYY-MM-DDTHH:MM:SS.000Z e.g. : 2016-07-01T11:18:00.SSSZ. Rent End Date should be later than the Rent Start Date.
deviceId.barcode | String | 50 | Optional | This input should be the barcode of the tracker in order to map the Vehicle with the tracker.In order to get the list of tracker that you can attach to a vehicle, you will need to either access the Loginext portal with your login or contact our CSA and get the list. On LogiNext portal, you can access the tracker list - LogiNext → Resource → Tracker.

### Get

> Definition

```json
https://api.loginextsolutions.com/VehicleApp/haul/v1/:reference_id
```



> Response

```json
{
  "status": 200,
  "message": "success",
  "data": {
    "vehicleId": 1182,
    "vehicleName": null,
    "guid": "1efc418bd9f54bd99955cfdcccdc27a2",
    "vehicleNumber": "1ABC234",
    "vehicleMake": null,
    "vehicleModel": null,
    "vehicleType": null,
    "typeOfBody": "",
    "unladdenWeight": null,
    "capacityInUnits": 12,
    "capacityInVolume": 12,
    "capacityInWeight": 12,
    "chasisNumber": null,
    "engineNumber": null,
    "markerName": null,
    "registrationNumber": null,
    "pucValidity": null,
    "insuranceValidity": null,
    "vehiclePermit": null,
    "ownerName": null,
    "clientBranchId": 1402,
    "rentEndDate": null,
    "rentStartDate": null,
    "transporter": null,
    "financer": null,
    "permit": null,
    "ownership": null,
    "accidentHistory": null,
    "deviceId": {
      "deviceId": null,
      "barcode": null,
      "statusCd": null,
      "trackeeId": null
    },
    "registrationCopy": [],
    "pucCopy": [],
    "insuranceCopy": [],
    "registrationCopyExists": null,
    "insuranceCopyExists": null,
    "pucValidityExists": null,
    "clientBranchName": "Jonson Logistics"
  },
  "hasError": false
}

```

Use this API to read all data for a particular vehicle using its reference ID.


#### Request

<span class="post">GET</span>`https://api.loginextsolutions.com/VehicleApp/haul/v1/:reference_id`


#### Request Parameters

Parameter | DataType | Length | Required | Description
-----------|-------|-------|------|----------
reference_id | String | 32 | Mandatory | Reference Id associated with the vehicle.


### Get List

> Definition

```json
https://api.loginextsolutions.com/VehicleApp/haul/v1
```

> Response

```json
{
  "status": 200,
  "message": "success",
  "data": {
    "totalCount": 119,
    "otherCount": 0,
    "results": [
      {
        "vehicleName": null,
        "vehicleNumber": "VH-00-1122",
        "vehicleMake": null,
        "vehicleModel": null,
        "vehicleType": null,
        "typeOfBody": "",
        "previousVehiclenumber": null,
        "unladdenWeight": null,
        "capacityInUnits": 12,
        "capacityInVolume": 12,
        "capacityInWeight": 12,
        "chasisNumber": null,
        "engineNumber": null,
        "markerName": null,
        "batteryPercentage": null,
        "registrationNumber": null,
        "mediaList": null,
        "pucValidity": null,
        "insuranceValidity": null,
        "vehiclePermit": null,
        "ownerName": null,
        "rentEndDate": null,
        "rentStartDate": null,
        "transporter": null,
        "financer": null,
        "status": "Available",
        "permit": null,
        "ownership": null,
        "lat": null,
        "lng": null,
        "accidentHistory": null,
        "lastTrackingDate": null,
        "vendorName": null,
        "deviceId": {
          "barcode": "Not Assigned",
          "statusCd": null,
          "trackeeId": null
        },

        "tripDetail": null,
        "insuranceAlertWindow": null,
        "pucAlertWindow": null,
        "lastInsuranceAlertSentDt": null,
        "lastPUCAlertSentDt": null,
        "gpsStatus": null,
        "speed": null,
        "branchName": null,
        "referenceId": "538649a7b9fc45be8d75b5932cc8ab60"
      }
    ]
  },
  "hasError": false
}

```

This API is used to list all existing vehicles in the system. All vehicle related data values will be returned.

#### Request

<span class="get">GET</span>`https://api.loginextsolutions.com/VehicleApp/haul/v1`


### Update

You can update the data for any of the vehicle mapped to your account by using this API.
You will have to pass the reference Id of the vehicle whose information needs to be updated.This reference Id is supplied to you as a response when the vehicle is created.

Note that you will be able to update the information of only those vehicles which are available. If the status of the vehicle is “In Transit”, then that vehicle cannot be updated and in this case you will get error message - 400 - Bad Request

> Definition

```json
https://api.loginextsolutions.com/VehicleApp/haul/v1
```

> Request Body

```json
[
  {
    "referenceId":"a9be39b9347911e6829f000d3aa04450",        
        "vehicleNumber":"MH-111",
        "vehicleMake":"2015",
          "vehicleModel":"Chevy",
        "typeOfBody":"Flat Bed",
        "unladdenWeight":1099,
        "capacityInWeight":1099,
        "capacityInUnits":1099,
        "capacityInVolume":1099,
        "chasisNumber":"CHASIS-123",
        "engineNumber":"A-12353-D1234",
        "markerName":"Marker-1",
        "registrationNumber":"",
        "pucValidity":"2016-07-01T11:18:00.000Z",
        "insuranceValidity":"2016-07-01T11:18:00.000Z",
        "vehiclePermit":"New York, NY",
        "ownership":"company",
        "ownerName":"Mathew Richardson",
        "transporter":"",
        "financer":"",
        "accidentHistory":"",
        "rentStartDate":null,
        "rentEndDate":null,
        "deviceId":{
            "barcode":""
        }
    }
]
```

> Response

```json
{
  "status": 200,
  "message": "success",
  "data": null,
  "hasError": false
}

```
This API is used to update a particular vehicle based on its reference ID.

#### Request

<span class="post">PUT</span>`https://api.loginextsolutions.com/VehicleApp/haul/v1`


#### Request Parameters

Parameter | DataType |  Length | Required | Description
-----------|-------|------- | ----------|------------
vehicleNumber | String | 255 | Mandatory | Unique name to identify the vehicle
vehicleMake | String | 255 |Optional | Make of the vehicle like Mazda, Volvo, etc.
vehicleModel | String | 40 | Optional | Model of the vehicle as specified by manufacturer like FH series, MethaneDiesel, etc.
typeOfBody | String | 40 | Optional | Body Type of the vehicle. This is static field and can have only one of the below values - 4 wheeler, 2 wheeler, 24FT, 20FT, 32FT, 19FT, TATA 407, 14 FT CANTER, 17FT, TRLR, TRUCK
unladdenWeight | Integer | 10 | Optional | Unladen weight of the vehicle in Kg.
capacityInWeight | Integer | 10 | Optional | Capacity of vehicle in Kg.
capacityInUnits | Integer | 10 | Optional | Capacity of the vehicle in Units
capacityInVolume | Integer | 10 | Optional | Capacity of the vehicle on cubic centimeters
chasisNumber | String | 255 | Optional | Chassis / VIN number of the vehicle
engineNumber | String | 255 | Optional | Engine Number of the vehicle
markerName | String | 255 | Optional | Name of the Sub-ordinate who is driving along with the driver
registrationNumber | String | 255 | Optional | Registered Number provided by the local transportation authority
pucValidity | Date | | Optional | Date till which PUC certificate is valid.Format - YYYY-MM-DDTHH:MM:SS.SSSZ e.g. : 2016-07-01T11:18:00.000Z. This date always needs to be later than the current date.
insuranceValidity | Date | | Optional | Date till which insurance of the vehicle is valid. Format - YYYY-MM-DDTHH:MM:SS.000Z e.g. : 2016-07-01T11:18:00.SSSZ.This date always needs to be later than the current date.
vehiclePermit | String | 40 | Optional | Full name of the states of India in which the vehicle is permitted to travel
ownership | String | 50 | Optional | Entity that owns the vehicle. This field can have only below two values - Company , Vendor
ownerName | String | 255 | Optional | Name of the Company / Vendor who owns the vehicle
transporter | String | 40 | Optional | Name of the transporter / carrier / 3PL provider responsible for the delivery.
financer | String | 40 | Optional | If the vehicle is on loan, then name of the financer
accidentHistory | String | 160 | Optional | If vehicle has any accident records against it, then please document the details through this field
rentStartDate | Date | | Optional | This input is valid only if the vehicle’s owner is a vendor. Format - YYYY-MM-DDTHH:MM:SS.000Z e.g. : 2016-07-01T11:18:00.SSSZ. Rent start Date should be earlier than the Rent End Date.
rentEndDate  | Date | | Optional | This input is valid only if the vehicle’s owner is a vendor. Format - YYYY-MM-DDTHH:MM:SS.000Z e.g. : 2016-07-01T11:18:00.SSSZ. Rent End Date should be later than the Rent Start Date.
deviceId.barcode | String |  50 | Optional | This input should be the barcode of the tracker in order to map the Vehicle with the tracker.In order to get the list of tracker that you can attach to a vehicle, you will need to either access the Loginext portal with your login or contact our CSA and get the list. On LogiNext portal, you can access the tracker list - LogiNext → Resource → Tracker.


### Delete

Using this API, you can delete any of the vehicles listed against your account name.
You will have to pass the reference Id of the vehicle whose information needs to be updated.This reference Id is supplied to you as a response when the vehicle is created.

You can delete multiple vehicles, by passing multiple reference IDs in the Request body.

Note that you will be able to delete only which are available. If the status of the vehicle is “In Transit”, then that vehicle cannot be deleted. You will get error message - 400- Bad Request

Also, note that if a tracker is mapped to the vehicles that is deleted, then that tracker will be unmapped from that vehicle.

> Definition

```json
https://api.loginextsolutions.com/VehicleApp/haul/v1
```

> Request Body

```json
["a9be39b9347911e6829f000d3aa04450"]
```

> Response

```json
{
  "status": 200,
  "message": "success",
  "data": null,
  "hasError": false
}

```

This API is used to delete a particular vehicle based on its reference ID.

#### Request

<span class="post">DELETE</span>`https://api.loginextsolutions.com/VehicleApp/haul/v1`



#### Request Body

Parameter | DataType |  Required | Description
-----------|-------|------- | ----------
reference_ids | List | Mandatory | Reference Id associated with the vehicle.

## Driver

### Create
> Definition

```json
https://api.loginextsolutions.com/DriverApp/haul/v1/driver/create
```

> Request Body

```json
[
    {

        "driverName":"Test_Driver",
        "phoneNumber":1234565632,
        "emailId":"test@testing.com",
        "dateOfBirth":"2016-06-13",
        "languageList":[{"name":"English"},{"name":"Spanish"}],
        "salary":"10000",
        "maritalStatus":"married",
        "gender":"male",
        "experience":10,

        "licenseValidity":"2020-06-13",
        "licenseNumber":"LIC_104",
        "licenseType":"4 wheeler",
        "licenseIssueBy":"DMV",

        "addressList":[ {
                                "apartment":"10 Suite No. A1901",
                                "streetName": "Walton Avenue",
                                "landmark":"Opp. Chiptole",
                                "countryShortCode":"USA",
                                "stateShortCode":"IL",
                                "city":"Chicago",
                                "pincode":72712,
                                "isCurrentAddress":true
                        },
                        {
                                "apartment":"A-902",
                                "streetName": "50 E 78th St",
                                "landmark":"Opp. Strand Bookstore",
                                "countryShortCode":"USA",
                                "stateShortCode":"NY",
                                "city":"New York",
                                "pincode":10075,
                                "isCurrentAddress":false
                        }],


        "driverEmployeeId":"D23",
        "shiftList":[{
                            "shiftStartTime"  :"07:03pm",
                            "shiftEndTime":"07:10am",
                            "startTime":"2016-06-13",
                            "endTime":"2016-06-15"

        }],

        "previousCompanyName":"ABC",
        "reportingManager":"Chris",
        "managerPhoneNumber":1234567890,
        "managerEmailId":"chris@gologistic.com"
    }    
]
```

>  Response

```json
{
  "status": 201,
  "message": "success",
  "data": [
    "122e948ce6cc40fb85492c4c5a600816"
  ],
  "hasError": false
}

```

Create a new driver by passing form data through json.

The acknowledgement will provide the driver reference ID.

#### Request

<span class="post">POST</span> `https://api.loginextsolutions.com/DriverApp/haul/v1/driver/create`



#### Request Parameters

Parameter | DataType | Length | Required | Description
-----------|-------|-------|------|----------
driverName | String | 255 | Mandatory |  Driver's full name
phoneNumber | String | 255 | Mandatory | Phone No
emailId | String | 100 | Optional | EmailId
dateOfBirth | String | | Optional | Date of Birth. Format - YYYY-MM-DD e.g. : 2016-07-01
languageList | List of Objects | | Optional | Language(s) known to the driver
languageList.name | String | 40 | Optional | Name of language
salary | String | 18 | Optional | Current salary of Driver
maritalStatus | String | 20 | Optional | Marital Status. Ex: married, unmarried.
gender | String | 12 | Optional | Gender. Ex - male,female.
experience | Integer | 3 | Optional | No of yrs. of driving experience
licenseValidity | String | | Optional | License validity date. Format - YYYY-MM-DD e.g. : 2016-07-01
licenseNumber | String | 255 | Mandatory | License No
licenseType | String | 40 | Optional | License Type. Ex: 2 wheeler, 4 wheeler
licenseIssueBy | String | 40 | Optional | License Issuing Authority Name
addressList.apartment | String | 512 | Mandatory | Apartment name/no
addressList.streetName | String | 512 | Mandatory | Society/Street name
addressList.landmark | String | 512 | Mandatory | Landmark
addressList.areaName | String | 255 | Optional | Locality/Area name
addressList.countryShortCode | String | 3 | Mandatory | Country code.Please refer to the list of country codes provided in the "Country Codes" section.
addressList.stateShortCode | String | 3 |  Mandatory | State short code.Please refer to the list of state codes provided in the "State Codes" section.
addressList.city | String | 512 | Mandatory | City
addressList.pincode | Integer | 12 | Mandatory | Pincode
addressList.isCurrentAddress | Boolean | | Mandatory | Indicates whether this is current address of driver or not. Ex: true - Current Address, false - Permanent Address
driverEmployeeId | String | 50 | Optional | EmployeeId
shiftList.startTime | String | | Mandatory | Shift start date. Format - HH:MMaa e.g. : 07:00pm
shiftList.endTime | String | | Mandatory | Shift end date. Format - HH:MMaa e.g. : 17:00pm
shiftList.shiftStartTime | String |  | Mandatory | Shift start time. Format - YYYY-MM-DD e.g. : 2016-07-01
shiftList.shiftEndTime | String |  | Mandatory | Shift end time. Format - YYYY-MM-DD e.g. : 2016-07-01
previousCompanyName | String | 255 | Optional | Driver's last company name
reportingManager | String | 40 | Optional | Driver's last company's reporting manager's name
managerPhoneNumber | String | 255 | Optional | Driver's last company'smanager's phone no
managerEmailId | String | 100 | Optional | Driver's last company's manager's email id






### Get

> Definition

```json
https://api.loginextsolutions.com/DriverApp/haul/v1/driver/list
```

> Request Body

```json
["1c3a551f47534b98a29d916b0405fd6d"]
```

> Response

```json
{
  "status": 200,
  "message": "success",
  "data": [
    {

      "driverName": "Test_Driver",
      "phoneNumber": "1234565632",
      "emailId": "test@testing.com",
      "licenseNumber": "LIC_104",
      "licenseValidity": 1591986600000,
      "license": null,
      "salary": 10000,
      "capacity": null,
      "addressLine1": null,
      "addressLine2": null,
      "city": null,
      "state": null,
      "pinCode": null,
      "licenseType": "4 wheeler",
      "defaultVehicle": null,
      "vehicleNumber": null,
      "licenseAlertWindow": null,
      "attendance": null,
      "workHour": null,
      "status": null,
      "dateOfBirth": 1465776000000,
      "experience": "11",
      "maritalStatus": "married",
      "gender": "female",
      "languageList": [
        {
          "name": "English",
        },
        {
          "name": "Hindi",
        }

      ],
      "licenseIssueBy": "Maharashtra Govt.",
      "tripName": null,
      "previousCompanyName": "ABC",
      "driverEmployeeId": "D23",
      "reportingManager": "Rahul",
      "managerPhoneNumber": "1234567890",
      "managerEmailId": "test@test.com",
      "deviceId": null,
      "trackingDate": null,
      "deviceBarcode": null,
      "shiftList": [
        {
          "shiftStartTime": "2017-09-12T14:00:00Z",
          "shiftEndTime": "2017-09-12T15:00:00Z",
          "startTime": null,
          "endTime": null
        }
      ],
      "addressList": [],
      "lat": null,
      "lng": null,
      "isPresent": null,
      "tripStatus": null,
      "batteryPerc": null,
      "lastLicenseAlertSentDt": null,
      "clientBranchName": null,
      "previousPhoneNumber": null,
      "referenceId": "1c3a551f47534b98a29d916b0405fd6d"
    }
  ],
  "hasError": false
}

```

Use this API to read all data for a particular driver using its reference ID.

#### Request

<span class="post">POST</span>` https://api.loginextsolutions.com/DriverApp/haul/v1/driver/list`

#### Request Body

Parameter | DataType |  Required | Description
-----------|-------|------- | ----------
reference_ids | List | Mandatory | Reference Id associated with the driver.


### Update

> Definition

```json
https://api.loginextsolutions.com/DriverApp/haul/v1/driver/update
```

> Request Body

```json
[
{
        "referenceId":"1c3a551f47534b98a29d916b0405fd6d",
        "driverName":"Test_Driver",
        "phoneNumber":"1234565632",
        "emailId":"test@testing.com",
        "dateOfBirth":"2016-06-13",
        "languageList":[{"name":"English"},{"name":"Hindi"}],
        "salary":"10000",
        "maritalStatus":"married",
        "gender":"female",
        "experience":11,

        "licenseValidity":"2020-06-13",
        "licenseNumber":"LIC_104",
        "licenseType":"4 wheeler",
        "licenseIssueBy":"Maharashtra Govt.",

        "addressList":[ {
                                "apartment":"A-901",
                                "streetName": "Hiranandani Street",
                                "landmark":"DMart",
                                "countryShortCode":"IND",
                                "stateShortCode":"MH",
                                "city":"Mumbai",
                                "pincode":400076,
                                "isCurrentAddress":true
                        },
                        {
                                "apartment":"A-902",
                                "streetName": "LBS Marg",
                                "landmark":"SBI",
                                "countryShortCode":"IND",
                                "stateShortCode":"MH",
                                "city":"Mumbai",
                                "pincode":400092,
                                "isCurrentAddress":false
                        }],


        "driverEmployeeId":"D23",
        "shiftList":[{
                            "shiftStartTime"  :"07:03pm",
                            "shiftEndTime":"07:10am",
                            "startTime":"2016-06-13",
                            "endTime":"2016-06-15"

        }],

        "previousCompanyName":"ABC",
        "reportingManager":"Rahul",
        "managerPhoneNumber":"1234567890",
        "managerEmailId":"test@test.com"
    }  
  ]  
```

> Response

```json
{
  "status": 200,
  "message": "success",
  "data": null,
  "hasError": false
}

```

This API is used to update a particular driver based on its reference ID.

#### Request

<span class="post">PUT</span>`https://api.loginextsolutions.com/DriverApp/haul/v1/driver/update`



#### Request Parameters

Parameter | DataType | Length | Required | Description
-----------|-------|-------|------|----------
referenceId | String | 32 | Mandatory |  ReferenceId of the record
driverName | String | 255 | Mandatory |  Driver's full name
phoneNumber | String | 255 | Mandatory | Phone No
emailId | String | 100 | Optional | EmailId
dateOfBirth | String | | Optional | Date of Birth. Format - YYYY-MM-DD e.g. : 2016-07-01
languageList | List of Objects | | Optional | Language(s) known to the driver
languageList.name | String | 40 | Optional | Name of language
salary | String | 18 | Optional | Current salary of Driver
maritalStatus | String | 20 | Optional | Marital Status. Ex: married, unmarried.
gender | String | 12 | Optional | Gender. Ex - male,female.
experience | Integer | 3 | Optional | No of yrs. of driving experience
licenseValidity | String | | Optional | License validity date. Format - YYYY-MM-DD e.g. : 2016-07-01
licenseNumber | String | 255 | Mandatory | License No
licenseType | String | 40 | Optional | License Type. Ex: 2 wheeler, 4 wheeler
licenseIssueBy | String | 40 | Optional | License Issuing Authority Name
addressList.apartment | String | 512 | Mandatory | Apartment name/no
addressList.streetName | String | 512 | Mandatory | Society/Street name
addressList.landmark | String | 512 | Mandatory | Landmark
addressList.areaName | String | 255 | Optional | Locality/Area name
addressList.countryShortCode | String | 3 | Mandatory | Country code.Please refer to the list of country codes provided in the "Country Codes" section.
addressList.stateShortCode | String | 3 |  Mandatory | State short code.Please refer to the list of state codes provided in the "State Codes" section.
addressList.city | String | 512 | Mandatory | City
addressList.pincode | Integer | 12 | Mandatory | Pincode
addressList.isCurrentAddress | Boolean | | Mandatory | Indicates whether this is current address of driver or not. Ex: true - Current Address, false - Permanent Address
driverEmployeeId | String | 50 | Optional | EmployeeId
shiftList.startTime | String | | Mandatory | Shift start date. Format - HH:MMaa e.g. : 07:00pm
shiftList.endTime | String | | Mandatory | Shift end date. Format - HH:MMaa e.g. : 17:00pm
shiftList.shiftStartTime | String |  | Mandatory | Shift start time. Format - YYYY-MM-DD e.g. : 2016-07-01
shiftList.shiftEndTime | String |  | Mandatory | Shift end time. Format - YYYY-MM-DD e.g. : 2016-07-01
previousCompanyName | String | 255 | Optional | Driver's last company name
reportingManager | String | 40 | Optional | Driver's last company's reporting manager's name
managerPhoneNumber | String | 255 | Optional | Driver's last company'smanager's phone no
managerEmailId | String | 100 | Optional | Driver's last company's manager's email id

### Delete

> Definition

```json
https://api.loginextsolutions.com/DriverApp/haul/v1/driver/delete
```

> Request Body

```json
["e0eaebdd84ac4c40af72d827ab610090"]
```

> Response

```json
{
  "status": 200,
  "message": "success",
  "data": null,
  "hasError": false
}

```

This API is used to delete a particular driver based on its reference ID.

#### Request

<span class="post">DELETE</span>`https://api.loginextsolutions.com/DriverApp/haul/v1/driver/delete`

#### Request Body

Parameter | DataType |  Required | Description
-----------|-------|------- | ----------
reference_ids | List | Mandatory | Reference Id associated with the driver.

## Trip

### Create

> Definition

```json
https://api.loginextsolutions.com/TripApp/haul/v1/trip/create
```

> Request Body

```json
{
  "shipmentType": "Bag",
  "sealNumber":"SN-123",
  "lrNumber":"LR123",
  "originAddr": "CNND",
  "awbNumber": "FG-123-GH",
  "destinationAddr": "NAGD",
  "name": "CNN-NAG-12221",
  "packageWeight": 6,
  "packageValue": 8,
  "packageVolume": 10,
  "vehicleReportingDate": "2016-02-27T18:30:00.000Z",
  "modeOfTransport": "ROAD",
  "vehicleNumber": "MH40AK0175",
  "barcode": "LN00590915",
  "routeConfigurationName":"route53",
  "note":"This vehicle is carrying fragile goods",
  "goodTypeName":"Benzene",
  "startNow":false
}
```

> Response

```json
{
  "status": 200,
  "message": "Trip created successfully.Reference Id for future access:1880d6906e9d426995b815a83aa3927f",
  "data": null,
  "hasError": false
}

```

Create a new trip using this API. Form data is passed through json.

The acknowledgement will contain the trip reference ID.

#### Request

<span class="post">POST</span>`https://api.loginextsolutions.com/TripApp/haul/v1/trip/create`



#### Request Parameters

Parameter | DataType |  Length | Required | Description
-----------|-------|-------|---------|----------
shipmentType | String | 45 | Mandatory | Type of the Shipment being created.Examples:"Bag","Package","Manifest"
originAddr | String | 1000 |  Mandatory | Origin point of the trip.Examples:-AMDD,BLRX
destinationAddr | String | 1000 | Mandatory | Destination point of the trip.Examples:-CNND,BOMX
awbNumber | String | 255 | Optional | AWB Number of the Order.
name | String | 255 | Mandatory | Name of the trip.Has to be unique.Example:-CNND-BOMX-123_456
packageWeight | Integer | 10 | Optional | Capacity of the shipment in terms of Kgs
packageValue | Integer | 10 | Optional | Capacity of the shipment in terms of the number of units present in it
packageVolume | Integer | 10 | Optional | Capacity of the shipment in terms of cc
vehicleReportingDate | Date | | Mandatory | Reporting date of the vehicle at the origin hub. Format - YYYY-MM-DDTHH:MM:SS.000Z e.g. : 2016-07-01T11:18:00.SSSZ.
modeOfTransport | String | 12 | Mandatory | Mode of transit for the trip.Examples:-ROAD,AIR,RAIL
lrNumber | String | 255 | Mandatory(Conditional) | Lorry Receipt Number if modeOfTransport selected as ROAD.
flightNum| String | 30 | Mandatory(Conditional) | Flight Number if modeOfTransport selected as AIR.
trainNum| String | 30 | Mandatory(Conditional) | Rail Number if modeOfTransport selected as RAIL.
driverName | String | 255 | Optional | Name of the driver
vehicleNumber | String | 30 | Optional | Vehicle Number.
barcode | String | 50 | Mandatory | Barcode of the tracker used for attaching to vehicle during trip
routeConfigurationName | String | 50 | Optional | Name of the Route.
goodTypeName | String | 50 | Optional | This field can hold the types of goods being transported in the trip.
note| String | 50 | Optional | Notes to be added to the trip.
startNow | Boolean | 50 | Optional | This flag will automatically start the trip upon creation if set to true. If false a trip will be created but not started.


### Get

> Definition

```json
https://api.loginextsolutions.com/TripApp/haul/v1/trip/get
```

> Request Body

```json
[
 "842b0dd8422211e6860c0653055f4dfd", "sfygv54g",
 "Mum-DEL", "842fc7eb422211e6860c0653055f4dfd"
]
```

> Response

```json
{
  "status": 200,
  "message": "Trip Details fetched successfully",
  "referenceId": null,
  "data": [
    {
      "referenceId": "842b0dd8422211e6860c0653055f4dfd",
      "tripName": "Mum-AMD",
      "origin": "Mumbai",
      "destination": "AMDD",
      "tripStatus": "ENDED",
      "tripStartDt": null,
      "tripEndDt": null,
      "eta": "2016-03-25 03:50:00",
      "calculatedStartDt": null,
      "calculatedEndDt": null,
      "actualDistance": null,
      "packageWeight": 0,
      "packageVolume": 0,
      "packageValue": 0,
      "goodType": null,
      "phoneNumber": "9284819294",
      "isStuckFl": null,
      "lastStuckDt": null,
      "notesDescription": null,
      "barcode": "LN00840216",
      "lrNumber": "LR001",
      "awbNumber": null,
      "sealNumber": null,
      "challanNumber": null,
      "flightNum": null,
      "trainNum": null,
      "vehicle": "MH04-PT-2987",
      "vehicleType": null,
      "driver": "Madhav",
      "vehicleReportingTime": "2016-03-24 13:30:00",
      "tracking": "2016-03-28 12:18:29",
      "lastHub": null,
      "lastTrackedLatitude": 19.1118,
      "lastTrackedLongitude": 72.909683,
      "batteryPerc": 40,
      "speed": 54
    },
    {
      "referenceId": "842c59b0422211e6860c0653055f4dfd",
      "tripName": "Ahm-BLR",
      "origin": "Ahmedabad",
      "destination": "BLRH",
      "tripStatus": "ENDED",
      "tripStartDt": null,
      "tripEndDt": null,
      "eta": "2016-03-28 22:37:00",
      "calculatedStartDt": null,
      "calculatedEndDt": null,
      "actualDistance": null,
      "packageWeight": 0,
      "packageVolume": 0,
      "packageValue": 0,
      "goodType": null,
      "phoneNumber": "9284819294",
      "isStuckFl": null,
      "lastStuckDt": null,
      "notesDescription": null,
      "barcode": "LN00840216",
      "lrNumber": "lr0201",
      "awbNumber": null,
      "sealNumber": null,
      "challanNumber": null,
      "flightNum": null,
      "trainNum": null,
      "vehicle": "MH04-PT-2987",
      "vehicleType": null,
      "driver": "Madhav",
      "vehicleReportingTime": "2016-03-27 19:30:00",
      "tracking": "2016-03-29 09:03:52",
      "lastHub": null,
      "lastTrackedLatitude": 19.1118,
      "lastTrackedLongitude": 72.909683,
      "batteryPerc": 40,
      "speed": 54
    },
    {
      "referenceId": "842ce089422211e6860c0653055f4dfd",
      "tripName": "Ban-BOM",
      "origin": "Bangalore",
      "destination": "BOMX",
      "tripStatus": "ENDED",
      "tripStartDt": null,
      "tripEndDt": null,
      "eta": "2016-03-29 11:36:00",
      "calculatedStartDt": null,
      "calculatedEndDt": null,
      "actualDistance": 1.4559,
      "packageWeight": 0,
      "packageVolume": 0,
      "packageValue": 0,
      "goodType": null,
      "phoneNumber": "9284819294",
      "isStuckFl": null,
      "lastStuckDt": null,
      "notesDescription": null,
      "barcode": "LN00840216",
      "lrNumber": "lr002",
      "awbNumber": null,
      "sealNumber": null,
      "challanNumber": null,
      "flightNum": null,
      "trainNum": null,
      "vehicle": "MH04-PT-2987",
      "vehicleType": null,
      "driver": "Madhav",
      "vehicleReportingTime": "2016-03-28 19:30:00",
      "tracking": "2016-04-04 07:34:38",
      "lastHub": null,
      "lastTrackedLatitude": 19.1118,
      "lastTrackedLongitude": 72.909683,
      "batteryPerc": 40,
      "speed": 54
    }
  ],
  "error": {
    "1": "sfygv54g",
    "2": "842b0c25422211e6860c0653055f4dfd",
    "5": "842d9d2d422211e6860c0653055f4dfd"
  },
  "hasError": true
}

```

With this API you can fetch the list of your trips and its associated trip information.

#### Request

<span class="post">POST</span>`https://api.loginextsolutions.com/TripApp/haul/v1/trip/get`



#### Request Parameters

Parameter | DataType |  Required | Description
-----------|-------|------- | ----------
reference_ids<br>OR<br>trip names | List | Mandatory | Either the list of Reference Ids or the list of Trip Names is required to fetch list of trip information

### Update

```json
https://api.loginextsolutions.com/TripApp/haul/v1/trip/update
```

> Request Body

```json
{
"referenceId":"9620737172e44effacc834e2a2f56508",
"vehicleNumber": "GJ12Z3735",
"barcode":"GJ12Z3735",
"sealNumber":"SN-123",
  "lrNumber":"LR123",
  "originAddr": "Ahmendabad",
  "awbNumber": "FG-123-GH",
  "destinationAddr": "ATQD",
  "name": "CNN-NAG-12221",
  "packageWeight": 6,
  "packageValue": 8,
  "packageVolume": 10,
  "modeOfTransport": "ROAD",
  "notes": "CNN-NAG-12221",
  "driverName":"Ramesh"
  }
```

> Response

```json
{
    "status": 200,
    "message": "Trip(s) updated successfully.. Reference Id for future access: 9620737172e44effacc834e2a2f56508",
    "hasError": false
}

```

This API is used to cancel a trip using its reference ID.

#### Request

<span class="post">POST</span>`https://api.loginextsolutions.com/TripApp/haul/v1/trip/update`

#### Request Body

Parameter | DataType |  Required | Description
-----------|-------|------- | ----------
referenceIds | List | Mandatory | Reference Ids associated with trips
vehicleNumber | String | Optional | Vehicle Number associated with the Trip
barcode | String | Optional | Tracker Barcode asociated with the trip.
seal NUmber | String | Optional | Seal Number asociated with the trip.
lrNumber | String | Optional | LR Number asociated with the trip.
originAddr | String | Optional | Origin of the trip. THis should be one of the origins preconfigured in your account.
destinationAddr | String | Optional | Destination of the trip. THis should be one of the destinations preconfigured in your account.
name | String | Optional | Name of the trip.
awbNumber | String | Optional | AWB number of the order associated with that trip.
packageWeight | String | Optional | Package Weight.
packageValue | String | Optional | Package Value.
notes | String | Optional | Notes to be added in the trip.
driverName | String | Optional | Driver Name.

### Cancel

> Definition

```json
https://api.loginextsolutions.com/TripApp/haul/v1/trip/cancel
```

> Request Body

```json
[{
    "referenceId":"9620737172e44effacc834e2a2f56508",
    "reasonCd":"Truck is not available",
    "otherReason":"",
    "updateTime":"2016-07-18T10:31:00.000Z"
  }]
```

> Response

```json
{
  "status": 200,
  "message": "Trips cancelled successfully",
  "hasError": false
}

```

This API is used to cancel a trip using its reference ID.

#### Request

<span class="post">POST</span>`https://api.loginextsolutions.com/TripApp/haul/v1/trip/cancel`

#### Request Body

Parameter | DataType |  Required | Description
-----------|-------|------- | ----------
referenceIds | List | Mandatory | Reference Ids associated with trips
reasonCd | String | Mandatory | Reason for cancelleation of the trip. This should be one of the reasons configured for your client account
otherReason | String | Optional| This will be the reason in case the Reson code selected is other.
updateTime | String | Optional | This is the time of the cancel trip event.



### Start

> Definition

```json
https://api.loginextsolutions.com/TripApp/haul/v1/trip/start
```

> Request Body

```json
[
  "ca7fbf96a133461aadce8f94678084ee",
  "82b9ec9025b4454c9bcb86c704f49ce3",
  "980053a9ee4a48876b6d3d18412d03a0c"
]
```

> Response

```json
{
  "status": 200,
  "message": "Trips started successfully",
  "hasError": false
}

```

This API is used to start a trip using its reference ID.

#### Request

<span class="post">PUT</span>`https://api.loginextsolutions.com/TripApp/haul/v1/trip/start`

#### Request Body

Parameter | DataType |  Required | Description
-----------|-------|------- | ----------
referenceIds | List | Mandatory | Reference Ids associated with trips

### Stop


```json
https://api.loginextsolutions.com/TripApp/haul/v1/trip/stop
```

> Request Body

```json
[
  "ca7fbf96a133461aadce8f94678084ee",
  "82b9ec9025b4454c9bcb86c704f49ce3",
  "980053a9ee4a48876b6d3d18412d03a0c"
]

```

> Response

```json
{
  "status": 200,
  "message": "Trips ended successfully",
  "hasError": false
}

```

This API is used to end an in-transit trip using its reference ID.

#### Request

<span class="post">POST</span>`https://api.loginextsolutions.com/TripApp/haul/v1/trip/stop`

#### Request Body

Parameter | DataType |  Required | Description
-----------|-------|------- | ----------
referenceIds | List | Mandatory | Reference Ids associated with trips


##Tracking

### Get iFrame

> Definition

```json
https://api.loginextsolutions.com/track/#/order?tripname=Trip-123&aid=4b41a94b-521b-4986-920d-6e4c1cf15fd0b6&key=$2a$08$dfVg6jJLhrHEsqOUfD1EJHyuelHeIgcUyvgTfGaeRmnzN5jGVi86k
```

The iFrame displays the last tracking for a trip, including current location and trip history, based on the trip name.

#### Request


<span class="post">GET</span>` https://api.loginextsolutions.com/track/#/order?tripname=<tripname>&aid=<aid>&key=<key>`

#### Request Parameters

Parameter | Sample Value | Description
--------- | ------- | -------------
aid | f522631c-490c-46fd-9f79-ca8d14a704d7 | Value of authentication token without 'BASIC' keyword
key | $2a$08$Vg6jJLhrHEsqOUfD1EJHyuelHeIgcUyvgT | Client Secret Key
tripname | TestTripName| Trip name


### Create Tracking Record

> Create Tracking Record - Sample Request

```json
{
  "trackerId": "4568088900",
  "latitude": 12.9003884,
  "longitude": 14.9889999,
  "time": "2016-07-14T09:11:56Z",
  "batteryPerc": 70.5,
  "speed": 40.4,
  "messageType": "REG",
  "temperature": 30.5
}
```

This endpoint adds tracking record.

#### Request

<span class="post">POST</span>`https://api.loginextsolutions.com/TrackingApp/track/put`


#### Request Parameters

Param | DataType |  Length | Required | Description
--------- | ------- | -----|---------- | ------------
trackerId | String | 12 | Mandatory |  Device's unique ID
latitude | Double | 13,10 | Mandatory | Latitude
longitude | Double | 13,10 | Mandatory | Longitude
time | Date |  | Mandatory | Tracking time in UTC. Format - YYYY-MM-DDTHH:MM:SS.SSSZ e.g. : 2016-07-01T11:18:00.000Z.
batteryPerc | Double | 5,2 | Mandatory | Battery Percentage of device
speed | Double | 5,2 | Optional | Speed with which consignment is moving
messageType | String | 10 | Mandatory | Message type. Ex: REG
temperature | Double | 5,2 | Optional | Consignment's temperature


### Create Tracking Record (Bulk)

> Create Tracking Record - Sample Request

```json
[
  {
  "trackerId": "358899056518932",
  "latitude": 12.9003884,
  "longitude": 14.9889999,
  "time": "2018-01-04T07:21:56Z",
  "batteryPerc": 70.5,
  "speed": 40.4,
  "messageType": "REG",
  "temperature": 30.5
  }, {
  "trackerId": "4209917397",
  "latitude": 12.9003884,
  "longitude": 14.9889999,
  "time": "2018-01-04T07:21:56Z",
  "batteryPerc": 70.5,
  "speed": 40.4,
  "messageType": "REG",
  "temperature": 30.5
  }
]
```

This API allows you to add upto 20 tracking points in a single call of the API. For example - If you are receiving tracking data from multiple trackers simultaneously, you can batch them up and send them in one call to LogiNext in a single call of this API.

This API has a rate limit of 1 req/sec.

#### Request

<span class="post">POST</span>`https://api.loginextsolutions.com/TrackingApp/haul/v1/tracking/put`


#### Request Parameters

Param | DataType |  Length | Required | Description
--------- | ------- | -----|---------- | ------------
trackerId | String | 12 | Mandatory |  Device's unique ID
latitude | Double | 13,10 | Mandatory | Latitude
longitude | Double | 13,10 | Mandatory | Longitude
time | Date |  | Mandatory | Tracking time in UTC. Format - YYYY-MM-DDTHH:MM:SS.SSSZ e.g. : 2016-07-01T11:18:00.000Z.
batteryPerc | Double | 5,2 | Mandatory | Battery Percentage of device
speed | Double | 5,2 | Optional | Speed with which consignment is moving
messageType | String | 10 | Mandatory | Message type. Ex: REG
temperature | Double | 5,2 | Optional | Consignment's temperature


### Get Tracker (List)

> Definition

```json
https://api.loginextsolutions.com/DeviceApp/device/v1/haul
```

> Response


```json
{
  "status": 200,
  "message": null,
  "referenceId": null,
  "data": [
    {
      "clientName": null,
      "deviceId": 1255,
      "productId": null,
      "supplierId": null,
      "barcode": "LN02510915",
      "suppliedDt": null,
      "standardPriceAmt": null,
      "discountPct": null,
      "createdByUserId": null,
      "createdOnDt": null,
      "supplierName": null,
      "phoneNumber": null,
      "simId": null,
      "lookupDesc": null,
      "supplierDesc": null,
      "updatedByUserId": null,
      "updatedOnDt": null,
      "isAvailableFl": "\u0000",
      "batteryPerc": 100,
      "status": "Intransit",
      "lastTrackedDt": 1469510397000,
      "lastTrackedDate":2016-07-26'T'05:19:57,
      "lastTrackLocation": null,
      "clientBranchId": null,
      "deviceType": null,
      "deviceTypeId": null,
      "speed": 67.78,
      "extraField1": "13141",
      "extraField2": null,
      "extraField3": null,
      "extraField4": null,
      "extraField5": null,
      "isActiveFl": "Y",
      "isActive": true,
      "lat": 16.646592,
      "lng": 74.275329,
      "simNumber": null,
      "serviceProvider": null,
      "serviceProviderId": null,
      "planType": null,
      "planTypeId": null,
      "cost": null,
      "gpsStatus": "Offline",
      "clientBranchName": "Mahindra Logistics Ltd",
      "temperature": null,
      "odometer": null,
      "direction": null,
      "fuel": null,
      "ignition": null,
      "vehicleNum": "MH12LT2092",
      "tripName": "ATQD-BOMZ-test",
      "originAddr": null,
      "destinationAddr": null,
      "driverName": null,
      "vehicleName": null,
      "imei": null
    },
    {
      "clientName": null,
      "deviceId": 1128,
      "productId": null,
      "supplierId": null,
      "barcode": "LN01240915",
      "suppliedDt": null,
      "standardPriceAmt": null,
      "discountPct": null,
      "createdByUserId": null,
      "createdOnDt": null,
      "supplierName": null,
      "phoneNumber": null,
      "simId": null,
      "lookupDesc": null,
      "supplierDesc": null,
      "updatedByUserId": null,
      "updatedOnDt": null,
      "isAvailableFl": "\u0000",
      "batteryPerc": 100,
      "status": "Available",
      "lastTrackedDt": 1467372218000,
      "lastTrackedDate":2016-07-01'T'11:23:38,
      "lastTrackLocation": null,
      "clientBranchId": null,
      "deviceType": null,
      "deviceTypeId": null,
      "speed": 0,
      "extraField1": "13006",
      "extraField2": null,
      "extraField3": null,
      "extraField4": null,
      "extraField5": null,
      "isActiveFl": "Y",
      "isActive": true,
      "lat": 26.90774,
      "lng": 75.846686,
      "simNumber": null,
      "serviceProvider": null,
      "serviceProviderId": null,
      "planType": null,
      "planTypeId": null,
      "cost": null,
      "gpsStatus": "Offline",
      "clientBranchName": "Mahindra Logistics Ltd",
      "temperature": null,
      "odometer": null,
      "direction": null,
      "fuel": null,
      "ignition": null,
      "vehicleNum": null,
      "tripName": null,
      "originAddr": null,
      "destinationAddr": null,
      "driverName": null,
      "vehicleName": null,
      "imei": null
    },
    {
      "clientName": null,
      "deviceId": 2491,
      "productId": null,
      "supplierId": null,
      "barcode": "LN01470915",
      "suppliedDt": null,
      "standardPriceAmt": null,
      "discountPct": null,
      "createdByUserId": null,
      "createdOnDt": null,
      "supplierName": null,
      "phoneNumber": null,
      "simId": null,
      "lookupDesc": null,
      "supplierDesc": null,
      "updatedByUserId": null,
      "updatedOnDt": null,
      "isAvailableFl": "\u0000",
      "batteryPerc": 100,
      "status": "Available",
      "lastTrackedDt": 1469513910000,
      "lastTrackedDate":2016-07-26'T'06:18:30,
      "lastTrackLocation": null,
      "clientBranchId": null,
      "deviceType": null,
      "deviceTypeId": null,
      "speed": 53.12,
      "extraField1": "13030",
      "extraField2": null,
      "extraField3": null,
      "extraField4": null,
      "extraField5": null,
      "isActiveFl": "Y",
      "isActive": true,
      "lat": 13.964397,
      "lng": 77.679164,
      "simNumber": null,
      "serviceProvider": null,
      "serviceProviderId": null,
      "planType": null,
      "planTypeId": null,
      "cost": null,
      "gpsStatus": "Offline",
      "clientBranchName": "Mahindra Logistics Ltd",
      "temperature": null,
      "odometer": null,
      "direction": null,
      "fuel": null,
      "ignition": null,
      "vehicleNum": null,
      "tripName": null,
      "originAddr": null,
      "destinationAddr": null,
      "driverName": null,
      "vehicleName": null,
      "imei": null
    }
  ]
}
```

Tracker API fetches the details of all the trackers of the client.

#### Request

<span class="post">GET</span>`https://api.loginextsolutions.com/DeviceApp/device/v1/haul`

### Get Location

> Definition

```json
https://api.loginextsolutions.com/TrackingApp/haul/v1/track/lastlocation?address=true
```

> Request Body

```json
["112-EastZone-115-WestZone","123-NorthSector-132-EastHub"]
```

> Response

```json
{
  "status": 200,
  "message": "Latest Location found successfully",
  "data": [
    {
      "lat": 10.394535555555555,
      "lng": 77.96088,
      "eta": "2018-08-18 06:43:00",
      "revisedETA": "2018-08-17 16:26:01",
      "lastTrackedAt": "2018-08-17 16:26:01",
      "tripName": "ABCAL-NY",
      "speed": 0,
      "batteryPerc": 1,
      "trackerId": "6309682521",
      "vehicleNo": "MH 03 CP 1056",
      "baname": "Joes Transports"
    },
    {
      "lat": 23.484535,
      "lng": 79.460987,
      "eta": "2018-08-18 06:43:00",
      "tripName": "GL-MAS",
      "lastTrackedAt": "2018-07-20 05:56:02",
      "speed": 0,
      "batteryPerc": 1,
      "trackerId": "6309682521",
      "vehicleNo": "NC1F56",
      "baname": "PacknPick"
    }
  ],
  "hasError": false
}
```

This API fetches the latest location and the reverse geocoded address for a trip.

#### Request

<span class="post">POST</span>`https://api.loginextsolutions.com/TrackingApp/haul/v1/track/lastlocation?address=false`

#### Request Parameters

Parameter | DataType |  Required | Description
-----------|-------|------- | ----------
address | Boolean | Optional | To be passed as "true" if reverse geocoded address is needed,else "false"

#### Request Body

Parameter | DataType |  Required | Description
-----------|-------|------- | ----------
- | List of Strings | Mandatory | List of Trip names

#### Response Body

Parameter | DataType | Description
-----------|-------| ----------
lat | Double | Specifies the latitude of the last tracked location
lng | Double | Specifies the longitude of the last tracked location
eta | Date   | Estimated time of arrival at the destination
revisedETA | Date | Revised Estimated time of arrival at the destination after the trip has started of the vehicle has existed an Intransit geofence.
lastTrackedAt | Date | The last tracked date and time in UTC of the GPS device
address | String | The reverse geocoded address will be fetched if the "address" parameter is passed as true
tripName | String | Specifies the name of the trip of the last tracked location.
speed | Number | Speed of the vehicle at the last tracked location
batteryPerc | Number | Battery percentage.
trackerId | String | tracker ID of the tracker.
vehicleNo | String | Vehicle Number



# LogiNext Mile <sup>TM</sup>

Mile Product refers to the first mile and last mile shipment deliveries. Mile product will help you create -  

Pick-up orders thereby catering to your first leg of logistics, wherein shipments are ‘picked’ from your customer / merchants / suppliers / vendors and transported to the hub for aggregation.

Delivery orders by loading the items for different orders from a Single Point of Pick Up (Hub) and deliver the same to your customers (Multiple Drop Points).


1. Once the resources are created, then you can add shipments or orders in the LogiNext database by calling Create Order API. You need to provide the Order Number, Date and time window on which order should be picked-up / delivered and the pick-up / delivery address details. Additionally you can also specify the Crate level and line item level details contained in that order.The response consists of the Reference ID against each Order ID which needs to be stored in your system for future references.

2. Once the optimization for capacity and route planning is completed, trips will be created by the LogiNext system and you can mark the trip as started by calling the Start Trip API and mark the same trip as stopped by calling Stop Trip API. In both these API you will have to pass the trip reference ID.

3. Finally you can track your pick-up / delivery executive in transit through the Track Last Location API. In this case also you need to pass the Trip Reference Id.

4. You can also mark a particular order as cancelled by calling the Cancel Order API and passing the order reference ID.

5. In case, your account is being configured into the LogiNext system as a pick-up and delivery both, the you can also create the return shipment for the order thereby optimizing you reverse logistics and return planning.


## Customer 

### Create

> Sample Request

```json
[
  {
    "name":"James Wan",
    "mobile":"341245673212",
    "email":"james@ablogs.com",
    "customerType":"Preferred",
    "billingAddress": {
      "apartment":"Suite No. 1, Milsons Towers",
          "streetName":"Michigan Avenue",
          "landmark":"Opp. Subway",
          "locality":"Dowtown Chicago",
          "city":"Chicago 11",
          "state":"NY",
          "country":"USA",
          "pincode":"10045",
          "latitude": 72.9555,
          "longitude": 19.555
    }
  }
]
```

> Sample Response

```json
{
    "status": 200,
    "message": "Customer(s) created successfully",
    "data": [
        {
            "index": 0,
            "referenceId": "6a34c7274df0489f97c0f891514b488b",
            "accountCode": "apinew1"
        }
    ],
    "hasError": false
}

```

You can create a new Customer the LogiNext system with this API. A new Customer will be created and assigned a unique Reference ID that can be used to identify the Customer later.

If you have Customers created inyour current system that you would like to push to LogiNext, call this API with the parameters mentioned below to add these Customers in LogiNext.

This API will create a Customer Entity with contact information and an optional Billing Address for a Customer. To create a Shipping/ Delivery address for a Customer, call the Create Address API.

These are the customers you would create Orders for in LogiNext. The Customer ID you use to identify indivuduak customers can be used in the Create Order API to create an Order.

This API will only accept inputs if your Customer Profiling property is set in LogiNext. To know more about the Customer Profiling property, please reach out to us at support@loginextsolutions.com.

You can create a maximum of 5 Customers in LogiNExt in one call of this API.

#### Request

<span class="post">POST</span>`https://api.loginextsolutions.com/ClientApp/customer/v1/create`


#### Request Parameters

Parameter | DataType | Length |  Required | Description
-----------|-------|------- |------- | ----------
accountCode | String | 50 | Mandatory | Unique Customer ID used to identify a Customer.
name | String | 255 | Mandatory | Customer name.
mobile | String | 255 | Mandatory | Customer Mobile NUmber.
email | String | 255 |Optional | Customer Email ID.
customerType | String | 255 | Optional | This is the delivery associate's mobile number.
billingAddress.apartment | String | 40 |Optional | Customer's Billing Address apartment.
billingAddress.streetName | String | 100 | Optional | Customer's Billing Address Street Name.
billingAddress.landmark | String | 255 | Mandatory | Customer's Billing Address landmark.
billingAddress.locality | String | 255 | Mandatory | Customer Billing Address locality.
billingAddress.city | Integer | 20 | Mandatory | Customer Billing Address city.
billingAddress.state | Integer | 20 | Optional | Customer Billing Address state. This will be based on the state codes in LogiNext for the country selected by you.
billingAddress.country | String | 255 | Optional | Customer's Billing Address Country.
billingAddress.pincode | String | 255 | Optional | Customer's Billing Address Pincode.
billingAddress.latitude | Double | 20 | Optional | Customer's Billing Address geo-coordinate(latitude)
billingAddress.longitude | Double | 20 | Optional | Customer's Billing Address geo-coordinate(longitude)
clientCode | String | 50 | Optional | Sub Client Name. With this field, you can create Customers for your  clients in LogiNext.

### Get 


> Sample Request

```json
https://api.loginextsolutions.com/ClientApp/customer/v1/get/list?ids=cust1,65ba00dbdcf04fb789311df6aa40e3ba

```

Retrieve a List of Customers using this API. Pass the LogiNext Reference IDs or Customer IDs for the Customers you want to search for in the Request Body. 

If you have the LogiNext Customer IDs of your Customers and require the Customer Reference IDs to update a Customer, than you can call this API to get the Reference ID.

In case you only have the Customer ID, you can fetch the Customer details by calling this API. 

This API does not return the Shipping/ Delivery Addresses Associated with a Customer.

This API accepts upto 20 Customer IDs or Reference IDs in a comma separated format in the URL.


> Sample Response

```json
{
   "status": 207,
   "message": "Customer Details fetched successfully",
   "data": [
       {
            "name":"James Wan",
            "mobile":"341245673212",
            "email":"james@ablogs.com",
            "customerType":"Preferred",
            "billingAddress": {
              "apartment":"Suite No. 1, Milsons Towers",
                  "streetName":"Michigan Avenue",
                  "landmark":"Opp. Subway",
                  "locality":"Dowtown Chicago",
                  "city":"Chicago 11",
                  "state":"NY",
                  "country":"USA",
                  "pincode":"10045",
                  "latitude": 72.9555,
                  "longitude": 19.555
                   },
           "isActive": "Y",
           "referenceId": "241ccf29a4404046a033f31cc3384ac7"
       }
   ],
   "error": {
       "1": "65ba00dbdcf04fb789311df6aa40e3ba"
   },
   "hasError": true
}

```


#### Request

<span class="post">GET</span>` https://api.loginextsolutions.com/ClientApp/customer/v1/get/list?ids=cust1,65ba00dbdcf04fb789311df6aa40e3ba`


### Update

> Sample Request

```json
[
  {
    "referenceId":"65ba00dbdcf04fb789311df6aa40e3ba",
    "name":"James Wan",
    "mobile":"341245673212",
    "email":"james@ablogs.com",
    "customerType":"Preferred",
    "billingAddress": {
      "apartment":"Suite No. 1, Milsons Towers",
          "streetName":"Michigan Avenue",
          "landmark":"Opp. Subway",
          "locality":"Dowtown Chicago",
          "city":"Chicago 11",
          "state":"NY",
          "country":"USA",
          "pincode":"10045",
          "latitude": 72.9555,
          "longitude": 19.555
    }
  }
]
```

> Sample Response

```json
{
    "status": 200,
    "message": "Customer(s) updated successfully",
    "data": [
        {
            "index": 0,
            "referenceId": "65ba00dbdcf04fb789311df6aa40e3ba"
        }
    ],
    "hasError": false
}

```

You can update a  Customer the LogiNext system with this API.


This API will update a Customer Entity with the details provided. To update a Shipping/ Delivery address for a Customer, call the Update Address API.

This API will only accept inputs if your Customer Profiling property is set in LogiNext. To know more about the Customer Profiling property, please reach out to us at support@loginextsolutions.com.

You can create a maximum of 5 Customers in LogiNExt in one call of this API.


#### Request

<span class="post">POST</span>`https://api.loginextsolutions.com//ClientApp/customer/v1/update`


#### Request Parameters

Parameter | DataType | Length |  Required | Description
-----------|-------|------- |------- | ----------
referenceId  | String | 32 | Mandatory | Unique Customer ID used to identify a Customer.
accountCode | String | 50 | Optional | Unique Customer ID used to identify a Customer.
name | String | 255 | Optional | Customer name.
mobile | String | 255 | Optional | Customer Mobile NUmber.
email | String | 255 |Optional | Customer Email ID.
customerType | String | 255 | Optional | This is the delivery associate's mobile number.
billingAddress.apartment | String | 40 |Optional | Customer's Billing Address apartment.
billingAddress.streetName | String | 100 | Optional | Customer's Billing Address Street Name.
billingAddress.landmark | String | 255 | Optional | Customer's Billing Address landmark.
billingAddress.locality | String | 255 | Optional | Customer Billing Address locality.
billingAddress.city | Integer | 20 | Optional | Customer Billing Address city.
billingAddress.state | Integer | 20 | Optional | Customer Billing Address state. This will be based on the state codes in LogiNext for the country selected by you.
billingAddress.country | String | 255 | Optional | Customer's Billing Address Country.
billingAddress.pincode | String | 255 | Optional | Customer's Billing Address Pincode.
billingAddress.latitude | Double | 20 | Optional | Customer's Billing Address geo-coordinate(latitude)
billingAddress.longitude | Double | 20 | Optional | Customer's Billing Address geo-coordinate(longitude)
clientCode | String | 50 | Optional | Sub Client Name. With this field, you can create Customers for your  clients in LogiNext.


## Address 

### Create

> Sample Request

```json
[
  {
    "customerReferenceId":"65ba00dbdcf04fb789311df6aa40e3ba",
    "addressId":"HomeAdd",
    "addressType":"Home",
    "addressServiceTime":"5",
    "breakTime":[
      {
        "startTime":"10:00",
        "endTime":"11:30"
      },
      {
        "startTime":"12:00",
        "endTime":"13:30"
      },
      {
        "startTime":"18:00",
        "endTime":"19:00"
      }
    ],
    "preferredStartTime":"11:30",
    "preferredEndTime":"21:30",
    "weeklyOffList":["SUNDAY","WEDNESDAY"],
    "address":{
      "apartment":"Suite No. 1111, Milsons Towers",
          "streetName":"Michigan Avenue 1111",
          "landmark":"Opp. Subway 1111",
          "locality":"Dowtown Chicago 111",
          "city":"Chicago 1111",
          "state":"MH",
          "country":"IND",
          "pincode":"400076",
          "latitude": 72.9555,
          "longitude": 19.555
    },
    "isPrimary":"Y",
    "clientCode":"MyKart",
    "timeZone":"America/Chicago"
  }
  
]
```

> Sample Response

```json
 {
    "status": 200,
    "message": "Address(s) created successfully",
    "data": [
        {
            "index": 0,
            "addressId":"HomeAdd",
            "referenceId": "6a34c7274df0489f97c0f891514b488b",
            "customerReferenceId": "65ba00dbdcf04fb789311df6aa40e3ba"
        }
    ],
    "hasError": false
}

```

You can create an Address for an existing Customer in the LogiNext system with this API. A new Customer Address will be created and assigned a unique Reference ID that can be used to identify the Address later.

If you have Addresses created in your current system that you would like to push to LogiNext, call this API with the parameters mentioned below to add them in LogiNext.

This API will create an Address Entity with contact information and an optional Billing Address for a Customer. To create a Shipping/ Delivery address for a Customer, call the Create Address API.

These are the customers you would create Orders for in LogiNext. The Customer ID you use to identify indivuduak customers can be used in the Create Order API to create an Order.

This API will only accept inputs if your Customer Profiling property is set in LogiNext. To know more about the Customer Profiling property, please reach out to us at support@loginextsolutions.com.

You can create a maximum of 5 Customers in LogiNExt in one call of this API.

#### Request

<span class="post">POST</span>`https://api.loginextsolutions.com/ClientApp/address/v1/create`


#### Request Parameters

Parameter | DataType | Length |  Required | Description
-----------|-------|------- |------- | ----------
customerReferenceId | String | 32 | Mandatory | Unique Customer ID used to identify the Customer the address is being created for.
addressId | String | 255 | Optional | Address ID used to identify the address of that customer. The address ID must be unique within a Customer entity.
addressType | String | 255 | Optional | Address Type epending on the values configured for you in LogiNext. eg - 'HOME', 'OFFICE', 'OTHER'.
addressServiceTime | String | 255 |Optional | Service Time for that address in minutes.
breakTime.startTime | String | 255 | Conditional Mandatory | Break Start time of the Address in HH:MM format.. This field is mandatory if a break end time is provided.
breakTime.endTime | String | 40 |Conditional Mandatory | Break end time of the Address in HH:MM format.. This field is mandatory if a break start time is provided.
preferredStartTime | String | 100 | Optional | If a particular customer location has preferred times within which it should be serviced, you can enter those times here. They will be considered during planning deliveries to that address location. This field accepts values in HH:MM format.
preferredEndTime | String | 255 | Mandatory | If a particular customer location has preferred times within which it should be serviced, you can enter those times here. They will be considered during planning deliveries to that address location. This field accepts values in HH:MM format.
weeklyOffList | LIST | 255 | Mandatory | Days of the week this location is OFF i.e not serviceable.
address.city | Integer | 20 | Mandatory | Address city.
address.state | Integer | 20 | Optional |  Address state. This will be based on the state codes in LogiNext for the country selected by you.
address.country | String | 255 | Optional | Address Country.
address.pincode | String | 255 | Optional | Address Pincode.
address.latitude | Double | 20 | Optional |  Address geo-coordinate(latitude)
address.longitude | Double | 20 | Optional | Address geo-coordinate(longitude)
clientCode | String | 50 | Optional | Sub Client Name. With this field, you can create Customers for your  clients in LogiNext.
timeZone | String | | Optional | The timzone of the address field. If not passed, it will default the timezone configured for your account for the address being created.




## Delivery Associate

### Create

> Sample Request

```json
[
 {
"employeeId":"ALL123469",
"branchName":"LMDCalifornia",
"userGroupName":"MobileUser_LMDemo",
"deliveryMediumMasterName":"James",
"phoneNumber":9892147969,
"imei":123456789012123,
"emailId":"test@test.com",
"userName":"james003",
"password":"admin",
"capacityInUnits":10,
"capacityInVolume":10,
"capacityInWeight":10,
"dob":"2016-12-12",
"deliveryMediumMapList": [
     {
       "name": "SPANISH"

     },
     {
       "name": "ENGLISH"

     }
   ],
"gender":"Male",
"deliveryMediumMasterTypeCd":"Delivery Associate",
"isOwnVehicleFl":"Company",
"vehicleNumber":"1AB54F",
"dmPreference":"10035",
"shiftTimeList": [
            {
                "shiftStartTime": "12:30",
                "shiftEndTime": "14:30"
            }
        ],
        "breakTimeList": [
            {
                "breakStartTime": "13:00",
                "breakEndTime": "13:30",
                "breakDurationInMins": 12
            }
        ],
"loadingTimeInMins": 20,
"weeklyOffList": [
     "Thursday",
     "Monday"
   ],
"maxDistance":10,
"fixedCost":10,
"variableCost":10,
"isPresentFl":"Y",
"addressList": [ { 
"apartment":"901",
"streetName":"2142 3rd Ave",
"landmark":"Opp. McDonalds",
"countryShortCode":"USA",
"city":"Ney York",
"pincode":"10035",
"addressType":"PERMANENT" 
},
{ 
"apartment":"901",
"streetName":"2142 3rd Ave",
"landmark":"Opp McDonalds",
"countryShortCode":"USA",
"city":"New York",
"pincode":"10035",
"addressType":"CURRENT" 
}

],
"maritalStatus":"Single",
"alternateMobileNo":9892134489,
"landlineNo":28215678,
"licenseValidity":"2026-12-12",
"licenseValidityInYears":10,
"licenseIssuanceDate":"2016-12-12",
"licenseNumber":2123123123
}
]
```

> Sample Response

```json
{
  "status": 201,
  "message": "success",
  "data": [
    "d7b0f3f8e1174742bd6a8ae451866cb1"
  ],
  "hasError": false
}

```

Create a new Delivery Associate in the LogiNext system with this API. A delivery associate will be created and assigned a unique Reference ID that can be used to identify the Delivery Associate later.

#### Request

<span class="post">POST</span>`https://api.loginextsolutions.com/DeliveryMediumApp/mile/v1/create`


#### Request Parameters

Parameter | DataType | Length |  Required | Description
-----------|-------|------- |------- | ----------
employeeId | String | 50 | Mandatory | This is the Employee ID with which the Delivery Associate is to be created in the LogiNext Application.
userGroupName | String | 255 | Mandatory | This is the delivery associate's user group name.
branchName | String | 255 | Mandatory | This is the delivery associate's client branch name.
deliveryMediumMasterName | String | 255 |Mandatory | Full name of Delivery associate.
phoneNumber | String | 255 | Mandatory | This is the delivery associate's mobile number.
imei | String | 40 |Optional | This is the delivery associate's IMEI number.
emailId | String | 100 | Optional | This is the delivery associate's email ID.
userName | String | 255 | Mandatory | This is the delivery associate's username.
password | String | 255 | Mandatory | This is the delivery associate's password.
capacityInUnits | Integer | 20 | Mandatory | Capacity of Delivery associate in units
capacityInVolume | Integer | 20 | Optional | Capacity of Delivery associate in volume
capacityInWeight | Integer | 20 |Optional | Capacity of Delivery associate in weight
dob | String |  | Optional | Date of birth
gender | ISODate | 12 |Optional | Gender. Ex - Male,Female
deliveryMediumMasterTypeCd | String | 255 |Optional | Delivery associate type. Ex - Truck, Delivery Boy
isOwnVehicleFl | String | 1 |Optional | Owner of vehicle. Ex - Owned, Company
vehicleNumber | String | 255 | Optional | Vehicle number to be assigned to the delivery associate
weeklyOffList  | String | 255 |Optional | Array of week's off days. Ex - Monday, Tuesday etc.
maxDistance | Integer | 20 |Optional | This is the maximum distance the Delivery Associate is allowed to cover within a trip. This value is considered when creating a route plan for the Delivery Associate.
deliveryMediumMapList.name | String | 255 | Optional | Name of language
shiftTimeList.shiftStartTime  | String|  |Optional | Shift start time in HH:MM format. 
shiftTimeList.shiftEndTime  | String |  |Optional | Shift end time in HH:MM format
breakTimeList | List | | Optional | This is the break time of the Delivery Associate. The LogiNext Route Planning engine will not assign orders with Service time windows within a Delivery Associate's break time to that Delivery Associate. 
breakTimeList.breakStartTime  | String |  |Optional | Break start time in HH:MM format.
breakTimeList.breakEndTime  | String |  | Optional | Break end time in HH:MM format.
breakTimeList.breakDurationInMins  | Integer | | Optional | Break Time Duration in minutes
dmPreference  | String | 255 | Optional | Preferred Pincode of Delivery associate. The Route Planning engine will consider this piccode preference when assignming Orders to the Delivery Associate if the Pin Code Preference' property is set.
addressList | List | | | Holds the address details of the Delivery Associate.
addressList.apartment | String | Optional | 255 | Delivery Associate's Apartment number.
addressList.streetName | String | Optional | 255 | Delivery Associate's Street Name.
addressList.landmark | String | Optional | 255 | Delivery Associate's landmark.
addressList.countryShortCode | String | Optional | 255 | This is the  Delivery Associate's country code. Please refer to the list of country codes provided in the "Country Codes" section.
addressList.city | String | Optional | 255 | Delivery Associate's city.
addressList.pincode | String | Optional | 255 | Delivery Associate's pincode.
addressList.addressType | String | Optional | 255 | Identifies if this is the current or permanent address of the Delivery Associate. If set to "CURRENT", it will select the entered address as current. If "PERMANENT", it will set the entered address as permanent. This field does not accept any other value. You must send this field if adding an address for the Delivery Associate.
maritalStatus | String | Optional | 255 | Delivery Associate's Marital Status.
alternateMobileNo | String | Optional | 255 | Alternate Mobile NUmber of the Delivery Associate.
landlineNo | String | Optional | 255 | Landline Number of the Delivery Associate.
licenseValidity | String | Optional | 255 | This is the expiry Date of the Driver's License in YYYY-MM-HH format.
licenseValidityInYears | Optional | String | 255 | License Validity in years.
licenseIssuanceDate |String | Optional | 255 | License Issuance Date in YYYY-MM-HH format.

### Get 


> Sample Request

```json

["d7f173453bab40cf83dc79bb86ea2edb"]
```

Retrieve a List of all the Delivery Associates using this API. Pass the LogiNext Reference IDs or Username for the Delivery Associates you want to search for in the Request Body. 

The API returns a link of the profile picture of the Delivery Associate, if one was uploaded in LogiNext, in the 'profilePicture' field.This can be used in the case where the Delivery Associate's image may need to be displayed on your mobile application screen to show Customers who is fulfilling their Order.
Note that in case you are storing this link in your system, this link has a life time of 1 hour post which it will expire, and will need to be fetched again.

#### Request Parameters

Parameter | DataType | Length |  Required | Description
-----------|-------|------- |------- | ----------
referenceId | List | 32 | Conditional Mandatory | This is the LogiNext Reference ID of the Delivery Associate to be updated. 
userName | List | 50 | Conditional Mandatory | This is the Username of the Delivery Associate to be updated.


> Sample Response

```json
{
    "status": 200,
    "data": {
        "totalCount": 1,
        "otherCount": 0,
        "clientBranchId": 0,
        "results": [
            {
                "isActiveFl": true,
                "capacityInUnits": 10,
                "capacityInVolume": 100,
                "capacityInWeight": 1098,
                "deliveryMediumMasterTypeCd": "Truck",
                "imei": "",
                "statusCd": "Available",
                "employeeId": "NBVA114",
                "weeklyOff": "Monday",
                "maxDistance": 100,
                "licenseValidity": "2018-12-20",
                "dob": "2000-12-01",
                "gender": "Male",
                "phoneNumber": "9215697602",
                "userName": "robin123456",
                "shiftTimeList": [
                    {
                        "shiftStartTime": "12:30",
                        "shiftEndTime": "14:30"
                    }
                ],
                "breakTimeList": [
                    {
                        "breakStartTime": "13:00",
                        "breakEndTime": "13:30",
                        "breakDurationInMins": 12
                    }
                ],
                "loadingTimeInMins": 20,
                "branchName": "Snappbox_UAT Main Branch",
                "userGroupName": "Snappbox_UAT Mob",
                "emailId": "abc@d.com",
                "languageList": [
                    "HINDI",
                    "ENGLISH"
                ],
                "dmPreference": "400010",
                "isOnBreakFl": "N",
                "deliveryMediumLoginDetails": {
                    "type": "NOTLOGEDIN"
                },
                "profilePicture": "https://loginext-user-image.s3-ap-southeast-1.amazonaws.com/user32330_209.jpg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Date=20180629T120457Z&X-Amz-SignedHeaders=host&X-Amz-Expires=3599&X-Amz-Credential=AKIAI4W45JCJJU7CQPPQ%2F20180629%2Fap-southeast-1%2Fs3%2Faws4_request&X-Amz-Signature=211c72fa8ca01f6a0d8a5a8e9c0fd62a48a970611802bba887ccd8ca36700349",
                "deliveryMediumName": "Robin New 3",
                "cashPaid": 0,
                "cashCollected": 0,
                "cashBalance": 0,
                "referenceId": "fa7716b25fe5432a96d1a709a28bd6d8"
            }
        ]
    },
    "hasError": false
}

```


#### Request

<span class="post">POST</span>` https://api.loginextsolutions.com/DeliveryMediumApp/mile/v1/list`


### Update

> Sample Request

```json
[
 {
 "referenceId":"f0094fd13acc4d76827898bddc2ce0e3",
"employeeId":"ALL123469",
"branchName":"LMDCalifornia",
"userGroupName":"MobileUser_LMDemo",
"deliveryMediumMasterName":"James",
"phoneNumber":9892147969,
"imei":123456789012123,
"emailId":"test@test.com",
"userName":"james003",
"password":"admin",
"capacityInUnits":10,
"capacityInVolume":10,
"capacityInWeight":10,
"dob":"2018-104-01T13:30:00Z",
"deliveryMediumMapList": [
     {
       "name": "SPANISH"

     },
     {
       "name": "ENGLISH"

     }
   ],
"gender":"Male",
"deliveryMediumMasterTypeCd":"Delivery Associate",
"isOwnVehicleFl":"Company",
"vehicleNumber":"1AB54F",
"dmPreference":"10035",
"shiftTimeList": [
    {
        "shiftStartTime": "12:30",
        "shiftEndTime": "14:30"
    }
],
"breakTimeList": [
    {
        "breakStartTime": "13:00",
        "breakEndTime": "13:30",
        "breakDurationInMins": 12
    }
],
"loadingTimeInMins": 20,
"weeklyOffList": [
     "Thursday",
     "Monday"
   ],
"maxDistance":10,
"licenseValidity":"2018-104-01T13:30:00Z",
"fixedCost":10,
"variableCost":10,
"isPresentFl":"Y",
"addressList": [ { 
"apartment":"901",
"streetName":"2142 3rd Ave",
"landmark":"Opp. McDonalds",
"countryShortCode":"USA",
"city":"New York",
"pincode":"10035",
"addressType":"PERMANENT" 
},
{ 
"apartment":"901",
"streetName":"2142 3rd Ave",
"landmark":"Opp McDonalds",
"countryShortCode":"USA",
"city":"New York",
"pincode":"10035",
"addressType":"CURRENT" 
}

],
"maritalStatus":"Single",
"alternateMobileNo":9892134489,
"landlineNo":28215678,
"licenseValidityInYears":10,
"licenseIssuanceDate":"2018-104-01T13:30:00Z",
"licenceNumber":2123123123
}
]
```

> Sample Response

```json
{
  "status": 201,
  "message": "success",
  "data": [
    "d7b0f3f8e1174742bd6a8ae451866cb1"
  ],
  "hasError": false
}

```

Update the details of a Delivery Associate in the LogiNext system with this API. 

#### Request

<span class="post">POST</span>`https://api.loginextsolutions.com/DeliveryMediumApp/mile/v1/update`


#### Request Parameters

Parameter | DataType | Length |  Required | Description
-----------|-------|------- |------- | ----------
referenceId | String | 32 | Mandatory | This is the LogiNext Reference ID of the Delivery Associate to be updated.
employeeId | String | 50 | Optional | This is the delivery associate's employee Id.
userGroupName | String | 255 | Optional | This is the delivery associate's user group name.
branchName | String | 255 | Optional | This is the delivery associate's client branch name.
deliveryMediumMasterName | String | 255 | Optional | Full name of Delivery associate.
phoneNumber | String | 255 | Optional | This is the delivery associate's mobile number.
imei | String | 40 | Optional | This is the delivery associate's IMEI number.
emailId | String | 100 | Optional | This is the delivery associate's email ID.
userName | String | 255 | Optional | This is the delivery associate's username.
password | String | 255 | Optional | This is the delivery associate's password.
capacityInUnits | Integer | 20 | Optional | Capacity of Delivery associate in units
capacityInVolume | Integer | 20 | Optional | Capacity of Delivery associate in volume
capacityInWeight | Integer | 20 |Optional | Capacity of Delivery associate in weight
dob | String |  | Optional | Date of birth.This field accepts values in UTC format.
gender | ISODate | 12 |Optional | Gender. Ex - Male,Female
deliveryMediumMasterTypeCd | String | 255 |Optional | Delivery associate type. Ex - Truck, Delivery Boy
isOwnVehicleFl | String | 1 |Optional | Owner of vehicle. Ex - Owned, Company
vehicleNumber | String | 255 | Optional | Vehicle number to be assigned to the delivery associate
weeklyOffList  | String | 255 |Optional | Array of week's off days. Ex - Monday, Tuesday etc.
maxDistance | Integer | 20 |Optional | Max. allowed distance
licenseValidity | String |  | Optional | License validity date. This field accepts values in UTC format.
deliveryMediumMapList.name | String | 255 | Optional | Name of language
shiftList.shiftStartTime  | UTC Date |  |Optional | Shift start time
shiftList.shiftEndTime  | UTC Date|  |Optional | Shift end time
dmPreference  | String | 255 | Optional | Preferred Pincode of Delivery associate. The Route Planning engine will consider this piccode preference when assignming Orders to the Delivery Associate if the Pin Code Preference' property is set.
shiftTimeList.shiftStartTime  | String|  |Optional | Shift start time in HH:MM format. 
shiftTimeList.shiftEndTime  | String |  |Optional | Shift end time in HH:MM format
breakTimeList.breakStartTime  | String |  |Optional | Break start time in HH:MM format.
breakTimeList.breakEndTime  | UTC |  | Optional | Break end time in HH:MM format.
breakTimeList.breakDurationInMins  | Integer  |Optional | Break Time Duration in minutes
addressList | List | | | Holds the address details of the Delivery Associate.
addressList.apartment | String | 255 | Optional | Delivery Associate's Apartment number.
addressList.streetName | String | 255 | Optional | Delivery Associate's Street Name.
addressList.landmark | String | 255 | Optional | Delivery Associate's landmark.
addressList.countryShortCode | String | 255 | Optional | This is the  Delivery Associate's country code. Please refer to the list of country codes provided in the "Country Codes" section.
addressList.city | String | 255 | Optional | Delivery Associate's city.
addressList.pincode | String | 255 | Optional | Delivery Associate's pincode.
addressList.addressType | String | 255 | Optional | Identifies if this is the current or permanent address of the Delivery Associate. If set to "CURRENT", it will select the entered address as current. If "PERMANENT", it will set the entered address as permanent. This field does not accept any other value. You must send this field if adding an address for the Delivery Associate.
maritalStatus | String | 255 | Optional | Delivery Associate's Marital Status.
alternateMobileNo | String | 255 | Optional | Alternate Mobile NUmber of the Delivery Associate.
landlineNo | String | 255 | Optional | Landline Number of the Delivery Associate.
licenseValidity | String | Optional | String | 255 | This is the expiry Date of the Driver's License in YYYY-MM-HH format.
licenseValidityInYears | Optional | String | 255 | License Validity in years.
licenseIssuanceDate |String | Optional | 255 | License Issuance Date in YYYY-MM-HH format.



### Update Status

> Sample Request

```json
{
  "newStatus":"ACTIVE",
  "deliveryMediumDetails":
  [
    {
            "referenceId":"6186d5fc6e324c42abb5ea1a32e05f66",
            "reasonCd":"DBUNAVAILABLE",
            "latitude":19.67890,
            "longitude":78.6758
    },
    {
            "referenceId" : "bae83999422211e6860c0653055f4dfd",
            "reasonCd":"DBUNAVAILABLE",
            "latitude":19.67890,
            "longitude":78.67589
    }
  ]
}
```

> Sample Response

```json
{
    "status": 200,
    "message": "Deliverymedium break status update successfully",
    "hasError": false
}

```

Update the status of a previously created delivery associate with this API. Pass the new status of the associate in the 'newStatus' field, along with an optional reason and the geocoordinates of the delivery associate.

#### Request

<span class="post">PUT</span>`https://api.loginextsolutions.com/DeliveryMediumApp/mile/v1/update/status`


#### Request Parameters

Parameter | DataType | Length |  Required | Description
-----------|-------|------- |------- | ----------
newStatus | String | 50 | Mandatory | This will be the new status of the delivery associate . It can be "ACTIVE", "INACTIVE", "ONBREAK", or "OFFBREAK".
deliveryMediumDetails.referenceID | String | 32 | Mandatory | This is the referenceID of the delivery associate.
deliveryMediumDetails.reasonCd | String | 255 | Optional | This is the reason  for the updated status of the delivery associate.
deliveryMediumDetails.latitude | Double |  | Optional | The geolocation coordinate (latitude) of the delivery associate.
deliveryMediumDetails.longitude | Double |  | Optional | The geolocation coordinate (longitude) of the delivery associate.

## Hub

### Create

> Definition

```json
https://api.loginextsolutions.com/ClientApp/v1/branch/create
```

> Request Body

```json

[{
"clientParentBranchName":"Reeta Foods Main Branch",
"branchName":"Marque Downtown Chicago",
"address":{
        "apartment":"Suite No. 99, Milsons Towers",
        "streetName":"Michigan Avenue",
        "landmark":"Opp. Subway",
        "locality":"Dowtown Chicago",
        "city":"Chicago",
        "stateShortCode":"IL",
        "countryShortCode":"USA",
        "pincode":"60606"
},
"division":"ADIV",
"isOwnBranchFl":"N",
"isHubFl":"Y",
"geoFenceRadius":"2.0",
"branchDescription":"desc",
"billingContactName":"name",
"officeNumber":"2798678712",
"adminContactName":"John K.",
"mobileNumber":"9033977123",
"emailAddress":"superjames@gmails.com",
"longitude": 19.111755,
"latitude": 72.9095327,
"timeZone":"America/Chicago"
}]

```

> Response

```json
{
    "status": 200,
    "message": "Create Hub success.",
    "data": {
        "referenceId": "hcgsyuc334"
    },
    "hasError": false
}
```

Create hubs / branches / distribution centers in the LogiNext system with the Create Hub API. Hubs will be created and will be assigned a unique Reference ID that can be used to look up the hub later.

#### Request

<span class="post">POST</span>`https://api.loginextsolutions.com/ClientApp/v1/branch/create`


#### Request Body

Parameter | DataType | Length |  Required | Description
-----------|-------| ------- |------- | ----------
clientParentBranchName | String | 255 | Mandatory | This is name of the Parent Branch under which you want to create the new branch.<br>Please note that you cannot create the Main Parent branch for your account through this API.<br>The Main Parent Branch gets created automatically when your account is configured in LogiNext system.<br>If you want to know the name of the Main Parent Branch Name, please get in touch with your assigned Account Manager
branchName | String | 255 | Mandatory | This is the name of the branch / hub / distribution center/ that you want to add.
Address.apartment | String | 512 | Mandatory | This is Address Line 1. This is the Apartment Name / House Name / Building Name / Suite No.<br>For example - A 203 Richmond Avenue
Address.streetName | String | 512 | Mandatory | This is Address Line 2.This is the name of the Street where the Hub is situated.<br>Sample Value - Off Highway I96 or Walton Boulevard
Address.landmark | String | 512 | Mandatory | Any nearby landmark to identify your Hub quickly.<br>Sample Value - Opp. McDonalds or Behind Mercy Hospital
branchName | String | 255 | Optional | Any nearby landmark to identify your Hub quickly.<br>Sample Value - Opp. McDonalds or Behind Mercy Hospital
Address.locality | String | 512 | Mandatory | This is area in which the Hub is located<br>Sample Value - Southern Industry Park or Dubai Downtown<br><br>If you think that your specific region in which you operate does not have localities, then please raise the support request with your Account Manager to make this non-mandatory
Address.city | String | 512 | Mandatory | This is name of the city in which your Hub is situated<br>Sample Value - Atlanta or Kuala Lampur
Address.stateShortCode | String | 11 | Mandatory | This is code of State / Province.<br>Sample Value - For Georgia use GA ; For Jawa Barat use JB<br><br>Please refer to the section where we have listed down state codes for each country.<br>If you think that your specific region in which you operate does not have States / Provinces, then please raise the support request with your Account Manager to make this non-mandatory.
Address.countryShortCode | String | 11 | Mandatory | This is code of Country.<br>Sample Value - For India use IND; For China use CHN<br><br>Please refer to the section where we have listed down country codes.
Address.pincode | String | 20 | Mandatory | This is the postal code / zip code of the area in which your Hub is situated<br>Sample Value - 72712 ; 400076<br><br>If you think that your specific region in which you operate does not have postal codes, then please raise the support request with your Account Manager to make this non-mandatory.
division | String | 255 | Optional | Ex. ADIV
isOwnBranchFl | String | 1 | Mandatory | There can be two values here -  In Mile Hardcode this to N
isHubFl | String | 1 | Mandatory | There can be two values here -  In Mile Hardcode this to Y
geoFenceRadius | String | 255 | Optional | This is the radius in KMs that you have to enter if you want to create a geofence for your hub.<br>If no value is passed, then the default value of 2 Kms is taken.<br>Ideally a geofence radius should range between - 200 meters to 2 KMs
branchDescription | String | 500 | Optional | If you would like add a brief description name for the hub, use this field.
billingContactName | String | 500 | Mandatory | Name of the Contact Person at this Branch / Hub
officeNumber | String | 255 | Mandatory | Fixed Line Number of the Branch  / Hub
adminContactName | String | 255 | Mandatory | Name of the Supervisor / Alternate Contact for this Hub
mobileNumber | String | 255 | Mandatory | Mobile Phone No. of the contact person
emailAddress | String | 255 | Mandatory | Email Address of the contact person
timeZone | String | | Optional | The timezone of the Hub location you are creating. This will default yo your account configured timezone if not passed.



### Update

> Definition

```json
https://api.loginextsolutions.com/ClientApp/v1/branch/update
```

> Request Body

```json

[{
  "referenceId":"8d0a36e01c524022ab9ff2d66c14281c",
  "address":{
    "apartment":"Himalaya Mall",
    "streetName":"Driving Road",
    "pincode":"380061",
    "locality":"Drive in Road",
    "stateShortCode":"GJ",
    "countryShortCode":"IND"
  },

  "division":"BDIC",
  "isOwnBranchFl":"N",
  "isHubFl":"Y",
  "geoFenceRadius":"4.0",
  "branchDescription":"DEC",
  "billingContactName":"bill",
  "officeNumber":"971545813943",
  "adminContactName":"name",
  "mobileNumber":"971545813943",
  "emailAddress":"hack1@gmail.com"
}]

```

> Response

```json
{
    "status": 200,
    "message": "Create Hub success.",
    "data": {
        "referenceId": "hcgsyuc334"
    },
    "hasError": false
}
```

Update hubs / branches / distribution centers in the LogiNext system with the Update Hub API. 

#### Request

<span class="post">POST</span>`https://api.loginextsolutions.com/ClientApp/v1/branch/update`


#### Request Body

Parameter | DataType | Length |  Required | Description
-----------|-------| ------- |------- | ----------
referenceId | String | 255 | Mandatory | This is the reference ID of the branch to be updated.
Address.apartment | String | 512 | Optional | This is Address Line 1. This is the Apartment Name / House Name / Building Name / Suite No.<br>For example - A 203 Richmond Avenue
Address.streetName | String | 512 | Optional | This is Address Line 2.This is the name of the Street where the Hub is situated.<br>For example - Off Highway I96 or Walton Boulevard
Address.landmark | String | 512 | Optional | Any nearby landmark to identify your Hub quickly.<br>For example - Opp. McDonalds or Behind Mercy Hospital
branchName | String | 255 | Optional | Any nearby landmark to identify your Hub quickly.<br>For example - Opp. McDonalds or Behind Mercy Hospital
Address.locality | String | 512 | Optional | This is area in which the Hub is located<br>For example - Southern Industry Park or Dubai Downtown<br><br>If you think that your specific region in which you operate does not have localities, then please raise the support request with your Account Manager to make this non-mandatory
Address.city | String | 512 | Optional | This is name of the city in which your Hub is situated<br>For example - Atlanta or Kuala Lampur
Address.stateShortCode | String | 11 | Optional | This is code of State / Province.<br>For example - For Georgia use GA ; For Jawa Barat use JB<br><br>Please refer to the section where we have listed down state codes for each country.<br>If you think that your specific region in which you operate does not have States / Provinces, then please raise the support request with your Account Manager to make this non-mandatory.
Address.countryShortCode | String | 11 | Mandatory | This is code of Country.<br>For example - For India use IND; For China use CHN<br><br>Please refer to the section where we have listed down country codes.
Address.pincode | String | 20 | Mandatory | This is the postal code / zip code of the area in which your Hub is situated<br>For example - 72712 ; 400076<br><br>If you think that your specific region in which you operate does not have postal codes, then please raise the support request with your Account Manager to make this non-mandatory.
division | String | 255 | Optional | Ex. ADIV
isOwnBranchFl | String | 1 | Optional | There can be two values here -  In Mile Hardcode this to N
isHubFl | String | 1 | Optional | There can be two values here -  In Mile Hardcode this to Y
geoFenceRadius | String | 255 | Optional | This is the radius in KMs that you have to enter if you want to create a geofence for your hub.<br>If no value is passed, then the default value of 2 Kms is taken.<br>Ideally a geofence radius should range between - 200 meters to 2 KMs
branchDescription | String | 500 | Optional | If you would like add a brief description name for the hub, use this field.
billingContactName | String | 500 | Optional | Name of the Contact Person at this Branch / Hub
officeNumber | String | 255 | Optional | Fixed Line Number of the Branch  / Hub
adminContactName | String | 255 | Optional | Name of the Supervisor / Alternate Contact for this Hub
mobileNumber | String | 255 | Optional | Mobile Phone No. of the contact person
emailAddress | String | 255 | Optional | Email Address of the contact person

## Geofence

### Get

> Definition

```json
https://api.loginextsolutions.com/GeofenceApp/geofence/v1/get?geofenceIds=MMD-White Marsh,MMD-Patapsco High/Dundalk&page_no=1&page_size=50&status=ACTIVE
```

> Response


```json
{
    "status": 200,
    "message": "Geofence details fetched successfully.",
    "data": [
        {
            "isActiveFl": true,
            "customFields": [
                {
                    "field": "deliveryDay",
                    "value": "1533081600000",
                    "type": "date"
                },
                {
                    "field": "deliveryTime",
                    "value": "10:00",
                    "type": "time"
                },
                {
                    "field": "cutOffDay",
                    "value": "1533168000000",
                    "type": "date"
                },
                {
                    "field": "cutOffTime",
                    "value": "11:00",
                    "type": "time"
                }
            ],
            "geofenceName": "MMD-Patapsco High/Dundalk",
            "referenceId::"987ygr43wefghyu89oikjhytrew34",
            "geofenceShape": "Polygon",
            "geofenceArea": 0,
            "geoCoordinates": [
                {
                    "latitude": 39.2363378,
                    "longitude": -76.53115
                },
                {
                    "latitude": 39.2257375,
                    "longitude": -76.5072441
                },
                {
                    "latitude": 39.2014656,
                    "longitude": -76.5027766
                },
                {
                    "latitude": 39.1995356,
                    "longitude": -76.4608956
                },
                {
                    "latitude": 39.2201521,
                    "longitude": -76.4421844
                },
                {
                    "latitude": 39.2402943,
                    "longitude": -76.4087104
                }
            ]
        }
    ],
    "hasError": false
}
```

If you have configured geofences in LogiNext to identify your Hubs or particular locations, you can call this API to fetch the details and geo coordinates of your geofences.



By default, the API returns all the Active geofences


#### Request Parameters

Parameter | DataType |  Required | Description
-----------|-------|------- | ----------
geofenceIds | String | Optional | You can pass the LogiNext geofence reference ID or geofence name in this parameter. If there are special characters present in the geofence name, encoded values for these characters will be accepted by the API. For example, a space(' ') will be denoted by '%20' Multiple geofence identifiers can be passed in a comma separated format.
status | String | Optional | This can be 'ACTIVE', 'INACTIVE' or 'ALL'. If not passed, this API will return all geofences by default.
page_no | Integer | Optional | You can specify whihc page to fetch for the API. By default this will be 1.
page_size | Integer | Optional |  You can the specify the number of records to be fetched with this parameter. By default the API will return 100

#### Response Body

Parameter | DataType | Description
-----------|-------| ----------
isActiveFl | Boolean | Specifies if the Geofence is active or not.
referenceId | String | Reference ID of the Geofence.
geofenceName | String  | The name of the Geofence specified at the time of Geofence creation.
geofenceShape | Date   | This will be POLYGON by by default.
geofenceArea | Date | The area of the geofence in the unit system property units configured in LogiNext. If you have configured meters, than this will be in square meters.
geoCoordinates.latitude | Double | The geo coordinate(latitude) of the geofence edge. 
geoCoordinates.longitude | Double | The geo coordinate(longitude) of the geofence edge. 


## Order

Create Orders in the LogiNext system using the Orders API. Orders will be assigned a referenceId that will be returned in the API response. This refernceId can be used to identify the Order later.

To view the Orders created in the LogiNext Web Application, select the correct date range in the date filter on the screen.

You can use the property of Customer Profiling while creating orders in LogiNext to store customer information context. 
When Customer Profiling is turned ON -
1. You can only enter the corresponding accountCode field that will hold the customer ID. If passed, ad the accountCode exists in the LogiNext system, LogiNext will use the customer information associated with that accountCode in the Order creation. It will overlook other customer information like Name, Email and Phone Number.
2. In Order to select a particular address for that customer, you can pass the address ID associated with that address for that customer. If passed, and the address ID exists in LogiNext for a previously created address, the address information associated with that address ID will be used.


### Create Pick Up Only

> Definition

```json
https://api.loginextsolutions.com/ShipmentApp/mile/v2/create
```

> Request Body

```json
[
  {
    "orderNo": "GR432U5",
    "awbNumber": "435-16685675",
    "shipmentOrderTypeCd": "PICKUP",
    "orderState": "FORWARD",
    "autoAllocateFl": "N",
    "shipmentOrderDt": "2016-07-15T10:30:00.000Z",
    "pickupStartTimeWindow": "2016-07-16T10:31:00.000Z",
    "pickupEndTimeWindow": "2016-07-18T10:31:00.000Z",
    "pickupServiceTime": "20",
    "deliveryType": "Groceries",
    "deliveryLocationType":"HOME",
    "pickupBranch": "East Manhatten",
    "distributionCenter": "Brooklyn",
    "partialDeliveryAllowedFl": "Y",
    "cancellationAllowedFl": "N",    
    "returnAllowedFl": "Y",
    "returnBranch": "Chicago North",
    "numberOfItems": 2,
    "packageWeight":"10",
    "packageVolume": "4500",
    "paymentType": "COD",
    "packageValue": "5000",
    "pickupNotes": "Please ring my Door Bell",
    "pickupAccountCode": "jim001",
    "pickupAddressId": "home",
    "pickupAccountName": "James Walker",
    "pickupEmail": "james.w@ablogs.com",
    "pickupPhoneNumber": "5163063377",
    "pickupApartment": "901",
    "pickupStreetName": "2142 3rd Ave",
    "pickupLandmark": "Opp. McDonalds",
    "pickupLocality": "East Harlem",
    "pickupCity": "New York",
    "pickupState": "NY",
    "pickupCountry": "USA",
    "pickupPinCode": "10035",
    "pickupLatitude":40.760838,
    "pickupLongitude":-73.96732299999996,    
    "pickupAddressTimezone":"America/New_York",
    "clientCode": "Salestap",

    "shipmentCrateMappings": [
      {
        "crateCd": "CR5002",
        "crateAmount":1000,
        "crateType":"Case",
        "noOfUnits":3,
        "shipmentlineitems": [
          {
            "itemCd": "IT038",
            "itemName": "Milk tetra pack small",
            "itemPrice": 100,
            "itemQuantity": 1,
            "itemType": "dairy",
            "itemWeight": 10
          },
          {
            "itemCd": "IT043",
            "itemName": "Chicken Soup 2X200gm",
            "itemPrice": 500,
            "itemQuantity": 1,
            "itemType": "soup",
            "itemWeight": 10
          },
          {
            "itemCd": "IT030",
            "itemName": "WholeBeanCoffee 6x1kg",
            "itemPrice": 400,
            "itemQuantity": 1,
            "itemType": "coffee",
            "itemWeight": 10
          }
        ]

      },
{
        "crateCd": "CR002",
        "crateAmount":200,
        "crateType":"Case",
        "noOfUnits":1,
        "shipmentlineitems": [
          {
            "itemCd": "IT043",
            "itemName": "Chicken Soup 2X200gm",
            "itemPrice": 20,
            "itemQuantity": 2,
            "itemType": "soup",
            "itemWeight": 50
          }
]
}
    ]
  }
]
```



> Success Response

```json
{
    "status": 200,
    "message": "Order(s) created successfully",
    "data": [
        {
            "index": 0,
            "referenceId": "6a34c7274df0489f97c0f891514b488b",
            "orderNumber": "ww1223",
            "shipmentOrderTypeCd": "PICKUP",
            "orderState": "FORWARD"
        },
        {
            "index": 1,
            "referenceId": "a0108f976b3b41f1b51e438d4e8c7bf5",
            "orderNumber": "ww1225",
            "shipmentOrderTypeCd": "PICKUP",
            "orderState": "FORWARD"
        }
    ],
    "hasError": false
}

```

> Failure Response

```json
{
   "status": 409,
   "message": "",
   "moreResultsExists": false,
   "error": [
       {
           "index": 0,
           "orderNo": "TFC003",
           "orderState": "FORWARD",
           "shipmentOrderTypeCd": "PICKUP",
           "errorList": [
               {
                   "key": "pickupAccountCode",
                   "message": [
                       "Pickup Customer id  is mandatory."
                   ]
               }
           ]
       }
   ],
   "hasError": true
}

```

Create pickup orders with this API in the LogiNext system. Orders will be created and assigned a reference ID that can be used at a leter time to identify the order.

#### Request

<span class="post">POST</span>`https://api.loginextsolutions.com/ShipmentApp/mile/v2/create`



#### Request Parameters

Param | DataType | Length |  Required | Description
--------- | ------- | ------- | ---------- | ------------
orderNo | String | 100 | Mandatory | This is the Order No.
awbNumber | String | 1000 | Optional | If you want an AWB no. to be associated with an order, you can pass the same here.
shipmentOrderTypeCd | String | 40 | Mandatory | The value in this field has to be "PICKUP" always.
orderState | String | 512 | Mandatory | If an order is a Forward way (Pickup from Merchant for Customer Delivery), then value here should be "FORWARD"<br>If an order is a Return way (Return from the Customer), then value here should be "REVERSE"
autoAllocateFl| String | 50 | Optional | This can be "Y" or "N". If set to "Y", the Order will be automatially allocated to the nearest Delivery Associate when it is created in the system. If "N", the Delivery Associate will get notified if the Order is ready to be allocated to them, and they can choose to Accept or Reject it.<br>Pass this Flag as 'P' if you want to assign the newly created Order to an existing planned trip. This assignment event can impact the sequence of Order previously created for that trip.
shipmentOrderDt | Date |  | Mandatory | The date and time on which the order is created.<br>Note that this date and time has to be in UTC.<br>For example - "2017-07-15T10:30:00.000Z"
distributionCenter | String | 255 | Mandatory | Distribution center's name
packageWeight | Double | 10 | Optional | This is the weight of package in Kg.
packageVolume | Double | 10 | Optional | This is the volume of package in CC
packageValue | Double | 10 | Optional | This is the value of package
paymentType | String | 40 | Optional | This is the mode of payment. Ex: COD - Cash On Delivery, Prepaid
numberOfItems | Integer | 20 | Optional | This is the number of items in the order.
deliveryType | String | 40 | Optional | In certain operations, there are different skill sets / special delivery requirements through which the Delivery has to take place.<br>For e.g. - Groceries / Food items has to be separated with Toiletries<br>Orders for Cake cannot be clubbed with the Order for Flowers while delivering.<br>In such cases, if you want to classify the orders by using Delivery Type such that these orders get assigned to Pickup Associates who are configured in LogiNext system with these special skill-sets or types, then you can use this field.<br>Please note that before you pass orders with certain Delivery Types, you will have to first configure the Delivery Types.<br>Please ask your Account Manager to set these values for you.
deliveryLocationType | String | 255 | Optional | This parameter if passed helps the Operation Managers / Pickup Associates to know if the Pick location is Residence or Office or Pick-up point, etc.<br>partialDeliveryAllowedFl | String | 50 | Optional | Is Partial Delivery allowed. Ex: Y/N. Default value is N.
returnAllowedFl | String | 1 | Optional | This identifies if order return allowed. Ex: Y/N. Default value is Y.
cancellationAllowedFl | String | 1 | Optional | This identifies if order cancellation is allowed. Ex: Y/N. Default value is Y.
pickupBranch | String | 255 | Mandatory | For Pick-Up type of orders, this is the Branch / Distribution Center / Hub to which the Delivery Associate will Deliver the order / shipment /parcel to.<br>Note that you will have to first Add your Operation Branch / Distribution Center / Hub either through the Add Branch API or through the Add Branch Screen. <br>If you have any access related issue while creating branch, please reach out to your Account Manager
pickupServiceTime | Integer | 11 | Mandatory | This is the time that the Pickup Associate is going to take at the Pickup location to pickup the orders.
pickupStartTimeWindow | Date |  | Mandatory | This is the start date and time for the time slot of the Pickup.<br>Note that this date and time has to be greater than the Order Creation Date and Time.<br>Note that this date and time has to be in UTC.<br>For example - "2017-07-15T11:30:00.000Z
distributionCenter |
pickupEndTimeWindow | Date |  | Mandatory | This is the end date and time for the time slot of the Pickup.<br>Note that this date and time has to be greater than the Pickup Start Date and Time.<br>Note that this date and time has to be in UTC.<br>For example - "2017-07-15T12:30:00.000Z"
pickupAccountCode | String | 255 | Mandatory | This is the pickup account code.
pickupAccountName | String | 255 | Mandatory | This is the pickup account Name.
pickupAddressId | String | 255 | Optional | This is the Address ID of the pickup Customer.
pickupEmail | String | 100 | Optional | This is the email ID of the pickup customer.
pickupPhoneNumber | String | 255 | Optional | This is the phone number of the pickup customer. This field in Non Mandatory in case Customer Profiling in ON.
pickupApartment | String | 512 | Conditional Mandatory | This is the apartment details of the pickup customer. This field in Non Mandatory in case Customer Profiling in ON.
pickupStreetName | String | 512 | Mandatory | This is the street name of the pickup customer. This field in Non Mandatory in case Customer Profiling in ON.
pickupLandmark | String | 512 | Optional | This field holds any landmarks near the pickup location. This field in Non Mandatory in case Customer Profiling in ON.
pickupLocality | String | 512 | Conditional Mandatory | This is the locality of the pickup customer. This field in Non Mandatory in case Customer Profiling in ON.
pickupCity | String | 512 | Conditional Mandatory | This is the city name of the pickup customer. This field in Non Mandatory in case Customer Profiling in ON.
pickupState| String | 512 | This field in Non Mandatory in case Customer Profiling in ON. Mandatory | This is the state name of the pickup customer. Please refer to the list of state codes provided in the "State Codes" section. This field in Non Mandatory in case Customer Profiling in ON.
pickupCountry | String | 512 | Conditional Mandatory | This is the country name of the pickup customer. This field in Non Mandatory in case Customer Profiling in ON.Please refer to the list of country codes provided in the "Country Codes" section.
pickupPinCode | String | 20 | Conditional Mandatory | This is the pincode of the pickup customer. This field in Non Mandatory in case Customer Profiling in ON.
pickupLatitude | Double |  | Optional | This is the geolocation coordinate (latitude) of the pickup customer.
pickupLongitude | Double |  | Optional | The geolocation coordinate (longitude) of the pickup customer.
pickupAddressTimezone | String | | Optional | The timezone of the pickup location. Refer to the timezone codes list to get the full list of values you can pass here. If not passed, the timezone associated with the pickup location will be the branch timezone.
pickupNotes | String | 512 | Optional | Additional pickup comments associated with the order.
deliverNotes | String | 512 | Optional | Additional delivery comments associated with the order.
clientCode | String | 32 | Optional | Using this field you can create orders for sub clients, by passing the sub client name in this field.

#### Request Parameters (Crates)

Param | DataType | Length |  Required | Description
--------- | ------- | ------- | ---------- | ------------
shipmentCrateMappings | Array of objects |  | Optional | Shipment crates
shipmentCrateMappings.crateCd | String | 128 | Mandatory | Crate code.
shipmentCrateMappings.crateAmount | Double |  | Optional | Crate amount
shipmentCrateMappings.crateType | String | 100 | Optional | Type of crate. Ex: cake, juice, sweet, furniture etc.
shipmentCrateMappings.noOfUnits | Integer | 10 | Optional | No. of crate units
shipmentCrateMappings.shipmentlineitems.itemCd | String | 200 | Mandatory | Item code
shipmentCrateMappings.shipmentlineitems.itemName | String | 255 | Optional | Item name
shipmentCrateMappings.shipmentlineitems.itemPrice | Double |  | Mandatory | Item price
shipmentCrateMappings.shipmentlineitems.itemQuantity | Double | 10 | Mandatory | Item quantity
shipmentCrateMappings.shipmentlineitems.itemType | String | 100 | Optional | Item type
shipmentCrateMappings.shipmentlineitems.itemWeight | Double | 10 | Optional | Item weight





### Create Delivery Only

> Definition

```json
https://api.loginextsolutions.com/ShipmentApp/mile/v2/create
```

> Request Body

```json
[
  {
    "orderNo": "GR432U5",
    "awbNumber": "435-16685675",
    "shipmentOrderTypeCd": "DELIVER",
    "orderState": "FORWARD",
    "autoAllocateFl": "N",
    "shipmentOrderDt": "2016-07-15T10:30:00.000Z",
    "distributionCenter": "Chicago",
    "packageWeight":"10",
    "packageVolume": "4500",
    "paymentType": "Prepaid",
    "packageValue": "500",
    "numberOfItems": 1,
    "partialDeliveryAllowedFl": "Y",
    "returnAllowedFl": "Y",
    "cancellationAllowedFl": "N",    
    "deliverBranch": "Boston",
    "deliverServiceTime": "20",
    "deliverEndTimeWindow": "2016-07-18T10:31:00.000Z",
    "deliverStartTimeWindow": "2016-07-16T10:31:00.000Z",
    "deliveryType": "Groceries",
    "deliveryLocationType":"Home",
    "deliverAccountCode": "Matt001",
    "deliverAddressId": "Home",
    "deliverAccountName": "Mathew Richardson",
    "deliverEmail":"m.richardson@testmail.com",
    "deliverPhoneNumber":"3125096995",
    "deliverApartment": "201",
    "deliverStreetName": "E Randolph St",
    "deliverLandmark": "Opp. Chiptole",
    "deliverLocality": "Down Towm Chicago",
    "deliverCity": "Chicago",
    "deliverState": "IL",
    "deliverCountry": "USA",
    "deliverPinCode": "60602",
    "deliverLatitude":41.882702,
    "deliverLongitude":-87.619392, 
    "deliverAddressTimezone":"America/Chicago",   
    "returnBranch": "Chicago",
    "pickupNotes": "PickedUp",
    "deliverNotes": "Delivered",
    "clientCode": "Salestap",
    "shipmentCrateMappings": [
      {
        "crateCd": "CR041",
        "crateAmount":100.65,
        "crateType":"case",
        "noOfUnits":2,
        "shipmentlineitems": [
          {
            "itemCd": "IT043",
            "itemName": "Chicken Soup 2X200gm",
            "itemPrice": 500,
            "itemQuantity": 1,
            "itemType": "soup",
            "itemWeight": 10
          },
          {
            "itemCd": "IT030",
            "itemName": "WholeBeanCoffee 6x1kg",
            "itemPrice": 400,
            "itemQuantity": 2,
            "itemType": "coffee",
            "itemWeight": 10
          }
        ]

      }
    ]
  }
]
```


> Success Response

```json
{
    "status": 200,
    "message": "Order(s) created successfully",
    "data": [
        {
            "index": 0,
            "referenceId": "6a34c7274df0489f97c0f891514b488b",
            "orderNumber": "ww1223",
            "shipmentOrderTypeCd": "DELIVER",
            "orderState": "FORWARD"
        },
        {
            "index": 1,
            "referenceId": "a0108f976b3b41f1b51e438d4e8c7bf5",
            "orderNumber": "ww1225",
            "shipmentOrderTypeCd": "DELIVER",
            "orderState": "FORWARD"
        }
    ],
    "hasError": false
}
```

> Failure Response

```json
{
   "status": 409,
   "message": "",
   "moreResultsExists": false,
   "error": [
       {
           "index": 0,
           "orderNo": "WFQ001",
           "orderState": "FORWARD",
           "shipmentOrderTypeCd": "DELIVER",
           "errorList": [
               {
                   "key": "deliverEndTimeWindow",
                   "message": [
                       "Deliver end-time window is mandatory."
                   ]
               }
           ]
       }
   ],
   "hasError": true
}
```

Create delivery orders with this API in the LogiNext system. Orders will be created and assigned a reference ID that can be used at a leter time to identify the order.

#### Request

<span class="post">POST</span>`https://api.loginextsolutions.com/ShipmentApp/mile/v2/create`

#### Request Parameters

Param | DataType | Length |  Required | Description
--------- | ------- | ---------- | ---------- | ------------
orderNo | String | 100 | Mandatory |  This is the order No.
awbNumber | String  | 1000 | Optional | If you want an AWB no. to be associated with an order, you can pass the same here.
shipmentOrderTypeCd | String  | 40 | Mandatory | This is the order type code. DELIVER for delivery leg order
orderState | String  | 512 | Mandatory | State of order. Ex: FORWARD
autoAllocateFl| String | 50 | Optional | This can be "Y" or "N". If set to "Y", the Order will be automatially allocated to the nearest Delivery Associate when it is created in the system. If "N", the Delivery Associate will get notified if the Order is ready to be allocated to them, and they can choose to Accept or Reject it.<br>Pass this Flag as 'P' if you want to assign the newly created Order to an existing planned trip. This assignment event can impact the sequence of Order previously created for that trip.
shipmentOrderDt | Date |  | Mandatory | Order Date Format - YYYY-MM-DDTHH:MM:SS.SSSZ e.g. : 2016-07-01T11:18:00.000Z.
distributionCenter | String | 255 | Mandatory | This is the distribution center's name
packageWeight | Double | 10 | Optional | This is the weight of package in Kg.
packageVolume | Double | 10 | Optional | This is the volume of package in CC
packageValue | Double | 10 | Optional | This is the value of package
numberOfItems | Integer | 20 | Optional | This is the number of crates
paymentType | String | 40 | Optional | This is the payment mode. Ex: COD - Cash On Delivery, Prepaid
partialDeliveryAllowedFl | String | 50 | Optional | This is the is Partial Delivery allowed. Ex: Y/N. Default value is N.
returnAllowedFl | String | 1 | Optional | This field specifies if the order can be returned. Ex: Y/N. Default value is Y.
cancellationAllowedFl | String | 1 | Optional | Is Cancellation allowed. Ex: Y/N. Default value is Y.
deliverBranch | String | 255 | Mandatory | Name of delivery branch
deliverServiceTime | Integer | 11 | Mandatory | Deliver service time in mins.
deliverStartTimeWindow | Date |  | Mandatory | Deliver start time window. Format - YYYY-MM-DDTHH:MM:SS.SSSZ e.g. : 2016-07-01T11:18:00.000Z.
deliverEndTimeWindow | Date |  | Mandatory | Deliver end time window. Format - YYYY-MM-DDTHH:MM:SS.SSSZ. For example - 2016-07-01T11:18:00.000Z.
deliveryType | String | 40 | Optional | Order delivery type. For example - ‘Groceries’ for grocery type of Orders
deliveryLocationType | String | 40 | Optional | Type of delivery location. For example - CUSTOMER
deliverAccountCode | String | 255 | Mandatory | This is the customer code of the deliver customer.
deliverAddressId | String |255 | Optional | This is the Address ID of the deliver customer.
deliverAccountName | String | 255 | Conditional Mandatory | This is the deliver account name. This field in Non Mandatory in case Customer Profiling in ON.
deliverEmail | String | 100 | Optional | This is the email ID details of the customer.
deliverPhoneNumber | String | 255 | Optional | This is the phone number of the delivery customer.
deliverApartment | String | 512 | Conditional Mandatory | This is the apartment details of the delivery customer. This field in Non Mandatory in case Customer Profiling in ON.
deliverStreetName | String | 512 | Conditional Mandatory | This is the street name of the delivery customer.
deliverLandmark | String | 512 | Optional | This field holds any identifying landmark's around the customer's address.
deliverLocality | String | 512 | Conditional Mandatory | This is the locality of the delivery customer. This field in Non Mandatory in case Customer Profiling in ON.
deliverCity | String | 512 | Conditional Mandatory | This is the city name of the delivery customer. This field in Non Mandatory in case Customer Profiling in ON.
deliverState| String | 512 | Conditional Mandatory | This is the state code of the delivery customer. Please refer to the list of state codes provided in the "State Codes" section. This field in Non Mandatory in case Customer Profiling in ON.
deliverCountry | String | 512 | Conditional Mandatory | This is the country code of the delivery customer. Please refer to the list of country codes provided in the "Country Codes" section. This field in Non Mandatory in case Customer Profiling in ON.
deliverPinCode | String | 20 | Conditional Mandatory | This is the pincode of the delivery customer. This field in Non Mandatory in case Customer Profiling in ON.
deliverLatitude | Double |  | Optional | The geolocation coordinate (latitude) of the delivery customer.
deliverLongitude | Double |  | Optional | The geolocation coordinate (longitude) of the delivery customer.
deliverAddressTimezone | String | | Optional | The timezone of the pickup location. Refer to the timezone codes list to get the full list of values you can pass here. If not passed, the timezone associated with the pickup location will be the branch timezone.
returnBranch | String | 255 | Mandatory | Name of return branch.
pickupNotes | String | 512 | Optional | Additional pickup comments associated with the order.
deliverNotes | String | 512 | Optional | Additional delivery comments associated with the order.
clientCode | String | 32 | Optional | Using this field you can create orders for sub clients, by passing the sub client name in this field.

#### Request Parameters (Crates)

Param | DataType | Length |  Required | Description
--------- | ------- | ------- | ---------- | ------------
shipmentCrateMappings | Array of objects |  | Optional | These are the order crates.
shipmentCrateMappings.crateCd | String | 128 | Mandatory | This is the crate code for a crate.
shipmentCrateMappings.crateAmount | Double |  | Mandatory | This is the crate amount for a crate.
shipmentCrateMappings.crateType | String | 100 | Mandatory | Crate type.
shipmentCrateMappings.noOfUnits | Integer | 10 | Mandatory | This is the Number of items in the crate.
shipmentCrateMappings.shipmentlineitems.itemCd | String | 200 | Mandatory | This is the crate item code.
shipmentCrateMappings.shipmentlineitems.itemName | String | 255 | Optional | This is the crate item name.
shipmentCrateMappings.shipmentlineitems.itemPrice | Double |  | Mandatory | This is the crate item price.
shipmentCrateMappings.shipmentlineitems.itemQuantity | Double | 10 | Mandatory | This is the crate item quantity.
shipmentCrateMappings.shipmentlineitems.itemType | String | 100 | Optional | This is the crate item type.
shipmentCrateMappings.shipmentlineitems.itemWeight | Double | 10 | Optional | This is the crate item weight.




### Create Pickup & Delivery

> Definition

```json
https://api.loginextsolutions.com/ShipmentApp/mile/v2/create
```

> Request Body

```json
[
  {
    "orderNo": "GR432U5",
    "awbNumber": "435-16685675",
    "shipmentOrderTypeCd": "BOTH",
    "orderState": "FORWARD",
    "autoAllocateFl": "N",
    "shipmentOrderDt": "2016-07-15T10:30:00.000Z",
    "distributionCenter": "Down Town Chicago",
    "packageWeight":"10",
    "packageVolume": "4500",
    "paymentType": "Prepaid",
    "packageValue": "5000",
    "numberOfItems": 1,
    "partialDeliveryAllowedFl": "Y",
    "returnAllowedFl": "Y",
    "cancellationAllowedFl": "N",    
    "deliverBranch": "Boston",
    "deliverServiceTime": "20",
    "deliverEndTimeWindow": "2016-07-18T10:31:00.000Z",
    "deliverStartTimeWindow": "2016-07-16T10:31:00.000Z",
    "deliveryType": "Groceries",
    "deliveryLocationType":"Home",
    "deliverEmail":"m.richardson@testmail.com",
    "deliverPhoneNumber":"9891234567",
    "deliverAccountCode": "Matt001",
    "deliverAddressId": "home",
    "deliverAccountName": "Mathew Richardson",
    "deliverApartment": "201",
    "deliverStreetName": "E Randolph St",
    "deliverLandmark": "Opp. Chiptole",
    "deliverLocality": "Down Towm Chicago",
    "deliverCity": "Chicago",
    "deliverState": "IL",
    "deliverCountry": "USA",
    "deliverPinCode": "60602",
    "deliverLatitude":41.882702,
    "deliverLongitude":-87.619392,   
    "deliverAddressTimezone":"America/Chicago",  
    "pickupBranch":"East Manhattan",
    "pickupServiceTime": "50",
    "pickupStartTimeWindow": "2016-07-16T14:24:00.000Z",
    "pickupEndTimeWindow": "2016-07-17T14:24:00.000Z",
    "pickupEmail":"james.w@ablogs.com",
    "pickupPhoneNumber": "5163063377",
    "pickupAccountCode": "jim001",
    "pickupAddressId": "Home",
    "pickupAccountName": "James Walker",
    "pickupApartment": "901",
    "pickupStreetName": "2142 3rd Ave",
    "pickupLandmark": "Opp. McDonalds",
    "pickupLocality": "East Harlem",
    "pickupCity": "New York",
    "pickupState": "NY",
    "pickupCountry": "USA",
    "pickupPinCode": "10035",
    "pickupLatitude":40.760838,
    "pickupLongitude":-73.96732299999996,  
    "pickupAddressTimezone":"America/New_York",  
    "returnBranch": "East Manhatten",
    "returnStartTimeWindow": "2016-05-18T03:00:00.000Z",
    "returnEndTimeWindow": "2016-05-18T16:00:00.000Z",
    "returnAccountCode": "jim001",
    "returnAddressId": "Home",
    "returnAccountName": "James Walker",
    "returnEmail": "james.w@ablogs.com",
    "returnPhoneNumber": "9891234567",
    "returnApartment": "901",
    "returnStreetName": "2142 3rd Ave",
    "returnLandmark": "OOpp. McDonalds",
    "returnLocality": "East Harlem",
    "returnCity": "New York",
    "returnState": "NY",
    "returnCountry": "USA",
    "returnPinCode": "10035",
    "pickupNotes": "PickedUp",
    "deliverNotes": "Delivered",
    "clientCode": "Salestap",
    "shipmentCrateMappings": [
      {
        "crateCd": "CR121",
        "crateAmount":100.65,
        "crateType":"case",
        "noOfUnits":10,
        "shipmentlineitems": [
          {
            "itemCd": "IT043",
            "itemName": "Chicken Soup 2X200gm",
            "itemPrice": 500,
            "itemQuantity": 3,
            "itemType": "soup",
            "itemWeight": 10
          },
          {
            "itemCd": "IT030",
            "itemName": "WholeBeanCoffee 6x1kg",
            "itemPrice": 400,
            "itemQuantity": 1,
            "itemType": "coffee",
            "itemWeight": 10
          }
        ]

      }
    ]
  }
]
```



> Success Response

```json
{
    "status": 200,
    "message": "Order(s) created successfully",
    "data": [
        {
            "index": 0,
            "referenceId": "6a34c7274df0489f97c0f891514b488b",
            "orderNumber": "ww1223",
            "shipmentOrderTypeCd": "BOTH",
            "orderState": "FORWARD"
        },
        {
            "index": 1,
            "referenceId": "a0108f976b3b41f1b51e438d4e8c7bf5",
            "orderNumber": "ww1225",
            "shipmentOrderTypeCd": "BOTH",
            "orderState": "FORWARD"
        }
    ],
    "hasError": false
}

```

> Failure Response

```json
{
   "status": 409,
   "message": "",
   "moreResultsExists": false,
   "error": [
       {
           "index": 0,
           "orderNo": "HYN001",
           "orderState": "FORWARD",
           "shipmentOrderTypeCd": "BOTH",
           "errorList": [
               {
                   "key": "returnBranch",
                   "message": [
                       "Return Branch name is mandatory."
                   ]
               }
           ]
       }
   ],
   "hasError": true
}

```

Create pickup and delivery orders with this API in the LogiNext system. Orders will be created and assigned a reference ID that can be used at a leter time to identify the order.

#### Request

<span class="post">POST</span>`https://api.loginextsolutions.com/ShipmentApp/mile/v2/create`


#### Request Parameters

Param | DataType | Length |  Required | Description
--------- | ------- | ------- | ---------- | ------------
orderNo | String | 100 | Mandatory |  This is the order No.
awbNumber | String | 1000 | Optional | This is the airway Bill No.
shipmentOrderTypeCd | String | 40 | Mandatory | This is the order type code. BOTH for pickup & delivery leg order
autoAllocateFl| String | 50 | Optional | This can be "Y", "N", or "P". If set to "Y", the Order will be automatially allocated to the nearest Delivery Associate when it is created in the system. If "N", the Delivery Associate will get notified if the Order is ready to be allocated to them, and they can choose to Accept or Reject it.<br>Pass this Flag as 'P' if you want to assign the newly created Order to an existing planned trip. This assignment event can impact the sequence of Order previously created for that trip.
orderState | String | 512 | Mandatory | This is the state of order. Ex: FORWARD
shipmentOrderDt | Date |  | Mandatory | This is the order Date. Format - YYYY-MM-DDTHH:MM:SS.SSSZ e.g. : 2016-07-01T11:18:00.000Z.
distributionCenter | String | 255 | Mandatory | This is the distribution center's name
packageWeight | Double | 10 | Optional | This is the weight of package in Kg.
packageVolume | Double | 10 | Optional | This is the volume of package in CC
packageValue | Double | 10 | Optional | This is the value of package
numberOfItems | Integer | 20 | Optional | This is the number of crates
paymentType | String | 40 | Mandatory | This is the mode of payment. Ex: COD - Cash On Delivery, Prepaid
partialDeliveryAllowedFl | String | 50 | Optional | This field indicates if partial Delivery allowed. Ex: Y/N
returnAllowedFl | String | 1 | Optional | This field indicates if return is allowed. Ex: Y/N
cancellationAllowedFl | String | 1 | Optional | This field indicates if cancellation is allowed. Ex: Y/N
deliverBranch | String | 255 | Mandatory | Name of delivery branch
deliverServiceTime | Integer | 11 | Mandatory | Deliver service time in mins.
deliverStartTimeWindow | Date |  | Mandatory | Deliver start time window. Format - YYYY-MM-DDTHH:MM:SS.SSSZ e.g. : 2018-07-01T11:18:00.000Z.
deliverEndTimeWindow | Date |  | Mandatory | Deliver end time window. Format - YYYY-MM-DDTHH:MM:SS.SSSZ. For example - 2018-07-01T11:18:00.000Z.
deliveryType | String | 40 | Optional | Order delivery type. For example - ‘Groceries’ for grocery type of Orders.
deliveryLocationType | String | 40 | Optional | Type of delivery location. For example -  ‘CUSTOMER’.
deliverAccountCode | String | 255 | Mandatory | Customer ID of the Delivery Customer.
deliverAccountName | String | 255 | Conditional Mandatory | Deliver account name. This field in Non Mandatory in case Customer Profiling in ON.
deliverEmail| String | 100 | Optional | Email of the customer
deliverPhoneNumber| String | 255 | Optional | Phone number of the customer
deliverApartment | String | 512 | Conditional Mandatory | This is the delivery customer location's apartment details. This field in Non Mandatory in case Customer Profiling in ON.
deliverStreetName | String | 512 | Conditional Mandatory | This is the delivery customer location's Street name. This field in Non Mandatory in case Customer Profiling in ON.
deliverLandmark | String | 512 | Optional | This is the delivery customer location's Landmark.
deliverLocality | String | 512 | Conditional Mandatory | This is the delivery customer location's Locality. This field in Non Mandatory in case Customer Profiling in ON.
deliverCity | String | 512 | Conditional Mandatory | This is the delivery customer location's City. This field in Non Mandatory in case Customer Profiling in ON.
deliverState| String | 512 | Conditional Mandatory | This is the delivery customer location's state code. This field in Non Mandatory in case Customer Profiling in ON.
deliverCountry | String | 512 | Conditional Mandatory | This is the delivery customer location's country code. This field in Non Mandatory in case Customer Profiling in ON.
deliverPinCode | String | 20 | This field in Non Mandatory in case Customer Profiling in ON. Mandatory | This is the delivery customer location's Pincode. This field in Non Mandatory in case Customer Profiling in ON.
deliverLatitude | Double | 100 | Optional | The geolocation coordinate (latitude) of the delivery customer.
deliverLongitude | Double | 100 | Optional | The geolocation coordinate (latitude) of the delivery customer.
deliverAddressTimezone | String | | Optional | The timezone of the delivery location. Refer to the timezone codes list to get the full list of values you can pass here. If not passed, the timezone associated with the deliver location will be the branch timezone.
deliverNotes | String | 512 | Optional | Additional delivery comments associated with the order
pickupBranch | String | 255 | Mandatory | Name of pickup branch
pickupServiceTime | Integer | 11 | Mandatory | Pickup service time in mins.
pickupStartTimeWindow | Date |  | Mandatory | Pickup start time window. Format - YYYY-MM-DDTHH:MM:SS.SSSZ e.g. : 2016-07-01T11:18:00.000Z.
pickupEndTimeWindow | Date |  | Mandatory | Pickup end time window. Format - YYYY-MM-DDTHH:MM:SS.SSSZ e.g. : 2016-07-01T11:18:00.000Z.
pickupAccountCode | String | 255 | Mandatory | Pickup account code
pickupAccountName | String | 255 | Conditional Mandatory | Pickup account name. This field in Non Mandatory in case Customer Profiling in ON.
pickupEmail| String | 100 | Optional | Email of the merchant
pickupPhoneNumber| String | 255 | Optional | Phone number of the merchant
pickupApartment | String | 512 | Conditional Mandatory | This is the pickup location's apartment. This field in Non Mandatory in case Customer Profiling in ON.
pickupStreetName | String | 512 | Conditional Mandatory | This is the pickup location's street name. This field in Non Mandatory in case Customer Profiling in ON.
pickupLandmark | String | 512 | Optional | This is the pickup location's  landmark.
pickupLocality | String | 512 | Conditional Mandatory | This is the pickup location's locality. This field in Non Mandatory in case Customer Profiling in ON.
pickupCity | String | 512 | Conditional Mandatory | This is the pickup location's city. This field in Non Mandatory in case Customer Profiling in ON.
pickupState| String | 512 | Conditional Mandatory | This is the pickup location's state code. This field in Non Mandatory in case Customer Profiling in ON.
pickupCountry | String | 512 | Conditional Mandatory | This is the pickup location's country code. This field in Non Mandatory in case Customer Profiling in ON.
pickupPinCode | String | 20 | Conditional Mandatory | This is the pickup location's pincode. This field in Non Mandatory in case Customer Profiling in ON.
pickupLatitude | Double |  | Optional | The geolocation coordinate (latitude) of the pickup location.
pickupLongitude | Double |  | Optional | The geolocation coordinate (longitude) of the pickup location.
pickupAddressTimezone | String | | Optional | The timezone of the pickup location. Refer to the timezone codes list to get the full list of values you can pass here. If not passed, the timezone associated with the pickup location will be the branch timezone.
pickupNotes | String | 512 | Optional | Additional pickup comments associated with the order
returnBranch | String | 255 | Mandatory | Name of return branch
returnStartTimeWindow | Date |  | Mandatory | Return start time window. Format - YYYY-MM-DDTHH:MM:SS.SSSZ e.g. : 2016-07-01T11:18:00.000Z.
returnEndTimeWindow | Date |  | Mandatory | Return end time window. Format - YYYY-MM-DDTHH:MM:SS.SSSZ e.g. : 2016-07-01T11:18:00.000Z.
returnAccountCode | String | 255 | Mandatory | Return account code
returnAccountName | String | 255 | Mandatory | Return account name
returnEmail | String | 100 | Conditional Mandatory | Return account code. This field in Non Mandatory in case Customer Profiling in ON.
returnPhoneNumber | String | 255 | Conditional Mandatory | Return account name. This field in Non Mandatory in case Customer Profiling in ON.
returnApartment | String | 512 | Conditional Mandatory | This is the return location's Apartment. This field in Non Mandatory in case Customer Profiling in ON.
returnStreetName | String | 512 | Conditional Mandatory | This is the pickup location's street name. This field in Non Mandatory in case Customer Profiling in ON.
returnLandmark | String | 512 | Optional | This is the pickup location's landmark.
returnLocality | String | 512 | Conditional Mandatory | This is the pickup location's locality. This field in Non Mandatory in case Customer Profiling in ON.
returnCity | String | 512 | Conditional Mandatory | This is the pickup location's city. This field in Non Mandatory in case Customer Profiling in ON.
returnState| String | 512 | Conditional Mandatory | This is the pickup location's state code. Please refer to the list of state codes provided in the "State Codes" section. This field in Non Mandatory in case Customer Profiling in ON.
returnCountry | String | 512 | Conditional Mandatory | This is the pickup location's country code. Please refer to the list of country codes provided in the "Country Codes" section. This field in Non Mandatory in case Customer Profiling in ON.
returnPinCode | String | 20 | Conditional Mandatory | Return Pincode. This field in Non Mandatory in case Customer Profiling in ON.
clientCode | String | 32 | Optional | Using this field you can create orders for sub clients, by passing the sub client name in this field.


#### Request Parameters (Crates)

Param | DataType | Length |  Required | Description
--------- | ------- | ------- | ---------- | ------------
shipmentCrateMappings | Array of objects |  | Optional | These are the order crates.
shipmentCrateMappings.crateCd | String | 128 | Mandatory | This is the crate code for a crate.
shipmentCrateMappings.crateAmount | Double |  | Mandatory | This is the crate amount for a crate.
shipmentCrateMappings.crateType | String | 100 | Mandatory | Crate type.
shipmentCrateMappings.noOfUnits | Integer | 10 | Mandatory | This is the Number of items in the crate.
shipmentCrateMappings.shipmentlineitems.itemCd | String | 200 | Mandatory | This is the crate item code.
shipmentCrateMappings.shipmentlineitems.itemName | String | 255 | Optional | This is the crate item name.
shipmentCrateMappings.shipmentlineitems.itemPrice | Double |  | Mandatory | This is the crate item price.
shipmentCrateMappings.shipmentlineitems.itemQuantity | Double | 10 | Mandatory | This is the crate item quantity.
shipmentCrateMappings.shipmentlineitems.itemType | String | 100 | Optional | This is the crate item type.
shipmentCrateMappings.shipmentlineitems.itemWeight | Double | 10 | Optional | This is the crate item weight.





### Create Order Multi Stop

> Definition

```json
https://api.loginextsolutions.com/ShipmentApp/mile/v2/multidestination/create
```

> Request Body

```json
[{
  "parentOrderNo":"DN987679",
  "awbNumber": "VC7",
  "shipmentOrderDt": "2018-01-10T10:00:00.000Z",
  "autoAllocateFl": "N",
  "shipmentOrderTypeCd": "DELIVER",
  "orderState": "FORWARD",
  "shipmentBranch": "East Manhattan",
  "returnAllowedFl": "Y",
  "cancellationAllowedFl": "N",
  "returnBranch": "East Manhattan",
  "pickupNotes": "PickedUp",
  "optimiseOrderSequenceFl":"N",
  "backToOriginFl": "N",
  "endTimeWindow": "2018-01-17T09:20:00.000Z",
  "startTimeWindow": "2018-01-17T06:30:00.000Z",
  "destinations": [
    {
      "orderNo": "DNC987679" ,
      "packageWeight": "10",
      "packageVolume": "450",
      "paymentType": "Prepaid",
      "deliverServiceTime": "10",
      "packageValue": "100",
      "numberOfItems": "1",
      "partialDeliveryAllowedFl": "Y",
      "deliveryLocationType": "Groceries",
      "deliverAccountCode": "LO0981",
      "deliverAccountName": "Dest User 1",
      "deliverEmail": "james.w@ablogs.com",
      "deliverPhoneNumber": "5163063377",
      "deliverApartment": "901",
      "deliverStreetName": "2142 3rd Ave",
      "deliverLandmark": "Opp. McDonalds",
      "deliverLocality": "Downtown Manhattan",
      "deliverCity": "New York",
      "deliverState": "NY",
      "deliverCountry": "USA",
      "deliverPinCode": "10035",
      "deliverLatitude": 40.760838,
      "deliverLongitude": -73.96732299999996,
      "deliverNotes": "Delivered",
      "shipmentCrateMappings": [
        {
          "crateCd": "CRATE001",
          "crateAmount": 100.65,
          "crateType": "case",
          "noOfUnits": 1,
          "shipmentlineitems": [
            {
            "itemCd": "1_120000256",
            "itemName": "Bourbon 2x400gm",
            "itemPrice": 12,
            "itemQuantity": 12,
            "itemType": "Biscuit",
            "itemWeight": 50
          }
        ]
        }
      ]
    }
]
}
]

```

> Response

```json
{
    "status": 200,
    "message": "Add Orders to manifest success.",
    "data": {
        "manifestId": "hcgsyuc334"
    },
    "hasError": false
}
```

Create single Pick Up and multiple destination type orders with this API in the LogiNext system. Orders will be created and assigned a reference ID that can be used at a leter time to identify the order.

This API can also be used for single Pick Up location and single destinaton.


#### Request

<span class="post">POST</span>`https://api.loginextsolutions.com/ShipmentApp/mile/v2/multidestination/create`


#### Request Body

Parameter | DataType | Length |  Required | Description
-----------|-------| ------- |------- | ----------
clientCode | String |255 | Optional | The account for which the Order is being created.
parentOrderNo | String | 255 | Mandatory | This is the Order No.
awbNumber | String | 1000 | Optional | If you want a AWB no. to be associated with an order, you can pass the same here.
shipmentOrderDt | String | | Mandatory | The date and time on which the order is created.<br>Note that this date and time has to be in UTC.<br>For example - "2017-07-15T10:30:00.000Z"
shipmentOrderTypeCd| String | 10 | Mandatory | The value in this field has to be "DELIVER" always.
orderState| String | 10 | Mandatory | If an order is a Forward way (Delivery to the Customer), then value here should be "FORWARD"<br>If an order is a Retrun way (Return from the Customer), then value here should be "REVERSE"
deliverStartTimeWindow| String | | Mandatory | This is the start date and time for the time slot of the Delivery.<br>Note that this date and time has to be greater than the Order Creation Date and Time.<br>Note that this date and time has to be in UTC.<br>For example - "2017-07-15T11:30:00.000Z<br><br>If the you set the auto allocation flag  "autoAllocateFl" as "Y", then the Pick-up start Date and Time is also taken as the  same.<br>If the you set the auto allocation flag  "autoAllocateFl" as "N", then the Pick-up Date and Time is NOT set.
deliverEndTimeWindow| String | | Mandatory | This is the end date and time for the time slot of the Delivery.<br>Note that this date and time has to be greater than the Delivery Start Date and Time.<br>Note that this date and time has to be in UTC.<br>For example - "2017-07-15T12:30:00.000Z"<br><br>If you set the auto allocation flag  "autoAllocateFl" as "Y", then the Pick-up end Date and Time is also taken as the  same.<br>If you set the auto allocation flag  "autoAllocateFl" as "N", then the Pick-up Date and Time is NOT set.
deliveryType| String | 40 | Optional | This is an Optional Field. You can choose to leave it blank.<br>In certain operations, there are different skill sets / special delivery requirements through which the Delivery has to take place.<br>For e.g. - Groceries / Food items has to be seperated with Toileteries<br>Orders for Cake cannot be clubbed with the Order for Flowers while delivering.<br><br>In such cases, if you want to classify the orders by using Delivery Type such that these orders get assigned to Delivery Associates who are configured in LogiNext system with these special skill-sets or types, then you can use this field.<br>Please note that before you pass orders with certain Delivery Types, you will have to first configure the Delivery Types.<br>Please ask your Account Manager to set these values for you.
shipmentBranch| String | 255 | Mandatory | For Pick-Up type of orders, this is the Branch / Distribution Center / Hub to which the Delivery Associate will Deliver the order / shipment /parcel to.<br>For Delivery type of orders, this is the Branch / Distribution Center / Hub from where the Delivery Associate will pick-up the order / shipment / parcel and deliver it to the end customer.<br><br>Note that you will have to first Add your Operation Branch / Distribution Center / Hub either through the Add Branch API or through the Add Branch Screen.<br>If you have any access related issue while creating branch, please reach out to your Account Manager
returnAllowedFl| String | 1 | Optional | If your Business process allows the customer to return the orders back to you, then you will have to mark this Flag as  "Y". This way your OMS / WMS / ERP system(integrated with LogiNext system) or you Operations Manager will be able to create a return request for an order.<br>If you mark this flag as "N", LogiNext system will not allow you to create a return request referencing to this order.<br><br>You will always have any option to create a new order all-together for Returns by passing "REVERSE" in the "orderState" field.<br>If you have not set this Flag, it will be defaulted to "N"
cancellationAllowedFl| String | 1 | Optional | If your Business process allows the customer to cancel the orders before it is delivered to their doorstep, then you will have to mark this Flag as "Y". This way your OMS / WMS / ERP system(integrated with LogiNext system) or you Operations Manager will be able to cancel an order.<br>If you mark this flag as "N", LogiNext system will not allow you to cancel an order.<br><br>If you have not set this Flag, it will be defaulted to "N"
returnBranch| String | 255 | Conditional Mandatory | If the "returnAllowedFl" is marked as "Y", then this is mandatory.<br>Else this this optional and you can choose to leave it blank.<br>For Pick-Up type of orders, this is the Branch / Distribution Center / Hub to which the Delivery Associate will return the orders to. This is generally the Merchant's / Seller's Branch / Hub form where the shipment / parcel was picked up.<br>For Delivery type of orders, this is the Branch / Distribution Center / Hub where the Delivery Associate will have to bring back the shipment / parcel to.  <br>Note that you will have to first Add your Operation Branch / Distribution Center / Hub either through the Add Branch API or through the Add Branch Screen. <br>If you have any access related issue while creating branch, please reach out to your Account Manager
pickupNotes| String | 100 | Optional | You can enter instructions (if any) for the Delivery Associate while picking-up the order.
autoAllocateFl| String | 1 | Mandatory | Pass this Flag as "Y" If you add any order which needs to be allocated automatically to the logged-in Delivery Associate.<br>Pass this Flag as "N" If you add any order which you want to allocate manually to the Delivery Associate OR<br>If you want to run the Route optimization on the set of orders and want system to identify the Delivery Associates.<br>Pass this Flag as 'P' if you want to assign the newly created Order to an existing planned trip. This assignment event can impact the sequence of Order previously created for that trip.
optimiseOrderSequenceFl| String | 1 | Mandatory | This flag is to be used only if you have Multi- Destination Orders.<br>If you set this Flag as "N", system would plan the Delivery routes by keeping the sequence of the Orders same as what you have supplied.<br>If you set this Flag as "Y", system would optimize the route and re-arrange the sequence in which Order needs to be delivered.
backToOrigin| String | 1 | Mandatory | If you want the Pick-up Branch from where the Delivery Associate has picked-up the order / shipment / parcel to be the last Destination, then set this Flag as "Y" else set this flag as "N"
destinations| List | | Mandatory | Array - This is the list of orders and its information.
orders.orderNo| String | 255 | Conditional Mandatory | This is the Order No.<br>In case of Single Destination, this Order No. is same as the Parent Order No. It is mandatory.<br>In case of Multi -Destination, this Order No. should not be same as the Parent Order No.<br>In this case, it is order no. for each destination.<br>If you do not have a separate order for each destination, you can leave it blank.<br>LogiNext will generate Order No. with the format - Parent_Order_No_1, Parent_Order_No_2, etc.
orders.deliverySequence| String | 1 | Mandatory | In case of Single Destination, this is to be "1" always.<br>In case of Multi-destination, this is the sequence that you want the order to be delivered in.
orders.packageWeight| String | 10 | Optional | This is an optional field. You can choose to leave it blank.<br>If you have any package weight that needs to be specified to the Delivery Associate, you can pass the value here as a FYI.<br>Also, LogiNext system allows you to configure the capacity (weight) of Delivery Associate. If particular capacity (weight) of an order is specified in this field, then the order will get assigned to the Delivery Associate whose capacity is greater than or equal to this capacity.
orders.packageVolume| String | 10 | Optional | This is an optional field. You can choose to leave it blank.<br>If you have any package volume that needs to be specified to the Delivery Associate, you can pass the value here as a FYI.<br>Also, LogiNext system allows you to configure the capacity (volume) of Delivery Associate. If particular capacity (volume) of an order is specified in this field, then the order will get assigned to the Delivery Associate whose capacity is greater than or equal to this capacity.<br>Note that volume here is overall cubic volume (L*B*H)
orders.paymentType| String | 10 | Mandatory | If an order value is already paid by the customer through online payment or wallet, etc. then the value here should be "PREPAID".<br>If the customer is going to pay for the order at the doorstep, then the value here should be "COD".<br>Note that COD either means Cash on Delivery or Card on Delivery.<br>If your Delivery Associates use mPOS devices for accepting Card on Delivery and you want it to integrate with LogiNext TrackNext App., you can raise integration request with your Account Manager.
orders.packageValue| String | 10 | Conditional Mandatory | If the payment type is "PREPAID", then this can be optional.<br>If the payment type is "COD", then this is mandatory to be passed. This is the total amount that the Delivery Associate has to collect from the Customer.
orders.numberOfItems| String | 255 | Conditional Mandatory | LogiNext system allows you to set your account as either of three level of Order Hierarchy - <br>1. Only Order - Single parcel, document, shipment.<br>2. Order and Crates - Single Shipment Bag and the items in that Shipment bag.<br>3. Order, Crate and Line Items - Single Shipment bag having multiple crates and each crate having multiple items.<br><br>If your account type is set to pass only orders, then this field is optional. <br>You can pass the no. of items (if any)  to let the delivery associate know as a FYI.<br>But, if your account is configured to have Order &  Crates Hierarchy or Order, Crates * Line Items Hierarchy, then it is mandatory for you pass the number of items and it should be equal to the number of Crates.
orders.deliverServiceTime| String | 10 | Mandatory | In minutes. This is the time that the Delivery Associate is going to take at the Customer's doorstep to deliver the orders.
orders.deliveryLocationType| String | 50 | Optional | This is an optional field. You can choose to leave it blank.<br>This parameter if passed helps the Operation Managers / Delivery Associates to know if the Customer location is Residence or Office or Pick-up point, etc.
orders.partialDeliveryAllowedFl| String | 1 | Optional | This is an optional field. You can choose to leave it blank.<br>If you Business operations allow to deliver partial orders to the customers, then set this flag as "Y". <br>This flag is applicable only when your order Hierarchy Model is either Order & Crates or Oder, Crates & Line items
orders.deliverAccountCode| String | 255 | Mandatory | LogiNext system allows you to set your Customer's addresses with unique address Id so that you do not have to send the Address parameters with every Order.<br>Customer's Address ID is mandatorily required to be set though this field.
orders.deliverAccountName| String | 255 | Mandatory | LogiNext system allows you to set your Customer's addresses with unique address Id so that you do not have to send the Address parameters with every Order.<br>Customer's Address Name is mandatorily required to be set though this field.
orders.deliverEmail| String | 100 | Optional | This is an optional field. You can choose to leave it blank.<br>If you want to send any Order related notifications to the Customer's email Address, please pass the Customer's Email address.
orders.deliverPhoneNumber| String | 100 | Optional | This is an optional field. You can choose to leave it blank.<br>If you want to send any Order related notifications to the Customer through the SMS or you allow the delivery associate to call your customers directly, please pass the Customer Phone no.
orders.deliverApartment| String | 512 | Conditional Mandatory | If you have the Customer Profiling set to allow the LogiNext to select the Address based on the Account Code passed, then this field is optional.<br>If you have the Lat. and Long of the Customer, then this fields is optional.<br><br>If you are passing the value in this field, then - <br>This is Address Line 1.<br>This is the Apartment Name / House Name / Building Name / Suite No.<br>For example - A 901 Supreme Business Center
orders.deliverStreetName| String | 512 | Conditional Mandatory | If you have the Customer Profiling set to allow the LogiNext to select the Address based on the Account Code passed, then this field is optional.<br>If you have the Lat. and Long of the Customer, then this fields is optional.<br>If you are passing the value in this field, then - <br>This is Address Line 2.<br>This is the name of the Street where the Customer's / Delivery location is present.<br>For example - Walton Boulevard
orders.deliverLandmark| String | 512 | Optional | Any nearby landmark to identify your Customer Address<br>For example - Opp. McDonalds or Behind Mercy Hospital<br>Orders.deliverLocality| String | 255 | Conditional Mandatory | If you have the Customer Profiling set to allow the LogiNext to select the Address based on the Account Code passed, then this field is optional.<br>If you have the Lat. and Long of the Customer, then this fields is optional.<br>If you are passing the value in this field, then -<br>This is area or locality in which the is Customer's address is located<br>For example - Southern Industry Park or Dubai Downtown<br>If you think that your specific region in which you operate does not have localities, then please raise the support request with your Account Manager to make this non-mandatory
orders.deliverCity| String | 512 | Conditional Mandatory | If you have the Customer Profiling set to allow the LogiNext to select the Address based on the Account Code passed, then this field is optional.<br>If you have the Lat. and Long of the Customer, then this fields is optional.<br>If you are passing the value in this field, then - <br>This is name of the city.<br>For example - Atlanta or Kuala Lampur
orders.deliverState| String | 3 | Conditional Mandatory | If you have the Customer Profiling set to allow the LogiNext to select the Address based on the Account Code passed, then this field is optional.<br>If you have the Lat. and Long of the Customer, then this fields is optional.<br>If you are passing the value in this field, then - <br>This is code of State / Province.<br>For example - For Georgia use GA ; For Jawa Barat use JB<br><br>Please refer to the section where we have listed down state codes for each country.<br>If you think that your specific region in which you operate does not have States / Provinces, then please raise the support request with your Account Manager to make this non-mandatory.
orders.deliverCountry| String | 3 | Conditional Mandatory | If you have the Customer Profiling set to allow the LogiNext to select the Address based on the Account Code passed, then this field is optional.<br>If you have the Lat. and Long of the Customer, then this fields is optional.<br>If you are passing the value in this field, then - <br>This is code of Country.<br>Sample Value - For India use IND; For China use CHN<br>Please refer to the section where we have listed down country codes.
orders.deliverPinCode| String | 255 | Conditional Mandatory | If you have the Customer Profiling set to allow the LogiNext to select the Address based n the Account code passed, then this field is optional<br>If you have the Lat. and Long of the Customer, then this fields is optional.<br>This is the postal code / zip code of the area.<br>Sample Value - 72712 ; 400076<br>If you think that your specific region in which you operate does not have postal codes, then please raise the support request with your Account Manager to make this non-mandatory.
orders.deliverLatitude| String |  | Conditional Mandatory | If you are passing the Customer Address, then this field is optional or <br>If you have the Customer Profiling set to allow the LogiNext to select the Address based on the Account Code passed, then this field is optional.
orders.deliverLongitude| String |  | Conditional Mandatory | If you are passing the Customer Address, then this field is optional or <br>If you have the Customer Profiling set to allow the LogiNext to select the Address based on the Account Code passed, then this field is optional.
orders.deliverNotes| String | 255 | Optional | You can enter instructions (if any) for the Delivery Associate while delivering the order.
shipmentCrateMappings| Array of objects | |  | Array - <br>Note that if your account is configured to have Order &  Crates Hierarchy or Order, Crates * Line Items Hierarchy, then it is mandatory for you pass the details of the Crates / Line Items in this field.


#### Request Parameters (Crates)

Param | DataType | Length |  Required | Description
--------- | ------- | ------- | ---------- | ------------
crateCd | String | 128 | Mandatory | This is the unique Crate ID / Code
crateAmount | Double |  | Mandatory | This is the amount / value of the items in the Crate.<br>If you allow partial delivery, then this amount helps in recalculating the amount of the order.
crateType | String | 100 | Optional | This Optional Field. You can choose to leave it blank.
noOfUnits | Integer | 10 | Conditional Mandatory | If your account is configured to have  Order, Crates & Line Items Hierarchy, then it is mandatory for you pass the number of items and it should be equal to the number of Line Items in that Crate.
shipmentlineitems | Array of objects |  | Optional | Array - <br>Note that if your account is configured to have  Order, Crates & Line Items Hierarchy, then it is mandatory for you pass the details of the Crates / Line Items in this field.



#### Request Parameters (LineItems)

Param | DataType | Length |  Required | Description
--------- | ------- | ------- | ---------- | ------------
itemCd | String | 200 | Mandatory | This is the unique Item Code
itemName | String | 255 | Mandatory | This is the Item Name
itemPrice | Double |  | Mandatory | This is the amount / value of the item.<br>If you allow partial delivery, then this amount helps in recalculating the amount of the order.
itemQuantity | Double | 10 | Optional | Quantity of the Items.
itemType | String | 100 | Optional | Any description in addition to Item name that you want to pass. For e.g. - Discounted Item, etc.
itemWeight | Double | 10 | Optional | Weight of Item


### Create Return

> Definition

```json
https://api.loginextsolutions.com/ShipmentApp/mile/v1/create/return
```

> Request Body

```json
[
  "863fe69239bc4f738ca275a809c3b2e2",
  "ca275a9239bc4f738ca275a809c35fr3",
  "5a809c239bc4f738ca275a809c3b23e4"
]
```

> Response

```json
{
  "status": 201,
  "message": "success",
  "referenceId": [
    "d7b0f3f8e1174742bd6a8ae451866cb1",
    "8e117a9239bc4f738ca275a809c35fr3",
    "3csefc239bc4f738ca275a209c38e117"
  ],
 "hasError": false,

}
```


Create return orders for existing orders with this API in the LogiNext system.

#### Request

<span class="post">POST</span>`https://api.loginextsolutions.com/ShipmentApp/mile/v1/create/return`

#### Request Body

Parameter | DataType |  Required | Description
-----------|-------|------- | ----------
reference_ids | List | Mandatory | Reference Id associated with the order.



### Get

> Definition

```json
https://api.loginextsolutions.com/ShipmentApp/mile/v1/shipment?end_date=2017-03-07+18:29:59&start_date=2016-02-01+18:30:00&status=ALL&order_no=GKS12567&customer_code=123&employee_id=134367&page_no=1&page_size=10
```



> Response

```json
{
  "status": 200,
  "message": "SUCCESS",
  "referenceId": null,
  "data": [
  {
      "referenceId": "f40cf4493a5949199775499b5750a272",
      "orderNo": "GR432U5",
      "parentOrderNo": "GKS12",
      "awbNumber": "435-16685675",
      "clientName": "UNY Logistics",
      "branchName": "West Brooklyn",
      "origin": "West Brooklyn",
      "destination": "2142 3rd Ave",
      "shipmentOrderTypeCd": "DELIVER",
      "orderState": "FORWARD",
      "deliveryType": "TRK",
      "deliveryLocationType": "PUP",
      "shipmentOrderDt": 1485153536000,
      "startTimeWindow": 1485174600000,
      "endTimeWindow": 1485181800000,
      "paymentType": "COD",
      "notes": "Order recieved successfully.Thanks",
      "packageValue": 0,
      "recalculatedValue": 0,
      "status": "DELIVERED",
      "plannedServiceTime": 5,
      "serviceTime": 2,
      "deliveryMediumName": "5T-ACOM2",
      "assignedThrough": "Manually",
      "tripName": "T35D33",
      "eta": 1485155640000,
      "actualStartDt": 1485154380000,
      "actualEndDt": 1485155021000,
      "plannedDistance": 16.708,
      "actualDistance": 6430.184,
      "distanceFromHub": null,
      "plannedStartDt": 1485154380000,
      "plannedEndDt": 1485155640000,
      "timeTakenDifferenceInMins": 10,
      "pickupLatitude": 40.760838,
      "pickupLongitude": -73.96732299999996,
      “employeeId”: 3224567,
      "pickupCheckInTime": 1485154765000,
      "pickupCheckOutTime": 1485154887000,
      "pickupCheckInLatitude": 40.760838,
      "pickupCheckInLongitude": -73.96732299999996,
      "pickupCheckOutLatitude": 40.760838,
      "pickupCheckOutLongitude": -73.96732299999996,
      "deliverLatitude": 41.882702,
      "deliverLongitude":101.706872,
      "deliverCheckInTime": 1485154905000,
      "deliverCheckOutTime": 1485155021000,
      "deliverCheckInLatitude": 41.882702,
      "deliverCheckInLongitude": -87.61939,
      "deliverCheckOutLatitude": 41.882702,
      "deliverCheckOutLongitude": -87.61939,
      "orderSequence": 5,
      "pickupAccountCode":"PDT_124",
      "customerCode": "CST_ACL1",
      "customerName": "Sg",
      "amountCollected": 200,
      "podCount": 2,
      "noOfCrates": 1,
      "packageWeight": 0,
      "packageVolume": 0,
      "customerComments": "",
      "deliveryNotes": "Order delivered successfully",
      "customerRatings": 5,
      "customerPhoneNumber": "5163063377",
      "deliveryMediumPhoneNumber":"3125096995",
      "reason": null,
      "vehicleNumber": "MH 02 T 123",
      "noOfAttempts": 1,
      "deliveryGeofenceEnterTime": 1484727378000,
      "deliveryGeofenceExitTime": 1484727387000,
      "isDelayed": false,
      "delayedBy": null,
      "pickupEmail":"steve@movenpick.com",
      "deliverEmail":"james@ablog.com",
      "shipmentCrateMappings": [
        {
          "crateCd": "Crate1",
          "statusCd": "UNLOADED",
          "crateType": "CRATE",
          "crateAmount": 0,
          "shipmentlineitems": [],
          "noOfUnits": 1,
          "loadedUnits": 1,
          "unloadedUnits": 1,
          "orderNo": "TEST_ACL1",
          "crateQuantity": 0,
          "amountToCollect": 0,
        }
      ]
    }
  ],
  "hasError": false
}

```

Retrieve orders and all the order associated information with this API.

#### Request

<span class="post">GET</span>`https://api.loginextsolutions.com/ShipmentApp/mile/v1/shipment`


#### Request Parameters

Param | DataType | Length |  Required | Description
--------- | ------- | ------- | ---------- | ------------
start_date | Date |  | Conditional Mandatory |  If order_no is not passed in the request, then this field is mandatory. Range of date from which orders can be searched. This will return orders based on the order fulfillment date start time window. <BR>Format 'yyyy-MM-dd HH:mm:ss'
end_date | Date |  | Conditional Mandatory |  If order_no is not passed in the request, then this field is mandatory. Range of date upto which orders can be searched. This will return orders that have fulfillment end times less than the entered time.<BR>Format 'yyyy-MM-dd HH:mm:ss'
status | String | 20 | Optional |  If order_no is passed in the request,then status will not be considered for filtering the orders.Order status. <BR>Ex: NOTDISPATCHED,INTRANSIT,COMPLETED,<BR>NOTCOMPLETED,PICKEDUP(Only for First Mile),CANCELLED
order_no | String | 100 | Optional | Order Number(Only one order number can be passed at a time.If not passed ,all the orders for the specified date range will be fetched)
page_no | Integer | | Optional | This parameter lets you specify the page number. It is used to page through the orders. This is optional parameter and default value (if it isn't specified) will be 1. 
page_size | Integer | |  Optional |  This parameter lets you specify the count of orders to return in your API call. This is optional parameter and default value (if it isn't specified) will be 50. The maximum accepted value is 100; higher values will be accepted but you will only get 100 records.
customer_code | String | |  Optional | This is the Customer Address ID parameter. You can pass one customer Id at a time. The result will be list of all the orders created for the mentioned customer ID
employee_id | String | | Optional | This is the Driver National ID  parameter. You can pass one driver Id at a time. The result will be list of all the orders which were assigned to this Driver ID


Status | Filter applied on orders
--------- | -------
NOTDISPATCHED | Orders will be fetched for which either the Order Start Date & Time Window or the Order End Date & Time Window lies within the range specified.
INTRANSIT | Orders will be fetched for which the Actual Delivery Start Date & Time lies within the range specified.
PICKEDUP | This is the status of the Order when it is marked as PICKEDUP
NOTPICKEDUP | This is the status of the Order when it is marked as Attempted Pickup
DELIVERED | This is the status of the Order when it is marked Delivered
NOTDELIVERED | This is the status of the Order when it is marked Attempted Delivered.
COMPLETED | For First Mile, an order is marked COMPLETED when it is PICKEDUP and DELIVERED at the hub. For Last Mile, an order is marked COMPLETED once it is DELIVERED to the end customer.<BR>Orders will be fetched for which the Actual Delivery End Date & Time lies within the range specified.
NOTCOMPLETED | For First Mile, when the order is  NOTPICKEDUP,it is marked as NOTCOMPLETED. For Last Mile, when the order is PICKEDUP but  NOTDELIVERED, it is marked as NOTCOMPLETED. <BR>Orders will be fetched for which the Actual Delivery End Date & Time lies within the range specified.
CANCELLED | Orders will be fetched for which the Cancellation Date & Time lies within the range specified.
ALL | Superset of all the filters mentioned for the above statuses will be considered.

### Get Status

> Definition

```json
https://api.loginextsolutions.com/ShipmentApp/mile/v1/status
```

> Request Body

```json
["c8714df4347911e6829f000d3aa04450"]
```

> Response

```json
{
  "status": 200,
  "data": [
    {
      "state": "FORWARD",
      "status": "NOTDISPATCHED",
      "referenceId": "c8714528347911e6829f000d3aa04450"
    }
  ],
  "hasError": false
}

```
Know the status of an order using this API.

#### Request

<span class="post">POST</span>`https://api.loginextsolutions.com/ShipmentApp/mile/v1/status`

#### Request Body

Parameter | DataType |  Required | Description
-----------|-------|------- | ----------
reference_ids | List | Mandatory | Reference Id associated with the order.

### Update

> Definition

```json
https://api.loginextsolutions.com/ShipmentApp/mile/v1/update
```

> Request Body

```json
[
  {
    "referenceId":"04c1c0c283a34769a5baca01c987b51a",
    "orderNo": "GR432U5",
    "awbNumber": "435-16685675",
    "shipmentOrderDt": "2016-07-15T10:30:00.000Z",
    "packageWeight":"10",
    "packageVolume": "450",
    "paymentType": "Prepaid",
    "packageValue": "65",
    "numberOfItems": "10",
    "partialDeliveryAllowedFl": "Y",
    "returnAllowedFl": "Y",
    "cancellationAllowedFl": "N",    
    "deliverBranch": "test",
    "deliverServiceTime": "20",
    "deliverEndTimeWindow": "2016-07-18T10:31:00.000Z",
    "deliverStartTimeWindow": "2016-07-16T10:31:00.000Z",
    "deliveryType": "DLBOY",
    "deliveryLocationType":"PUP",
    "deliverAccountCode": "Matt001",
    "deliverAddressId":"MattHome",
    "deliverAccountName": "Mathew Richardson",
    "deliverApartment": "10 Suite No. A1901",
    "deliverStreetName": "Walton Avenue",
    "deliverLandmark": "Opp. Chiptole",
    "deliverLocality": "Down Towm Chicago",
    "deliverCity": "Chicago",
    "deliverState": "IL",
    "deliverCountry": "USA",
    "deliverPinCode": "60602",    
    "pickupBranch":"New York",
    "pickupServiceTime": "50",
    "pickupStartTimeWindow": "2017-07-16T14:24:00.000Z",
    "pickupEndTimeWindow": "2017-07-17T14:24:00.000Z",
    "pickupAccountCode": "jim001",
    "pickupAccountName": "James Walker",
    "pickupApartment": "901",
    "pickupStreetName": "2142 3rd Ave",
    "pickupLandmark": "Opp. McDonalds",
    "pickupLocality": "East Harlem",
    "pickupCity": "New York",
    "pickupState": "NY",
    "pickupCountry": "USA",
    "pickupPinCode": "10035",    
    "returnBranch": "New York",
    "returnStartTimeWindow": "2017-05-18T03:00:00.000Z",
    "returnEndTimeWindow": "2017-05-18T16:00:00.000Z",
    "returnAccountCode": "retAcc123",
    "returnAddressId":"JeffOffice"
    "returnAccountName": "retAcc1234",
    "returnEmail": "james.w@ablogs.com",
    "returnPhoneNumber": "9891235886",
    "returnApartment": "901",
    "returnStreetName": "50 E 78th St",
    "returnLandmark": "Opp. Strand Bookstore",
    "returnLocality": "Upper East Side",
    "returnCity": "New York",
    "returnState": "NY",
    "returnCountry": "USA",
    "returnPinCode": "10035"
  }
]
```



> Response

```json
{
  "status": 200,
  "message": "success",
  "hasError": false
}

```
With this API, you will be able to update the order information unless and until that order is not delivered and not associated with any Trip.
You can pass multiple order reference IDs and can update one or more parameters.

#### Request

<span class="post">POST</span>`https://api.loginextsolutions.com/ShipmentApp/mile/v1/update`


#### Request Parameters

Param | DataType | Length |  Required | Description
--------- | ------- | ------- | ---------- | ------------
referenceId | String | 32 | Mandatory |  This is the system generated order Reference id.
orderNo | String | 100 | Optional |  This is the order number
awbNumber | String | 1000 | Optional | This is the airway Bill number.
shipmentOrderDt | Date | | Optional | This is the order date in UTC format. Format - YYYY-MM-DDTHH:MM:SS.SSSZ e.g. : 2016-07-01T11:18:00.000Z.
packageWeight | Double | 10 | Optional | This is the weight of package in Kg.
packageVolume | Double | 10 | Optional | This is the volume of package in CC.
packageValue | Double | 10 | Optional | This is the value of the order package.
numberOfItems | Integer | 20 | Optional | This is the number of crates in the order.
paymentType | String | 40 | Optional | This is the payment mode. Ex: COD - Cash On Delivery, Prepaid.
partialDeliveryAllowedFl | String | 50 | Optional | This identifies if partial delivery is allowed. Ex: Y/N.
returnAllowedFl | String | 1 | Optional | This identifies if order return allowed. Ex: Y/N. Default value is Y.
cancellationAllowedFl | String | 1 | Optional | This identifies if order cancellation is allowed. Ex: Y/N
deliverBranch | String | 255 | Optional | Name of delivery branch
deliverServiceTime | Integer | 11 | Optional | Deliver service time in mins.
deliverStartTimeWindow | Date | | Optional | Deliver start time window. Format - YYYY-MM-DDTHH:MM:SS.SSSZ e.g. : 2016-07-01T11:18:00.000Z.
deliverEndTimeWindow | Date | | Optional | Deliver end time window. Format - YYYY-MM-DDTHH:MM:SS.SSSZ e.g. : 2016-07-01T11:18:00.000Z.
deliveryType | String | 40 | Optional | Order delivery type. Ex: TRK - Truck, VAN - Van, DLBOY - Delivery Boy
deliveryLocationType | String | 40 | Optional | Type of delivery location. Ex: CUSTOMER, PUP
deliverAccountCode | String | 255 | Optional | This is the delivery customer's account code.
deliverAddressId | String | 255 | Optional | This is the delivery customer's address Id.
deliverAccountName | String| 255  | Optional | This is the delivery customer's account name.
deliverApartment | String | 512 | Optional | This is the delivery customer location's apartment details.
deliverStreetName | String | 512 | Optional | This is the delivery customer location's street name.
deliverLandmark | String | 512 | Optional | This is the delivery customer location's landmark.
deliverLocality | String | 512 | Optional | This is the delivery customer location's Locality.
deliverCity | String | 512 | Optional | This is the delivery customer location's city.
deliverState| String | 512 | Optional | This is the delivery customer location's state code.
deliverCountry | String | 512 | Optional | This is the delivery customer location's apartment details country code.
deliverPinCode | String | 20 | Optional | This is the delivery customer location's apartment details pincode.
pickupBranch | String | 255 | Optional | This is the pickup branch's name.
pickupServiceTime | Integer | 11 | Optional | This is the pickup service time in mins.
pickupStartTimeWindow | Date | | Optional | Pickup start time window. Format - YYYY-MM-DDTHH:MM:SS.SSSZ e.g. : 2016-07-01T11:18:00.000Z.
pickupEndTimeWindow | Date | | Optional | Pickup end time window. Format - YYYY-MM-DDTHH:MM:SS.SSSZ e.g. : 2016-07-01T11:18:00.000Z.
pickupAccountCode | String | 255 | Optional | This is the pickup customer's account code.
pickupAddressId | String | 255 | Optional | This is the pickup customer's address Id.
pickupAccountName | String | 255 | Optional | This is the pickup customer's account name.
pickupApartment | String | 512 | Optional | This is the pickup customer's Apartment number.
pickupStreetName | String | 512 | Optional | This is the pickup customer's street name.
pickupLandmark | String | 512 | Optional | This is the pickup customer's Landmark.
pickupLocality | String | 512 | Optional | This is the pickup customer's locality.
pickupCity | String | 512 | Optional | This is the pickup customer's city.
pickupState| String | 512 | Optional | This is the pickup customer's state code. Please refer to the list of state codes provided in the "State Codes" section.
pickupCountry | String | 512 | Optional | This is the pickup customer's country code. Please refer to the list of country codes provided in the "Country Codes" section.
pickupPinCode | String | 20 | Optional | This is the pickup customer's pincode.
returnBranch | String | 255 | Optional | Name of return branch
returnStartTimeWindow | Date | | Optional | Return start time window. Format - YYYY-MM-DDTHH:MM:SS.SSSZ e.g. : 2016-07-01T11:18:00.000Z.
returnEndTimeWindow | Date | | Optional | Return end time window. Format - YYYY-MM-DDTHH:MM:SS.SSSZ e.g. : 2016-07-01T11:18:00.000Z.
returnAccountCode | String | 255 | Optional | This is the return customer's account code.
returnAddressId | String | 255 | Optional | This is the return customer's address Id.
returnAccountName | String | 255 | Optional | This is the return customer's account name.
returnEmail | String | 500 | Optional | This is the return customer's email ID.
returnPhoneNumber | String | 255 | Optional | This is the return customer's phone number.
returnApartment | String | 512 | Optional | This is the return customer's apartment.
returnStreetName | String | 512 | Optional | This is the return customer's street name.
returnLandmark | String | 512 | Optional | This is the return customer's landmark.
returnLocality | String | 512 | Optional | This is the return customer's locality.
returnCity | String | 512 | Optional | This is the return customer's city.
returnState| String | 512 | Optional | Return State code. Please refer to the list of state codes provided in the "State Codes" section.
returnCountry | String | 512 | Optional | Return Country code. Please refer to the list of country codes provided in the "Country Codes" section.
returnPinCode | String | 20 | Optional | This is the return customer's pincode.

### Update Status

> Definition

```json
https://api.loginextsolutions.com/ShipmentApp/mile/v1/update/status
```

> Request Body

```json
{
  "newStatus":"NOTDELIVERED",
  "orderDetails":
  [{
    "orderReferenceId":"6186d5fc6e324c42abb5ea1a32e05f66",
    "reasonCd":"DBUNAVAILABLE",
    "otherReason":"",
    "latitude": 19.117369,
    "longitude": 72.910214,
    "updateTime":"2016-07-18T10:31:00.000Z"
  },
  {
    "orderReferenceId":"6186d7r5te324c42abb5ea1a32x45f66",
    "reasonCd":"DBUNAVAILABLE",
    "otherReason":"",
    "latitude": 19.117369,
    "longitude": 72.913214,
    "updateTime":"2016-07-18T10:31:00.000Z"

  },
  {
    "orderReferenceId":"6156ty46e324c42abb5ea1a32y45f66",
    "reasonCd":"OTHER",
    "otherReason":"Technical Issues",
    "latitude": 19.117369,
    "longitude": 72.910321,
    "updateTime":"2016-07-18T10:31:00.000Z"

  }]

}
```



> Response

```json
{
  "status": 200,
  "message": "Status updated successfully",
  "hasError": false
}

```
With this API, you will be able to update the order information unless and until that order is not dispatched and not associated with any Trip.
You can pass multiple order reference IDs and can update one or more parameters.

#### Request

<span class="post">PUT</span>`https://api.loginextsolutions.com/ShipmentApp/mile/v1/update/status`


#### Request Parameters

Param | DataType | Length |  Required | Description
--------- | ------- | ---------- | ---------- | ------------
newStatus | String | 20 | Mandatory |  One status for multiple orders.The orders will be updated with this new status<br>Available Values - <br>DELIVERED - When an order has been Delivered by the associate<br>NOTPICKEDUP - When the associate reached the Pick-up location, but could not pick-up the order due to one or the other reason<br>NOTDELIVERED - When the associate reached the delivery location, but could not deliver the order due to one or the other reason
orderReferenceId | String | 100 | Mandatory |  This is the LogiNext Reference ID for the Order<br>This is generated when the order is added in the LogiNext application.
reasonCd | String | 255 | Conditional Mandatory | Mandatory depending upon the status selected : NOTDELIVERED, NOTPICKEDUP, CANCELLED<br>Else Optional.<br>If you have pre-configured the reasons for Order Status Update - NOTDELIVERED, NOTPICKEDUP and CANCELLED in LogiNext application, then it is mandatory to mention that relevant configured reason here.<br>One of the other values here is OTHER, in case the delivery Associate selects the reason as Others.
otherReason | Date |  | Conditional Mandatory | Mandatory when reasonCd is OTHER
latitude | Double | 15 | Conditional Optional | Geo-location where Order status was updated<br>Sample Value - "17.996"
otherReason | Date | 15 | Conditional Optional | Geo-location where Order status was updated<br>Sample Value - "17.996"
updateTime | Date | 15 | Conditional Optional | This is the timestamp (in UTC format) when the order status was changed. This cannot be greater than the time at which the API is hit. If not passed, the timestamp of the API hit is considered as the timestamp for the status change.


### Update Crates and Line Items

> Definition

```json
https://api.loginextsolutions.com/ShipmentApp/mile/v1/updateCrates
```

> Request Body

```json
{
  "referenceId": "ae9a2eed3fc54784905345f9c71b9e5f",
  "shipmentCrates": [
    {
      "crateCd": "00009595951000000492",
      "shipmentlineitems": [
        {
          "itemCd": "1_120000256",
          "itemName": "Bourbon",
          "itemPrice": 12,
          "itemQuantity": 12,
          "itemType": "Biscuit",
          "itemWeight": 50
        }
      ]
    },
    {
      "crateCd": "00009595951000000490",
      "shipmentlineitems": [
        {
          "itemCd": "1_120000244",
          "itemName": "Noodles Chicken 50 Gm",
          "itemPrice": 12,
          "itemQuantity": 3,
          "itemType": "Soup",
          "itemWeight": 30
        },
        {
          "itemCd": "1_120000243",
          "itemName": "Silk Chocolate",
          "itemPrice": 12,
          "itemQuantity": 5,
          "itemType": "Chocolate",
          "itemWeight": 25
        }
      ]
    }
  ]
}
```



> Response

```json
{
  "status": 200,
  "message": "success",
  "hasError": false
}

```
Call this API to update the crate and line items information for an order. Note that this can be done until that order is dispatched and not associated with any Trip.

This API can be used to Add new crates and line items, or update existing ones. For eg. If you create an Order with crate A and crate B, and then call this API to to add a new crate C, you only need to pass the information for crate C. Once the API is called with a success response, the Order will now have crates A,B, and C.

Alternatively, if an order has crate A and crate B, and the crate A item needs to be updated, call this API and pass crateCd 'A', and update the properties for the crate.

This API will not delete existing crates.

You can pass multiple crate and line items.

#### Request

<span class="post">POST</span>`https://api.loginextsolutions.com/ShipmentApp/mile/v1/updateCrates`

#### Request Parameters (Crates)

Param | DataType | Length |  Required | Description
--------- | ------- | ------- | ---------- | ------------
shipmentCrates | Array of objects | | Optional | This specifies the crate level information of the order.
shipmentCrates.crateCd | String | 128 | Mandatory | This is the crate code.
shipmentCrates.crateAmount | Double | | Optional | This is the crate amount.
shipmentCrates.crateType | String | 100 | Optional | Type of crate. Ex: cake, juice, sweet, furniture etc.
shipmentCrates.noOfUnits | Integer | 10 | Optional | This is the number of crate units.
shipmentCrates.shipmentlineitems.itemCd | String | 200 | Mandatory | This is the item code.
shipmentCrates.shipmentlineitems.itemName | String | 255 | Optional | This is the item name.
shipmentCrates.shipmentlineitems.itemPrice | Double | | Mandatory | This is the item price.
shipmentCrates.shipmentlineitems.itemQuantity | Double | 10 | Mandatory | This is the item quantity.
shipmentCrates.shipmentlineitems.itemType | String | 100 | Optional | This is the item type.
shipmentCrates.shipmentlineitems.itemWeight | Double | 10 | Optional | This is the item weight.


### Assign

> Definition

```json
https://api.loginextsolutions.com/ShipmentApp/mile/v1/manual/assign
```

> Request Body

```json
{
  "trip":{
    "referenceId":"879098765678909876a87656s"
  },
  "deliveryMedium":{
    "identifier":"employeeId",
    "identifierValue":"77381"
  },
  "orderReferenceIds":["87678909876aa987659876sa","9876789asd98765456712"]
}
```



> Success Response

```json
{
    "status": 200,
    "message": "Order(s) Assigned Successfully!",
    "hasError": false
}

```

> Failure Response

```json
{
   "status": 409,
   "message": "Assignment Failed",
   "moreResultsExists": false,
   "error": {
       "order": [
           {
               "key": "orderReferenceIds",
               "message": [
                   "Order Reference ID is invalid"
               ]
           }
       ]
   },
   "hasError": true
}

```

With this API, you can add Orders to a particular Trip or a Delivery Associate's Default, Not Started Trip.

If you have a set of Orders to be manually assigned to a particular Delivery Associate or Trip, for eg- in the case that a Delivery Associate is Abesent or On Break, you can assign the Orders to be fulfilled to another Trip of another Delivery Associate using this API.

The API will take as input the Trip or Delivery boy details and the list of orders to be added for that trip or Delivery Associate.
The API can be used in 2 ways:
If the trip details are passed (through trip reference id), then Delivery Associate details are not required and the list of orders will be added to that trip, irrespective of the trip being Started or Not Started. Other order and trip validations remain as is.
If the trip details are not passed, then the Delivery Associate details will be required to be passed, either through username, mobile number or employee id (unique identifiers) and a control flag identifying which of these values is being passed. 
The orders will be added to the Default trip (Started or Not Started) of the Delivery boy.

The Rate Limit for this API is 1 call/sec.

#### Request

<span class="post">PUT</span>`https://api.loginextsolutions.com/ShipmentApp/mile/v1/manual/assign`


#### Request Parameters

Param | DataType | Length |  Required | Description
--------- | ------- | ---------- | ---------- | ------------
trip.referenceId | String | 32 | Conditional Mandatory | Reference ID of the trip to which the Order has to be assigned. This field has to be passed in case the Delivery Associate details are not passed.
deliveryMedium.identifier | String | 32 | Conditional Mandatory |  This is the control flag field for the Delivery Associate, to identify which details of the Delivery Associate are being passed. Possible values are 'employeeId', 'phoneNumber', 'userName'.
deliveryMedium.identifierValue | String | 32 | Conditional Mandatory | This field will hold the Delivery Associate information to whom the Order is to be assigned, as per the flag set above. For eg - If you wish to assign an Order to a Delivert Associate whose 'employeeId' is 'John1', you would send 'employeeId' in the identifier field and 'John1' in the identifierValue field.
orderReferenceIds | List | |  Mandatory | These are the Reference IDs of the Order to be assigned.


### Cancel

> Definition

```json
https://api.loginextsolutions.com/ShipmentApp/mile/v1/cancel
```

> Request Body

```json
[
     "c8714df4347911e6829f000d3aa044508",
     "c8714df4347911e6829f654677aa04450",
     "c8714df4347911e436667888d3aa04450"
]
```

> Success Response

```json
{
  "status": 200,
  "message": "success",
  "hasError": false
}
```

> Failure Response

```json
{
   "status": 409,
   "message": "Order(s) couldn't be cancelled",
   "moreResultsExists": false,
   "hasError": false
}
```


Use this API to cancel an order.

With this API, you can cancel Orders that were created with a 'cancellationAllowedFl' set to 'Y'. If you try to cancel Orders that have a 'cancellationAllowedFl' set to 'N', the API will return an error response.

#### Request

<span class="post">PUT</span>`https://api.loginextsolutions.com/ShipmentApp/mile/v1/cancel`

#### Request Body

Parameter | DataType | Required | Description
-----------|-------|------- | ----------
reference_ids | List  | Mandatory | This is the order reference Id.

### Get EPOD and ESIGN

This endpoint downloads the EPODs and ESIGNs for given order, delivery dates and status of order. The response is in form of a zip file. NOTE: The dates accepted are in UTC.

#### Request

<span class="post">GET</span>`https://api.loginextsolutions.com/ShipmentApp/shipment/fmlm/epod/list?orderstartdt=2015-06-16 00:00:00&orderenddt=2016-06-16 00:30:00&deliverystartdt=2015-06-15 00:00:00&deliveryenddt=2016-06-15 00:00:00&status=NOTDISPATCHED`

#### Request Parameters

Parameter | DataType | Length |  Required | Description
-----------|-------|------- |------- | ----------
orderstartdt | String |  | Optional | This parameter will retrieve the EPODs for Orders with an Order Date greater than or equal to the date entered. The date format entered should be YYYY-MM-DD HH:MM:SS . This parameter has to be entered along with orderenddt.
orderenddt | String |  | Optional | This parameter will retrieve the EPODs for Orders  with an Order Date less than or equal to the date entered. The date format entered should be YYYY-MM-DD HH:MM:SS. This parameter has to be entered along with orderstartdt.
deliverystartdt | String |  | Optional | This parameter will retrieve the EPODs for Orders with an Order Deliver Date  greater than or equal to the date entered. The date format entered should be YYYY-MM-DD HH:MM:SS. This parameter has to be entered along with deliveryenddt. 
deliveryenddt | String |  | Optional | This parameter will retrieve the EPODs for Orders  with an Order Deliver Date less than or equal to the date entered. The date format entered should be YYYY-MM-DD HH:MM:SS . This parameter has to be entered along with deliverystartdt. 
startDateFilter | String |  | Optional | This field will work based on status - if status is ALL then it will retrieve the data greater than this date.if status is NOTDISPATCHED, it will get EPODs for Orders between ORDER start time window and end time window. Else it will get data between ORDER actual START and END Date. This parameter has to be entered along with endDateFilter. 
endDateFilter | String |  | Optional | It will work based on status if status = ALL then it will get all data less than this date.if status*=*NOTDISPATCHED then it will retrieve EPODs for Orders between ORDER start time window and end time window, else it will get data between ORDER actual START and END Date. This parameter has to be entered along with startDateFilter. 
status | String | 20 | Optional | Order status. <BR>Ex: NOTDISPATCHED,INTRANSIT,DELIVERED,<BR>NOTDELIVERED,PICKEDUP,NOTPICKEDUP,CANCELLED

#### Response

Response is a binary zip file.<br>
The images for the EPODs and ESIGNs will be downloaded in .png formats when unzipped
In any browser just hit the url and zip file download will start automatically.<br>
In tools like POSTMAN instead of clicking 'Send' button click on 'Send & Download' button, which will save the zip file.


## Manifest

### Create / Update

> Definition

```json
https://api.loginextsolutions.com/ShipmentApp/mile/v1/scan/manifest/addshipment
```

> Request Body

```json
{
   "manifestId":"hcgsyuc334",
   "manifestType":"ORDER",
   "cancelledOrderAllowedFl": false,
   "orderReferenceIds":["843d70885de84d20b46279d0d5149758","5e10b5c270ad46a5969b323d48b60c0a"]
}

```

> Response

```json
{
    "status": 200,
    "message": "Add Orders to manifest success.",
    "data": {
        "manifestId": "hcgsyuc334"
    },
    "hasError": false
}
```

Call this API to create Manifests for your shipments.​ ​The scan status​ ​of your order​ ​will get updated to
"​Out-scanned"​ ​if the Manifest is created successfully.​

​Pass the LogiNext​ ​Order Reference ID as a parameter to this API.The Order Reference ID is generated when an order is created in the LogiNext system.
If you do not store the Reference ID for orders,  you will need to fetch the same through the Get Order API.

You can also manifest Cancelled Orders (by turning this flag to "true") in case you have to return (out-scan) the cancelled orders back to the merchant / origin.

This API will do the following when called:<br>
If you pass the manifestId, there would be a check if that Manifest ID exists in LogiNext application.<br>
If it exists, then the orders (through order reference ID) will be updated in the LogiNext application.<br>
If it does not exist, then a new manifest will be created with the provided Manifest ID.


#### Request

<span class="post">POST</span>`https://api.loginextsolutions.com/ShipmentApp/mile/v1/scan/manifest/addshipment`


#### Request Body

Parameter | DataType | Length |  Required | Description
-----------|-------| ------- |------- | ----------
manifestId | String | 11 | Optional | Pass the Manifest ID as one of the Request parameters​ ​if your system​ ​generates such​ ​ID. If not​ ​passed, LogiNext​ ​will create the Manifest ID. This Manifest ID will also be passed as one of the response parameters. You can store the same for any future reference.
manifestType | String | 25 | Optional | The default manifestType is 'ORDER'.
cancelledOrderAllowedFl | String | 1 | Optional | By default the value will be taken as  "false". If you would like to OutScan Cancelled orders, then please pass "true".
orderReferenceIds | List |  | Mandatory | This is the LogiNext Order Reference ID.




## Trip


### Start

> Definition

```json
https://api.loginextsolutions.com/TripApp/mile/v1/trip/start
```

> Request Body

```json
[
    "a9be39b9347911e6829f000d3aa04450",
    "a9be39b9347911e6829f07657aa04450"
]
```

> Response

```json
{
  "status": 200,
  "message": "2 trip(s) started",
  "data": true,
  "hasError": false
}

```
Start the trip for a Delivery Associate using this API.

#### Request

<span class="post">POST</span>`https://api.loginextsolutions.com/TripApp/mile/v1/trip/start`

#### Request Body

Parameter | DataType |  Required | Description
-----------|-------|------- | ----------
reference_ids | List | Mandatory | Reference Id associated with the trip.

### Stop

> Request Body

```json
[{
    "tripReferenceId":"a9be39b9347911e6829f000d3aa04450",
    "notDispatchedOrders":["c8714df4347911e6829f000d3aa04450"],
    "deliveredOrders":["c8714cac347911e6829f000d3aa04450"]
}]
```

> Response

```json
{
  "status": 200,  
  "message": "Trips ended successfully",
  "data": true,
  "hasError": false
}

```
Stop the trip for a Delivery Associate using this API. The API accepts 2 lists of Order reference IDs to update the statuses of these Orders when the trip is stopped. For example, if there are 5 Not Delivered Orders at the time of calling this API, you can specify which Orders are to be marked Delivered and which ones are to be marked Not Dispatched, so they can be assigned to another trip and fulfilled at a later time.


#### Request

<span class="post">POST</span>`https://api.loginextsolutions.com/TripApp/mile/v1/trip/stop`

#### Request Body

Parameter | DataType | Length |  Required | Description
-----------|-------|-------|------- | ----------
tripReferenceId | String  | 32 | Mandatory | Reference Id associated with the trip.
notDispatchedOrders | List  |  | Mandatory | Order Reference Ids of Orders to be marked as Not Dispatched on the Stop Trip event. If no Orders are to be marked Not Dispatched, send an empty list.
deliveredOrders | List |  | Mandatory | Order Reference Ids of Orders to be marked as Delviered on the Stop Trip event. If no Orders are to be marked Delivered, send an empty list.


### Get 


> Response

```json
{
    "status": 200,
    "message": "Success",
    "data": {
    "tripId": 410840,
    "tripName": "VILE PARLE WEST-TRIP-13924",
    "referenceId": "2becf481189f4525a23889a35c554e61",
    "status": "NOTSTARTED",
    "plannedStartDt": 1522618200000,
    "plannedEndDt": 1522626600000,
    "totalPlannedDistance": 30.1302,
    "totalPlannedTime": 140,
    "vehicleNumber": "MH04-HD9389",
    "deliveryMediumName": "tetestrer",
    "deliveryMediumPhoneNumber": "9968995522",
    "deliveryMediumBranch": "AAA0",
    "orderDetails": [
        {
            "referenceId": "3e7262c47a47441295d37dba81425827",
            "orderNo": "Andri55",
            "state": "FORWARD",
            "status": "NOTDISPATCHED",
            "orderSequence": 2,
            "shipmentOrderTypeCd": "DELIVER",
            "startTimeWindow": 1522661400000,
            "endTimeWindow": 1522665000000,
            "plannedStartTime": 1546908814000,
            "plannedEndTime": 1546914874000,
            "revisedStartTime": 1522657800000,
            "revisedEndTime": 1522662000000

        },
        {
            "referenceId": "d7b47e622a33432da70c0fddec1b3a7d",
            "orderNo": "Andri57",
            "state": "FORWARD",
            "status": "NOTDISPATCHED",
            "orderSequence": 1,
            "shipmentOrderTypeCd": "DELIVER",
            "startTimeWindow": 1522661400000,
            "endTimeWindow": 1522665000000,
            "plannedStartTime": 1546908814000,
            "plannedEndTime": 1546914874000,
            "revisedStartTime": 1522657800000,
            "revisedEndTime": 1522661700000
        },
        {
            "referenceId": "baab317214584d0a996a4dfb0b7fac85",
            "orderNo": "Andri147",
            "state": "FORWARD",
            "status": "NOTDISPATCHED",
            "orderSequence": 3,
            "shipmentOrderTypeCd": "DELIVER",
            "startTimeWindow": 1522661400000,
            "endTimeWindow": 1522665000000,
            "plannedStartTime": 1546908814000,
            "plannedEndTime": 1546914874000,
            "revisedStartTime": 1522657800000,
            "revisedEndTime": 1522662300000
        },
    ]
},
    "hasError": false
}

```
Get all the details of a trip with this API. You can call this API to get the Order ETAs for Orders within a particular trip. The API will provide both the original ETAs and revised ETAs of Orders within that trip.

#### Request
<span class="post">GET</span>`https://api.loginextsolutions.com/TripApp/mile/v1/trip/get?referenceId=7f389cfa7ae64d85a915ee6297bd9c3f&tripname=TRIP-26516`

#### Request Parameters

Param | DataType | Length |  Required | Description
--------- | ------- | ------- | ---------- | ------------
referenceId | String |  | Conditional Mandatory |  If tripname is not passed in the request, then this field is mandatory. This is the reference ID of the trip.
tripname | String |  | Conditional Mandatory |  If referenceId is not passed in the request, then this field is mandatory. This is the trip name of the trip for which details are to be fetched.


## Tracking

### Track Last Location

> Definition

```json
https://api.loginextsolutions.com/TrackingApp/mile/v1/track/lastlocation?shipmentReferences=25a565a9c9d540cd9e6c02fae890cb67,c7afc8b1b97b48468c3417aa425eff81,27121903f4f047bcb378a6457bee2fec,21b538edf7f047028334480036179c70
```



> Response

```json
{
  "status": 200,
  "message": "Latest Location found successfully",
  "data": [
    {
      "lat": 19.1119794,
      "lng": 72.9094968,
      "shipmentReference": "21b538edf7f047028334480036179c70"
    },
    {
      "lat": 19.0668898,
      "lng": 72.8320575,
      "shipmentReference": "25a565a9c9d540cd9e6c02fae890cb67"
    },
    {
      "lat": 19.0741246,
      "lng": 72.824772,
      "shipmentReference": "27121903f4f047bcb378a6457bee2fec"
    },
    {
      "lat": 19.1200864,
      "lng": 72.9010175,
      "shipmentReference": "c7afc8b1b97b48468c3417aa425eff81"
    }
  ],
  "hasError": false
}

```
Use this to find out last tracked location for any order/ Delivery Associate.

#### Request

<span class="post">GET</span>`https://api.loginextsolutions.com/TrackingApp/mile/v1/track/lastlocation`


### iFrame

> Definition

```json
https://api.loginextsolutions.com/track/#/order?ordno=1234&aid=4b41a94b-521b-4986-920d-6e4c1cf15fd0b6
```

The iFrame displays the last tracking for an order, including current location, based on the order no.

#### Request


<span class="post">GET</span>` https://api.loginextsolutions.com/track/#/order?ordno=<ordno>&aid=<aid>`

#### Request Parameters

Parameter | Sample Value | Description
--------- | ------- | -------------
aid | f522631c-490c-46fd-9f79-ca8d14a704d7 | Value of authentication token without 'BASIC' keyword
ordno | 1234| Order no


## Mobile

If you have got your own order fulfillment application, use LogiNext's Mobile APIs to push data directly into LogiNext.

NOTE: These APIs require the Delivery Associate's token. Please view the Authenticate Section of this page for more information on acquiring a Delivery Associate Token.


### Accept Order

> Definition

```json
https://api.loginextsolutions.com/ShipmentApp/v1/mobile/order/accept
```

> Request Body

```json
{
  "orderReferenceId":"a3bee4486d9f467d72e96f4d32c5569b",
  "parentOrderNo":"1316MDO",
  "orderAcceptTime":"2017-12-27T10:00:00Z",
  "latitude": 19.111555,
  "longitude": 72.9099327
}
```

> Response

```json
{
  "status": 200,
  "message": "success",
  "hasError": false
}
```

With this API, you can mark the Order as Accepted by the Delivery Associate / Associate / Driver / Fried Executive.
Please note that in headers for this API, you will have to pass the Delivery Associate's Token and Key and not the Account level Token and Key.

You can fetch the Delivery Associate's Token and Key by calling the Delivery Associate Authenticate API.

#### Request

<span class="post">PUT</span>`https://api.loginextsolutions.com/ShipmentApp/v1/mobile/order/accept`

#### Request Body

Parameter | DataType | Length | Required | Description
-----------|-------|------- | ----|----------
orderReferenceId | String | 32 | Mandatory | This is the LogiNext Order Reference ID created when the order is added in the LogiNext system.<br>If your Order is Single Pick-up - Single destination, then pass the Order Reference ID generated against that Order No.<br>If your Order is Single Pick-up - Multiple destination, then pass any one of the order's Reference ID. <br>Please note, if you pass the Order Reference ID in combination with the Parent Order No., then all the orders under that Parent Order No. will be updated with the ACCEPTED status.<br>If you want to update the status of only one specific order (out of the many orders under a particular Parent Order No.) , then you need not have to pass the Parent Order No.
parentOrderNo | String | 100 | Optional | If your Order is Single Pick-up - Multiple destination and if you want to update the status of the all orders under the Parent Order, then pass the Parent Order No. <br>If you want to update the status of only one specific order (out of the many orders under a particular Parent Order No.) , then you need not have to pass the Parent Order No. <br>If your Order is Single Pick-up - Single, then you need not have to pass the Parent Order no.
orderAcceptTime | String | 32 | Optional | This is the timestamp (in UTC format) when the order was accepted. <br>This cannot be greater than the current time (time at which the API request is called). <br>If not passed, the current timestamp will be considered as the timestamp for the order acceptance.<br>Sample Value - 2017-12-27T10:00:00Z
latitude | Double | 15 | Optional | Geo-location where Order was accepted. Note that this is not used for ETA calculation. That happens using Tracking points.
Sample Value - "17.996"
longitude | Double | 15 | Optional | Geo-location where Order was accepted. Note that this is not used for ETA calculation. That happens using Tracking points.
Sample Value - "17.996"

### Reject Order

> Definition

```json
https://api.loginextsolutions.com/ShipmentApp/v1/mobile/checkin
```

> Request Body

```json
{
  "orderReferenceIds":["6b106144208243ffb4b8c4114fd44f123d"],
  "checkInLocation":"PICKUP",
  "checkinLatitude":12.11,
  "checkinLongitude":78.11223,
  "checkInTime":"2018-02-08T09:30:00Z"
}
```

> Response

```json
{
  "status": 200,
  "message": "success",
  "hasError": false
}
```

With this API, the delivery assosicate can check In at the pickup or delivery location

Please note that in headers for this API, you will have to pass the Delivery Associate's Token and Key and not the Account level Token and Key.

You can fetch the Delivery Associate's Token and Key by calling the Delivery Associate Authenticate API.

#### Request

<span class="post">PUT</span>`https://api.loginextsolutions.com/ShipmentApp/v1/mobile/checkin`

#### Request Body

Parameter | DataType | Length | Required | Description
-----------|-------|------- | ----|----------
orderReferenceIds | String | 100 | Mandatory | This is the list of order Reference Ids for which the check in event is being called.
checkInLocation | String | 32 | Mandatory | This will be 'PICKUP' in case of the pickup location and 'DELIVER' for the delivery location.
checkinLatitude | Double | 15 | Optional | The geolocation coordinate (latitude) of the checkinLocation.
checkinLongitude | Double | 15 | Optional | The geolocation coordinate (longitude) of the checkinLocation.
checkinTime | Date | | Mandatory | This is the timestamp of the check in event. Input is expected in UTC format

### Check In

> Definition

```json
https://api.loginextsolutions.com/ShipmentApp/v1/mobile/checkin
```

> Request Body

```json
{
  "orderReferenceIds":["6b106144208243ffb4b8c4114fd44f123d"],
  "checkInLocation":"PICKUP",
  "checkinLatitude":"12.11",
  "checkinLongitude":"78.11223",
  "checkInTime":"2018-02-08T09:30:00Z"
}
```

> Response

```json
{
    "status": 200,
    "message": "Check in marked successfully",
    "hasError": false
}

```

With this API, the Delivery associate can Check In at the time of Order Delivery at the Deliver location.

Please note that in headers for this API, you will have to pass the Delivery Associate's Token and Key and not the Account level Token and Key.

You can fetch the Delivery Associate's Token and Key by calling the Delivery Associate Authenticate API.

#### Request

<span class="post">PUT</span>`https://api.loginextsolutions.com/ShipmentApp/v1/mobile/checkin`

#### Request Body

Parameter | DataType | Length | Required | Description
-----------|-------|------- | ----|----------
orderReferenceId | List | 32 | Mandatory | This is the LogiNext Order Reference ID created when the order is added in the LogiNext system.<br>If your Order is Single Pick-up - Single destination, then pass the Order Reference ID generated against that Order No.<br>If your Order is Single Pick-up - Multiple destination, then pass any one of the order's Reference ID.
checkInLocation | String | 100 | Mandatory | This can be "PICKUP" or "DELIVER".
checkinLatitude | Double | 100 | Optional | Geocoordinate(Latitude) for the Check In location.
checkinLongitude | Double | 100 | Optional | Geocoordinate(Longitude) for the Check In location.
checkInTime | Date | 100 | Mandatory | Check In Time in UTC format - YYYY-MM-DDTHH:MM:SS.SSSZ e.g. : 2016-07-01T11:18:00.000Z.

### Create Tracking

> Definition

```json
https://products.loginextsolutions.com/TrackingApp/track/mobile/put 
```

> Request Body

```json
{
  "location": [{
    "latitude": 19.1119129,
    "longitude": 72.9094089,
    "speed": 0,
    "battery": 100,
    "locationSource": "fused",
    "trackingDt": "2017-12-11T07:21:39Z",
    "type": "MOBREG",
    "distanceFromLastLocation": 0,
    "accuracy": 23.878000259399414,
    "bearing": 0,
    "altitude": 0,
    "hasAccuracy": "0",
    "hasBearing": "0",
    "hasSpeed": "0",
    "lastLatitude": 19.1119129,
    "lastLongitude": 72.9094089,
    "isFirstPointFl": "0",
    "currentTime": 1512976899548,
    "previousTime": 1512976899532,
    "userId": 4955,
    "signalStrength": 30,
    "appStatus": "100",
    "networkType": "WIFI",
    "dataNetworkType": "Unknown",
    "isGsmFl": false,
    "isActiveNetworkMetered": false,
    "imei": "911380458661315"
  }, {
    "latitude": 19.1119129,
    "longitude": 72.9094089,
    "speed": 0,
    "battery": 100,
    "locationSource": "fused",
    "trackingDt": "2017-12-11T07:21:19Z",
    "type": "MOBREG",
    "distanceFromLastLocation": 0,
    "accuracy": 23.87700080871582,
    "bearing": 0,
    "altitude": 0,
    "hasAccuracy": "0",
    "hasBearing": "0",
    "hasSpeed": "0",
    "lastLatitude": 19.1119129,
    "lastLongitude": 72.9094089,
    "isFirstPointFl": "0",
    "currentTime": 1512976879541,
    "previousTime": 1512976879521,
    "userId": 4955,
    "signalStrength": 30,
    "appStatus": "100",
    "networkType": "WIFI",
    "dataNetworkType": "Unknown",
    "isGsmFl": false,
    "isActiveNetworkMetered": false,
    "imei": "911380458661315"
  }]
}

```

> Success Response

```json
{
    "status": 200,
    "data": {
        "msg": [
            "2018-11-11T07:20:59",
            "2018-11-11T07:21:19",
            "2018-11-11T07:21:39"
        ],
        "previousTimes": [
            1512976859528,
            1512976879521,
            1512976899532
        ]
    },
    "hasError": false
}

```


> Failure Response


```json
{
    "status": 200,
    "data": {
        "msg": [
            "2018-11-11T07:20:59",
            "2018-11-11T07:21:19",
            "2018-11-11T07:21:39"
        ],
        "previousTimes": [
            1512976859528,
            1512976879521,
            1512976899532
        ]
    },
    "hasError": false
}

```


With this API, you can send the current position of your Delivery Associates / Field Executives when they are not using LogiNext Mobile App.

#### Request

<span class="post">POST</span>`https://products.loginextsolutions.com/TrackingApp/track/mobile/put`

#### Request Body

Parameter | DataType |  Length | Required | Description
-----------|-------|------- | ----|----------
latitude|Double | 13,10 |Mandatory|The geocoordinate(Latitude) of the Delivery Associate's location. Sample Value - 19.1119129
longitude|Double | 13,10 |Mandatory|The geocoordinate(Longitude) of the Delivery Associate's location. Sample Value - 72.9094089
trackingDt|String| | Mandatory|This is the timestamp of the tracking Date and Time in UTC and the mentioned Format. Sample Value - 2018-12-11T07:21:39Z
currentTime|Long| |Mandatory|This is the current timestamp at the time of sending the tracking data to LogiNext. Sample Value - 2018-12-11T07:21:39Z
speed|Number| | Mandatory| The speed of the Delivery Associate at the time of sending the tracking data.Current Speed in meters / second. This can be received from the Android system classes. More information on this can be found in the Android documentation <a href="https://developer.android.com/reference/android/location/Location.html#getSpeed()" target="_top">here
battery|Integer| 2 |Mandatory|This is the pattery percentage on the Delivery Associate's phone at the time of sending the tracking point. Sample Value - 92. MOre details on this can be found here<a href="https://developer.android.com/reference/android/net/ConnectivityManager#TYPE_MOBILE" target="_blank">.
accuracy|Number| | Mandatory|Estimated accuracy of the current location in meters Sample Value - 23.878000259
altitude|Number| | Optional|In meters Sample Value - 235
bearing |Number| | Optional|Horizontal distance of travel of the device, in degrees. If the phone has this sensor, then send this value. Sample Value - Any value between 0 to 3600. 0 is North.  Consider Clockwise movement.
locationSource|String| | Optional|Location Provider Values like - “fused” , “wifi”, “gps”
type |String| |Mandatory| | The tracking type field is used to identify if the tracking is coming from the Delivery Associate's phone or some other device. This is to be hardcoded to “MOBREG” in case the tracking points will be coming from the phone.
isFirstPointFl|Boolean| 1 | Mandatory| This is used to identify if the current tracking data being sent from the Delivery Associate's device is the first update after every login.|First Point - 0 Then there afterwards - 1 Sample Value -  0 (= False)  1 (= True)
lastLatitude|Double| 13,10 | Mandatory| Last known Latitude Note that if the isFirstPointFl value is “1”, then you can pass zero in this field Sample Value - 19.1119129
lastLongitude| Double | 13,10 | Mandatory|  Last known Longitude Note that if the isFirstPointFl value is “1”, then you can pass zero in this field Sample Value - 72.9094089
distanceFromLastLocation| Number|| Mandatory| Distance between last location update in meters. Note that if the isFirstPointFl value is “1”, then you can pass zero as the distance from last location. Sample Value - 23.5
previousTime|Long| | Mandatory|Timestamp of last location update in milliseconds Sample Value - 23.878000259
hasAccuracy|Boolean| 1 |Optional|True, if the current location has an accuracy 0 (= False) / 1 (= True)
hasBearing |Boolean| 1 |Optional|True, if the current location has a bearing 0 (= False) / 1 (= True)
hasSpeed | Boolean| 1 | Optional|True, if the current location has a speed 0 (= False) / 1 (= True)
userId|String| | Optional|User Id, as identified by LogiNext Sample Value - JohnD
networkType|String| |Optional|This field is used to identify the network type the Delivery Associate's phone is connected to when the tracking point is sent. This can be received from the Android core Connectivity Manager APIs <a href="https://developer.android.com/reference/android/net/ConnectivityManager#TYPE_MOBILE" target="_blank">here</a>. Sample Value can include WIFI / MOBILE / UNKNOWN
signalStrength|Integer| |Mandatory| This field is to signify the strength of the mobile network on the Delivery Associate's phone at the time when the tracking point is sent. (Wifi, GSM, LTE)|Sample Value - 23. This can be received from the Android core Connectivity Manager <a href="https://developer.android.com/reference/android/telephony/SignalStrength.html#getGsmSignalStrength()" target="_blank">here.
dataNetworkType|String| |Optional|Data Connectivity Type. Sample Values - 1xRTT, EDGE, LTE, CDMA, GPRS, HSPA
isGsmFl|Boolean| 1 | Optional|Current connectivity type. Sample Value - 0 (= False) 1 (= True). This can be received from the Android core Connectivity Manager <a href="https://developer.android.com/reference/android/telephony/SignalStrength.html#isGsm()" target="_blank">here.
isActiveNetworkMetered|Boolean| 1 |Optional| Is the currently active data network is metered. A network is classified as metered when the user is sensitive to heavy data usage on that connection due to monetary costs, data limitations or battery/performance issues. Sample Value -  0 (= False)  1 (= True). This can be received from the Android core Connectivity Manager APIs <a href="https://developer.android.com/reference/android/net/ConnectivityManager#isActiveNetworkMetered()" target="_blank">here.
appStatus| Integer||Optional| Activity status of the app (Foreground, Background, Service, Gone, Sleep, Visible, Unknown). Sample Values - 100 (~ Foreground) 400 (~ Background) 500 (~ Empty) 125 (~ Foreground_Service) 1000 (~ Gone) 200 (~ Visible). More information on this can be found on the Android Activity Manager documentation <a href="https://developer.android.com/reference/android/app/ActivityManager.RunningAppProcessInfo" target="_blank">here.
imei|String||Mandatory|IMEI number for device Sample Value - 911380134661315


### ESIGN / EPOD Upload

> Definition

```json
https://api.loginextsolutions.com/ShipmentApp/v1/mobile/image/upload
```

> Request Body

```json
{
"imageName": "image.png",
"orderLocation" : "DELIVERYLOCATION",
"imageType" : "ESIGN",
"orderReferenceIds":["a3bee2286d9f447d92e96f4d32c5569b", "a3bee2286d9f447d92e96f4d32c5569b"],
"latitude": 19.111755,
"longitude": 72.9095327
}
```



> Response

```json
{
  "status": 200,
  "message": "Uploaded successfully",
  "hasError": false
}

```
You can use this API to upload the Esign / Epod for the orders.
Please note that in the API Header, you will have to pass Content Type as multipart/form-data

#### Request

<span class="post">PUT</span>`https://api.loginextsolutions.com/ShipmentApp/v1/mobile/image/upload`


#### Request Parameters

Param | DataType | Length |  Required | Description
--------- | ------- | --------- | ---------- | ------------
imageName | String | 100 | Mandatory | This is the name with which the uploaded image will be saved. application.
orderLocation | Double | 15 | Mandatory | Possible values: PICKUPLOCATION, DELIVERYLOCATION<br>This defines that the image being uploaded is for order Pickup location or order Delivery location
imageType | String | 100 | Mandatory | Possible values: ESIGN, EPOD<br>This defines that the image being uploaded is of type ESIGN or EPOD
orderReferenceId | List |  |  | This is the Order Reference ID generated by the LN system for the order created. At least one referenceId is mandatory.
longitude | Double | 15 | Optional | Geo-location where where EPOD/ESIGN was taken<br>Sample Value - "17.996"
longitude | Double | 15 | Optional | Geo-location where where EPOD/ESIGN was taken<br>Sample Value - "17.996"


## Route Planning

> Definition

```json
https://api.loginextsolutions.com/TripApp/deliveryplanner/v1/plan
```

> Request Body

```json
{
  "routeName":"fas",
  "startLocation": {
    "latitude": 19.1164057,
    "longitude": 72.9047021
  },
  "vehicles":[{
    "name" : "cc",
    "capacity" : {
      "units" : 10,
      "weight" : 100,
      "volume" : 100
    },
    "type":["a","b","c"]
  }],
  "shipments":[{
    "name" :"s1",
    "location" : {
      "latitude": 19.1172561,
      "longitude": 72.8925094
    },
    "start" : "2017-10-27T16:00:00Z",
    "end" : "2017-10-27T18:00:00Z",
    "serviceTime" : 10,
    "weight" : 10,
    "volume" : 10,
    "type":["a","b","c"],
    "shipmentType" : "DELIVER"
  }]
}
```

> Response

```json
{
"status": 200,
"message": "We have received your request for delivery planning, it will take some time to plan all your deliveries. We will push the planned routes to your system once the planning is completed. Thank you!",
"hasError": false
}
```

#### Request

<span class="post">POST</span>`https://api.loginextsolutions.com/TripApp/deliveryplanner/v1/plan`


#### Request Body

Parameter | DataType | Length |  Required | Description
-----------|-------|------- |------- | ----------
routeName | String | 150 | Mandatory | Route name
startLocation.latitude | Double | 20 | Mandatory | Latitude of start location
startLocation.longitude | Double | 20 | Mandatory | Longitude of start location
vehicles | List |  | Mandatory | List of Delivery Associate
vehicles.name | String | 255 | Mandatory | Delivery Associate name
vehicles.capacity.weight | Integer | 20 | Optional | Capacity of Delivery Associate
vehicles.capacity.volume | Integer | 20 | Optional | Volume of Delivery Associate
vehicles.type | List |  | Optional | Type of Delivery Associate
shipments | List |  | Mandatory | List of orders
shipments.name | String | 100 | Mandatory | Order no.
shipments.location.latitude | Double | 20 | Mandatory | Order Latitude
shipments.location.longitude | Double | 20 | Mandatory | Order Longitude
shipments.start | String |  | Mandatory | Order start time window
shipments.end | String |  | Mandatory | Order end time window
shipments.serviceTime | Integer | 11 | Optional | Order service time in mins.
shipments.weight | Integer | 10 | Optional | Weight of order in Kg.
shipments.volume | Integer | 10 | Optional | Volume of order in cc.
shipments.type | List |  | Mandatory | Type of orders

## Geocoding

> Get Geocode - Sample Request

```json
{
  "apartment": "summerset building",
  "streetName": "powai",
  "landmark": "dmart",
  "locality": "hirananddanin",
  "city": "mumbai",
  "country": "India",
  "state": "Maharashtra",
  "pincode": "400076"
}
```

> Get Geocode - Sample Response

```json
{
 "status": 200,
 "message": "Geocodes Fetched Successfully",
 "data": [
   {
     "lat": 19.11736939999999,
     "lng": 72.9103214,
     "geocodingSource": "GOOGLE_PLACES"
   }
 ],
 "hasError": false
}

```

This API gets coordinates for a given location.

#### Request

<span class="post">POST</span>`https://api.loginextsolutions.com/GeofenceApp/mile/v1/serviceability/get`


#### Request Parameters

Parameter | DataType |  Required | Description
-----------|-------|------- | ----------
apartment | String | Optional | This is the apartment details.
streetName | String | Optional | This is the street name.
landmark | String | Optional | This is an address landmark.
locality | String | Optional | This is the address locality.
city | String | Optional | This is the address city.
country | String | Optional | This is the address country.
state | String |Optional | This is the address state.
pincode | String | Mandatory | This is the address pincode.



## Get Location Serviceability

> Sample Request

```json

{
"latitude" : "19.014585", 
"longitude" : "72.832830",
"apartment": "Inorbit Mall",
"streetName": "Link Road",
"locality": "Goregaon West",
"city": "Mumbai",
"country": "IND",
"state": "MH",
"postalCode": "4000104"
}

```

> Sample Response

```json
{
    "status": 200,
    "data": {
        "geofenceName": "GeofenceA",
        "geofenceType": "Hub",
        "geofenceShape": "Polygon",
        "geofenceArea": 335.55,
        "deliveryAssociates": [
            {
                "isActiveFl": true,
                "deliveryAssociateName": "John Doe",
                "deliveryAssociateRefId": "5c4fa64a97e24399a6cf91ef9767f980"
            }
        ]
    },
    "hasError": false
}

```

You can call this API to check if a particular location is serviceable. 

You can pass the geocoordinates (latitude and longitude) or address of a location  in the request body, and get a response regarding if an existing geofence exists with those geocoordinates. 

If address information without geocoordinates are passed, then this API will geocode the address provided and check for the generated geocoordinates.

This information can be used to tell users if your operations are present in certain areas or not.

The API returns data for 1 location per call.

Rate limit of this API is 20requests/second.

#### Request

<span class="post">POST</span>`https://api.loginextsolutions.com/GeofenceApp/mile/v1/serviceability/get`


#### Request Parameters

Parameter | DataType |  Required | Description
-----------|-------|------- | ----------
latitude | String | Conditional Mandatory | Geocoordinates(latitude) of the location, serviceability is to be checked for. If longitude is passed in the request, this field is mandatory.
longitude | String | Conditional Mandatory | Geocoordinates(longitude) of the location, serviceability is to be checked for. If latitude is passed in the request, this field is mandatory.
apartment | String | Optional | Apartment 
streetName | String | Optional | Street Name.
locality | String | Optional | Locality
city | String | Optional | City
country | String | Optional | Country
state | String | Optional | State
postalCode | String |Optional | Postal Code



# LogiNext OnDemand <sup>TM</sup>


## Order

### Create (Fixed Pickup)

> Definition

```json
https://api.loginextsolutions.com/ShipmentApp/ondemand/v1/create
```

> Request Body

```json
[ 
{
"cashOnDelivery" : 1000,
"cashOnPickup" : 1000,
"customerName" : "Anuradha S.",
"locality" : "McD Malaysia",
"subLocality" : "Petaling Jaya",
"address" : "JVLR Powai, Mumbai 400076",
"deliverPhoneNumber" : "60166788040",
"orderNo" : "testod3",
"distributionCenter" : "McDonald's Malaysia",
"paymentType" : "COD",
"latitude":31.1370445,
"longitude":80.6210216,
"deliverServiceTime":3,
"pickupServiceTime":3 ,
"deliveryType": "Groceries"
}
]
```



> Response

```json
{
  "status": 200,
  "message": "success",
  "referenceId": [
    "80ecfaccd4544980805aedeefc9325d3"
  ],
  "data": null,
  "hasError": false
}


```
Place a new delivery leg order with this API.

#### Request

<span class="post">POST</span>`https://api.loginextsolutions.com/ShipmentApp/ondemand/v1/create`

#### Request Parameters

Param | DataType |  Length | Required | Description
--------- | ------- | -------|------- | ------------
orderNo | String | 100 | Mandatory |  Order No.
distributionCenter | String | 255 | Mandatory | Distribution center's name
paymentType | String | 40 | Mandatory | Payment mode. Ex: COD, Prepaid
packageValue | Double | 10 | Optional | Package Value (This will be used when paymentType is Prepaid)
cashOnDelivery | Double | 10 | Mandatory(if paymentType is COD) | Cash to be collected on delivery
cashOnPickup | Double | 10 | Optional | Cash to be given on pickup
locality | String | 512 | Conditional Mandatory | Locality name of the delivery location. This has to be passed if geo coordinates are not passed for the Order to be of fixed pickup type.
subLocality | String | 512 | Conditional Mandatory | Sub-locality name. This has to be passed if geo coordinates are not passed for the Order to be of fixed pickup type.
address | String | 512 | Optional | Address where delivery should be done
deliverPhoneNumber | String | 255 | Mandatory | End customer contact number
customerName | String | 255 | Mandatory | End customer name
latitude | Double | 14 | Conditional Mandatory | geo coordinates(latitude) of the delivery location. This has to be passed if the locality and subLocality fields are not passed for the Order to be of fixed pickup type.
longitude | Double | 14 | Conditional Mandatory | geo coordinates(longitude) of the delivery location. This has to be passed if the locality and subLocality fields are not passed for the Order to be of fixed pickup type.
pickupServiceTime | Integer | 14 | Optional | Service time at the pickup location in minutes.
deliverServiceTime | Integer | 14 | Optional | Service time at the delivery location in minutes.
deliveryType | String | 40 | Optional | In certain operations, there are different skill sets / special delivery requirements through which the Delivery has to take place.<br>For e.g. - Groceries / Food items has to be separated with Toiletries<br>Orders for Cake cannot be clubbed with the Order for Flowers while delivering.<br>In such cases, if you want to classify the orders by using Delivery Type such that these orders get assigned to Pickup Associates who are configured in LogiNext system with these special skill-sets or types, then you can use this field.<br>Please note that before you pass orders with certain Delivery Types, you will have to first configure the Delivery Types.<br>Please ask your Account Manager to set these values for you.



### Create (Variable Pickup)

> Definition

```json
https://api.loginextsolutions.com/ShipmentApp/ondemand/v1/create
```

> Request Body

```json
[
  {
    "awbNumber": "AWB000001",
    "cashOnDelivery" : 1000.0,
    "cashOnPickup" : 1000.0,
    "pickupAccountCode" : "1234",
    "pickupAccountName" : "Name1",
    "pickupEmail" : "demo1@ymail.com",
    "pickupPhoneNumber" : "8888990000",
    "pickupApartment" : "Apartment1",
    "pickupStreetName" : "SC1",
    "pickupLandmark" : "LM1",
    "pickupLocality" : "AN1",
    "pickupCountry" : "INDIA",
    "pickupState" : "Maharashtra",
    "pickupCity" : "Mumbai",
    "pickupPinCode" : "400076",
    "pickupStartTimeWindow": "2016-07-15T08:00:00.000Z",
    "pickupEndTimeWindow": "2016-07-15T08:45:00.000Z",
    "pickupLatitude" : 19.1239285,
    "pickupLongitude" : 72.9094407,
    "pickupNotes" : "",
    "deliverAccountCode" : "5678",
    "deliverAccountName" : "Name2",
    "deliverEmail" : "demo2@ymail.com",
    "deliverPhoneNumber" : "7788888899",
    "deliverApartment" : "Apartment2",
    "deliverStreetName" : "SC2",
    "deliverLandmark" : "LM2",
    "deliverLocality" : "AN2",
    "deliverCountry" : "INDIA",
    "deliverState" : "Maharashtra",
    "deliverCity" : "Mumbai",
    "deliverPinCode" : "400077",
    "deliverNotes" : "",
    "deliverStartTimeWindow": "2016-07-16T08:00:00.000Z",
    "deliverEndTimeWindow": "2016-07-16T10:00:00.000Z",
    "deliverLatitude" : 19.0778737,
    "deliverLongitude" : 72.9055627,
    "orderNo" : "TestOrder",
    "paymentType" : "COD",
    "distributionCenter":"Mumbai",
    "isPartialDeliveryAllowedFl" : "N",
    "shipmentOrderDt" : "2016-07-15T08:00:00.000Z",
    "deliverCapacityInVolume":123.32,
    "deliverCapacityInWeight":15.2,
    "deliveryType":"Groceries"
  }
]
```



> Response

```json
{
  "status": 200,
  "message": "success",
  "referenceId": [
    "80ecfaccd4544980805aedeefc9325d3"
  ],
  "data": null,
  "hasError": false
}


```
Place a new delivery leg order with this API.

#### Request

<span class="post">POST</span>`https://api.loginextsolutions.com/ShipmentApp/ondemand/v1/create`

#### Request Parameters

Param | DataType |  Length | Required | Description
--------- | ------- | -------|-------- | ------------
orderNo | String | 100 | Mandatory |  Order No.
awbNumber | String | 1000 | Optional |  Awb No.
distributionCenter | String | 255 | Mandatory | Distribution center's name
shipmentOrderDt | Double | | Mandatory | Order Date. Format - YYYY-MM-DDTHH:MM:SS.SSSZ e.g. : 2016-07-01T11:18:00.000Z.
deliverCapacityInVolume | 10 | Double | Optional | Weight of package in Kg.
deliverCapacityInUnits | 10 | Double | Optional | Volume of package in CC
paymentType | String | 40 | Optional | Payment mode. Ex: COD, Prepaid
packageValue | Double | 10 | Optional | Package Value (This will be used when paymentType is Prepaid)
cashOnDelivery | Double | 10 | Mandatory(if paymentType is Delivery) | Cash to be collected on delivery
cashOnPickup | Double | 10 | Optional | Cash to be given on pickup
isPartialDeliveryAllowedFl | String | 1 | Optional | Is Partial Delivery allowed. Ex: Y/N
pickupAccountCode | String | 255 | Mandatory | Pickup customer-id
pickupAccountName | String | 255 | Mandatory | Pickup customer name
pickupEmail | String | 100 | Optional | Pickup customer email-id
pickupPhoneNumber | String | 255 | Mandatory | Pickup customer contact number
pickupApartment | String | 512 | Mandatory | Pickup customer apartment
pickupStreetName | String | 512 | Mandatory | Pickup customer street name
pickupLandmark | String | 512 | Optional | Pickup customer landmark
pickupLocality | String | 512 | Mandatory | Pickup area name
pickupCountry | String | 512 | Mandatory | Pickup country code
pickupState | String | 512 | Mandatory | Pickup state code
pickupCity | String | 512 | Mandatory | Pickup city
pickupPincode | String |20 | Mandatory | Pickup pincode
pickupStartTimeWindow | Date | | Mandatory | Pickup Start time window of order. Format - YYYY-MM-DDTHH:MM:SS.SSSZ e.g. : 2016-07-01T11:18:00.000Z.
pickupEndTimeWindow | Date | | Mandatory | Pickup End time window of order. Format - YYYY-MM-DDTHH:MM:SS.SSSZ e.g. : 2016-07-01T11:18:00.000Z.
pickupLatitude | Double |  | Optional | Latitude of pickup location
pickupLongitude | Double |  | Optional | Longitude of pickup location
pickupNotes | String | 512 | Optional | Pickup notes
deliverAccountCode | String | 255 | Mandatory | Deliver customer-id
deliverAccountName | String | 255 | Mandatory | Deliver customer name
deliverEmail | String | 100 | Optional | Deliver customer email-id
deliverPhoneNumber | String | 255 | Mandatory | Deliver customer contact number
deliverApartment | String | 512 | Mandatory | Deliver customer apartment
deliverStreetName | String | 512 | Mandatory | Deliver customer street name
deliverLandmark | String | 512 | Optional | Deliver customer landmark
deliverLocality | String | 512 | Mandatory | Deliver area name
deliverCountry | String | 512 | Mandatory | Deliver country code
deliverState | String | 512 | Mandatory | Deliver state code
deliverCity | String | 512 | Mandatory | Deliver city
deliverPincode | String | 20 | Mandatory | Deliver pincode
deliverStartTimeWindow | Date | 100 | Mandatory | Deliver Start time window of order. Format - YYYY-MM-DDTHH:MM:SS.SSSZ e.g. : 2016-07-01T11:18:00.000Z.
deliverEndTimeWindow | Date | 100 | Mandatory | Deliver End time window of order. Format - YYYY-MM-DDTHH:MM:SS.SSSZ e.g. : 2016-07-01T11:18:00.000Z.
deliverLatitude | Double | | Optional | Latitude of deliver location
deliverLongitude | Double | | Optional | Longitude of deliver location
deliverNotes | String | 512 | Optional | Deliver notes
deliveryType | String | 40 | Optional | In certain operations, there are different skill sets / special delivery requirements through which the Delivery has to take place.<br>For e.g. - Groceries / Food items has to be separated with Toiletries<br>Orders for Cake cannot be clubbed with the Order for Flowers while delivering.<br>In such cases, if you want to classify the orders by using Delivery Type such that these orders get assigned to Pickup Associates who are configured in LogiNext system with these special skill-sets or types, then you can use this field.<br>Please note that before you pass orders with certain Delivery Types, you will have to first configure the Delivery Types.<br>Please ask your Account Manager to set these values for you.

### Get

> Definition

```json
 https://api.loginextsolutions.com/ShipmentApp/ondemand/v1/shipment?end_date=2017-03-07+18:29:59&start_date=2016-02-01+18:30:00&status=ALL&order_no=LN01234567
```

> Response

```json
{
    "status": 200,
    "message": "SUCCESS",
    "data": [
        {
            "referenceId": "f68420e67be84b2894aab6ea9634c4f9",
            "orderNo": "LN01234567",
            "awbNumber": "awbcheck",
            "clientName": "Tezz Foods",
            "branchName": "Green Leaf",
            "origin": "Apartment1,SC1,AN1,LM1,Mumbai,400076",
            "destination": "Apartment2,SC2,AN2,LM2,Mumbai,400077",
            "shipmentOrderTypeCd": "DELIVER",
            "orderState": "FORWARD",
            "shipmentOrderDt": 1468569600000,
            "startTimeWindow": 1468569600000,
            "endTimeWindow": 1468663200000,
            "paymentType": "COD",
            "notes": "",
            "packageValue": 1000,
            "status": "NOTDISPATCHED",
            "plannedServiceTime": 0,
            "plannedDistance": 22.6,
            "customerCode": "5678",
            "customerName": "Name2",
            "customerPhoneNumber": "7788888899",
            "noOfAttempts": 0,
            "isDelayed": true
        }
    ],
    "hasError": false
}
```

With this API you can fetch the list of your orders and the associated order information.

#### Request

<span class="post">PUT</span>` https://api.loginextsolutions.com/ShipmentApp/ondemand/v1/shipment?end_date=2017-03-07+18:29:59&start_date=2016-02-01+18:30:00&status=ALL&order_no=LN01234567`

#### Request Body

Param | DataType |  Required | Description
--------- | ------- | ---------- | ------------
start_date | Date | Conditional Mandatory |  If order_no is not passed in the request,then this field is mandatory.Range of date from which orders can be searched.<BR>Format 'yyyy-MM-dd HH:mm:ss'
end_date | Date | Conditional Mandatory |  If order_no is not passed in the request,then this field is mandatory.Range of date upto which orders can be searched.<BR>Format 'yyyy-MM-dd HH:mm:ss'
status | String | Optional |  If order_no is passed in the request,then status will not be considered for filtering the orders.Order status. <BR>Ex: NOTDISPATCHED,INTRANSIT,COMPLETED,<BR>NOTCOMPLETED,PICKEDUP(Only for First Mile),CANCELLED
order_no | String | Optional | Order Number(Only one order number can be passed at a time.If not passed ,all the orders for the specified date range will be fetched)

Status | Filter applied on orders
--------- | -------
NOTDISPATCHED | Orders will be fetched for which either the Order Start Date & Time Window or the Order End Date & Time Window lies within the range specified.
INTRANSIT | Orders will be fetched for which the Actual Delivery Start Date & Time lies within the range specified.
COMPLETED | For First Mile, an order is marked COMPLETED when it is PICKEDUP and DELIVERED at the hub. For Last Mile, an order is marked COMPLETED once it is DELIVERED to the end customer.<BR>Orders will be fetched for which the Actual Delivery End Date & Time lies within the range specified.
NOTCOMPLETED | For First Mile, when the order is  NOTPICKEDUP,it is marked as NOTCOMPLETED. For Last Mile, when the order is PICKEDUP but  NOTDELIVERED, it is marked as NOTCOMPLETED. <BR>Orders will be fetched for which the Actual Delivery End Date & Time lies within the range specified.
CANCELLED | Orders will be fetched for which the Cancellation Date & Time lies within the range specified.
ALL | Superset of all the filters mentioned for the above statuses will be considered.


### Cancel

> Definition

```json
https://api.loginextsolutions.com/ShipmentApp/ondemand/v1/cancel
```

> Request Body

```json
[
  "e0eaebdd84ac4c40af72d827ab610090",
  "f68420e67be84b2894aab6ea9634c4f9"
]
```

> Response

```json
{
  "status": 200,
  "data": "Order(s) cancelled successfully",
  "hasError": false
}
```

Use this API to cancel an order.

#### Request

<span class="post">PUT</span>`https://api.loginextsolutions.com/ShipmentApp/ondemand/v1/cancel`

#### Request Body

Parameter | DataType |  Required | Description
-----------|-------|------- | ----------
reference_ids | List  | Mandatory | Reference Id associated with the order.


## Mobile

Push data into the LogiNext system through your field application. 

NOTE: These APIs require the Delivery Associate's token. Please view the Authenticate Section of this page for more information on acquiring a Delivery Associate Token.


### Accept Order

> Definition

```json
https://api.loginextsolutions.com/ShipmentApp/v1/mobile/order/accept
```

> Request Body

```json
{
  "orderReferenceId":"a3bee4486d9f467d72e96f4d32c5569b",
  "parentOrderNo":"1316MDO",
  "orderAcceptTime":"2017-12-27T10:00:00Z",
  "latitude": 19.111555,
  "longitude": 72.9099327
}
```

> Response

```json
{
  "status": 200,
  "message": "success",
  "hasError": false
}
```

With this API, you can mark the Order as Accepted by the Delivery Associate / Associate / Driver / Fried Executive.
Please note that in headers for this API, you will have to pass the Delivery Associate's Token and Key and not the Account level Token and Key.

You can fetch the Delivery Associate's Token and Key by calling the Delivery Associate Authenticate API.

#### Request

<span class="post">PUT</span>`https://api.loginextsolutions.com/ShipmentApp/v1/mobile/order/accept`

#### Request Body

Parameter | DataType | Length | Required | Description
-----------|-------|------- | ----|----------
orderReferenceId | String | 32 | Mandatory | This is the LogiNext Order Reference ID created when the order is added in the LogiNext system.<br>If your Order is Single Pick-up - Single destination, then pass the Order Reference ID generated against that Order No.<br>If your Order is Single Pick-up - Multiple destination, then pass any one of the order's Reference ID. <br>Please note, if you pass the Order Reference ID in combination with the Parent Order No., then all the orders under that Parent Order No. will be updated with the ACCEPTED status.<br>If you want to update the status of only one specific order (out of the many orders under a particular Parent Order No.) , then you need not have to pass the Parent Order No.
parentOrderNo | String | 100 | Optional | If your Order is Single Pick-up - Multiple destination and if you want to update the status of the all orders under the Parent Order, then pass the Parent Order No. <br>If you want to update the status of only one specific order (out of the many orders under a particular Parent Order No.) , then you need not have to pass the Parent Order No. <br>If your Order is Single Pick-up - Single, then you need not have to pass the Parent Order no.
orderAcceptTime | String | 32 | Optional | This is the timestamp (in UTC format) when the order was accepted. <br>This cannot be greater than the current time (time at which the API request is called). <br>If not passed, the current timestamp will be considered as the timestamp for the order acceptance.<br>Sample Value - 2017-12-27T10:00:00Z
latitude | Double | 15 | Optional | Geo-location where Order was accepted. Note that this is not used for ETA calculation. That happens using Tracking points.
Sample Value - "17.996"
longitude | Double | 15 | Optional | Geo-location where Order was accepted. Note that this is not used for ETA calculation. That happens using Tracking points.
Sample Value - "17.996"

### Reject Order

> Definition

```json
https://api.loginextsolutions.com/ShipmentApp/v1/mobile/checkin
```

> Request Body

```json
{
  "orderReferenceIds":["6b106144208243ffb4b8c4114fd44f123d"],
  "checkInLocation":"PICKUP",
  "checkinLatitude":12.11,
  "checkinLongitude":78.11223,
  "checkInTime":"2018-02-08T09:30:00Z"
}
```

> Response

```json
{
  "status": 200,
  "message": "success",
  "hasError": false
}
```

With this API, the delivery assosicate can check In at the pickup or delivery location

Please note that in headers for this API, you will have to pass the Delivery Associate's Token and Key and not the Account level Token and Key.

You can fetch the Delivery Associate's Token and Key by calling the Delivery Associate Authenticate API.

#### Request

<span class="post">PUT</span>`https://api.loginextsolutions.com/ShipmentApp/v1/mobile/checkin`

#### Request Body

Parameter | DataType | Length | Required | Description
-----------|-------|------- | ----|----------
orderReferenceIds | String | 100 | Mandatory | This is the list of order Reference Ids for which the check in event is being called.
checkInLocation | String | 32 | Mandatory | This will be 'PICKUP' in case of the pickup location and 'DELIVER' for the delivery location.
checkinLatitude | Double | 15 | Optional | The geolocation coordinate (latitude) of the checkinLocation.
checkinLongitude | Double | 15 | Optional | The geolocation coordinate (longitude) of the checkinLocation.
checkinTime | Date | | Mandatory | This is the timestamp of the check in event. Input is expected in UTC format


### Check In

> Definition

```json
https://api.loginextsolutions.com/ShipmentApp/v1/mobile/checkin
```

> Request Body

```json
{
  "orderReferenceIds":["6b106144208243ffb4b8c4114fd44f123d"],
  "checkInLocation":"PICKUP",
  "checkinLatitude":"12.11",
  "checkinLongitude":"78.11223",
  "checkInTime":"2018-02-08T09:30:00Z"
}
```

> Response

```json
{
    "status": 200,
    "message": "Check in marked successfully",
    "hasError": false
}

```

With this API, the Delivery associate can Check In at the time of Order Delivery at the Deliver location.

Please note that in headers for this API, you will have to pass the Delivery Associate's Token and Key and not the Account level Token and Key.

You can fetch the Delivery Associate's Token and Key by calling the Delivery Associate Authenticate API.

#### Request

<span class="post">PUT</span>`https://api.loginextsolutions.com/ShipmentApp/v1/mobile/checkin`

#### Request Body

Parameter | DataType | Length | Required | Description
-----------|-------|------- | ----|----------
orderReferenceId | List | 32 | Mandatory | This is the LogiNext Order Reference ID created when the order is added in the LogiNext system.<br>If your Order is Single Pick-up - Single destination, then pass the Order Reference ID generated against that Order No.<br>If your Order is Single Pick-up - Multiple destination, then pass any one of the order's Reference ID.
checkInLocation | String | 100 | Mandatory | This can be "PICKUP" or "DELIVER".
checkinLatitude | Double | 100 | Optional | Geocoordinate(Latitude) for the Check In location.
checkinLongitude | Double | 100 | Optional | Geocoordinate(Longitude) for the Check In location.
checkInTime | Date | 100 | Mandatory | Check In Time in UTC format - YYYY-MM-DDTHH:MM:SS.SSSZ e.g. : 2016-07-01T11:18:00.000Z.


### ESIGN / EPOD Upload

> Definition

```json
https://api.loginextsolutions.com/ShipmentApp/v1/mobile/image/upload
```

> Request Body

```json
{
"imageName": "image.png",
"orderLocation" : "DELIVERYLOCATION",
"imageType" : "ESIGN",
"orderReferenceIds":["a3bee2286d9f447d92e96f4d32c5569b", "a3bee2286d9f447d92e96f4d32c5569b"],
"latitude": 19.111755,
"longitude": 72.9095327
}
```



> Response

```json
{
  "status": 200,
  "message": "Uploaded successfully",
  "hasError": false
}

```
You can use this API to upload the Esign / Epod for the orders.
Please note that in the API Header, you will have to pass Content Type as multipart/form-data

#### Request

<span class="post">PUT</span>`https://api.loginextsolutions.com/ShipmentApp/v1/mobile/image/upload`


#### Request Parameters

Param | DataType | Length |  Required | Description
--------- | ------- | --------- | ---------- | ------------
imageName | String | 100 | Mandatory | This is the name with which the uploaded image will be saved. application.
orderLocation | Double | 15 | Mandatory | Possible values: PICKUPLOCATION, DELIVERYLOCATION<br>This defines that the image being uploaded is for order Pickup location or order Delivery location
imageType | String | 100 | Mandatory | Possible values: ESIGN, EPOD<br>This defines that the image being uploaded is of type ESIGN or EPOD
orderReferenceId | List |  |  | This is the Order Reference ID generated by the LN system for the order created. At least one referenceId is mandatory.
longitude | Double | 15 | Optional | Geo-location where where EPOD/ESIGN was taken<br>Sample Value - "17.996"
longitude | Double | 15 | Optional | Geo-location where where EPOD/ESIGN was taken<br>Sample Value - "17.996"


# LogiNext Field TM

## Tasks

Create Tasks in the LogiNext system using the Tasks API. Tasks will be assigned a referenceId that will be returned in the API response. This refernceId can be used to identify the Task later.

To view the Tasks created in the LogiNext Web Application, select the correct date range in the date filter on the screen.

### Create

> Definition

```json
https://api.loginextsolutions.com/ShipmentApp/field/v2/create
```

> Request Body

```json
[
  {
    "taskNo": "GR432U5",
    "awbNumber": "435-16685675",
    "shipmentTaskTypeCd": "DELIVER",
    "taskState": "FORWARD",
    "autoAllocateFl": "N",
    "shipmentTaskDt": "2016-07-15T10:30:00.000Z",
    "distributionCenter": "Chicago",
    "packageWeight":"10",
    "packageVolume": "4500",
    "paymentType": "Prepaid",
    "packageValue": "500",
    "numberOfItems": 1,
    "partialDeliveryAllowedFl": "Y",
    "returnAllowedFl": "Y",
    "cancellationAllowedFl": "N",    
    "deliverBranch": "Boston",
    "deliverServiceTime": "20",
    "deliverEndTimeWindow": "2016-07-18T10:31:00.000Z",
    "deliverStartTimeWindow": "2016-07-16T10:31:00.000Z",
    "deliveryType": "Groceries",
    "deliveryLocationType":"Home",
    "deliverAccountCode": "Matt001",
    "deliverAddressId": "Home",
    "deliverAccountName": "Mathew Richardson",
    "deliverEmail":"m.richardson@testmail.com",
    "deliverPhoneNumber":"3125096995",
    "deliverApartment": "201",
    "deliverStreetName": "E Randolph St",
    "deliverLandmark": "Opp. Chiptole",
    "deliverLocality": "Down Towm Chicago",
    "deliverCity": "Chicago",
    "deliverState": "IL",
    "deliverCountry": "USA",
    "deliverPinCode": "60602",
    "deliverLatitude":41.882702,
    "deliverLongitude":-87.619392,    
    "returnBranch": "Chicago",
    "pickupNotes": "PickedUp",
    "deliverNotes": "Delivered"
    
  }
]
```



> Response

```json
{
    "status": 200,
    "message": "Task(s) created successfully",
    "data": [
        {
            "index": 0,
            "referenceId": "6a34c7274df0489f97c0f891514b488b",
            "taskNumber": "ww1223",
            "shipmentTaskTypeCd": "DELIVER",
            "taskState": "FORWARD"
        }
    ],
    "hasError": false
}

```
Create delivery tasks with this API in the LogiNext system. Tasks will be created and assigned a reference ID that can be used at a leter time to identify the task.

#### Request

<span class="post">POST</span>`https://api.loginextsolutions.com/ShipmentApp/field/v2/create`

#### Request Parameters

Param | DataType | Length |  Required | Description
--------- | ------- | ---------- | ---------- | ------------
taskNo | String | 100 | Mandatory |  This is the Task No.
awbNumber | String  | 1000 | Optional | This is the airway Bill No.
shipmentTaskTypeCd | String  | 40 | Mandatory | This is the task type code. DELIVER for delivery leg task
taskState | String  | 512 | Mandatory | State of task. Ex: FORWARD
autoAllocateFl| String | 50 | Optional | This can be "Y" or "N". If set to "Y", the Task will be automatially allocated to the nearest Delivery Associate when it is created in the system. If "N", the Delivery Associate will get notified if the Task is ready to be allocated to them, and they can choose to Accept or Reject it.
shipmentTaskDt | Date |  | Mandatory | Task Date Format - YYYY-MM-DDTHH:MM:SS.SSSZ e.g. : 2016-07-01T11:18:00.000Z.
distributionCenter | String | 255 | Mandatory | This is the distribution center's name
packageWeight | Double | 10 | Optional | This is the weight of package in Kg.
packageVolume | Double | 10 | Optional | This is the volume of package in CC
packageValue | Double | 10 | Optional | This is the value of package
numberOfItems | Integer | 20 | Optional | This is the number of crates
paymentType | String | 40 | Optional | This is the payment mode. Ex: COD - Cash On Delivery, Prepaid
partialDeliveryAllowedFl | String | 50 | Optional | This is the is Partial Delivery allowed. Ex: Y/N. Default value is N.
returnAllowedFl | String | 1 | Optional | This field specifies if the task can be returned. Ex: Y/N. Default value is Y.
cancellationAllowedFl | String | 1 | Optional | Is Cancellation allowed. Ex: Y/N. Default value is Y.
deliverBranch | String | 255 | Mandatory | Name of delivery branch
deliverServiceTime | Integer | 11 | Mandatory | Deliver service time in mins.
deliverStartTimeWindow | Date |  | Mandatory | Deliver start time window. Format - YYYY-MM-DDTHH:MM:SS.SSSZ e.g. : 2016-07-01T11:18:00.000Z.
deliverEndTimeWindow | Date |  | Mandatory | Deliver end time window. Format - YYYY-MM-DDTHH:MM:SS.SSSZ e.g. : 2016-07-01T11:18:00.000Z.
deliveryType | String | 40 | Optional | Task delivery type. Ex: TRK - Truck, VAN - Van, DLBOY - Delivery Boy
deliveryLocationType | String | 40 | Optional | Type of delivery location. Ex: CUSTOMER, PUP
deliverAccountCode | String | 255 | Mandatory | This is the cutomer code of the deliver customer.
deliverAddressId | String |255 | Optional | This is the Address ID of the deliver customer.
deliverAccountName | String | 255 | Conditional Mandatory | This is the deliver account name. This field in Non Mandatory in case Customer Profiling in ON.
deliverEmail | String | 100 | Optional | This is the email ID details of the customer.
deliverPhoneNumber | String | 255 | Optional | This is the phone number of the delivery customer.
deliverApartment | String | 512 | Conditional Mandatory | This is the apartment details of the delivery customer. This field in Non Mandatory in case Customer Profiling in ON.
deliverStreetName | String | 512 | Conditional Mandatory | This is the street name of the delivery customer.
deliverLandmark | String | 512 | Optional | This field holds any identifying landmark's around the customer's addess.
deliverLocality | String | 512 | Conditional Mandatory | This is the locality of the delivery customer. This field in Non Mandatory in case Customer Profiling in ON.
deliverCity | String | 512 | Conditional Mandatory | This is the city name of the delivery customer. This field in Non Mandatory in case Customer Profiling in ON.
deliverState| String | 512 | Conditional Mandatory | This is the state code of the delivery customer. Please refer to the list of state codes provided in the "State Codes" section. This field in Non Mandatory in case Customer Profiling in ON.
deliverCountry | String | 512 | Conditional Mandatory | This is the country code of the delivery customer. Please refer to the list of country codes provided in the "Country Codes" section. This field in Non Mandatory in case Customer Profiling in ON.
deliverPinCode | String | 20 | Conditional Mandatory | This is the pincode of the delivery customer. This field in Non Mandatory in case Customer Profiling in ON.
deliverLatitude | Double |  | Optional | The geolocation coordinate (latitude) of the delivery customer.
deliverLongitude | Double |  | Optional | The geolocation coordinate (longitude) of the delivery customer.
returnBranch | String | 255 | Mandatory | Name of return branch.
pickupNotes | String | 512 | Optional | Additional pickup comments associated with the task.
deliverNotes | String | 512 | Optional | Additional delivery comments associated with the task.



### Get

> Definition

```json
https://api.loginextsolutions.com/ShipmentApp/field/v1/task?end_date=2017-03-07+18:29:59&start_date=2016-02-01+18:30:00&status=ALL&task_no=GKS12567&customer_code=123&employee_id=134367&page_no=1&page_size=10
```



> Response

```json
{
    "status": 200,
    "message": "SUCCESS",
    "data": [
        {
            "taskReferenceId": "d4f455a2ff074449acf79371ea55a0fe",
            "taskNo": "ST3421S",
            "clientName": "WritCare  Private Limited_UAT",
            "branchName": "WritCare Private Limited Main Branch",
            "origin": "WritCare  Private Limited Main Branch",
            "destination": ".Mumbai, Maharashtra, INDIA, .",
            "shipmentTaskTypeCd": "DELIVER",
            "taskState": "FORWARD",
            "shipmentTaskDt": 1529799037000,
            "startTimeWindow": 1530347401000,
            "endTimeWindow": 1530376801000,
            "paymentType": "COD",
            "packageValue": 0,
            "status": "NOTDISPATCHED",
            "deliveryMediumName": "Custodian4",
            "deliverMediumPhoneNumber": "9999999994",
            "assignedThrough": "Manually",
            "tripName": "TRIP-58",
            "eta": 1530361561000,
            "plannedDistance": 3.254,
            "distanceFromHub": 7.713,
            "plannedStartDt": 1530342001000,
            "plannedEndDt": 1530361561000,
            "orderSequence": 20,
            "customerCode": "P3ENMI17",
            "customerName": "P3ENMI17",
            "customerPhoneNumber": "",
            "packageWeight": 0,
            "noOfAttempts": 0,
            "isDelayed": false,
            "originLatitude": 19.082,
            "originLongitude": 72.849
        }
    ]
}

```

Retrieve orders and all the order associated information with this API.

#### Request

<span class="post">GET</span>`https://api.loginextsolutions.com/ShipmentApp/field/v1/task`


#### Request Parameters

Param | DataType | Length |  Required | Description
--------- | ------- | ------- | ---------- | ------------
start_date | Date |  | Conditional Mandatory |  If task_no is not passed in the request, then this field is mandatory. Range of date from which tasks can be searched. This will return tasks based on the task fulfillment date start time window. <BR>Format 'yyyy-MM-dd HH:mm:ss'
end_date | Date |  | Conditional Mandatory |  If task_no is not passed in the request, then this field is mandatory. Range of date upto which tasks can be searched. This will return tasks that have fulfillment end times less than the entered time.<BR>Format 'yyyy-MM-dd HH:mm:ss'
status | String | 20 | Optional |  If task_no is passed in the request,then status will not be considered for filtering the orders.Task status. <BR>Ex: NOTDISPATCHED,INTRANSIT,COMPLETED,<BR>NOTCOMPLETED,PICKEDUP(Only for First Mile),CANCELLED
order_no | String | 100 | Optional | Task Number(Only one order number can be passed at a time.If not passed ,all the tasks for the specified date range will be fetched)
page_no | Integer | | Optional | This parameter lets you specify the page number. It is used to page through the tasks. This is optional parameter and default value (if it isn't specified) will be 1. 
page_size | Integer | |  Optional |  This parameter lets you specify the count of tasks to return in your API call. This is optional parameter and default value (if it isn't specified) will be 50. The maximum accepted value is 100; higher values will be accepted but you will only get 100 records.
customer_code | String | |  Optional | This is the Customer Address ID parameter. You can pass one customer Id at a time. The result will be list of all the tasks created for the mentioned customer ID
employee_id | String | | Optional | This is the Driver National ID  parameter. You can pass one driver Id at a time. The result will be list of all the tasks which were assigned to this Driver ID


Status | Filter applied on orders
--------- | -------
NOTDISPATCHED | Tasks will be fetched for which either the Tasks Start Date & Time Window or the Tasks End Date & Time Window lies within the range specified.
INTRANSIT | Tasks will be fetched for which the Actual Delivery Start Date & Time lies within the range specified.
COMPLETED | For First Mile, an Task is marked COMPLETED when it is PICKEDUP and DELIVERED at the hub. For Last Mile, an order is marked COMPLETED once it is DELIVERED to the end customer.<BR>Orders will be fetched for which the Actual Delivery End Date & Time lies within the range specified.
NOTCOMPLETED | For First Mile, when the Task is  NOTPICKEDUP,it is marked as NOTCOMPLETED. For Last Mile, when the Tasks is PICKEDUP but  NOTDELIVERED, it is marked as NOTCOMPLETED. <BR>Tasks will be fetched for which the Actual Delivery End Date & Time lies within the range specified.
CANCELLED | Orders will be fetched for which the Cancellation Date & Time lies within the range specified.
ALL | Superset of all the filters mentioned for the above statuses will be considered.


### Update Status

> Definition

```json
https://api.loginextsolutions.com/ShipmentApp/field/v1/update/status
```

> Request Body

```json
{
  "newStatus":"NOTDISPATCHED",
  "taskDetails":
  [{
    "taskReferenceId":"6186d5fc6e324c42abb5ea1a32e05f66",
    "reasonCd":"DBUNAVAILABLE",
    "otherReason":"",
    "latitude": 19.117369,
    "longitude": 72.910214,
    "updateTime":"2018-07-18T10:31:00.000Z"
  },
  {
    "taskReferenceId":"6186d7r5te324c42abb5ea1a32x45f66",
    "reasonCd":"DBUNAVAILABLE",
    "otherReason":"",
    "latitude": 19.117369,
    "longitude": 72.913214,
    "updateTime":"2018-07-18T10:31:00.000Z"

  }]

}
```

> Response

```json
{
    "status": 200,
    "message": "Task status changed successfully",
    "hasError": false
}


```
With this API, you will be able to update the the status of an Order.
You can pass multiple order reference IDs and can update one or more parameters.

#### Request

<span class="post">PUT</span>`https://api.loginextsolutions.com/ShipmentApp/field/v1/update/status`


#### Request Parameters

Param | DataType | Length |  Required | Description
--------- | ------- | ---------- | ---------- | ------------
newStatus | String | 20 | Mandatory |  One status for multiple orders.The orders will be updated with this new status<br>Available Values - <PICKEDUP> - When an Order has been picked up by a Delivery Associate<br>DELIVERED - When an order has been Delivered by the associate<br>NOTPICKEDUP - When the associate reached the Pick-up location, but could not pick-up the order due to one or the other reason<br>NOTDELIVERED - When the associate reached the delivery location, but could not deliver the order due to one or the other reason
orderReferenceId | String | 100 | Mandatory |  This is the LogiNext Reference ID for the Order<br>This is generated when the order is added in the LogiNext application.
reasonCd | String | 255 | Conditional Mandatory | Mandatory depending upon the status selected : NOTDELIVERED, NOTPICKEDUP, CANCELLED<br>Else Optional.<br>If you have pre-configured the reasons for Order Status Update - NOTDELIVERED, NOTPICKEDUP and CANCELLED in LogiNext application, then it is mandatory to mention that relevant configured reason here.<br>One of the other values here is OTHER, in case the delivery Associate selects the reason as Others.
otherReason | Date |  | Conditional Mandatory | Mandatory when reasonCd is OTHER
latitude | Double | 15 | Conditional Optional | Geo-location where Order status was updated<br>Sample Value - "17.996"
otherReason | Date | 15 | Conditional Optional | Geo-location where Order status was updated<br>Sample Value - "17.996"
updateTime | Date | 15 | Conditional Optional | This is the timestamp (in UTC format) when the order status was changed. This cannot be greater than the time at which the API is hit. If not passed, the timestamp of the API hit is considered as the timestamp for the status change.

# Custom Fields

> Request

```json

"customFields":[
    {

    "field":"cutOffDate",
    "value":""2018-06-25T07:31:39Z"
    }
    
    ]
```


If you require certain additional fields to store information regarding your Orders or Resources in LogiNext, you can use our Custom Fields features.

With Custom Fields, you can enter information for reporting and analytics purposes specific to your business use case.

For eg - If you need to look for specific servicability constraints like cut off times within with a certain area/ geofence can be serviced, you can configure a cut off time custom field in LogiNext that will display the availability timelines for that area/ geofence.

To configure Custom Fields for your account, You can do so from the Custom Fields section of your Admin module.

Once configured, you can enter data for the custom fields like any other field in LogiNext. These fields are currently available in the APIs and UI.

Please Note that if you send these fields in the API without first configuring them in your LogiNext account, the LogiNext API will NOT create a new Custom Field. You will receive a success response from such an API call, but the data sent in the 'customField object will not be considered. The data passed in the API can only be associated with an already existing Custom Field with the identifier specified in the request. 

If using the API, you will need to add the Custome Fields object on the right as part of the API request body to create the new fields in LogiNext.

For eg - If you have Custom Fields configured for the Orders module, you will need to append the request on the right to the request body of the create order API.

For a Custom Field you must define the following attributes

Attribute|Description
----------|-----------
Type| Data Type of the Custom field.
Field| the name of the custom field.

LogiNext currently supports the following field types - 

Text.

Number.

Dropdown.

DateTime.

Date.

Time.

Note that Date and DateTime type of type of Custom Fields will be sent in UTC format in POST API calls, and will be fetched in Epoch format in Get API calls. 

You can include the following validations in your custom fields at the time of creating them -

Mandatoy/ Optional.

Min length/ Man length.


# Webhooks

Webhooks allow you to build or set up integrations which subscribe to certain events like Order Creation, Route Planning, Trip Start, etc. on LogiNext System. When one of those events is triggered, we'll send a HTTP POST request to the webhook's configured URL (end point).

Note -

1. LogiNext Webhooks are sent via HTTP REST protocol.
2. The default content type for all the LogiNext Webhooks is "application/ json".
3. If you have a request to support the other content types like "application/xml " or "application/x-www-form-urlencoded", then please get in touch with your assigned CSA (Customer Service Associate) and request the same.
4. All the dates and timestamps that are represented in the Webhooks are in the UTC timezones.
5. Please share the end-point on your system to consume the Webhooks with your assigned CSAs.
6. You can choose to configure an additional security parameter in the LogiNext webhooks Header in the 'x-loginext-signature' header. You can choose to have an APP SECRET configured in LogiNext for this header, and LogiNext will send this APP SECRET in all your configured webhooks. You can validate the value of this header to verify that the webhook request originated from LogiNext.


## Create Order

> Response

```json
{
  "orderNo": "CATS487",
  "orderState": "FORWARD",
  "orderLeg": "DELIVER",
  "awbNumber": "AW234-TG",
  "notificationType": "ORDERCREATIONNOTIFICATION",
  "timestamp": "2018-06-25 07:31:39",
  "referenceId": "143b28d87ghf46098de38b0ccce51a5d",
  "deliverAccountCode": "B1372"
  "deliverAddressId": "HOME"
}
```

This notification is sent when an order is created.

Param | DataType | Description
--------- | ------- | ----------
orderNo | String | Order No.
orderState | String | State of order. Ex: FORWARD, REVERSE
orderLeg | String | Order leg Ex: PICKUP, DELIVER
awbNumber | String | AWB Number for the order
notificationType | String | ORDERCREATIONNOTIFICATION
timestamp | String | Order creation timestamp
referenceId | String | Order reference id.
deliverAccountCode| String| Custoemr ID of the deliver customer
deliverAddressId | String | Address ID of the delivery customer

## Update Order

> Response

```json
{
  "orderNo": "P_Aetos1",
	"notificationType": "ORDERUPDATENOTIFICATION",
  "orderReferenceId": "93780c3292ba4ee4809ad125ef97",
  "vehicleNumber":"MH04DY69",
	"awbNumber": "AWB001",
	"deliveryMediumName": "kumari2",
	"phoneNumber": "6590110114",
	"orderState": "FORWARD",
	"shipmentCrateMapping":  [
    {
      "crateCd": "Crt A001",
      "crateAmount": 500.65,
      "shipmentlineitems": [
        {
          "itemCd": "10001001",
          "itemName": "Fresh Basket Lemon",
          "itemPrice": 12,
          "itemQuantity": 1,
          "itemType": "P",
          "itemWeight": 0,
          "statusCd": "PACKED",
          "loadedQuantity": 0,
          "unloadedQuantity": 0,
          "isActiveFl": true
        }
      ],
      "noOfUnits": 14,
      "loadedUnits": 0,
      "unloadedUnits": 0,
      "orderNo": "P_Aetos1",
      "isActiveFl": true
    }
  ],
	"startTimeWindow": "2017-08-17 02:00:00",
	"endTimeWindow": "2017-08-17 03:00:00",
	"tripReferenceId": "c1aa3beae7844b77a90bb6fe0518992c",
	"orderReferenceId": "b7b15a79d6734297a00a93755856e8c8",
	"numberOfItems": 1,
	"packageWeight": 10.0,
	"packageVolume": 4500.0,
	"originAddr": "123,Supreme Business Park,Hiranandani,DMart,Mumbai,400076",
	"destinationAddr": "Destinatioln Address",
	"shipmentOrderTypeCd": "PICKUP",
	"clientNodeName": "Client Node Name",
	"clientNodeCd": "Client Node Code",
	"address": "145 West Coast Road, Singapore, Singapore, Singapore, SINGAPORE, 127367",
	"deliveryType": "DLBOY",
	"shipmentNotes": "PickedUp",
	"assignmentMethod": "MANUAL",
	"calculatedStartDt": "2017-08-18 12:53:00",
	"calculatedEndDt": "2017-08-17 02:52:00",
  "orderStatus": "INTRANSIT"
}
```


This notification is sent when an order is updated.

Param | DataType | Description
--------- | ------- | ----------
orderNo | String | Order No.
notificationType | String| eg. ORDERUPDATENOTIFICATION
vehicleNumber | String | Vehicle Number
awbNumber | String | AWB Number
deliveryMediumName | String | Delivery Associate's name
phoneNumber | Integer | Delivery Associate's phone number
orderState | String | eg. FORWARD or REVERSE
clientId | Integer | Client Id
shipmentCrateMapping | Array | Array of String of mapped crate
startTimeWindow | String | Order's start time window
endTimeWindow | String  | Order's end time window
tripReferenceId | String | Trip Reference Id
orderReferenceId | String | Order Reference Id
numberOfItems | Integer | No. of Orders / Items
packageWeight | Double | Package weight
packageVolume | Double | Package volume
originAddr | String  | Origin address
destinationAddr | String  | Destination address
shipmentOrderTypeCd | String  | Order type e.g. PICKUP or DELIVER
clientNodeName | String  | Node name Mapped for the client order
clientNodeCd | String  |  Code Mapped for the client order node
address | String  | Client Address
deliveryType | String  | Delivery type
shipmentNotes | String  | eg . PickedUp
assignmentMethod | String  | Order assigned to the Trip. eg MANUAL
calculatedStartDt | String  | Calculated start date
calculatedEndDt | String  | Calculated end date
orderStatus | String | The current state of the Order.


## Accept Order

> Response

```json
{
  "clientShipmentId": "Order_001",
  "status": "ORDER ACCEPTED",
  "awbNumber": "AWB123456789",
  "vehicleNumber":"A123D2",
  "deliveryMediumName": "Thomas Watson",
  "deliveryMediumUserName": "Thomas",
  "phoneNumber": 9881234567,
  "tripName": "Trip_1227",
  "updatedOn": "2016-06-30 19:43:07",
  "trackUrl": "https://goo.gl/qhZP63",
  "pickupEndDate": "2017-11-20 10:23:20",
  "deliveryEndDate": "2017-11-20 10:23:20",
  "orderReferenceId": "b7b15a79d6734297a00a93755856e8c8"
}

```

This notification is sent when an order is accepted by a delivery Associate.



#### Response Parameters


Param | DataType | Description
--------- | ------- | ----------
clientShipmentId | String | Order No.
status | String | Status of the order
awbNumber | String | AWB No.
deliveryMediumName | String | Name of Delivery Associate
deliveryMediumUserName | String | Username of Delivery Associate
latitude | Double | The geo-coordinate(latitude) of the Delivery Associate when the Order was accepted
longitude | Double | The geo-coordinate(longitude) of the Delivery Associate when the Order was accepted
phoneNumber | Long | Delivery Associate's phone no.
tripName | String | Trip name
updatedOn | String | Accept order timestamp
trackUrl | String | Url to track Order
deliveryEndDate | String | Delivery end date.
pickupEndDate | String | Planned ETA for the Delivery Associate to complete the Pick-up activity.
orderReferenceId | String | Order Reference Id


## Reject Order

> Response

```json
{
  "clientShipmentId": "Order_001",
  "status": "ORDER REJECTED",
  "tripName": "Trip_100123",
  "updatedOn": "2016-06-30 20:47:20",
  "reasonOfRejection": "Cannot reach on ETA",
  "orderReferenceId": "b7b15a79d6734297a00a93755856e8c8"
}
```

This notification is sent when an order is rejected by a delivery Associate.

#### Response Parameters

Param | DataType | Description
--------- | ------- | ----------
clientShipmentId | String | Order No.
status | String | Status of the order
tripName | String | Trip name
updatedOn | String | Reject order timestamp
reasonOfRejection | String | Reason provided by Delivery Associate while rejecting the order
orderReferenceId | String | Order Reference Id



## Cancel Order

> Response

```json
{
  "orderNo": "Order_001",
  "notificationType": "CANCELLEDNOTIFICATION",
  "orderLeg": "DELIVER",
  "awbNumber": "AWB123456789",
  "deliveryMediumName": "Abhi.P",
  "phoneNumber": "9922904337",
  "orderState": "FORWARD",
  "customerName": "Name",
  "reason": "Customer Unavailable",
  "reasonCd": "Customer Unavailable Cd",
  "tripName": "TRIP-809",
  "customerCode": "Cust122435",
  "cancellationTime": "2016-12-05 12:59:16",
  "cancelledBy": "M. Smith",
  "isCancelOccurAfterPickupFl": false
}
```

This notification is sent when an order is cancelled.

#### Response Parameters

Param | DataType | Description
--------- | ------- | ----------
orderNo | String | Order No.
notificationType | String | CANCELLEDNOTIFICATION
orderLeg | String | Order leg Ex: PICKUP, DELIVER
awbNumber | String | AWB Number for the order
deliveryMediumName | String | Name of Delivery Associate
phoneNumber | Long | Delivery Associate's phone no.
orderState | String | State of order. Ex: FORWARD, REVERSE
customerName | String | Name of customer
reason | String | Reason for the order being cancelled
reasonCd | String | Reason code
cancellationTime | String | Cancellation timestamp
cancelledBy | String | Cancelled by user name
isCancelOccurAfterPickupFl | Boolean | whether order was cancelled after Pickup


## Check In

> Response

```json

{
  "orderNo": "GW458R6",
  "notificationType": "CHECKINPUSHNOTIFICATION",
  "awbNumber": "435-16685675",
  "tripName": "TRIP-15264",
  "orderReferenceId": "6b106144208243ffb4b8c44fd44f123d",
  "deliveryMediumReferenceId": "ec3dc344ad304bbbba710eb84fd7462b",
  "locationType": "PICKUP",
  "checkInTime": "2018-02-08T15:00:00Z",
  "checkinLatitude": 40.760838,
  "checkinLongitude": -73.96732299999996,
  "parentOrderNo":"GW433F3"
}
```

This notification is sent when a delivery resource checks in on their application during order pickup or delivery.

#### Response Parameters

Param | DataType | Description
--------- | ------- | ----------
orderNo | String | This is the order number.
notificationType | String | This is the type of notification. It will always be 'CHECKINPUSHNOTIFICATION' for the check in event.
awbNumber | String | This is the AWB number associated with the order.
tripName | String | This is the name of the trip as created in the system.
orderReferenceId | String | This is the system generated reference ID of the order.
deliveryMediumReferenceId | Long | This is the system generated reference ID of the delivery associate.
locationType | String | This will be PICKUP for order pickup, and DELIVER for order delivery.
checkInTime | String | This is the timestamp of the check in event.
checkinLatitude | String | This is the geolocation coordinate(latitude) of the check in event.
checkinLongitude | String | This is the geolocation coordinate(longitude) of the check in event.
parentOrderNo | String | This is the order number of the parent order.



## Load Items

```json
{
  "orderNo": "Order_0001",  
  "orderState":"FORWARD",
  "orderLeg":"PICKUP",
  "awbNumber":"AWB123456789",
  "notificationType": "LOADITEMNOTIFICATION",
  "orderReferenceId": "b7b15a79d6734297a00a93755856e8c8",
   "shipmentCrateMapping": [
      {
        "crateCd": "CRATE001",
        "crateType": "CRATE001",
        "statusCd": "CRATE001",
        "crateAmount": 100.30,
        "crateQuantity":3,
        "loadedUnits": 1,
        "unloadedUnits": 0,
        "shipmentlineitems": [
          {
            "itemCd": "CODE001",
            "statusCd":"StatusCd",
            "itemName": "ITEM1",
            "itemPrice": 100,
            "itemQuantity": 1,
            "isActiveFl": true
          }
        ]
      }
    ],
    "isActiveFl": true
}
```


This notification is sent when crates are loaded onto an order.

Param | DataType | Description
--------- | ------- | ----------
orderNo | String | Order No.
orderState | String | State of order. Ex: FORWARD, REVERSE
orderLeg | String | Order leg Ex: PICKUP, DELIVER
awbNumber | String | AWB Number for the order
notificationType | String | LOADITEMNOTIFICATION
orderReferenceId | String | Order Reference Id
shipmentCrateMapping.crateCd | String | Crate code
shipmentCrateMapping.crateType | String | Crate type
shipmentCrateMapping.statusCd | String | Crate Status. It will be LOADED.
shipmentCrateMapping.crateAmount | Double | Crate amount
shipmentCrateMapping.crateQuantity | Integer | No of loaded units
shipmentCrateMapping.shipmentlineitems.itemCd | String | Item code
shipmentCrateMapping.shipmentlineitems.statusCd | String | Item status. It will be LOADED.
shipmentCrateMapping.shipmentlineitems.itemName | String | Name of item
shipmentCrateMapping.shipmentlineitems.itemPrice | Double | Item price
shipmentCrateMapping.shipmentlineitems.itemQuantity | Integer | Item quantity

## Load Complete

```json
{
  "clientShipmentIds": ["TestOrder1","TestOrder2"],
  "deliveryMediumName":"TestDeliveryMedium",
  "tripName":"TestTrip",
  "startTime":"2016-07-01 09:13:00",
  "phoneNumber":1234567890,
  "driverName":"TestDriverName",
  "vehicleNumber":"MH 03992",
  "revisedEta" : "2016-07-01 10:13:00",
  "notificationType": "LOADINGDONENOTIFICATION"
}
```


This notification is sent when crates are loaded onto an order.

#### Response Parameters

Param | DataType | Description
--------- | ------- | ----------
clientShipmentIds | String | Order Nos.
deliveryMediumName | String | Name of Delivery Associate
tripName | String | Trip name
startTime | Date | Time when loading is completed.
phoneNumber | Long | Delivery Associate's phone no.
driverName | String | Driver's name
vehicleNumber | String | Vehicle no.
revisedEta | Date | Revised ETA
notificationType | String | LOADINGDONENOTIFICATION

## Delivered

> Response

```json
{
  "orderNo": "Order_1001",
  "latitude": 19.1118589,
  "longitude": 72.9095639,
  "notificationType": "DELIVEREDNOTIFICATION",
  "orderLeg": "DELIVER",
  "awbNumber": "AWB012345678",
  "customerComment": "User comments",
  "customerRating": 5,
  "deliveryMediumName": "Suresh",
  "phoneNumber": 1234567864,
  "orderState": "FORWARD",
  "customerName": "John Watson",
  "clientId": 209,
  "deliveryTime": "2016-11-19 06:11:27",
  "cashAmount": 0,
  "deliveryLocationType": "",
  "transactionId": "12456",
  "actualCashAmount": 120,
  "paymentMode": "COD",
  "tripName": "TRIP-195",
  "recipientName": "Rahul",
  "branchName": "AAA0",
  "paymentSubType": "",
  "orderReferenceId": "733a42098c1946c98aad410a1dcef75e",
}

```

This notification is sent when an order is delivered by a delivery Associate to customer.



#### Response Parameters

Key | DataType | Description
--------- | ------- |-------
orderNo | String | Order No.
latitude | Double | Latitude where order was delivered
longitude | Double | Longitude where order was delivered
notificationType | String | DELIVEREDNOTIFICATION
orderLeg | String | Order leg, Possible values : DELIVER, PICKUP
awbNumber | String | Awb No.
customerComment | String | Customer comments
customerRating | Double | Rating provided by customer
deliveryMediumName | String | Name of Delivery Associate
phoneNumber | Long | Delivery Associate's phone no.
orderState | String | Order state, Possible values : FORWARD, REVERSE
customerName | String | Customer name
clientId | String | Client ID
deliveryTime | String | Delivery timestamp
cashAmount | Double | Cash amount to collect
deliveryLocationType | String | Delivery Location
transactionId | String | Transaction id
paymentMode | String | Paymode mode, Possible values : PREPAID, COD
tripName| String | Trip the Order is attached to
actualCashAmount | Double | Cash amount actually collected
recipientName | String | Name of recipient
branchName | String | Branch Name
paymentSubType | String | Possible values : CASH, CARD_AUTO, CARD_MANUAL,MOMOE,MSWIPE
orderReferenceId | String | Order Reference Id


## Partially Delivered

> Response

```json
{
  "orderNo": "145129097",
  "statusCd": "PARTIALLYDELIVERED",
  "notificationType": "PARTIALDELIVERYNOTIFICATION",
  "orderLeg": "DELIVER",
  "awbNumber": "AWB001",
  "customerComment": "Test user comments",
  "customerRating": 0,
  "deliveryMediumName": "Suresh",
  "phoneNumber": 8447608650,
  "orderState": "FORWARD",
  "customerName": "23768",
  "reason": "Product damaged in transit",
  "reasonCd": "PDL001",
  "deliveryTime": "2016-11-19 06:14:34",
  "cashAmount": 0,
  "deliveryLocationType": "",
  "branchName": "Manhattan Main Branch",
  "transactionId": "",
  "paymentMode": "COD",
  "actualCashAmount": 532.55,
  "shipmentCrateMappingList": [
    {
        "crateCd": "CRATE001",
        "crateType": "CRATE001",
        "statusCd": "CRATE001",
        "crateAmount": 100.30,
        "noOfUnits":3,
        "loadedUnits": 0,
        "unloadedUnits": 0,
        "shipmentLineItemsList": [
          {
            "itemCd": "CODE001",
            "itemType":"Type1",
            "statusCd":"StatusCd",
            "itemName": "ITEM1",
            "itemPrice": 100,
            "itemQuantity": 1,
            "itemWeight": 100,
            "actualItemQuantity": 5,
            "isActiveFl": true
          }
        ],
        "isActiveFl": true
      }
  ],
  "recipientName": "Pratik",
  "apartment": "supreme business park",
  "streetName": "Powai",
  "city": "Mumbai",
  "state": "Maharashtra",
  "country": "INDIA",
  "pincode": "400078",
  "customerEmailAddress": "",
  "customerPhoneNumber": "",
  "paymentSubType": "CASH"
}

```

This notification is sent when an order is partially delivered by a delivery Associate to customer.



#### Response Parameters

Key | DataType | Description
--------- | ------- |-------
orderNo | String | Order No.
statusCd | String | PARTIALLYDELIVERED
notificationType | String | PARTIALDELIVERYNOTIFICATION
orderLeg | String | Order leg Ex: PICKUP, DELIVER
awbNumber | String | AWB Number for the order
customerComments | String | Customer comments
customerRating | Double | Rating provided by customer
deliveryMediumName | String | Name of Delivery Associate
phoneNumber | Long | Delivery Associate's phone no.
orderState | String | State of order. Ex: FORWARD, REVERSE
customerName | String | Customer name
reason | String | Reason for the order being partially delivered
reasonCd | String | Reason code
deliveryTime | String | Delivery timestamp
cashAmount | Double | Cash amount to be collected
deliveryLocationType | String | Delivery Location
branchName| String | Name of the Order Branch
transactionId | String | Transaction id
paymentMode | String | Mode of order payment
actualCashAmount | Double | Cash amount actually collected
shipmentCrateMappingList | Array of Objects | Shipment crates
shipmentCrateMappingList.crateCd | String | Crate code
shipmentCrateMappingList.crateType | String | Crate type
shipmentCrateMappingList.statusCd | String | Crate Status. It will be LOADED.
shipmentCrateMappingList.crateAmount | Double | Crate amount
shipmentCrateMappingList.noOfUnits | Integer | No of units
shipmentCrateMappingList.loadedUnits | Integer | No of units loaded
shipmentCrateMappingList.unloadedUnits | Integer | No of units unloaded
shipmentCrateMappingList.isActiveFl | Boolean | Crate is active
shipmentCrateMappingList.shipmentlineitems.itemCd | String | Item code
shipmentCrateMappingList.shipmentlineitems.itemType | String | Item type
shipmentCrateMappingList.shipmentlineitems.statusCd | String | Item status. It will be LOADED.
shipmentCrateMappingList.shipmentlineitems.itemName | String | Name of item
shipmentCrateMappingList.shipmentlineitems.itemPrice | Double | Item price
shipmentCrateMappingList.shipmentlineitems.itemQuantity | Integer | Item quantity
shipmentCrateMappingList.shipmentlineitems.itemWeight | Integer | Item weight
shipmentCrateMappingList.shipmentlineitems.actualItemQuantity | Integer | Unloaded Item quantity
shipmentCrateMappingList.shipmentlineitems.isActiveFl | Boolean | Line item is active
recipientName | String | Recipients Name
apartment | String | Recipients apartment
streetName | String | Recipients street name
city | String | Recipients city
state | String | Recipients state
country | String | Recipients country
pincode | Integer | Recipients pincode
customerEmailAddress | String | Customer email address
customerPhoneNumber | String | Customer phone number
paymentSubType | String | e.g. CASH, CARD_AUTO, CARD_MANUAL,MOMOE,MSWIPE

## Not Delivered

> Response

```json
{
  "orderNo": "Order001",
  "latitude": 19.1118589,
  "longitude": 72.9095639,
  "notificationType": "NOTDELIVEREDNOTIFICATION",
  "orderLeg": "DELIVER",
  "clientId": 209
  "awbNumber": "AWB001",
  "customerComment": "Test user comments",
  "customerRating": 0,
  "deliveryMediumName": "Suresh",
  "phoneNumber": 1234567876,
  "orderState": "FORWARD",
  "customerName": "Rahul",
  "reasonCd": "NDL001",
  "reason": "No customer at delivery location",
  "deliveryTime": "2016-11-19 06:10:32",
  "deliveryLocationType": "",
  "recipientName": "",
  "branchName": "MUMBAI (VISIONCARE-DW)",
  "orderReferenceId": "b7b15a79d6734297a00a93755856e8c8"
}

```

This notification is sent when an order is not delivered by a delivery Associate.



#### Response Parameters

Key | DataType | Description
--------- | ------- | -------
orderNo | String | Order No.
latitude | Double | Latitude where order was marked not delivered
longitude | Double | Longitude where order was marked not delivered
notificationType | String | NOTDELIVEREDNOTIFICATION
orderLeg | String | Order leg Ex: PICKUP, DELIVER
awbNumber | String | AWB Number for the order
clientId | String | Client ID
customerComments | String | Customer comments
customerRating | Double | Rating provided by customer
deliveryMediumName | String | Name of Delivery Associate
phoneNumber | Long | Delivery Associate's phone no.
orderState | String | State of order. Ex: FORWARD, REVERSE
customerName | String | Customer name
reason | String | Reason for the order not delivered
reasonCd | String | Reason code
deliveryTime | String | Undelivered timestamp
deliveryLocationType | String | Delivery location
recipientName | String | Name of recipient
branchName | String | Hub branch name
orderReferenceId | String | Order Reference Id

## Pickedup

> Response

```json
{
  "orderNo": "Order001",
  "latitude": 19.1119015,
  "longitude": 72.9095815,
  "pickedUpTime": "2016-11-19 06:33:48",
  "status": "PICKEDUP",
  "notificationType": "PICKEDUPNOTIFICATION",
  "orderLeg": "PICKUP",
  "awbNumber": "AWB001",
  "customerComment": "Test user comments",
  "customerRating": 0,
  "deliveryMediumName": "TestDB",
  "phoneNumber": 1234565435,
  "orderState": "FORWARD",
  "branchName": "1008",
  "orderReferenceId": "b7b15a79d6734297a00a93755856e8c8"
}


```

This notification is sent when an order is picked up by a delivery Associate.



#### Response Parameters

Key | DataType | Description
--------- | ------- |-------
orderNo | String | Order No.
latitude | Double | Latitude where order was pickedup
longitude | Double | Longitude where order was pickedup
pickedUpTime | String | Pickup order timestamp
status | String | PICKEDUP
notificationType | String | PICKEDUPNOTIFICATION
orderLeg | String | Order leg Ex: PICKUP, DELIVER
awbNumber | String | AWB Number for the order
customerComments | String | Customer comments
customerRating | Double | Rating provided by customer
deliveryMediumName | String | Name of Delivery Associate
phoneNumber | Long | Delivery Associate's phone no.
orderState | String | State of order. Ex: FORWARD, REVERSE
branchName | String | -
orderReferenceId | String | Order Reference Id


## Not Pickedup

> Response

```json
{
  "orderNo": "Order001",
  "notificationType": "NOTPICKEDUPNOTIFICATION",
  "orderLeg": "DELIVER",
  "awbNumber": "AWB001",
  "customerComment": "Test user comments",
  "customerRating": 0,
  "deliveryMediumName": "TestDM",
  "phoneNumber": 1234567890,
  "orderState": "FORWARD",
  "customerName": "Customer name",
  "reason": "Product damaged in transit",
  "reasonCd": "",
  "orderReferenceId": "b7b15a79d6734297a00a93755856e8c8"
}

```

This notification is sent when an order is picked up by a delivery Associate.



#### Response Parameters

Key | DataType | Description
--------- | ------- |-------
orderNo | String |  Order No.
notificationType | String |  NOTPICKEDUPNOTIFICATION
orderLeg | String |  Order leg
awbNumber | String | Airway Bill Number
customerComment | String |  Customer comments
customerRating | Double | Rating provided by customer
deliveryMediumName | String |  Name of Delivery Associate
phoneNumber | Long | Phone no of Delivery Associate
orderState | String | State of the order
customerName | String | Name of customer
reason | String | Reason for order not pickedup
reasonCd | String | Reason code
orderReferenceId | String | Order Reference Id

## Route Planning


> Response

```json
{
  "notificationType": "DELIVERYPLANNING",
  "notificationDetails": [
    {
      "tripName": "TRIP-46",
      "deliveryMediumName": "Ramesh",
      "referenceId": "d1c196e8bf384c40ae7f7ca0fd1a3d58",
      "phoneNumber": "9876543213",
      "driverName": "Matt",
      "vehicleNumber": "MH-13213",
      "orderDetails": [
        {
          "orderNo": "GRU453D",
          "startTimeWindow": "2018-04-14 11:18:00",
          "endTimeWindow": "2018-04-14 17:45:00",
          "calculatedStartDate": "2018-04-14 11:18:00",
          "calculatedEndDate": "2018-04-14 17:45:00",
          "deliveryOrder":1,
          "latitude": 19.1239285,
          "longitude": 72.90944069999999
        }
      ]
    }
  ]
}

```





#### Response Parameters

Key | DataType | Description
--------- | ------- |-------
notificationType | String |  DELIVERYPLANNING
notificationDetails | List | Notification details
tripName | String |  Trip name
deliveryMediumName | String |  Name of Delivery Associate
referenceId | String | Reference id of the trip
phoneNumber | String | Phone no of Delivery Associate
driverName | String |  Name of driver
vehicleNumber | String |  Vehicle no.
orderDetails | List | List of orders present in the trip
orderNo | String |  Order no.
startTimeWindow | String |  Estimated start time of order
endTimeWindow | String |  Estimated end time of order
deliveryOrder | Integer |  Delivery order
latitude | Double | Order Latitude
longitude | Double | Order Longitude

## Route Planning - API

> Response

```json
{
    "status": 200,
    "message": null,
    "data": {
        "routeName": "TEST_ROUTE",
        "routes": [
            {
                "vehicle": "cc",
                "shipments": [
                    {
                        "name": "Shipment 1",
                        "start": "2017-10-27T16:00:00Z",
                        "end": "2017-10-27T18:00:00Z",
                        "shipmentType": "DELIVER"
                    },

                    {
                        "name": "Shipment 2",
                        "start": "2017-10-27T16:00:00Z",
                        "end": "2017-10-27T18:00:00Z",
                        "shipmentType": "PICKUP"
                    }
                ],
                "start": "2017-10-27T15:59:13Z",
                "end": "2017-10-27T16:19:13Z"
            }
        ],
        "unassigned": ["Shipment 3", "Shipment 4", "Shipment 5"]
    },
    "hasError": false
}

```

This notification is sent when the Route Planning API is called.



#### Response Parameters

Key | DataType | Description
--------- | ------- |-------
status | String |  Standard HTTP Status Code
message | String | Response message. Will be displayed in case of Error
data | JSON |  Response JSON body
routeName | String | Name of the Milkrun or Route
routes | List |  List of optimised routes/ trips through which the shipments will be delivered/ picked-up
routes.start | String | Start Date and Time of Route / Trip. This date and time will be in UTC
routes.end | String | End Date and Time of Route / Trip. This date and time will be in UTC
route.vehicle | String |  Vehicle No. which will service the shipments for the mentioned route / trip
route.shipments | List |  List of shipments and their details
route.shipments.name | String |  Shipment name
route.shipments.start | String |  Start Date and Time slot of the shipment
route.shipments.end | String | End Date and Time slot of the shipment
route.shipments.shipmentType | String | Type of Shipment i.e. DELIVER, PICKUP
unassigned | List | List of shipment IDs that are not assigned to any trip because of constraints
hasError | Boolean | If true - There is error in processing your request. If false - The request is successfully processed

## Allocation End

> Response

```json

{
 "orderNo": "ORD00000002",
 "notificationType": "ORDERALLOCATIONSTOP",
 "orderReferenceId": "d39d14f7f08542b2b03e7e45e5aa4416",
 "lastRunDt": "2018-06-05T07:19:13Z",
 "isMaxAttemptsExhausted": false
}
```
This notification is triggered when the Auto Allocation process for an Order ends and a driver is not assigned to the order.

#### Response Parameters

Key | DataType | Description
--------- | ------- |-------
orderNo | String>|  Order No.s.
notificationType | String |  ORDERALLOCATIONSTOP
orderReferenceId | String |  Reference ID of the order.
lastRunDt | String |  Last run time of the allocation engine
isMaxAttemptsExhausted | String |  check if the max number of attempts was exhausted.


## Create Route

> Response

```json
{
  "notificationType": "CREATEROUTE",
  "totalDistance": 651,
  "routeConfigurationName": "DDI - DPI",
  "routeReferenceId": "07ead36fdf6644d6b877ca3c14d16b8a",
  "originName": "DDI71017",
  "destinationName": "DPI66009",
  "totalTime": 1122,
  "originServiceTime": 62,
  "intransitLocations": [
    {
      "sequence": 1,
      "locationName": "DPI66080",
      "transitTime": 100,
      "transitDistance": 97,
      "serviceTime": 10
    },
    {
      "sequence": 2,
      "locationName": "DPI66059",
      "transitTime": 200,
      "transitDistance": 34,
      "serviceTime": 20
    },
    {
      "sequence": 3,
      "locationName": "DPI66134",
      "transitTime": 300,
      "transitDistance": 288,
      "serviceTime": 30
    }
  ],
  "destinationTranistTime": 400,
  "destinationDistance": 232
}

```

This notification is sent when a route is created in LogiNext.

#### Response Parameters

Key | DataType | Description
--------- | ------- |-------
notificationType | String |  CREATEROUTE
totalDistance | String |  Total Distance of the Route
routeConfigurationName | String |  Name of the Route
routeReferenceId | String |  Reference ID of the Route
originName | String |  Origin Hub of the route
destinationName | String |  Destination Hub of the route
totalTime | Long | total time
originServiceTime | String |  Service time at the origin location
intransitLocations | List<String> |  List of in transit hubs in the route.
sequence | String |  Sequence of in transit hub.
locationName | String |  Name of In transit hub.
transitTime | String |  transit time to reach the hub.
transitDistance | String |  transit distance to reach the hub.
serviceTime | String |  service time at the hub.


## Route Status.

> Response

```json
{
  "notificationType": "ROUTESTATUS",
  "routeReferenceId": "7dd5e37fd8d641469a3195a236f2ab26",
  "originName": "PT. Great Giant Livestock-GGL",
  "destinationName": "PT. Great Giant Livestock-Bonanza Susu",
  "newStatus": "INACTIVE",
  "updateTime": "2018-06-27T17:45:08.520Z"
}

```

This notification is sent when a route status is changed in LogiNext.

#### Response Parameters

Key | DataType | Description
--------- | ------- |-------
notificationType | String |  ROUTESTATUS
routeReferenceId | String |  Reference ID of the route
originName | String |  Origin Name 
destinationName | String |  Destination Name
newStatus | String |  Origin Hub of the route
updateTime | String |  Timestamp of the update event

Status | Description
--------- | ------- 
ACTIVE | The Route is Active in the LogiNext system and can be selected for trips.
INACTIVE | The Route is Inactive in the LogiNext system and cannot be selected for trips.



## Start Trip

> Response

```json
{
  "latitude": 0,
  "longitude": 0,
  "notificationType": "STARTTRIP",
  "deliveryMediumName": "Suraj Singh",
  "phoneNumber": 1234567546,
  "startTime": "2016-11-19 06:42:44",
  "tripName": "TRIP-84",
  "vehicleNumber":"MH084819",
  "driverName":"Rahul",
  "clientShipmentIds": [
    "Order001",
    "Order002"
  ],
  "branchName": "Vikhroli"
}

```

This notification is sent when a trip is started.

#### Response Parameters

Key | DataType | Description
--------- | ------- |-------
clientShipmentIds | List<String> |  Order No.s.
notificationType | String |  STARTTRIP
tripName | String |  Trip name
vehicleNumber | String |  Vehicle no.
driverName | String |  Name of driver
deliveryMediumName | String |  Name of Delivery Associate
phoneNumber | Long | Phone no.
startTime | String |  Trip start time


## Stop Trip

> Response

```json
{
  "notificationType": "DELIVEREDNOTIFICATION",
  "deliveryMediumName": "John",
  "endTime": "2016-11-19 06:45:10",
  "tripName": "TRIP-95",
  "vehicleNumber": "MH014841",
  "driverName": "",
  "clientShipmentIds": [
    "Order001",
    "Order002"
   ]
}
```

This notification is sent when a trip is ended.

#### Response Parameters

Key | DataType | Description
--------- | ------- |-------
clientShipmentIds | List<String> |  Order Nos.
notificationType | String |  DELIVEREDNOTIFICATION
tripName | String |  Trip name
vehicleNumber | String |  Vehicle no.
driverName | String |  Name of driver
deliveryMediumName | String |  Name of Delivery Associate
endTime | String |  Trip end time

## Hub In

> Response

```json
{

  "url" : "endpoint url",
  "data" : "<?xml version=\"1.0\" encoding=\"UTF-8\" standalone=\"yes\"?>\n
          <geofencePushNotificationDTO>\n    
            <hubName>HubName</hubName>\n    
            <latitude>13.018617777777777</latitude>\n    
            <longitude>80.01128</longitude>\n    
            <sightingDate>201603091412</sightingDate>\n    
            <status>HUB IN</status>\n    
            <tripId>TripName</tripId>\n
          </geofencePushNotificationDTO>\n",
  "notificationType" : "HUB IN",
  "updatedDate" : "2016-03-09 07:09:10"
}

```

This notification is sent when a vehicle enters inside a hub.



#### Response Parameters

Key | DataType | Description
--------- | ------- |-------
url | String |  Endpoint URL
data | String |  Data in XML format
notificationType | String |  HUB IN
updatedDate | String | Timestamp


## Hub Out

> Response

```json
{

  "url" : "endpoint url",
  "data" : "<?xml version=\"1.0\" encoding=\"UTF-8\" standalone=\"yes\"?>\n
          <geofencePushNotificationDTO>\n    
            <hubName>HubName</hubName>\n    
            <latitude>13.018617777777777</latitude>\n    
            <longitude>80.01128</longitude>\n    
            <sightingDate>201603091412</sightingDate>\n    
            <status>HUB OUT</status>\n    
            <tripId>TripName</tripId>\n
          </geofencePushNotificationDTO>\n",
  "notificationType" : "HUB OUT",
  "updatedDate" : "2016-03-09 07:09:10"
}

```

This notification is sent when a vehicle enters inside a hub.



#### Response Parameters

Key | DataType | Description
--------- | ------- |-------
url | String |  Endpoint URL
data | String |  Data in XML format
notificationType | String |  HUB IN
updatedDate | String | Timestamp

## Allocation Engine

> Response

```json
{
  "originAddr": "Client Name Main Branch",
  "originLatitude": 19.116858,
  "originLongitude": 72.910157,
  "notificationType":"ORDERALLOCATION",
  "parentOrderNo": "Customer1_Parent_Order",
  "orderNo": "Customer1_Parent_Order_1",
  "orderReferenceId": "d1c196e8bf384c40ae7f7ca0fd1a3d58",
  "allocationTimeStamp": "2017-07-15T10:30:00.000Z",
  "deliveryMediums": [
    {
       "deliveryMediumMasterName": "Mathew S",
       "employeeId": "133467",
       "userName": "mathewsandroid",
       "phoneNumber": "9881127443",
       "latitude": 19.1119195,
       "longitude": 72.9093988,
       "pickupEta": "2016-07-15T10:47:00.000Z",
       "distanceInKms": 0.849,
       "timeInMin": 29,
       "expiryTime": "2016-07-15T10:30:45.000Z",
       "statusCd": "DISPATCHED",
       "tripStatus": "STARTED",
       "referenceId": "3622c618479e456b9da15f9263b28304"
    }
  ]
}
```

With this webhook, you can get the list of one or more nearest Drivers / Delivery Associate / Field Executives that the LogiNext Delivery Associate Allocation Engine has identified to deliver your On Demand (point to point) Orders.

#### Response Parameters

Key | DataType | Required | Description
--------- | ------- |-------|-----------
originAddr | String | Mandatory | This is the Order Reference ID generated by the LN system for the order created.<br>Note that this reference Id is for the "orderNo" and not for the "parentOrderNo"
originLatitude | String | Mandatory | Geo-location of the Pick-up location<br>Sample Value - "17.996"
originLongitude | String | Mandatory | Geo-location of the Pick-up location<br>Sample Value - "82.34"
parentOrderNo | String | Mandatory | In case the Order is Single Pick-up - Multiple destination, Parent order No. will be present<br>In case the Order is Single Pick-up - Single destination, Parent order No. will not be present<br>Sample Value - "1316MDO"
orderNo | String | Mandatory | In case the Order is Single Pick-up - Multiple destination, this is the first Order No. in the sequence<br>This order no. is just used as placeholder. <br>In case the Order is Single Pick-up - Single destination, this is the Order No. created in the system<br>Sample Value - "1316MDO_1"
orderReferenceId | String | Mandatory | This is the Order Reference ID generated by the LN system for the order created.<br>Note that this reference Id is for the "orderNo" and not for the "parentOrderNo"
allocationTimeStamp | String | Mandatory | This is the time at which the allocation engine has identified the nearest Delivery Boy / Driver / Associate / Field Executive.<br>Note that this date and time is in UTC.<br>Sample Value - "2017-07-15T10:30:00.000Z"
deliveryMediums | Array Of Object |  | Array - <br>This list would contain list of one or more nearest Delivery Boy / Driver / Associate / Field Executive identified for your order.<br>Note that if you have set your account configuration to identify only the nearest driver first, then this array would have only one value.<br>If your account configuration is set to identify X no. of drivers, then this array will have list of the X nearest drivers.
deliveryMediums.userGroupName | String | Mandatory | This is the name of the User Group which the Driver / Delivery Associate / Field Executive belongs to in the LogiNext application.<br>Each user that is created in the LN system is associated to a user group. <br>This user groups is used to provide relevant access to the users.<br>Sample Value - "Platinum User Group"
deliveryMediums.employeeId | String | Mandatory | This the Employee ID set for the Driver / Delivery Associate / Field Executive in the LogiNext application.<br>Sample Value - "133478"
deliveryMediums.userName | String | Mandatory | This the Use rName set for the Driver / Delivery Associate / Field Executive in the LogiNext application.<br>Sample Value - "Joshua.Anderson"
deliveryMediums.phoneNumber | String | Mandatory | This the Phone No. set for the Driver / Delivery Associate / Field Executive in the LogiNext application.<br>Sample Value - "9894965656"
deliveryMediums.latitude | Double | Optional | This the current geo-location of the Driver / Delivery Associate / Field Executive.<br>Sample Value - "17.897"
deliveryMediums.longitude | Double | Optional | This the current geo-location of the Driver / Delivery Associate / Field Executive.<br>Sample Value - "85.897"
deliveryMediums.pickupEta | String | Mandatory | This the time at which the Driver / Delivery Associate / Field Executive will reach the Pick-Up Location<br>Sample Value - "2016-07-15T10:47:00.000Z"
deliveryMediums.distanceInKms | Double | Mandatory | This the distance in KM that the Driver / Delivery Associate / Field Executive is away from the Pick-Up Location
deliveryMediums.timeInMin | Integer | Mandatory | This the time in Minutes which the Driver / Delivery Associate / Field Executive will take to reach the Pick-up Location.
deliveryMediums.expiryTime | String | Mandatory | This the time before which the Driver / Delivery Associate / Field Executive will have to "accept" the order  on his / her mobile app. If not accepted, the order will be removed and allocated to next available Delivery Associate.<br>Sample Value - "2016-07-15T10:30:00.000Z"<br><br>Note that the time till which you want the order to remain displayed in the Delivery Associate's app. is configurable through the Settings screen on the LogiNext application.
deliveryMediums.statusCd | String | Mandatory | This is the current Status of the Delivery Associate.<br>This will have either of the two values depending on the configuration you have set.<br>If you want the Delivery Associate to cater to only one order at a time, then this Status code will be AVAILABLE.<br>If you want an order to be allocated to the Delivery Associate to cater to multiple orders at any given time i.e. even when is catering another order, then the Status Code will be DISPATCHED in case he is delivering another order.
deliveryMediums.tripStatus | String | Mandatory | This is the current Status of the Trip of the Delivery Associate.<br>This will have either of the two values depending on the configuration you have set.<br>If you want the Delivery Associate to cater to only one order at a time, then this Status code will be NOT STARTED .<br>If you want an order to be allocated to the Delivery Associate to cater to multiple orders at any given time i.e. even when is catering another order, then the Status Code will be DISPATCHED in case he is delivering another order.
deliveryMediums.referenceId | String | Mandatory | This is the LogiNext reference ID of the Delivery Associate / Driver / Field Executive.

## Active / Inactive

> Response

```json
{
  "referenceId":"6186d5fc6e324c42abb5ea1a32e05f66",
  "deliveryMediumName":"Thomas Walton",
  "employeeId":"133456",
  "phoneNumber":"9881134567",
  "newStatus":"ACTIVE",
  "reasonCd":"DBUNAVAILABLE",
  "updateTime":"2016-07-18T10:31:00.000Z"
}
```

When the Delivery Associate is marked as Active / Inactive, you can consume this webhook

#### Response Parameters

Key | DataType | Description
--------- | ------- | -----------
referenceId | String | This is the LogiNext Reference ID for the Delivery Associate<br>This is generated when the Delivery Associate is added in the LogiNext application.
deliveryMediumName | String |  Name of the Delivery Associate / Delivery Associate / Driver / Field Executive
employeeId | String |  Employee of the Delivery Associate / Delivery Associate / Driver / Field Executive
phoneNumber | String |  Phone No. of the Delivery Associate / Delivery Associate / Driver / Field Executive
newStatus | String |  Status shall be one of the two below - <br>ACTIVE - if Delivery Associate is marked Active<br>INACTIVE - if Delivery Associate is marked Inactive
reasonCd | String |  When you activate / deactivate the Delivery Associate, you mention the reason for activation / deactivation.<br>The reasons shall be mentioned here
updateTime | String |  This is the time in UTC when the Delivery Associate was marked Active / Inactive

## Delivery Associate On Break/ Off Break

```json
{
  "latitude":19.6789,
  "longitude":78.6758,
  "timestamp":"2018-07-05 13:22:32",
  "deliveryMediumName":"Sam",
  "clientId":209,
  "tripName":"TRIP-17774",
  "referenceId":"dde5a971e67c4256af48436fe51f23c2",
  "employeeId":"7777777",
  "userName":"Sam1234",
  "breakStatus":"ONBREAK"

}

```

When the Delivery Associate is marked as Active / Inactive, you can consume this webhook

#### Response Parameters

Key | DataType | Description
--------- | ------- | -----------
latitude | String | Geo coordinate(latitude) of the event.
longitude | String |  Geo coordinate(longitude) of the event.
timestamp | String |  date time of the event in UTC format.
deliveryMediumName | String |  Name of the Delivery Associate
clientId | String | Clinet ID
referenceId | String | LogiNext Reference ID of the Delivery Associate.
employeeId | String | Employee ID of the Delivery Associate.
userName | String | Username of the Delivery Associate.
breakStatus | String |  Status shall be one of the two below - <br>ONBREAK - if Delivery Associate is marked On Break <br>OFFBREAK - if Delivery Associate is marked Off Break.

## Create Delivery Associate 

> Response

```json
{
    "referenceId": "f40cf4493a5949199775499b5750a272",
    "notificationType": "CREATEDELIVERYMEDIUMNOTIFICATION",
    "employeeId":"1001",
    "deliveryMediumName": "Amit",
    "phoneNumber": "63865471261",
    "imei": "123456789012645",
    "emailId": "test@test.com",
    "userName": "test003",
    "capacityInUnits": 10,
    "capacityInVolume": 0,
    "capacityInWeight": 0,
    "dob": "2016-12-12",
    "deliveryMediumLanguageList": ["HINDI","MARATHI","GUJARATI"],
    "gender": "Male",
    "deliveryMediumTypeCd": ["Delivery Boy"],
    "isOwnVehicleFl": "Company",
    "vehicleNumber": "MH034506",
    "dmPreference": ["400001"],
    "cashInHand":"4000",
    "shiftList": [
      {
        "shiftStart": "13:30:00",
        "shiftEnd": "14:30:00"
      }
    ],
    "maxDistance": 100,
    "licenseValidity": "2016-12-12T13:30:00Z",    
    "weeklyOffList": ["Thursday","Monday"],
    "fixedCost":"500",
    "variableCost":"30"
}
```

When the Delivery Associate is created in the system.

#### Response Parameters

Key | DataType | Description
--------- | ------- | -----------
referenceId | String | This is the LogiNext Reference ID for the Delivery Associate<br>This is generated when the Delivery Associate is added in the LogiNext application.
notificationType | String | This will always be - CREATEDELIVERYMEDIUMNOTIFICATION
deliveryMediumName | String |  Name of the Delivery Associate / Delivery Associate / Driver / Field Executive
employeeId | String |  Employee of the Delivery Associate / Delivery Associate / Driver / Field Executive
phoneNumber | String |  Phone No. of the Delivery Associate / Delivery Associate / Driver / Field Executive
imei | String |  The IMEI no. of the Phone that Delivery Associate will use. This is as per the value entered while creating the Delivery Associate
emailId | String |  This is the Email Address of the Delivery Associate
userName | String |  This is the username of the Delivery Associate as entered while creating the Delivery Associate
capacityInUnits | Integer |  This is the capacity i.e. count of the orders that the Delivery Associate can serve in one trip
capacityInVolume | Integer |  This is the capacity in volume (as per the set Unit of Measure) that the Delivery Associate can carry in one trip
capacityInWeight | Integer |  This is the capacity in WEIGHT (as per the set Unit of Measure) that the Delivery Associate can carry in one trip
dob | String |  The Date of the Birth for the Delivery Associate in "YYYY-MM-DD" format
deliveryMediumLanguageList | List |  This is the list of languages that the Delivery Associate is known to.
gender | String |  This is the gender of the Delivery Associate
deliveryMediumTypeCd | String |  In certain operations, there are different skill sets / special delivery requirements through which the Delivery has to take place.<br>For e.g. - Groceries / Food items has to be separated with Toiletries<br>Orders for Cake cannot be clubbed with the Order for Flowers while delivering.<br>In such cases, if you want to classify the orders by using Delivery Type such that these orders get assigned to Delivery Associates who are configured in LogiNext system with these special skill-sets or types, then you can use this field.<br>Please note that before you pass orders with certain Delivery Types, you will have to first configure the Delivery Types.<br>Please ask your Account Manager to set these values for you.
isOwnVehicleFl | String |  This field indicates if the Vehicle is owned by the Delivery Associate or is it the Organization's Vehicle
vehicleNumber | String |  The mapped Vehicle Number with the Delivery Associate
dmPreference | String |  This is the preferred Pin Codes i.e. that areas / zones in which the Delivery Associates will deliver the orders.<br>Orders out these preferred pin-codes / zones will not be assigned Delivery Associate
cashInHand | Double |  cash with delivery boy.
shiftList | List |  shift details.
shiftList.shiftStart | String |  shift start time
shiftList.shiftEnd | String |  shift end time
maxDistance | Integer |  This is the Maximum Distance in Kms
licenseValidity | String | This is the expiry Date of the Driver's License in UTC format.
reasonCd | String |  When you activate / deactivate the Delivery Associate, you mention the reason for activation / deactivation.<br>The reasons shall be mentioned here
updateTime | String |  This is the time in UTC when the Delivery Associate was marked Active / Inactive
weeklyOffList | List |  List of weekly off's
fixedCost | Integer |  fixed cost associated with delivery boy.
variableCost | Integer |  variable cost.


# Country Codes

When creating entities in LogiNext  that require country specific location information associated with them, use the country codes listed below. 
For example, if you want to create an Order that is to be picked up from a Pick-up location in the United States, you would pass USA as the 'pickupCOuntry' in the Create Order API.

If you wish to enter a country code not listed below, please reach out to your Account Manager, write to us at: <a href="mailto:support@loginextsolutions.com?Subject=Postal-Code%20Queries" target="_top">support@loginextsolutions.com</a> 

Country |  Code
--------- | ---------  
ALBANIA|AFG
ALGERIA|ALB
AMERICAN SAMOA|ASM
ANDORRA|AND
ANGOLA|AGO
ANGUILLA|AIA
ANTARCTICA|ATA
ANTIGUA AND BARBUDA|ATG
ARGENTINA|ARG
ARMENIA|ARM
ARUBA|ABW
AUSTRALIA|AUS
AUSTRIA|AUT
AZERBAIJAN|AZE
BAHAMAS|BHS
BAHRAIN|BHR
BANGLADESH|BGD
BARBADOS|BRB
BELARUS|BLR
BELGIUM|BEL
BELIZE|BLZ
BENIN|BEN
BERMUDA|BMU
BHUTAN|BTN
BOLIVIA|BOL
BOSNIA AND HERZEGOWINA|BIH
BOTSWANA|BWA
BOUVET ISLAND|BVT
BRAZIL|BRA
BRITISH INDIAN OCEAN TERRITORY|IOT
BRUNEI DARUSSALAM|BRN
BULGARIA|BGR
BURKINA FASO|BFA
BURUNDI|BDI
CAMBODIA|KHM
CAMEROON|CMR
CANADA|CAN
CAPE VERDE|CPV
CAYMAN ISLANDS|CYM
CENTRAL AFRICAN REPUBLIC|CAF
CHAD|TCD
CHILE|CHL
CHINA|CHN
CHRISTMAS ISLAND|CXR
COCOS (KEELING) ISLANDS|CCK
COLOMBIA|COL
COMOROS|COM
CONGO|COG
CONGO, THE DRC|COD
COOK ISLANDS|COK
COSTA RICA|CRI
COTE D.IVOIRE|CIV
CROATIA|HRV
CUBA|CUB
CYPRUS|CYP
CZECH REPUBLIC|CZE
DENMARK|DNK
DJIBOUTI|DJI
DOMINICA|DMA
DOMINICAN REPUBLIC|DOM
EAST TIMOR|TMP
ECUADOR|ECU
EGYPT|EGY
EL SALVADOR|SLV
EQUATORIAL GUINEA|GNQ
ERITREA|ERI
ESTONIA|EST
ETHIOPIA|ETHÃƒÆ’Ã†â€™Ãƒâ€ Ã¢
FALKLAND ISLANDS (MALVINAS)|FLK
FAROE ISLANDS|FRO
FIJI|FJI
FINLAND|FIN
FRANCE|FRA
FRANCE, METROPOLITAN|FXX
FRENCH GUIANA|GUF
FRENCH POLYNESIA|PYF
FRENCH SOUTHERN TERRITORIES|ATF
GABON|GAB
GAMBIA|GMB
GEORGIA|GEO
GERMANY|DEU
GHANA|GHA
GIBRALTAR|GIB
GREECE|GRC
GREENLAND|GRL
GRENADA|GRD
GUADELOUPE|GLP
GUAM|GUM
GUATEMALA|GTM
GUINEA|GIN
GUINEA-BISSAU|GNB
GUYANA|GUY
HAITI|HTI
HEARD AND MC DONALD ISLANDS|HMD
HOLY SEE (VATICAN CITY STATE)|VAT
HONDURAS|HND
HONG KONG|HKG
HUNGARY|HUN
ICELAND|ISL
INDIA|IND
INDONESIA|IDN
IRAN (ISLAMIC REPUBLIC OF)|IRN
IRAQ|IRQ
IRELAND|IRL
ISRAEL|ISR
ITALY|ITA
JAMAICA|JAM
JAPAN|JPN
JORDAN|JOR
KAZAKHSTAN|KAZ
KENYA|KEN
KIRIBATI|KIR
KOREA, D.P.R.O.|PRK
KOREA, REPUBLIC OF|KOR
KUWAIT|KWT
KYRGYZSTAN|KGZ
LAOS|LAO
LATVIA|LVA
LEBANON|LBN
LESOTHO|LSO
LIBERIA|LBR
LIBYAN ARAB JAMAHIRIYA|LBY
LIECHTENSTEIN|LIE
LITHUANIA|LTU
LUXEMBOURG|LUX
MACAU|MAC
MACEDONIA|MKD
MADAGASCAR|MDG
MALAWI|MWI
MALAYSIA|MYS
MALDIVES|MDV
MALI|MLI
MALTA|MLT
MARSHALL ISLANDS|MHL
MARTINIQUE|MTQ
MAURITANIA|MRT
MAURITIUS|MUS
MAYOTTE|MYT
MEXICO|MEX
MICRONESIA, FEDERATED STATES OF|FSM
MOLDOVA, REPUBLIC OF|MDA
MONACO|MCO
MONGOLIA|MNG
MONTENEGRO|MNE
MONTSERRAT|MSR
MOROCCO|MAR
MOZAMBIQUE|MOZ
MYANMAR (Burma)|MMR
NAMIBIA|NAM
NAURU|NRU
NEPAL|NPL
NETHERLANDS|NLD
NETHERLANDS ANTILLES|ANT
NEW CALEDONIA|NCL
NEW ZEALAND|NZL
NICARAGUA|NIC
NIGER|NER
NIGERIA|NGA
NIUE|NIU
NORFOLK ISLAND|NFK
NORTHERN MARIANA ISLANDS|MNP
NORWAY|NOR
OMAN|OMN
PAKISTAN|PAK
PALAU|PLW
PANAMA|PAN
PAPUA NEW GUINEA|PNG
PARAGUAY|PRY
PERU|PER
PHILIPPINES|PHL
PITCAIRN|PCN
POLAND|POL
PORTUGAL|PRT
PUERTO RICO|PRI
QATAR|QAT
REUNION|REU
ROMANIA|ROM
RUSSIAN FEDERATION|RUS
RWANDA|RWA
SAINT KITTS AND NEVIS|KNA
SAINT LUCIA|LCA
SAINT VINCENT AND THE GRENADINES|VCT
SAMOA|WSM
SAN MARINO|SMR
SAO TOME AND PRINCIPE|STP
SAUDI ARABIA|SAU
SENEGAL|SEN
SERBIA|SRB
SEYCHELLES|SYC
SIERRA LEONE|SLE
SINGAPORE|SGP
SLOVAKIA (Slovak Republic)|SVK
SLOVENIA|SVN
SOLOMON ISLANDS|SLB
SOMALIA|SOM
SOUTH AFRICA|ZAF
SOUTH SUDAN|SSD
SOUTH GEORGIA AND SOUTH S.S.|SGS
SPAIN|ESP
SRI LANKA|LKA
ST. HELENA|SHN
ST. PIERRE AND MIQUELON|SPM
SUDAN|SDN
SURINAME|SUR
SVALBARD AND JAN MAYEN ISLANDS|SJM
SWAZILAND|SWZ
SWEDEN|SWE
SWITZERLAND|CHE
SYRIAN ARAB REPUBLIC|SYR
TAIWAN, PROVINCE OF CHINA|TWN
TAJIKISTAN|TJK
TANZANIA|TZA
THAILAND|THA
TOGO|TGO
TOKELAU|TKL
TONGA|TON
TRINIDAD AND TOBAGO|TTO
TUNISIA|TUN
TURKEY|TUR
TURKMENISTAN|TKM
TURKS AND CAICOS ISLANDS|TCA
TUVALU|TUV
UGANDA|UGA
UKRAINE|UKR
UNITED ARAB EMIRATES|UAE
UNITED KINGDOM|GBR
UNITED STATES|USA
U.S. MINOR ISLANDS|UMI
URUGUAY|URY
UZBEKISTAN|UZB
VANUATU|VUT
VENEZUELA|VEN
VIET NAM|VNM
VIRGIN ISLANDS (BRITISH)|VGB
VIRGIN ISLANDS (U.S.)|VIR
WALLIS AND FUTUNA ISLANDS|WLF
WESTERN SAHARA|ESH
YEMEN|YEM
ZAMBIA|ZMB
ZIMBABWE|ZWE

# State Codes

When creating entities in LogiNext that require state specific location information associated with them, use the State codes listed below. 
For example, if you want to create an Order that is to be picked up from a Pick-up location in New York , you would pass 'NY' as the 'pickupState' in the Create Order API.
Note that the state code you enter should map to the country code entered in the corresponding country parameter. You cannot enter the state code for London if you have selected 'USA' as the country.

If you wish to enter a state code not listed below, please reach out to your Account Manager, write to us at: <a href="mailto:support@loginextsolutions.com?Subject=Postal-Code%20Queries" target="_top">support@loginextsolutions.com</a> 

## United States
State | Code
--------- | ---------
Alabama | AL
Alaska  | AK
Arizona | AZ
Arkansas  | AR
California  | CA
Colorado  | CO
Connecticut | CT
Delaware  | DE
District of Columbia  | DC
Florida | FL
Georgia | GA
Hawaii  | HI
Idaho | ID
Illinois | IL
Indiana | IN
Iowa  | IA
Kansas | KS
Kentucky | KY
Louisiana | LA
Maine | ME
Maryland | MD
Massachusetts | MA
Michigan  | MI
Minnesota | MN
Mississippi | MS
Missouri  | MO
Montana | MT
Nebraska | NE
Nevada  | NV
New Hampshire | NH
New Jersey | NJ
New Mexico | NM
New York | NY
North Carolina | NC
North Dakota | ND
Ohio | OH
Oklahoma | OK
Oregon | OR
Pennsylvania | PA
Rhode Island | RI
South Carolina | SC
South Dakota | SD
Tennessee | TN
Texas | TX
Utah | UT
Vermont | VT
Virginia | VA
Washington | WA
West Virginia | WV
Wisconsin | WI
Wyoming | WY

## India

State | Code
--------- | ---------
Delhi|DL
Andhra Pradesh|AP
Goa|GA
Jharkhand|JH
Manipur|MN
Punjab|PB
Uttar Pradesh|UP
Arunachal Pradesh|AR
Gujarat|GJ
Karnataka|KA
Meghalaya|ML
Rajasthan|RJ
Uttaranchal|UT
Assam|AS
Haryana|HR
Kerala|KL
Mizoram|MZ
Sikkim|SK
West Bengal|WB
Bihar|BR
Himachal Pradesh|HP
Madhya Pradesh|MP
Nagaland|NL
Tamil Nadu|TN
Chhattisgarh|CH
Jammu and Kashmir|JK
Maharashtra|MH
Orissa|OR
Tripura|TR
Telangana|TA
Andaman and Nicobar Islands|AN
Chandigarh|CD
Dadra and Nagar Haveli|DN
Daman and Diu|DD
Lakshadweep|LD
Puducherry|PC

## Australia

State | Code
--------- | ---------
New South Wales|New South
Victoria|Victoria
Queensland|Queensland
South Australia|South Aust
Tasmania|Tasmania

## Canada

State | Code
--------- | ---------
Alberta|Alberta
British Columbia|British Co
Manitoba|Manitoba
New Brunswick|New Brunsw
Newfoundland and Labrador|Newfoundla
Nova Scotia|Nova Scoti
Northwest Territory|Northwest
Nunavut Territory|Nunavut Te
Ontario|Ontario
Prince Edward Island|Prince Edw
Quebec|Quebec
Saskatchewan|Saskatchew
Yukon|Yukon


## Mexico

State | Code
--------- | ---------
Aguascalientes|AGU
Baja California|BCN
Baja California Sur|BCS
Campeche|CAM
Colima|CHH
Coahuila De Zaragoza|CHP
Chiapas|COA
Chihuahua|COL
Distrito Federal|DIF
Durango|DUR
Guerrero|GRO
Guanajuato|GUA
Hidalgo|HID
Jalisco|JAL
Mexico|MEX
Michoacan De Ocampo|MIC
Morelos|MOR
Nayarit|NAY
Nuevo Leon|NLE
Oaxaca|OAX
Puebla|PUE
Queretaro De Arteaga|QUE
Quintana Roo|ROO
Sinaloa|SIN
San Luis Potosi|SLP
Sonora|SON
Tabasco|TAB
Tamaulipas|TAM
Tlaxcala|TLA
Veracruz Llave|VER
Yucatan|YUC
Zacatecas|ZAC


## Saudi Arabia

State | Code
--------- | ---------
Ha'il|Ha'il
Qassim|Qassim
Riyadh|Riyadh
Tabuk|Tabuk
Madinah|Madinah
Makkah|Makkah
Bahah|Bahah
Northern Borders|Northern B
Jawf|Jawf
Jizan|Jizan
Asir|Asir
Najran|Najran
Eastern Province|Eastern Pr


## Tanzania

State | Code
--------- | ---------
Dar es salaam Tz|Dar es sal
Arusha Tz|Arusha Tz
Mbeya Tz|Mbeya Tz
Mtwara Tz|Mtwara Tz
Dodoma Tz|Dodoma Tz
Other States Tz|Other Stat

## United Arab Emirates

State | Code
--------- | ---------
Abu Dhabi|AZ
Dubai|DU
Sharjah|SH
Ajman|AJ
Umm Al Quwain|UQ
Ras Al Khaimah|RK
Fujairah|FU

## Malaysia

State | Code
--------- | ---------
Johor|JHR
Kedah|KDH
Kelantan|KTN
Kuala Lumpur|KUL
Labuan|LBN
Melaka|MLK
Negeri Sembilan|NSN
Pahang|PHG
Perak|PRK
Perlis|PLS
Pulau Pinang|PNG
Putrajaya|PJY
Sabah|SBH
Sarawak|SWK
Selangor|SGR
Terengganu|TRG

## Indonesia

State | Code
--------- | ---------
Jawa Barat|JB
Jakarta Raya|JK
Jawa Timur|JI
Jawa Tengah|JT
Sumatera Utara|SU
Yogyakarta|YO
Kalimantan Timur|KI
Sumatera Barat|SB
Banten|BT
Lampung|LA
Kalimantan Selatan|KS
Sulawesi Utara|SA
Bali|BA
Kalimantan Barat|KB
Jambi|JA
Nusa Tenggara Timur|NT
Nusa Tenggara Barat|NB
Aceh|AC
Sulawesi Tengah|ST
Bengkulu|BE
Sulawesi Tenggara|SG
Kalimantan Tengah|KT
Papua|PA
Riau|RI
Sulawesi Barat|SR
Maluku|MA
Irian Jaya Barat|PB
Sumatera Selatan|SS
Gorontalo|GO
Sulawesi Selatan|SN
Maluku Utara|MU
Kepulauan Riau|KR
Kepulauan Bangka Belitung|BB
Kalimantan Utara|KU
Papua Barat|PB

## Pakistan
State | Code
--------- | ---------
Punjab | PB
Sindh | SD
North-West Frontier | KP
Balochistan | BA
Northern Areas | GB
Azad Kashmir | JK
Federally Administered Tribal Areas | TA
Islamabad | IS

# Timezone Codes

When creating entities in LogiNext for which you want to associate Timezone specific information, use the Timezone codes listed below. 

For example, if you want to create an Order that is to be picked up from a Pick-up location in New York , you would pass 'America/New_York' as the 'pickupAddressTimezone' in the Create Order API.

If you wish to enter a Timezone code not listed below, please reach out to your Account Manager, write to us at: <a href="mailto:support@loginextsolutions.com?Subject=Postal-Code%20Queries" target="_top">support@loginextsolutions.com</a> 

Country Name|  Timezon ID
--------- | ---------
AFGHANISTAN|  Asia/Kabul
ALBANIA|  Etc/GMT-1
ALGERIA|  Etc/GMT-1
AMERICAN SAMOA| Etc/GMT+11
ANDORRA|  Europe/Andorra
ANGOLA| Africa/Luanda
ANGUILLA| America/Anguilla
ANTARCTICA| Antarctica/Palmer
ANTIGUA AND BARBUDA|  America/St_Johns
ARGENTINA|  America/Argentina/Buenos_Aires
ARMENIA|  Asia/Yerevan
ARUBA|  America/Aruba(-4:00)
AUSTRALIA|  Antarctica/Macquarie
AUSTRALIA|  Australia/Adelaide
AUSTRALIA|  Australia/Brisbane
AUSTRALIA|  Australia/Darwin
AUSTRALIA|  Australia/Hobart
AUSTRALIA|  Australia/Lord_Howe
AUSTRALIA|  Australia/Melbourne
AUSTRALIA|  Australia/Perth
AUSTRALIA|  Australia/Sydney
AUSTRIA|  Europe/Vienna
AZERBAIJAN| Asia/Baku
BAHAMAS|  America/Nassau
BAHRAIN|  Asia/Bahrain
BANGLADESH| Asia/Dhaka
BARBADOS| America/Barbados
BELARUS|  Europe/Minsk
BELGIUM|  Europe/Brussels
BELIZE| America/Belize
BENIN|  Africa/Porto-Novo
BERMUDA|  Atlantic/Bermuda
BHUTAN| Asia/Thimphu
BOLIVIA|  America/La_Paz
BOTSWANA| Africa/Gaborone
BOTSWANA| Canada/Atlantic
BOTSWANA| Canada/Central
BOTSWANA| Canada/Eastern
BOTSWANA| Canada/Mountain
BOTSWANA| Canada/Newfoundland
BOTSWANA| Canada/Pacific
BOUVET ISLAND|  Etc/GMT+5
BRAZIL| America/Sao_Paulo
BRUNEI| Asia/Brunei
BULGARIA| Europe/Sofia
BURKINA FASO| Africa/Ouagadougou
BURUNDI|  Africa/Bujumbura
CAMBODIA| Asia/Phnom_Penh
CAMEROON| Etc/GMT-1
CANADA| Canada/Atlantic
CANADA| Canada/Eastern
CANADA| Canada/Mountain
CAYMAN ISLANDS| America/Cayman
CHAD| Africa/Ndjamena
CHILE|  America/Santiago
CHINA|  Asia/Shanghai
CHRISTMAS ISLAND| Indian/Christmas
COLOMBIA| America/Bogota
COMOROS|  Etc/GMT-3
CONGO|  Africa/Brazzaville
CONGO, THE DRC| Africa/Kinshasa
COOK ISLANDS| Etc/GMT+10
COSTA RICA| America/Costa_Rica
CROATIA|  Etc/GMT-1
CUBA| America/Havana
CYPRUS| Asia/Nicosia
CZECH REPUBLIC| Europe/Prague
DENMARK|  Europe/Copenhagen
DJIBOUTI| Africa/Djibouti
DOMINICA| America/Dominica
DOMINICAN REPUBLIC| Europe/Copenhagen
EGYPT|  Africa/Cairo
EL SALVADOR|  America/El_Salvador
EQUATORIAL GUINEA|  Africa/Malabo
ERITREA|  Africa/Asmara
ESTONIA|  Europe/Tallinn
ETHIOPIA| Africa/Addis_Ababa
FAROE ISLANDS|  Atlantic/Faroe
FIJI| Pacific/Fiji
FINLAND|  Europe/Helsinki
FRANCE| Europe/Paris
FRENCH GUIANA|  Etc/GMT+3
FRENCH POLYNESIA| Etc/GMT+10
GABON|  Africa/Libreville
GAMBIA| Africa/Banjul
GEORGIA|  Atlantic/South_Georgia
GERMANY|  Europe/Berlin
GHANA|  Africa/Accra
GIBRALTAR|  Europe/Gibraltar
GREECE| Europe/Athens
GREENLAND|  Etc/GMT+3
GRENADA|  America/Grenada
GUADELOUPE| America/Guadeloupe
GUAM| Pacific/Guam
GUATEMALA|  America/Guatemala
GUINEA| Africa/Conakry
GUYANA| America/Guyana
HAITI|  America/Port-au-Prince
HONDURAS| America/Tegucigalpa
HONG KONG|  Asia/Hong_Kong
HUNGARY|  Europe/Budapest
ICELAND|  Atlantic/Reykjavik
INDIA|  Asia/Calcutta
INDONESIA|  Asia/Jakarta
IRAQ| Asia/Baghdad
IRELAND|  Europe/Dublin
ISRAEL| Asia/Jerusalem
ITALY|  Europe/Rome
JAMAICA|  America/Jamaica
JAPAN|  Asia/Tokyo
JORDAN| Asia/Amman
KAZAKHSTAN| Etc/GMT-5
KENYA|  Africa/Nairobi
KIRIBATI| Pacific/Tarawa
KOREA, D.P.R.O.|  Asia/Pyongyang
KOREA, REPUBLIC OF| Asia/Seoul
KUWAIT| Asia/Kuwait
KYRGYZSTAN| Asia/Bishkek
LAOS| Asia/Vientiane
LATVIA| Europe/Riga
LEBANON|  Asia/Beirut
LESOTHO|  Africa/Maseru
LIBERIA|  Africa/Monrovia
LIECHTENSTEIN|  Europe/Vaduz
LITHUANIA|  Europe/Vilnius
LUXEMBOURG| Europe/Luxembourg
MACAU|  Asia/Macau
MACEDONIA|  Etc/GMT-1
MADAGASCAR| Indian/Antananarivo
MALAWI| Etc/GMT-2
MALAYSIA| Asia/Kuala_Lumpur
MALDIVES| Indian/Maldives
MALI| Africa/Bamako
MALTA|  Europe/Malta
MARSHALL ISLANDS| Pacific/Majuro
MARTINIQUE| America/Martinique
MAURITANIA| Africa/Nouakchott
MAURITIUS|  Indian/Mauritius
MAYOTTE|  Indian/Mayotte
MEXICO| America/Mexico_City
MEXICO| Etc/GMT+7
MEXICO| Etc/GMT+7
MOLDOVA, REPUBLIC OF| Europe/Chisinau
MONACO| Europe/Monaco
MONGOLIA| Asia/Ulaanbaatar
MONTENEGRO| Etc/GMT-1
MONTSERRAT| America/Montserrat
MOROCCO|  Etc/GMT
MOZAMBIQUE| Africa/Maputo
MYANMAR (BURMA)|  Asia/Rangoon
NAMIBIA|  Africa/Windhoek
NAURU|  Pacific/Nauru
NEPAL|  Asia/Kathmandu
NETHERLANDS|  Europe/Amsterdam
NEW CALEDONIA|  Etc/GMT-11
NEW ZEALAND|  Pacific/Auckland
NICARAGUA|  America/Managua
NIGER|  Etc/GMT-1
NIGERIA|  Etc/GMT-1
NIUE| Pacific/Niue
NORFOLK ISLAND| Pacific/Norfolk
NORWAY| Europe/Oslo
OMAN| Asia/Muscat
PAKISTAN| Asia/Karachi
PALAU|  Pacific/Palau
PANAMA| America/Panama
PAPUA NEW GUINEA| Pacific/Port_Moresby
PARAGUAY| America/Asuncion
PERU| America/Lima
PHILIPPINES|  Asia/Manila
PITCAIRN| Pacific/Pitcairn
POLAND| Europe/Warsaw
PORTUGAL| Europe/Lisbon
PUERTO RICO|  America/Puerto_Rico
QATAR|  Asia/Qatar
REUNION|  Indian/Reunion
ROMANIA|  Europe/Bucharest
RWANDA| Africa/Kigali
SAINT LUCIA|  America/St_Lucia
SAMOA|  Pacific/Apia
SAN MARINO| Etc/GMT-1
SAUDI ARABIA| Asia/Riyadh
SENEGAL|  Africa/Dakar
SERBIA| Europe/Belgrade
SEYCHELLES| Etc/GMT-4
SIERRA LEONE| Africa/Freetown
SINGAPORE|  Asia/Singapore
SLOVENIA| Etc/GMT-1
SOLOMON ISLANDS|  Etc/GMT-11
SOMALIA|  Africa/Mogadishu
SOUTH AFRICA| Africa/Blantyre
SOUTH SUDAN|  Etc/GMT-3
SPAIN|  Europe/Madrid
SRI LANKA|  Asia/Colombo
SUDAN|  Africa/Khartoum
SURINAME| America/Paramaribo
SWAZILAND|  Africa/Mbabane
SWEDEN| Europe/Stockholm
SWITZERLAND|  Etc/GMT-1
TAJIKISTAN| Asia/Dushanbe
TANZANIA| Africa/Addis_Ababa
THAILAND| Asia/Bangkok
TOGO| Africa/Lome
TOKELAU|  Etc/GMT-13
TONGA|  Pacific/Tongatapu
TRINIDAD AND TOBAGO|  America/Port_of_Spain
TUNISIA|  Africa/Tunis
TURKEY| Etc/GMT-3
TURKMENISTAN| Asia/Ashgabat
TUVALU| Pacific/Funafuti
UGANDA| Africa/Kampala
UKRAINE|  Etc/GMT-2
UNITED ARAB EMIRATES| Asia/Dubai
UNITED KINGDOM| Europe/London
UNITED STATES|  America/Anchorage
UNITED STATES|  America/Chicago
UNITED STATES|  America/Denver
UNITED STATES|  America/Los_Angeles
UNITED STATES|  America/New_York
UNITED STATES|  Pacific/Honolulu
URUGUAY|  America/Montevideo
UZBEKISTAN| Asia/Tashkent
VANUATU|  Etc/GMT-11
VENEZUELA|  America/Caracas
VIETNAM|  Etc/GMT-7
YEMEN|  Etc/GMT-3
ZAMBIA| Africa/Lusaka
ZIMBABWE| Africa/Harare


# Postal Codes

If you are looking for a postal code/zip code list for your country, please reach out to your Account Manager to get it configured, or write to us at: <a href="mailto:support@loginextsolutions.com?Subject=Postal-Code%20Queries" target="_top">support@loginextsolutions.com</a> 

# Delivery Associate Status

The current Status of your Delivery Associate. The Status can be updated by calling the Update Status API for the Delivery Associate.

Status | Code | Description
--------- | --------- | -------------
Active | ACTIVE | A Delivery Associate that is Active will be assigned Orders and can Sign In to their TrackNext account. 
Inactive | INACTIVE | A Delivery Associate that is Inactive will not be assigned any orders, or be able to log in to their TrackNext account.
On Break | ONBREAK | The Delivery Associate is not currently fulfilling Orders. New Orders cannot be assigned to an On Break Delivery associate. Only Active Delivery Associates can be On Break.
Off Break | OFFBREAK | Delivery Associate is back from Break and ready to fulfill Orders. Only Active Delivery Associates can be On Break.

# Trip Status

Status | Description
---------|------------
Not Started | The Trip has been created in the LogiNext system, but the Delivery Associate has not started the Pick-up and Delivery of Orders.
In Transit | The Orders associated with the Trip are currently being serviced.
Ended | The Orders associated with the Trip have been serviced, and their statuses have been updated.

<style>
.sup{
  padding-right:4px !important;
  display:inline;
}
</style>
<script>
  setTimeout(function() {
    jQuery(".tocify-wrapper .tocify ul li a").filter(
    function(){   
       if(jQuery(this).text() == "LogiNext Haul TM"){
            jQuery(this).text("LogiNext Haul");
            jQuery(this).css("display","inline");
            jQuery(this).addClass("sup");
            // jQuery(this).css("padding-right","4px !important");
            jQuery(this).closest('li').append("<sup>TM</sup>")
        }
        if(jQuery(this).text() == "LogiNext Mile TM"){
            jQuery(this).text("LogiNext Mile");
            jQuery(this).css("display","inline");
            jQuery(this).addClass("sup");
            // jQuery(this).css("padding-right","4px !important");
            jQuery(this).closest('li').append("<sup>TM</sup>")
        }
        if(jQuery(this).text() == "LogiNext OnDemand TM"){
            jQuery(this).text("LogiNext OnDemand");
            jQuery(this).css("display","inline");
            jQuery(this).addClass("sup");
            // jQuery(this).css("padding-right","4px !important");
            jQuery(this).closest('li').append("<sup>TM</sup>")
        }
        if(jQuery(this).text() == "LogiNext Field TM"){
            jQuery(this).text("LogiNext Field");
            jQuery(this).css("display","inline");
            jQuery(this).addClass("sup");
            // jQuery(this).css("padding-right","4px !important");
            jQuery(this).closest('li').append("<sup>TM</sup>")
        }
    });
  }, 50);
</script>
