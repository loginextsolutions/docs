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

### Delivery Associate 

A Delivery Associate is the resource that would pickup or deliver your customers’ orders. Delivery Associates can be maintainence men, repair men, or Delivery Associates.

When a Delivery Associate is created in LogiNext, Login credentails are generated, using which the Delivery Associate can Sign-in to the TrackNext app.

###Vehicle

A Vehicle can be used to Pick-up and Deliver Orders that are part of the Trip. A Vehicle could be a bike, car, truck, van and more. 

###Driver 

A Driver is responsible for driving/riding the Delivery Vehicle.

Depending on the kind of business, the Driver and Delivery Associate could be the same person. In some cases they are different where in addition to a Driver, there is a Delivery Associate delivering the shipments home.

###Branch 

A Branch could be the fulfillment center or warehouse where Orders are either Delivered or Pickedup from. 

### Order

Orders are the base transaction entities in the LogiNext system. An Order has details of shipment you want to pickup from your merchant or deliver to your customer. Pick Up and Delivery could be different depending on the industry you are in. For example, in the Courier Industry, Pick Up and Delivery can be for Customers.


### Trip

A Trip is a run where a Delivery Associate fulfills one or more Orders. A Trip is created in the LogiNext System as a result of Route Planning or Auto-Assignment operations.

### Account

An Account is used to represent LogiNext’s Customer’s Customer. You can create an Account in LogiNext to represent different Customers. Orders can be created in LogiNext on behalf of your Customers using the 'clientCode' field in the APIs that support this functionality. Details will be mentioed in the specific APIs.

### Service Time 

Service Time is the time it takes to service an Order at a particular location. For example - If an Order is to be delivered at a Customer's Home address, the Service time would include the time for parking the Vehicle and accounting for security checks at the location if any. Similarly, if an Order is to be delivered at a warehouse, Service Time will account for parking, loading and unloading at the delivery location.



## Integration Details

Using the LogiNext API, you can integrate all the segments of your logistics and supply chain network into our product platform to create a seamless experience for your operations and executive team.

The LogiNext API is designed to allow our client partners to add delivery associates(resources), orders, plan a route, start the trip, track and follow the updates till the trip is completed and shipment is pickedup/delivered at the desired location.

Below are a few important steps that would explain what it takes for you, as our Client partner, to link your system with LogiNext’s.

<b><u>Step 1</u></b> –  Please read carefully the Request, Responses and Authentication section so that you can configure things on your end to integrate with LogiNext APIs.

<b><u>Step 2</u></b> – You will need to get the username and password which will be provided to you either by our system (in case of auto sign-up) or by your LogiNext Account Manager.

<b><u>Step 3</u></b> – (Optional) If you are planning to consume any of the LogiNext Webhooks, you will need to share the end-point URL of your system to consume the Webhook. This end-point will be configured in the LogiNext system by your Account Manager.

<br> In case of any queries during the integration process, please reach out to us at
<a href="mailto:support@loginextsolutions.com?Subject=Integration%20Queries" target="_top">support@loginextsolutions.com</a>.


# Requests

The base URL for all requests to the LogiNext API is:

https://api.loginextsolutions.com/

Our API is REST-based. This means:

1. It makes use of standard HTTP methods like GET, POST, DELETE.

2. The API uses standard HTTP error responses(status codes) to indicate status of your requests – success and error codes.

3. All LogiNext API requests are authenticated with an API Token. Details on how to obtain an authentication Token are mentioned in the <a href="https://developers.loginextsolutions.com/#authentication" target="_top">Authentication section</a> of this Documentation.

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
202 | Acknowledged | This status code indicates that a request has been received and taken up for processing. It may take some time to complete processing this kind of request, and LogiNext will typically send a webhook notification with the results of the response once the request has been successfully completed.
207 | Partial Success | This status code indicates that some of the entities in the request were successfully processed, while some others failed. The response will provide details regarding the state of each record that was sent in the request.
400 | Bad Request  | This message means that the request is syntactically incorrect. You will receive this med=ssage in a case where the request body sent is not a standard JSON or array object as is expected by LogiNext.
401 | Invalid username or password  | This message means that invalid credentials are passed.
404 | Not Found  | This message means that the resource could not be found.
405 | Method Not Allowed  | This message means that the method used to access the resource is invalid.
409 | Request Error  | This message means that there is a validation error in the data sent in the request body. This could either be missing out a mandatory field in the API or sending an incorrect branch name in the request body.
415 | Unsupported Media Type  |  This message means that the request is not in the format accepted by this method of target resource.
429 | Too Many Requests  |  This message means that too many resources are requested.
500 | Internal Server Error  | This message means that there is an issue with the LogiNext server.Please try accessing the request later.
503 | Service Unavailable  | This message means that the LogiNext applications are down for scheduled maintenance.  Please try accessing the request later.

# Authentication

##Authenticate

The LogiNext API uses Authentication tokens to provide you an authorized access. 

You can generate an Authentication token by logging in to your LogiNext Account and going to the 'API Token Management' page, or by calling the below API endpoint.

You will have to pass the username and password for your LogiNext Account, or by your LogiNext Account Manager.

The response will contain a the Authentication Token required to make calls to the LogiNext API.

If you want session to be valid for 1 Hour, then the "sessionExpiryTimeout" should be 1.<br>
Similarly for - <br>
24 Hours, it should be 24 <br>
6 months, it should be  180* 24 = 4320<br>
12 Months, it should be 365*24= 8760<br>
5 Years, it should be 365*5*24 = 43800<br>
10 Years, it should be 365*10*24= 87600<br>

<b><u>If you do not provide 'sessionExpiryTimeout', the validity of this session token will be 90 days(3 months).</u></b>

Ensure that you add the token as part of every Loginext API call.

Note that certain API fields like the 'paymentType' field in the Create Order API are dependant on the language preferences set for the user account the API token is created for when it is created. For a seamless integration experience, we recommend using an English language user account for creating your API tokens for integrating with LogiNext.

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

The response header will consist of Authentication Token. Please note that the validity of this token by default is 90 days.

Header | Sample Value
--------- | -------
WWW-Authenticate | BASIC 075b8961-bd02-454c-83eb-259f965f313f


## Authenticate Delivery Associate

Call the mobile authenticate API to obtain the authentication token for a Delivery Associate.

You will have to pass the username and password entered at the time of creating the Delivery Associate in the LogiNext system in the request body.

The response will contain an authentication token which is unique to every specific Delivery Associate. This token will have a validaity of 4 years from the time of creation.



> Definition

```json
  https://api.loginextsolutions.com/LoginApp/login/mobile/auth
```
> Request Body

```json
{
  "userName": "johnc",
  "password": "admin",
  "imei":"854437655912443",
  "latitude": 40.1114131,
  "longitude": 74.9094666,
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
userName | String | 255 | Mandatory | Username entered when created the Delivery Associate in the LogiNext system
password | String | 255 | Mandatory | Password entered when created the Delivery Associate in the LogiNext system
imei | String | 50 | Mandatory | IMEI Number of the Delivery Associate's phone
latitude | Double | 10,13 | Optional | Geolocation(latitude) coordinate of the Delivery Associate
longitude | Double | 10,13 | Optional | Geolocation(longitude) coordinate of the Delivery Associate
androidId | String | 10 | Optional | Device ID of the Delivery Associate
androidTime | Date | | Optional | Current Date and Time in UTC and the mentioned Format. Sample Value - 2017-12-11T07:21:39Z


#### Response
The response will consist of parameters as mentioned in the "Responses" section based on the request parameters passed.For example,the response can contain 200 - Success or 401 - Invalid username or password, etc.

#### Response Headers

The response header will consist of Authentication Token. Please note that the validity of this token and key is 4 years.

Header | Sample Value
--------- | -------
WWW-Authenticate | BASIC 075b8961-bd02-454c-83eb-259f965f313f


##Invalidate

You can fetch a fresh authentication token by calling the below API. This call will invalidate the existing token and you will be provided with a new authentication token which you will have to pass in every other API call.

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


LogiNext API defines Rate Limits based on the API being called. Different APIs have different Rate Limits depending on the use case and request body of the API. APIs are categorised as per the following criteria

API Type | Description |Rate Limit
--------- | ------- | -------------
Tier 1 APIs | Tier 1 APIs have a specified Rate Limit to allow for a varierty of operations in the LogiNext system.  | 5 requests per second
Tier 2 APIs | Tier 2 APIs have a more generous rate Limit than Tier 1 APIs, to support burst behaviour. | 10 requests per second
Special Tier APIs | Custom Rate Limits are defined for Special Tier APIs. For example, the  the Route Optimization API allows 1 request per minute. | Custom Rate Limits. Rate limit Will be mentioned in the API description.

Going beyond your rate limit will cause you to receive a temporary ban. You will receive a 429 'Max Request Limit Reached' error to your API calls if you go beyond this limit.

Note that all Rate Limits apply on a rolling time interval basis. If you are calling a Tier 1 API that supports a Rate Limit of 5 requests per second, that means you can send a total of 5 requests within a one second interval of each other.

## Batching

The LogiNext API supports multiple records per request. For eg - You can send upto 20 Orders to be created in a single call of the Create Order API. 

APIs that support batching will have rate limit depending on the tier of the API.

## Best Practices

1. We recommend using webhooks instead of polling GET APIs to get real time event updates. For example, if you wish to get the current status of an Order, consume the Update Order Status webhook rather than polling the Get Order API consistently to fetch Order related details.

2. You can decide if you wish to leverage the batching functionality of the LogiNext API depending on how your business operations run. For example, you may choose to send 20 Orders in a single request of the Create Order API if you witness large bursts in transactions in your system at certain times. In this case, the Create ORder API can return a partial success response where some of the Orders are successfully created in the LogiNext system, and some Orders did not get created. You will need to understand how to handle the partial success response and define business logic in your code to handle it.


3. We recommend implementing retry mechanism in case of the 429, or 500 error responses received from the LogiNext API.

4. Implement logic to respect the LogiNext API Rate limits. Exceeding these limits will cause API requests to receive a 429 error response from LogiNext.


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
      "lastTrackedLatitude": 40.760838,
      "lastTrackedLongitude": 74.909683,
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
      "lastTrackedLatitude": 40.760838,
      "lastTrackedLongitude": 74.909683,
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
      "lastTrackedLatitude": 40.760838,
      "lastTrackedLongitude": 74.909683,
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

This API is used to update a trip using its reference ID.

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
  "latitude": 40.760838,
  "longitude": 74.9889999,
  "time": "2016-07-14T09:11:56Z",
  "batteryPerc": 70.5,
  "speed": 40.4,
  "messageType": "REG",
  "temperature": 30.5,
  "reeferActive": true,
  "harshDriving": 63.5,
  "doorStatus":false

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
reeferActive | Boolean | | Optional | This represents the state of the Reefer. eeferActive=true represents the event when the Reefer is switched on and reeferActive=false refers to the event when Reefer is switched off
harshDriving | Double | 13,10 | Optional | Event when Harsh Acceleration / Harsh Deceleration has been observed and speed associated with the event. You can calculate harsh driving  as the change in” speed per second”. The SI units for harsh driving are m/s2, meters per second squared or meters per second per second, which means by how many meters per second the velocity changes every second. The units shall vary as per the Unit System preferences set in LogiNext Settings → System Preferences. In case if Harsh Acceleration occurs, the change in speed reported shall be positive. If Harsh Deceleration occurs, reported, the change in speed reported shall be negative.
doorStatus | Boolean |  | Optional | doorStatus=true represents the event when the Door is open and doorStatus=false refers to the event when Door is closed

### Create Tracking Record (Bulk)

> Create Tracking Record - Sample Request

```json
[
  {
  "trackerId": "358899056518932",
  "latitude": 40.760838,
  "longitude": 74.9889999,
  "time": "2018-01-04T07:21:56Z",
  "batteryPerc": 70.5,
  "speed": 40.4,
  "messageType": "REG",
  "temperature": 30.5,
  "reeferActive": true,
  "harshDriving": 63.5,
  "doorStatus":false
  }, {
  "trackerId": "4209917397",
  "latitude": 40.760838,
  "longitude": 74.9889999,
  "time": "2018-01-04T07:21:56Z",
  "batteryPerc": 70.5,
  "speed": 40.4,
  "messageType": "REG",
  "temperature": 30.5,
  "reeferActive": true,
  "harshDriving": 63.5,
  "doorStatus":false
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
reeferActive | Boolean | | Optional | This represents the state of the Reefer. eeferActive=true represents the event when the Reefer is switched on and reeferActive=false refers to the event when Reefer is switched off
harshDriving | Double | 13,10 | Optional | Event when Harsh Acceleration / Harsh Deceleration has been observed and speed associated with the event. You can calculate harsh driving  as the change in” speed per second”. The SI units for harsh driving are m/s2, meters per second squared or meters per second per second, which means by how many meters per second the velocity changes every second. The units shall vary as per the Unit System preferences set in LogiNext Settings → System Preferences. In case if Harsh Acceleration occurs, the change in speed reported shall be positive. If Harsh Deceleration occurs, reported, the change in speed reported shall be negative.
doorStatus | Boolean |  | Optional | doorStatus=true represents the event when the Door is open and doorStatus=false refers to the event when Door is closed

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

The Mile Product refers to the first mile and last mile Order Pick-up and Deliveries. The Mile product will help you create -  

Pick-up orders thereby catering to your first leg of logistics, wherein shipments are ‘picked’ from your customer / merchants / suppliers / vendors and transported to the hub for aggregation.

Delivery orders by loading the items for different orders from a Single Point of Pick Up (Hub) and deliver the same to your customers (Multiple Drop Points).

Point to Point Orders for variable Pick-up and Delivery locations.

1. Once the resources are created, then you can add shipments or orders in the LogiNext database by calling Create Order API. You need to provide the Order Number, Date and time window on which order should be picked-up / delivered and the pick-up / delivery address details. Additionally you can also specify the Crate level and line item level details contained in that order.The response consists of the Reference ID against each Order ID which needs to be stored in your system for future references.

2. Once the optimization for capacity and route planning is completed, trips will be created by the LogiNext system and you can mark the trip as started by calling the Start Trip API and mark the same trip as stopped by calling Stop Trip API. In both these API you will have to pass the trip reference ID.

3. Finally you can track your pick-up / delivery executive in transit through the Track Last Location API. In this case also you need to pass the Trip Reference Id.

4. You can also mark a particular order as cancelled by calling the Cancel Order API and passing the order reference ID.

5. In case, your account is being configured into the LogiNext system as a pick-up and delivery both, then you can also create the return shipment for the order thereby optimizing you reverse logistics and return planning.


## Customer 

### Create

> Sample Request

```json
[
  {
    "accountCode":"James",
    "name":"James Wan",
    "mobile":"341245673212",
    "email":"james@ablogs.com",
    "customerType":"Preferred",
    "billingAddress": {
          "apartment":"Suite No. 1, Milsons Towers",
          "streetName":"Michigan Avenue",
          "landmark":"Opp. Subway",
          "locality":"Dowtown Chicago",
          "city":"Chicago",
          "state":"IL",
          "country":"USA",
          "pincode":"10045",
          "latitude": 40.760838,
          "longitude": 79.555
    }
  }
]
```

> Success Response

```json
{
    "status": 200,
    "message": "Customer(s) created successfully",
    "data": [
        {
            "index": 0,
            "referenceId": "6a34c7274df0489f97c0f891514b488b",
            "accountCode": "cust001"
        }
    ],
    "hasError": false
}

```


> Partial Success Response

```json


{
    "status": 207,
    "message": "Customer(s) created partially",
    "moreResultsExists": false,
    "data": [
        {
            "index": 0,
            "referenceId": "3a973fdcb1eb41d5ad7408c57e13cc87",
            "accountCode": "cust001"
        }
    ],
    "error": [
        {
            "index": 1,
            "accountCd": "cust001",
            "errorList": [
                {
                    "key": "accountCode",
                    "message": [
                        "Account Code already exists for client"
                    ]
                }
            ]
        }
    ],
    "hasError": true
}

```


> Failure Response

```json

{
    "status": 409,
    "message": "Customer(s) creation failed",
    "moreResultsExists": false,
    "error": [
        {
            "index": 0,
            "accountCd": "cust001",
            "errorList": [
                {
                    "key": "mobile",
                    "message": [
                        "INVALID Mobile Number"
                    ]
                }
            ]
        }
    ],
    "hasError": true
}

```

Create a new Customer the LogiNext system with this API. A new Customer will be created and assigned a unique Reference ID that can be used to identify the Customer later.

If you have Customers created in your current system that you would like to push to LogiNext, call this API with the parameters mentioned below to add these Customers in LogiNext.

This API will create a Customer Entity with contact information and an optional Billing Address for a Customer. To create a Shipping/ Delivery address for a Customer, call the Create Address API.

These are the customers you would create Orders for in LogiNext. The Customer ID you use to identify individual customers can be used in the Create Order API to create an Order.

This API will only accept inputs if your Customer Profiling property is set in LogiNext. To know more about the Customer Profiling property, please reach out to us at support@loginextsolutions.com.

Address field validations will be based on the behaviour defined in the Address Configuration screen of your LogiNext account<a href="https://products.loginextsolutions.com/product/#/settings/addressfieldConfiguration" target="_top">here</a>

You can create a maximum of 5 Customers in LogiNext in one call of this API. This API has a rate limit of 1 request per second.

#### Request

<span class="post">POST</span>`https://api.loginextsolutions.com/ClientApp/customer/v1/create`


#### Request Parameters

Parameter | DataType | Length |  Required | Description
-----------|-------|------- |------- | ----------
accountCode | String | 50 | Mandatory | Unique Customer ID used to identify a Customer.
name | String | 255 | Mandatory | Customer name.
mobile | String | 255 | Mandatory | Customer Mobile NUmber.
email | String | 255 |Optional | Customer Email ID.
customerType | String | 255 | Optional |  Customer Type. For example, you can create 'Premium' Customers and identify them in LogiNext based on values in these fields. 
billingAddress.apartment | String | 40 | Address Validations | Customer Billing Address apartment.
billingAddress.streetName | String | 100 | Address Validations | Customer Billing Address Street Name.
billingAddress.landmark | String | 255 | Address Validations | Customer Billing Address landmark.
billingAddress.locality | String | 255 | Address Validations | Customer Billing Address locality.
billingAddress.city | Integer | 20 | Address Validations | Customer Billing Address city.
billingAddress.state | Integer | 20 | Address Validations | Customer Billing Address state. This will be based on the state codes in LogiNext for the country selected by you.
billingAddress.country | String | 255 | Address Validations | Customer Billing Address Country.
billingAddress.pincode | String | 255 | Address Validations | Customer Billing Address Pincode.
billingAddress.latitude | Double | 20 | Optional | Customer Billing Address geo-coordinate(latitude)
billingAddress.longitude | Double | 20 | Optional | Customer Billing Address geo-coordinate(longitude)
clientCode | String | 50 | Optional | This is the identifier for an Account. An Account is used to represent LogiNext’s Customer’s Customer. Pass the name of the Account in this field if you wish to create a Customer entity on behalf of one of your Customers.

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


> Success Response

```json
{
  {
    "status": 200,
    "message": "Customer Details fetched successfully",
    "moreResultsExists": false,
    "data": [
        {
            "accountCode": "name1",
            "name": "James Wan",
            "mobile": "5163063377",
            "email": "james@ablogs.com",
            "customerType": "Preferred",
            "billingAddress": {
                "apartment": "Suite No. 1, Milsons Towers",
                "streetName": "Michigan Avenue",
                "landmark": "Opp. Subway",
                "city": "Mumbai",
                "locality": "Dowtown Chicago",
                "state": "Maharashtra",
                "country": "INDIA",
                "pincode": "10045",
                "latitude": 40.760838,
                "longitude": 74.555
            },
            "isActive": "Y",
            "referenceId": "3a973fdcb1eb41d5ad7408c57e13cc87"
        }
    ],
    "error": [],
    "hasError": false
}

```

> Partial Success Response

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
                  "latitude": 40.760838,
                  "longitude": 74.555
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


> Failure Response

```json
{
    "status": 400,
    "message": "Incorrect reference id / Customer code",
    "moreResultsExists": false,
    "error": [
        "89889897iyguy"
    ],
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
          "latitude": 40.760838,
          "longitude": 74.555
    }
  }
]
```

> Success Response

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

> Partial Success Response

```json
{
    "status": 207,
    "message": "Customer(s) updated partially",
    "moreResultsExists": false,
    "data": [
        {
            "index": 0,
            "referenceId": "3a973fdcb1eb41d5ad7408c57e13cc87"
        }
    ],
    "error": [
        {
            "index": 1,
            "errorList": [
                {
                    "key": "referenceId",
                    "message": [
                        "Reference Id does not exists"
                    ]
                }
            ]
        }
    ],
    "hasError": true
}

```

> Failure Response

```json
{
    "status": 409,
    "message": "Customer(s) updation failed",
    "moreResultsExists": false,
    "error": [
        {
            "index": 0,
            "errorList": [
                {
                    "key": "referenceId",
                    "message": [
                        "Reference Id does not exists"
                    ]
                }
            ]
        }
    ],
    "hasError": true
}

```



Update a Customer the LogiNext system with this API.


This API will update a Customer Entity with the details provided. To update a Shipping/ Delivery address for a Customer, call the Update Address API.

This API will only accept inputs if your Customer Profiling property is set in LogiNext. To know more about the Customer Profiling property, please reach out to us at support@loginextsolutions.com.

Address field validations will be based on the behaviour defined in the Address Configuration screen of your LogiNext account<a href="https://products.loginextsolutions.com/product/#/settings/addressfieldConfiguration" target="_top">here</a>

You can create a maximum of 5 Customers in LogiNExt in one call of this API.


#### Request

<span class="post">POST</span>`https://api.loginextsolutions.com//ClientApp/customer/v1/update`


#### Request Parameters

Parameter | DataType | Length |  Required | Description
-----------|-------|------- |------- | ----------
referenceId  | String | 32 | Mandatory | LogiNext generated Reference ID used to identify a Customer.
accountCode | String | 50 | Optional | Unique Customer ID used to identify a Customer.
name | String | 255 | Optional | Customer name.
mobile | String | 255 | Optional | Customer Mobile NUmber.
email | String | 255 |Optional | Customer Email ID.
customerType | String | 255 | Optional | Customer Type. For example, you can create 'Premium' Customers and identify them in LogiNext based on values in these fields. 
billingAddress.apartment | String | 40 |Optional | Customer Billing Address apartment.
billingAddress.streetName | String | 100 | Optional | Customer Billing Address Street Name.
billingAddress.landmark | String | 255 | Optional | Customer Billing Address landmark.
billingAddress.locality | String | 255 | Optional | Customer Billing Address locality.
billingAddress.city | Integer | 20 | Optional | Customer Billing Address city.
billingAddress.state | Integer | 20 | Optional | Customer Billing Address state. This will be based on the state codes in LogiNext for the country selected by you.
billingAddress.country | String | 255 | Optional | Customer Billing Address Country.
billingAddress.pincode | String | 255 | Optional | Customer Billing Address Pincode.
billingAddress.latitude | Double | 20 | Optional | Customer Billing Address geo-coordinate(latitude)
billingAddress.longitude | Double | 20 | Optional | Customer Billing Address geo-coordinate(longitude)
clientCode | String | 50 | Optional | This is the identifier for an Account. An Account is used to represent LogiNext’s Customer’s Customer. Pass the name of the Account in this field if you wish to update a Customer entity on behalf of one of your Customers.


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
          "apartment":"1901 Wes",
          "streetName":"t Madison Street",
          "landmark":"United Center",
          "locality":"Dowtown Chicago",
          "city":"Chicago",
          "state":"IL",
          "country":"USA",
          "pincode":"60612",
          "latitude": 41.8807,
          "longitude": -87.6742
    },
    "additionalContactDetails": [
            {
                "name": "James Smith",
                "mobileNumber": "18552306564",
                "emailAddress": "james@ablogistics.com"
            },
            {
                "name": "John Barnes",
                "mobileNumber": "18552306565",
                "emailAddress": "john@ablogistics.com"
            }
        ],
    "isPrimary":"Y",
    "clientCode":"MyKart",
    "timeZone":"America/Chicago"
  }
  
]
```

> Success Response

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



Create an Address for an existing Customer in the LogiNext system with this API. A new Customer Address will be created and assigned a unique Reference ID that can be used to identify the Address later.

If you have Addresses created in your current system that you would like to push to LogiNext, call this API with the parameters mentioned below to add them in LogiNext.

This API will only accept inputs if your Customer Profiling property is set in LogiNext. To know more about the Customer Profiling property, please reach out to us at support@loginextsolutions.com.

Address field validations will be based on the behaviour defined in the Address Configuration screen of your LogiNext account<a href="https://products.loginextsolutions.com/product/#/settings/addressfieldConfiguration" target="_top">here</a>

You can create a maximum of 5 Addresses in LogiNext in one call of this API.

#### Request

<span class="post">POST</span>`https://api.loginextsolutions.com/ClientApp/address/v1/create`


#### Request Parameters

Parameter | DataType | Length |  Required | Description
-----------|-------|------- |------- | ----------
customerReferenceId | String | 32 | Mandatory | Unique Customer ID used to identify the Customer the address is being created for.
addressId | String | 255 | Optional | Address ID used to identify the address of that customer. The address ID must be unique within a Customer entity.
addressType | String | 255 | Optional | Address Type epending on the values configured for you in LogiNext. eg - 'HOME', 'OFFICE', 'OTHER'.
addressServiceTime | String | 255 |Optional | Address Service Time in minutes.
breakTime.startTime | String | 255 | Conditional Mandatory | Address Break Start time in HH:MM format. This field is mandatory if a break end time is provided.
breakTime.endTime | String | 40 |Conditional Mandatory | Address Break end time in HH:MM format.. This field is mandatory if a break start time is provided.
preferredStartTime | String | 100 | Optional | If a particular customer location has preferred times within which it should be serviced, you can enter those times here. They will be considered during planning deliveries to that address location. This field accepts values in HH:MM format.
preferredEndTime | String | 255 | Optional | If a particular customer location has preferred times within which it should be serviced, you can enter those times here. They will be considered during planning deliveries to that address location. This field accepts values in HH:MM format.
weeklyOffList | LIST | 255 | Mandatory | Days of the week this location is OFF i.e not serviceable.
address.city | Integer | 20 | Mandatory | Address city.
address.state | Integer | 20 | Optional |  Address state. This will be based on the state codes in LogiNext for the country selected by you.
address.country | String | 255 | Optional | Address Country.
address.pincode | String | 255 | Optional | Address Pincode.
address.latitude | Double | 20 | Optional |  Address geo-coordinate(latitude)
address.longitude | Double | 20 | Optional | Address geo-coordinate(longitude)
additionalContactDetails.name | String | 255 | Conditional Mandatory | Name of the additional contact person being added. This field is required if the additional Contact Details object is being passed. 
additionalContactDetails.mobileNumber | String | 20 | Conditional Mandatory |  Mobile Number of the additional contact person being added. Either mobile number or email is mandatory if name is passed.
additionalContactDetails.emailAddress | String | 255 | Conditional Mandatory | Email ID of the additional contact person being added. Either mobile number or email is mandatory if name is passed.
isPrimary | String | 1 | Optional | Identify if the current address is the end customer's primary address or not. If your end customer has a primary address, Orders can be created for that address passing only the customer ID in the accountCode field of the Create Order API, with no identifier needed for the address.
clientCode | String | 50 | Optional | This is the identifier for an Account. An Account is used to represent LogiNext’s Customer’s Customer. Pass the name of the Account in this field if you wish to create an Address entity on behalf of one of your Customers.
timeZone | String | | Optional | The timzone of the address field. If not passed, it will default the timezone configured for your account for the address being created.

### Update

> Sample Request

```json
[ 
{ "addressReferenceId": "65ba00dbdcf04fb789311df6aa40e3ba",
 "addressType":"Home", 
 "addressServiceTime":"5", 
 "breakTime":[ 
    { 
    "startTime":"10:00", 
    "endTime":"11:30" 
    }, 
    { "startTime":"12:00",
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
     "apartment":"1901 Wes",
          "streetName":"t Madison Street",
          "landmark":"United Center",
          "locality":"Dowtown Chicago",
          "city":"Chicago",
          "state":"IL",
          "country":"USA",
          "pincode":"60612",
          "latitude": 41.8807,
          "longitude": -87.6742
  }, 
  "isPrimary":"Y", 
  "clientCode":"MyKart", 
  "timeZone":"America/Chicago" 
  } 
]
```

> Success Response

```json
 {
    "status": 200,
    "message": "Address(s) updated successfully",
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


> Failure Response

```json
{
    "status": 409,
    "message": "Address(s) updation failed",
    "moreResultsExists": false,
    "error": [
        {
            "index": 0,
            "errorList": [
                {
                    "key": "addressReferenceId",
                    "message": [
                        "No address found for referenceId"
                    ]
                }
            ]
        }
    ],
    "hasError": true
}


```


Update an existing Address for an existing Customer in the LogiNext system with this API. This API identifies an Address using the Address Reference ID field created and returned in the API response when the Address was created in the system.

This API will only accept inputs if your Customer Profiling property is set in LogiNext. To know more about the Customer Profiling property, please reach out to us at support@loginextsolutions.com.

Address field validations will be based on the behaviour defined in the Address Configuration screen of your LogiNext account<a href="https://products.loginextsolutions.com/product/#/settings/addressfieldConfiguration" target="_top">here</a>

You can update one address in LogiNext in one call of this API. This API does not support bulk operations

#### Request

<span class="post">POST</span>`https://api.loginextsolutions.com/ClientApp/address/v1/update`


#### Request Parameters

Parameter | DataType | Length |  Required | Description
-----------|-------|------- |------- | ----------
addressReferenceId | String | 32 | Mandatory | Unique Address Reference ID used to identify the Address to be updated.
addressType | String | 255 | Optional | Address Type epending on the values configured for you in LogiNext. eg - 'HOME', 'OFFICE', 'OTHER'.
addressServiceTime | String | 255 |Optional | Address Service Time in minutes.
breakTime.startTime | String | 255 | Conditional Mandatory | Address Break Start time in HH:MM format. This field is mandatory if a break end time is provided.
breakTime.endTime | String | 40 |Conditional Mandatory | Address Break end time in HH:MM format.. This field is mandatory if a break start time is provided.
preferredStartTime | String | 100 | Optional | If a particular customer location has preferred times within which it should be serviced, you can enter those times here. They will be considered during planning deliveries to that address location. This field accepts values in HH:MM format.
preferredEndTime | String | 255 | Optional | If a particular customer location has preferred times within which it should be serviced, you can enter those times here. They will be considered during planning deliveries to that address location. This field accepts values in HH:MM format.
weeklyOffList | LIST | 255 | Optional | Days of the week this location is OFF i.e not serviceable.
address.city | Integer | 20 | Optional | Address city.
address.state | Integer | 20 | Optional |  Address state. This will be based on the state codes in LogiNext for the country selected by you.
address.country | String | 255 | Optional | Address Country.
address.pincode | String | 255 | Optional | Address Pincode.
address.latitude | Double | 20 | Optional |  Address geo-coordinate(latitude). If the geocoordniates are passed, then the Address will not be geocoded. 
address.longitude | Double | 20 | Optional | Address geo-coordinate(longitude). If the geocoordniates are passed, then the Address will not be geocoded. 
isPrimary | String | 1 | Optional | Identify if the current address is the end customer's primary address or not. If passed as Y, the Address in the request will become the new primary Address and the current primary address configured in the system will no longer be the primary Address. Note that the system requires one active Address to be the primary address. You cannot mark a Customer's primary address as non primary, i.e if you pass the isPrimaryfield as 'N' for the primary Address, you will eceive a validation error.
clientCode | String | 50 | Optional | This is the identifier for an Account. An Account is used to represent LogiNext’s Customer’s Customer. Pass the name of the Account in this field if you wish to create an Address entity on behalf of one of your Customers.
timeZone | String | | Optional | The timzone of the address field. If not passed, it will default the timezone configured for your account for the address being created.



## Delivery Associate

### Create

> Sample Request

```json
[
 {
"employeeId":"ALL123469",
"userGroupName":"MobileUser",
"branchName":"California",
"deliveryMediumMasterName":"James",
"phoneNumber":9892147969,
"imei":123456789012123,
"emailId":"james@ablogistics.com",
"userName":"james003",
"password":"admin",
"capacityInUnits":10,
"capacityInVolume":10,
"capacityInWeight":10,
"dob":"2016-12-12",
"gender":"Male",
"deliveryMediumMasterTypeCd": "Bakery",
"vehicleNumber":"1AB54F",
"isOwnVehicleFl":"Company",
"maxDistance":10,
"dmPreference":"10035",
"maritalStatus":"Single",
"alternateMobileNo":9892134489,
"landlineNo":28215678,
"licenseValidity":"2026-12-12",
"licenseValidityInYears":10,
"licenseIssuanceDate":"2016-12-12",
"licenseNumber":2123123123,
"loadingTimeInMins": 20,
"unloadingTimeInMins": 20,
"fixedCost":10,
"variableCost":10,
"isPresentFl":"Y",
"weeklyOffList": [
  "Thursday",
  "Monday"
],
"deliveryMediumMapList": [
   {
     "name": "SPANISH"

   },
   {
     "name": "ENGLISH"

   }
  ],
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
"addressList": [ 
  { 
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
]
}
]
```

> Success Response

```json
{
  "status": 201,
  "message": "success",
  "moreResultsExists": false,
  "data": [
    "d7b0f3f8e1174742bd6a8ae451866cb1"
  ],
  "hasError": false
}

```

> Failure Response 1

```json
{
    "status": 400,
    "message": "Some issue encountered in server",
    "moreResultsExists": false,
    "error": {
        "deliverymedium_0": [
            {
                "key": "employeeId",
                "message": [
                    "Employee Id is required" 
                ]
            }
        ],
        "deliverymedium_1": [
            {
                "key": "emailId",
                "message": [
                    "Invalid Email" 
                ]
            }
        ]
    },
    "hasError": true
}

```

> Failure Response 2

```json
{
    "status": 400,
    "message": "Some issue encountered in server",
    "moreResultsExists": false,
    "error": [
        {
            "key": "Invalid client branch name(s) found.",
            "message": [
                "PowaiSd" 
            ]
        },
        {
            "key": "Invalid usergroup name(s) found.",
            "message": [
                "Mobil" 
            ]
        },
        {
            "key": "Invalid delivery types(s) found.",
            "message": []
        },
        {
            "key": "Invalid pincodes.",
            "message": [
                "14252" 
            ]
        },
        {
            "key": "Invalid country code(s) found.",
            "message": []
        }
    ],
    "hasError": true
}

```
Create a new Delivery Associate in the LogiNext system with this API. A delivery associate will be created and assigned a unique Reference ID that can be used to identify the Delivery Associate later.

Address field validations will be based on the behaviour defined in the Address Configuration screen of your LogiNext account<a href="https://products.loginextsolutions.com/product/#/settings/addressfieldConfiguration" target="_top">here</a>

API Type: Tier 1 API

#### Request

<span class="post">POST</span>`https://api.loginextsolutions.com/DeliveryMediumApp/mile/v1/create`


#### Request Parameters

Parameter | DataType | Length |  Required | Description
-----------|-------|------- |------- | ----------
employeeId | String | 50 | Mandatory | Delivery Associate employee ID.
userGroupName | String | 255 | Mandatory | Delivery Associate user group name.
branchName | String | 255 | Mandatory | Delivery Associate client branch name.
deliveryMediumMasterName | String | 255 | Mandatory | Delivery Associate full name.
phoneNumber | String | 255 | Mandatory | Delivery associate mobile number.
imei | String | 40 | Optional | TDelivery Associate IMEI number.
emailId | String | 100 | Optional | Delivery Associate email ID.
userName | String | 255 | Mandatory | Delivery Associate username.
password | String | 255 | Mandatory | Delivery Associate password.
capacityInUnits | Integer | 20 | Mandatory | Delivery Associate capacity in units.
capacityInVolume | Integer | 20 | Optional | Delivery Associate capacity in volume.
capacityInWeight | Integer | 20 |Optional | Delivery Associate capacity in weight.
dob | String |  | Optional | Delivery Associate date of birth.
gender | ISODate | 12 |Optional | Delivery Associate Gender. Ex - Male,Female.
deliveryMediumMasterTypeCd | String | 255 |Optional | Delivery Associate type. For example, 'Bakery' if the Delivery Associate can fulfill Bakery type of Orders 'Groceries' if the Delivery Associate can fulfill Groceries' type of Orders. This will be mapped to the 'deliveryType' field at the Order level.
vehicleNumber | String | 255 | Optional | delivery associate Vehicle number.
isOwnVehicleFl | String | 1 |Optional | Owner of vehicle. Ex - Owned, Company
maxDistance | Integer | 20 |Optional | This is the maximum distance the Delivery Associate is allowed to cover within a trip. This value is considered when creating a route plan for the Delivery Associate.
dmPreference  | String | 255 | Optional | Delivery Associate Preferred Pincode. The Route Planning engine will consider this piccode preference when assignming Orders to the Delivery Associate if the Pin Code Preference' property is set.
maritalStatus | String | Optional | 255 | Delivery Associate Marital Status.
alternateMobileNo | String | Optional | 255 | Delivery Associate alternate Mobile NUmber.
landlineNo | String | Optional | 255 | Delivery Associate landline Number.
licenseValidity | String | Optional | 255 | This is the expiry Date of the Driver's License in YYYY-MM-HH format.
licenseValidityInYears | Optional | String | 255 | Delivery Associate license Validity in years.
licenseIssuanceDate |String | Optional | 255 | Delivery Associate license issuance Date in YYYY-MM-HH format.
loadingTimeInMins | Number | Optional | 32 | Average time taken to load Orders into the Vehicle at the Pickup location. This can be different for different types of Fleet. A larger Vehicle may require more time to load, whereas a small Vehicle may require only a few minutes.
unloadingTimeInMins | Number | Optional | 32 | Average time taken to load Orders into the Vehicle at the Delivery location. This can be different for different types of Fleet. A larger Vehicle may require more time to load, whereas a small Vehicle may require only a few minutes.
fixedCost | Number | Optional | Fixed cost associated with using a delivery medium in Route Optimization.
variableCost | Number | Optional | Variable cost associated with each unit of distance travelled by the Delivery Associate during a trip. This is considered in Route Optimization
weeklyOffList  | String | 255 |Optional | Delivery Associate days off. Ex - Monday, Tuesday etc.
deliveryMediumMapList.name | String | 255 | Optional | Delivery Associate language list.
shiftTimeList.shiftStartTime  | String|  |Optional | Delivery Associate Shift start time in HH:MM format. 
shiftTimeList.shiftEndTime  | String |  |Optional | Delivery Associate Shift end time in HH:MM format.
breakTimeList | List | | Optional | This is the break time of the Delivery Associate. The LogiNext Route Planning engine will not assign orders with Service time windows within a Delivery Associate's break time to that Delivery Associate. 
breakTimeList.breakStartTime  | String |  | Optional | Delivery Associate Break start time in HH:MM format.
breakTimeList.breakEndTime  | String |  | Optional | Delivery Associate Break end time in HH:MM format.
breakTimeList.breakDurationInMins  | Integer | | Optional | Delivery Associate Break Time Duration in minutes
addressList | List | | | Delivery Associate address details.
addressList.apartment | String | Optional | 255 | Delivery Associate Apartment number.
addressList.streetName | String | Optional | 255 | Delivery Associate Street Name.
addressList.landmark | String | Optional | 255 | Delivery Associate landmark.
addressList.countryShortCode | String | Optional | 255 | This is the  Delivery Associate country code. Please refer to the list of country codes provided in the "Country Codes" section.
addressList.city | String | Optional | 255 | Delivery Associate city.
addressList.pincode | String | Optional | 255 | Delivery Associate postal code.
addressList.addressType | String | Optional | 255 | Identifies if this is the current or permanent address of the Delivery Associate. If set to "CURRENT", it will select the entered address as current. If "PERMANENT", it will set the entered address as permanent. This field does not accept any other value. You must send this field if adding an address for the Delivery Associate.


### Get 


> Sample Request

```json

["d7f173453bab40cf83dc79bb86ea2edb"]
```

Retrieve a List of all the Delivery Associates using this API. Pass the LogiNext Reference IDs or Username for the Delivery Associates you want to search for in the Request Body. 

The API returns a link of the profile picture of the Delivery Associate, if one was uploaded in LogiNext, in the 'profilePicture' field.This can be used in the case where the Delivery Associate's image may need to be displayed on your mobile application screen to show Customers who is fulfilling their Order.
Note that in case you are storing this link in your system, this link has a life time of 1 hour post which it will expire, and will need to be fetched again.

API Type: Tier 1 API

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
                "imei": "873345632458765",
                "statusCd": "Available",
                "employeeId": "NBVA114",
                "weeklyOff": ["Monday"],
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
                "deliveryMediumName": "Robin Jones",
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

 {
"employeeId":"ALL123469",
"userGroupName":"MobileUser",
"branchName":"California",
"deliveryMediumMasterName":"James",
"phoneNumber":9892147969,
"imei":123456789012123,
"emailId":"james@ablogistics.com",
"userName":"james003",
"password":"admin",
"capacityInUnits":10,
"capacityInVolume":10,
"capacityInWeight":10,
"dob":"2016-12-12",
"gender":"Male",
"deliveryMediumMasterTypeCd": "Bakery",
"vehicleNumber":"1AB54F",
"isOwnVehicleFl":"Company",
"maxDistance":10,
"dmPreference":"10035",
"maritalStatus":"Single",
"alternateMobileNo":9892134489,
"landlineNo":28215678,
"licenseValidity":"2026-12-12",
"licenseValidityInYears":10,
"licenseIssuanceDate":"2016-12-12",
"licenseNumber":2123123123
"loadingTimeInMins": 20,
"unloadingTimeInMins": 20,
"fixedCost":10,
"variableCost":10,
"isPresentFl":"Y",
"weeklyOffList": [
  "Thursday",
  "Monday"
],
"deliveryMediumMapList": [
   {
     "name": "SPANISH"

   },
   {
     "name": "ENGLISH"

   }
  ],
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
"addressList": [ 
  { 
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
]
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

API Type: Tier 1 API

#### Request

<span class="post">POST</span>`https://api.loginextsolutions.com/DeliveryMediumApp/mile/v1/update`


#### Request Parameters

Parameter | DataType | Length |  Required | Description
-----------|-------|------- |------- | ----------
employeeId | String | 50 | Mandatory | Delivery Associate employee ID.
userGroupName | String | 255 | Optional | Delivery Associate user group name.
branchName | String | 255 | Optional | Delivery Associate client branch name.
deliveryMediumMasterName | String | 255 | Optional | Delivery Associate full name.
phoneNumber | String | 255 | Optional | Delivery associate mobile number.
imei | String | 40 | Optional | Delivery Associate IMEI number.
emailId | String | 100 | Optional | Delivery Associate email ID.
userName | String | 255 | Optional | Delivery Associate username.
password | String | 255 | Optional | Delivery Associate password.
capacityInUnits | Integer | 20 | Optional | Delivery Associate capacity in units.
capacityInVolume | Integer | 20 | Optional | Delivery Associate capacity in volume.
capacityInWeight | Integer | 20 |Optional | Delivery Associate capacity in weight.
dob | String |  | Optional | Delivery Associate date of birth.
gender | ISODate | 12 |Optional | Delivery Associate Gender. Ex - Male,Female.
deliveryMediumMasterTypeCd | String | 255 |Optional | Delivery Associate type. For example, 'Bakery' if the Delivery Associate can fulfill Bakery type of Orders 'Groceries' if the Delivery Associate can fulfill Groceries' type of Orders. This will be mapped to the 'deliveryType' field at the Order level.
vehicleNumber | String | 255 | Optional | delivery associate Vehicle number.
isOwnVehicleFl | String | 1 |Optional | Owner of vehicle. Ex - Owned, Company
maxDistance | Integer | 20 |Optional | This is the maximum distance the Delivery Associate is allowed to cover within a trip. This value is considered when creating a route plan for the Delivery Associate.
dmPreference  | String | 255 | Optional | Delivery Associate Preferred Pincode. The Route Planning engine will consider this piccode preference when assignming Orders to the Delivery Associate if the Pin Code Preference' property is set.
maritalStatus | String | Optional | 255 | Delivery Associate Marital Status.
alternateMobileNo | String | Optional | 255 | Delivery Associate alternate Mobile NUmber.
landlineNo | String | Optional | 255 | Delivery Associate landline Number.
licenseValidity | String | Optional | 255 | This is the expiry Date of the Driver's License in YYYY-MM-HH format.
licenseValidityInYears | Optional | String | 255 | Delivery Associate license Validity in years.
licenseIssuanceDate |String | Optional | 255 | Delivery Associate license issuance Date in YYYY-MM-HH format.
loadingTimeInMins | Number | Optional | 32 | Average time taken to load Orders into the Vehicle at the Pickup location. This can be different for different types of Fleet. A larger Vehicle may require more time to load, whereas a small Vehicle may require only a few minutes.
unloadingTimeInMins | Number | Optional | 32 | Average time taken to load Orders into the Vehicle at the Delivery location. This can be different for different types of Fleet. A larger Vehicle may require more time to load, whereas a small Vehicle may require only a few minutes.
fixedCost | Number | Optional | Fixed cost associated with using a delivery medium in Route Optimization.
variableCost | Number | Optional | Variable cost associated with each unit of distance travelled by the Delivery Associate during a trip. This is considered in Route Optimization
weeklyOffList  | String | 255 |Optional | Delivery Associate days off. Ex - Monday, Tuesday etc.
deliveryMediumMapList.name | String | 255 | Optional | Delivery Associate language list.
shiftTimeList.shiftStartTime  | String|  |Optional | Delivery Associate Shift start time in HH:MM format. 
shiftTimeList.shiftEndTime  | String |  |Optional | Delivery Associate Shift end time in HH:MM format.
breakTimeList | List | | Optional | This is the break time of the Delivery Associate. The LogiNext Route Planning engine will not assign orders with Service time windows within a Delivery Associate's break time to that Delivery Associate. 
breakTimeList.breakStartTime  | String |  | Optional | Delivery Associate Break start time in HH:MM format.
breakTimeList.breakEndTime  | String |  | Optional | Delivery Associate Break end time in HH:MM format.
breakTimeList.breakDurationInMins  | Integer | | Optional | Delivery Associate Break Time Duration in minutes
addressList | List | | | Delivery Associate address details.
addressList.apartment | String | Optional | 255 | Delivery Associate Apartment number.
addressList.streetName | String | Optional | 255 | Delivery Associate Street Name.
addressList.landmark | String | Optional | 255 | Delivery Associate landmark.
addressList.countryShortCode | String | Optional | 255 | This is the  Delivery Associate country code. Please refer to the list of country codes provided in the "Country Codes" section.
addressList.city | String | Optional | 255 | Delivery Associate city.
addressList.pincode | String | Optional | 255 | Delivery Associate postal code.
addressList.addressType | String | Optional | 255 | Identifies if this is the current or permanent address of the Delivery Associate. If set to "CURRENT", it will select the entered address as current. If "PERMANENT", it will set the entered address as permanent. This field does not accept any other value. You must send this field if adding an address for the Delivery Associate.



### Update Status

> Sample Request

```json
{
  "newStatus":"ACTIVE",
  "deliveryMediumDetails":
  [
    {
            "referenceId":"fa7716b25fe5432a96d1a709a28bd6d8",
            "reasonCd":"DBUNAVAILABLE",
            "latitude":40.760838,
            "longitude":74.6758
    },
    {
            "referenceId" : "bae83999422211e6860c0653055f4dfd",
            "reasonCd":"DBUNAVAILABLE",
            "latitude":40.760838,
            "longitude":74.67589
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

If you are marking a Delivery Associate's status as OFFBREAK with this API, the ETAs for all the subsequent Not Delivered Orders will be revised. This ETA revision logic will work as follows -

If the Delivery Associate's geocoordinates(latitude and longitude) are sent in the API request, ETAs will be revised considering these geocoordinates.
If the Delivery Associate's geocoordinates are not sent in the request, but a tracking location for the Delivery Associate was received in the last 5 minutes, then that tracking location will be used to revise ETAs.
If no tracking location was received for the Delviery Associate in the last 5 minutes, then the ETAs will not be revised for the Orders.

API Type: Tier 1 API

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
"deliveryMediumAutoAllocateFl": "Y",
"autoAllocateFl": "Y"
"geoFenceRadius":"2.0",
"branchDescription":"desc",
"billingContactName":"name",
"officeNumber":"2798678712",
"adminContactName":"John K.",
"mobileNumber":"9033977123",
"emailAddress":"superjames@gmails.com",
"longitude": 40.760838,
"latitude": 74.9095327,
"timeZone":"America/Chicago",
"loadingTime": 20,
"unloadingTime": 20
}]

```

> Response

```json
{
    "status": 200,
    "message": "Create Hub success.",
    "data": {
        "referenceId": "fa7716b25fe5432a96d1a709a28bd6d8"
    },
    "hasError": false
}
```

Create hubs / branches / distribution centers in the LogiNext system with the Create Hub API. Hubs will be created and will be assigned a unique Reference ID that can be used to look up the hub later.

API Type: Tier 1 API

#### Request

<span class="post">POST</span>`https://api.loginextsolutions.com/ClientApp/v1/branch/create`


#### Request Body

Parameter | DataType | Length |  Required | Description
-----------|-------| ------- |------- | ----------
clientParentBranchName | String | 255 | Mandatory | This is name of the Parent Hub under which you want to create the new branch.<br>Please note that you cannot create the Main Parent branch for your account through this API.<br>The Main Parent Branch gets created automatically when your account is configured in LogiNext system.<br>If you want to know the name of the Main Parent Branch Name, please get in touch with your assigned Account Manager
branchName | String | 255 | Mandatory | Hub Name.
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
autoAllocateFl  | String | 1 | Optional | If 'Y' this branch will be considered for Auto Assignment of Orders when the AutoAllocateFl is passed as 'Y' in the Create Order API. If 'N' then Orders will not be auto assigned to this branch even if the Order is created in the system with AutoAllocateFl 'Y'. This can be used when you do not want to consider a certain branch and its drivers for auto assignment of Orders if there are higher cost implications of using resources of the branch in Order fulfillment. You can still manually assign Orders to the branch and the Drivers of the branch. If not passed, this will default to 'Y'.
deliveryMediumAutoAllocateFl  | String | 1 | Optional | If 'Y', Drivers of this branch will be considered in Auto Assignment of Orders if you have configured the Resource Pooling property in the Auto Assignment profile. YOu can pass this as 'N' if you do not want Drivers of certain branches to be considered for auto assignment of Orders. Order can still be manually assigned to these Drivers. If not passed, this will default to 'Y'.
branchDescription | String | 500 | Optional | If you would like add a brief description name for the hub, use this field.
billingContactName | String | 500 | Mandatory | Name of the Contact Person at this Branch / Hub
officeNumber | String | 255 | Mandatory | Fixed Line Number of the Branch  / Hub
adminContactName | String | 255 | Mandatory | Name of the Supervisor / Alternate Contact for this Hub
mobileNumber | String | 255 | Mandatory | Mobile Phone No. of the contact person
emailAddress | String | 255 | Mandatory | Email Address of the contact person
timeZone | String | | Optional | The timezone of the Hub location you are creating. This will default yo your account configured timezone if not passed.
loadingTime | Number | Optional | 32 | Total time taken in minutes to load Orders into the Vehicle at the Branch. This can be used to consider the time spent in processes like security at the branch to load vehicles.
unloadingTime | Number | Optional | 32 | Total time taken in minutes to unload Orders from the Vehicle at the Branch. This can be used to consider the time spent in processes like security at the branch to unload vehicles.


### Update

> Definition

```json
https://api.loginextsolutions.com/ClientApp/v1/branch/update
```

> Request Body

```json

[{
  "referenceId":"fa7716b25fe5432a96d1a709a28bd6d8",
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
  "longitude": 40.760838,
  "latitude": 74.9095327,
  "timeZone":"America/Chicago",
  "loadingTime": 20,
  "unloadingTime": 20
}]

```

> Response

```json
{
    "status": 200,
    "message": "Create Hub success.",
    "data": {
        "referenceId": "fa7716b25fe5432a96d1a709a28bd6d8"
    },
    "hasError": false
}
```

Update hubs / branches / distribution centers in the LogiNext system with the Update Hub API. 

API Type: Tier 1 API

#### Request

<span class="post">POST</span>`https://api.loginextsolutions.com/ClientApp/v1/branch/update`


#### Request Body

Parameter | DataType | Length |  Required | Description
-----------|-------| ------- |------- | ----------
referenceId | String | 255 | Mandatory | Hub Reference ID
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
loadingTime | Number | Optional | 32 | Total time taken in minutes to load Orders into the Vehicle at the Branch. This can be used to consider the time spent in processes like security at the branch to load vehicles.
unloadingTime | Number | Optional | 32 | Total time taken in minutes to unload Orders from the Vehicle at the Branch. This can be used to consider the time spent in processes like security at the branch to unload vehicles.
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
                    "field": "cf_deliveryDay",
                    "value": "1533081600000",
                    "type": "date"
                },
                {
                    "field": "cf_deliveryTime",
                    "value": "10:00",
                    "type": "time"
                },
                {
                    "field": "cf_cutOffDay",
                    "value": "1533168000000",
                    "type": "date"
                },
                {
                    "field": "cf_cutOffTime",
                    "value": "11:00",
                    "type": "time"
                }
            ],
            "geofenceName": "MMD-Patapsco High/Dundalk",
            "referenceId::"fa7716b25fe5432a96d1a709a28bd6d8",
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

API Type: Tier 1 API

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

## Order Request

Create Order Requests in the LogiNext system using the Order Request API. Order Requests will be assigned a referenceId that will be returned in the API response. This refernceId can be used to identify the Order Request later.

To view the Order Requests created in the LogiNext Web Application, select the correct date range in the date filter on the screen.

When Customer Profiling is turned ON -

1. You can only enter the corresponding accountCode field that will hold the customer ID. If passed, ad the accountCode exists in the LogiNext system, LogiNext will use the customer information associated with that accountCode in the Order creation. It will overlook other customer information like Name, Email and Phone Number.

2. In Order to select a particular address for that customer, you can pass the address ID associated with that address for that customer. If passed, and the address ID exists in LogiNext for a previously created address, the address information associated with that address ID will be used.


### Create Pick Up Only

> Definition

```json
https://api.loginextsolutions.com/BookingApp/mile/v1/create
```

> Request Body

```json
[
   {
"shipmentRequestNo":"SH12432",
"awbNumber": "435-16685675",
"shipmentRequestDispatchDate": "2020-05-19T10:30:00.000Z",
"shipmentRequestType":"PICKUP",
"packageWeight":"10",
"packageVolume":"10",
"packageValue":"10",
"packageLength":"10",
"packageBreadth":"10",
"packageHeight":"10",
"priority":"Priority 1",
"paymentType":"COD",
"numberOfItems":3,
"deliveryType":"Groceries",
"serviceType":"Express",
"distributionCenter":"mea_allmile_sandbox Main Branch",
"pickupBranch":"mea_allmile_sandbox Main Branch",
"pickupServiceTime": "50",
"pickupStartTimeWindow": "2020-05-19T14:24:00.000Z",
"pickupEndTimeWindow": "2020-05-19T14:24:00.000Z",
"pickupEmail":"james.w@ablogs.com",
"pickupPhoneNumber": "5163063377",
"pickupAccountCode": "jim001",
"pickupAddressId": "Home",
"pickupAddressType":"Home",
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
"pickupNotes":"notes for pickup",
"clientCode":"ShipGenie",
"shipmentCrateMappings": [
     {
         "crateCd": "CR041",
         "crateAmount": 100.65,
         "crateType": "case",
         "noOfUnits": 2,
         "crateWeight": 10,
         "crateVolume": 11,
         "crateLength": 12,
         "crateBreadth": 13,
         "crateHeight": 14,
         "shipmentlineitems": [
             {
                 "itemCd": "IT043",
                 "itemName": "Chicken Soup 2X200gm",
                 "itemPrice": 500,
                 "itemQuantity": 1,
                 "itemType": "soup",
                 "itemWeight": 10,
                 "itemVolume": 11,
                 "itemLength": 12,
                 "itemBreadth": 13,
                 "itemHeight": 14
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
    "message": "Shipment Request(s) created successfully",
    "moreResultsExists": false,
    "data": [
        {
            "index": 0,
            "shipmentRequestReferenceId": "2c0dcb93ca494cfc92d5b830c1c8033a",
            "shipmentRequestNo": "SH12432",
            "shipmentRequestType": "PICKUP"
        }
    ],
    "hasError": false
}

```


> Failure Response

```json
{
    "status": 409,
    "message": "Shipment Request Creation Failed",
    "moreResultsExists": false,
    "error": [
        {
            "index": 0,
            "shipmentRequestNo": "SH12432",
            "shipmentRequestType": "PICKUP",
            "errorList": [
                {
                    "key": "pickupAccountCode",
                    "message": [
                        "Address not serviceable"
                    ]
                },
                {
                    "key": "deliveryType",
                    "message": [
                        "DeliveryType is invalid"
                    ]
                }
            ]
        }
    ],
    "hasError": true
}

```

Create pickup Order requests with this API in the LogiNext system. Order requests will be created and assigned a reference ID that can be used at a leter time to identify the order request.

API Type: Tier 1 API

#### Request

<span class="post">POST</span>`https://api.loginextsolutions.com/BookingApp/mile/v1/create`



#### Request Parameters

Param | DataType | Length |  Required | Description
--------- | ------- | ------- | ---------- | ------------
shipmentRequestNo | String | 100 | Optional | Order request Number. If not passed, the system will auto generate an Order request number
awbNumber | String | 1000 | Optional | Airway Bill Number associated with an Order request.
shipmentRequestDispatchDate | | | Optional | The requested Dispatch date for the Order request. The requested dispatch date is the date from which the system looks to start serviceing the order request, either through the service types, or zonal capacities configured. If not passed, the system considers the current date.
shipmentRequestType | String | 40 | Mandatory | The value in this field has to be "PICKUP" always.
distributionCenter | String | 255 | Mandatory | Distribution center name. The Distribution center is the Hub that is responsibile for fulfilling the Order. An Order can have different Pickup and Delivery leg branches, but will require a single Distribution center that is responsible for the fulfillment of the Order.
packageWeight | Double | 10,3 | Optional | Order request weight. The unit of measurement will be based on the unit of measurement selected for your account. For metric system this will be in Kg, and for Imperial system, this will be in pounds.
packageVolume | Double | 10,3 | Optional | Order request  volume. The unit of measurement will be based on the unit of measurement selected for your account. For metric system this will be in cubic centimeters(CC), and for Imperial system, this will be in cubic inches(CBI).
packageLength | Double | 10,3 | Optional | Order request length. The unit of measurement will be based on the unit of measurement selected for your account. For metric system this will be in centimeters(CM), and for Imperial system, this will be in inches.
packageBreadth| Double | 10,3 | Optional | Order request width.  The unit of measurement will be based on the unit of measurement selected for your account. For metric system this will be in centimeters(CM), and for Imperial system, this will be in inches.
packageHeight| Double | 10,3 | Optional | Order request hieght.  The unit of measurement will be based on the unit of measurement selected for your account. For metric system this will be in centimeters(CM), and for Imperial system, this will be in inches.
priority | String | 16 | Optional | Order priority. If you wish to segregate Orders based on certain Order priorities, say you want to Route Plan for Orders based on their priorities, you can set up this field in the settings module and define the values that LogiNext should accept of this field. For example, this could be 'PRIORITY1', 'PRIORITY2', or 'PRIORITY3'.
serviceType | String | 16 | Optional | Order request Service Type.
packageValue | Double | 10 | Optional | Order request value.
paymentType | String | 40 | Optional | Payment mode. Ex: COD - Cash On Delivery, Prepaid. If not passed, this will be defaulted to COD.
numberOfItems | Integer | 20 | Optional | Number of items in the order.
deliveryType | String | 40 | Optional | In certain operations, there are different skill sets / special delivery requirements through which the Delivery has to take place.<br>For e.g. - Groceries / Food items has to be separated with Toiletries<br>Orders for Cake cannot be clubbed with the Order for Flowers while delivering.<br>In such cases, if you want to classify the orders by using Delivery Type such that these orders get assigned to Pickup Associates who are configured in LogiNext system with these special skill-sets or types, then you can use this field.<br>Please note that before you pass orders with certain Delivery Types, you will have to first configure the Delivery Types.<br>Please ask your Account Manager to set these values for you. Note that you can pass multiple Delivery Types in a comma separated manner in this API.
deliveryLocationType | String | 255 | Optional | This parameter if passed helps the Operation Managers / Pickup Associates to know if the Pick location is Residence or Office or Pick-up point, etc.<br>
deliveryMediumUsername | STRING | | Optional |  If you know the Delivery Associate who will be fulfilling the Order, pass their usernam in this field.
pickupBranch | String | 255 | Optional | For Pick-Up type of order requests, this is the Branch / Distribution Center / Hub to which the Delivery Associate will Deliver the Order request to. It is recommended to not pass this field so the system can use the branch linked to the zone of the pickup location. You can pass this field if the Shipper the Order request is being created for is not linked with a Service area Profile on the LogiNext system.
pickupServiceTime | Integer | 11 | Optional | This is the time that the Pickup Associate is going to take at the Pickup location to pickup the order. 

distributionCenter | String |  | Mandatory | Distribution center's name. The Distribution center is the Hub that is responsibile for fulfilling the Order. An Order can have different Pickup and Delivery leg branches, but will require a single Distribution center that is responsible for the fulfillment of the Order.
pickupStartTimeWindow | Date |  | Mandatory | This is the start date and time for the time slot of the Pickup. It is recommended to not pass this field so the system can calculate the Order Time Windows based on the Service type or capacity configuration setup in your account. If this field is passed, and no Service area profile exists for the Shipper, the Time Window calculations will be skipped and the passed Time Windows will be used at Order level.<br>Note that this date and time has to be greater than the Order Creation Date and Time.<br>Note that this date and time has to be in UTC.<br>For example - "2017-07-15T11:30:00.000Z

pickupEndTimeWindow | Date |  | Mandatory | This is the end date and time for the time slot of the Pickup. It is recommended to not pass this field so the system can calculate the Order Time Windows based on the Service type or capacity configuration setup in your account. If this field is passed,  and no Service area profile exists for the Shipper, the Time Window calculations will be skipped and the passed Time Windows will be used at Order level.<br>Note that this date and time has to be greater than the Pickup Start Date and Time.<br>Note that this date and time has to be in UTC.<br>For example - "2017-07-15T12:30:00.000Z"
pickupAccountCode | String | 255 | Mandatory | Pick-up Customer ID.
pickupAccountName | String | 255 | Conditional Mandatory | Pick-up Customer name. This field in Non Mandatory in case Customer Profiling in ON.
pickupAddressId | String | 255 | Optional | Pick-up Customer Address ID.
pickupEmail | String | 100 | Optional | Pick-up Customer email ID.
pickupPhoneNumber | String | 255 | Optional | Pick-up Customer phone number. This field in Non Mandatory in case Customer Profiling in ON.
pickupApartment | String | 512 | Conditional Mandatory | This is the apartment details of the pickup customer. This field in Non Mandatory in case Customer Profiling in ON.
pickupStreetName | String | 512 | Mandatory | This is the street name of the pickup customer. Standard Address validations that were set while setting up your account in LogiNext will apply for this field. This field in Non Mandatory in case Customer Profiling in ON.
pickupLandmark | String | 512 | Conditional Mandatory | Pick-up Address landmark. This field in Non Mandatory in case Customer Profiling in ON.
pickupLocality | String | 512 | Conditional Mandatory | Pick-up Address locality. This field in Non Mandatory in case Customer Profiling in ON.
pickupCity | String | 512 | Conditional Mandatory | Pick-up Address city. This field in Non Mandatory in case Customer Profiling in ON.
pickupState| String | 512 | Conditional Mandatory | Pick-up Address State. This field in Non Mandatory in case Customer Profiling in ON. Please refer to the list of state codes provided in the "State Codes" section. This field in Non Mandatory in case Customer Profiling in ON.
pickupCountry | String | 512 | Conditional Mandatory | Pick-up Address Country. This field in Non Mandatory in case Customer Profiling in ON. Please refer to the list of country codes provided in the "Country Codes" section.
pickupPinCode | String | 20 | Conditional Mandatory | Pick-up Address postal code. This field in Non Mandatory in case Customer Profiling in ON.
pickupLatitude | Double |  | Optional | This is the geolocation coordinate (latitude) of the pickup customer.
pickupLongitude | Double |  | Optional | The geolocation coordinate (longitude) of the pickup customer.
pickupAddressTimezone | String | | Optional | The timezone of the pickup location. Refer to the timezone codes list to get the full list of values you can pass here. If not passed, the timezone associated with the pickup location will be the branch timezone.
pickupNotes | String | 512 | Optional | Additional Pick-up notes associated with the order. For example, This can have details regarding whether the Order is fragile.
deliverNotes | String | 512 | Optional | Additional Delivery notes associated with the order.
clientCode | String | 32 | Optional | This is the identifier for an Account. Account is used to represent LogiNext’s Customer’s Customer. Pass the name of the Account in this field if you wish to create Orders on behalf of one of your Customers.

#### Request Parameters (Crates)

Param | DataType | Length |  Required | Description
--------- | ------- | ------- | ---------- | ------------
shipmentCrateMappings | Array of objects |  | Optional | Shipment crates
shipmentCrateMappings.crateCd | String | 128 | Mandatory | Crate code.
shipmentCrateMappings.crateAmount | Double |  | Optional | Crate amount
shipmentCrateMappings.crateType | String | 100 | Optional | Type of crate. Ex: cake, juice, sweet, furniture etc.
shipmentCrateMappings.noOfUnits | Integer | 10 | Optional | No. of crate units
shipmentCrateMappings.crateVolume | Double | 10,3 | Optional | This is the volume of crate. The unit of measurement will be based on the unit of measurement selected for your account. For metric system this will be in CC, and for Imperial system, this will be in cubic inches.
shipmentCrateMappings.crateWeight | Double | 10,3 | Optional | This is the weight of crate. The unit of measurement will be based on the unit of measurement selected for your account. For metric system this will be in Kg, and for Imperial system, this will be in pounds.
shipmentCrateMappings.crateLength | Double | 10,3 | Optional | This is the length of package. The unit of measurement will be based on the unit of measurement selected for your account. For metric system this will be in centimeters(CM), and for Imperial system, this will be in inches.
shipmentCrateMappings.crateBreadth| Double | 10,3 | Optional | This is the width of package.  The unit of measurement will be based on the unit of measurement selected for your account. For metric system this will be in centimeters(CM), and for Imperial system, this will be in inches.
shipmentCrateMappings.crateHeight| Double | 10,3 | Optional | This is the height of package.  The unit of measurement will be based on the unit of measurement selected for your account. For metric system this will be in centimeters(CM), and for Imperial system, this will be in inches.
shipmentCrateMappings.shipmentlineitems.itemCd | String | 200 | Mandatory | Item code
shipmentCrateMappings.shipmentlineitems.itemName | String | 255 | Optional | Item name
shipmentCrateMappings.shipmentlineitems.itemPrice | Double |  | Mandatory | Item price
shipmentCrateMappings.shipmentlineitems.itemQuantity | Double | 10 | Mandatory | Item quantity
shipmentCrateMappings.shipmentlineitems.itemType | String | 100 | Optional | Item type
shipmentCrateMappings.shipmentlineitems.itemWeight | Double | 10 | Optional | Item weight
shipmentCrateMappings.shipmentlineitems.itemLength | Double | 10,3 | Optional | This is the length of item. The unit of measurement will be based on the unit of measurement selected for your account. For metric system this will be in centimeters(CM), and for Imperial system, this will be in inches.
shipmentCrateMappings.shipmentlineitems.itemBreadth| Double | 10,3 | Optional | This is the width of item.  The unit of measurement will be based on the unit of measurement selected for your account. For metric system this will be in centimeters(CM), and for Imperial system, this will be in inches.
shipmentCrateMappings.shipmentlineitems.itemHeight| Double | 10,3 | Optional | This is the height of item.  The unit of measurement will be based on the unit of measurement selected for your account. For metric system this will be in centimeters(CM), and for Imperial system, this will be in inches.


### Create Deliver Only

> Definition

```json
https://api.loginextsolutions.com/BookingApp/mile/v1/create
```

> Request Body

```json
[
   {
"shipmentRequestNo":"SH12432",
"awbNumber": "435-16685675",
"shipmentRequestDispatchDate": "2020-05-19T10:30:00.000Z",
"shipmentRequestType":"PICKUP",
"packageWeight":"10",
"packageVolume":"10",
"packageValue":"10",
"packageLength":"10",
"packageBreadth":"10",
"packageHeight":"10",
"priority":"Priority 1",
"paymentType":"COD",
"numberOfItems":3,
"deliveryType":"Groceries",
"serviceType":"Express",
"distributionCenter":""New York Main Branch",
"deliverBranch":"New York Main Branch",
deliverServiceTime:"10",
deliverStartTimeWindow: "2020-04-10T10:31:00.000Z",
deliverEndTimeWindow: "2020-04-10T10:31:00.000Z",
deliverAccountCode: "Matt001",
deliverAccountName:"Jane Doe",
deliverEmail:"m.richardson@testmail.com",
deliverPhoneNumber:"9891234567",
deliverAddressId: "home",
deliverAddressType:"Home",
deliverApartment: "201",
deliverStreetName: "E Randolph St",
deliverLandmark: "Opp. Chiptole",
deliverLocality: "Down Towm Chicago",
deliverCity: "Chicago",
deliverState: "IL",
deliverCountry: "USA",
deliverPinCode: "60602",
deliverLatitude:41.882702,
deliverLongitude:-87.619392,
deliverAddressTimezone:"America/Chicago",
deliverNotes:"notes for delivery",
"shipmentCrateMappings": [
     {
         "crateCd": "CR041",
         "crateAmount": 100.65,
         "crateType": "case",
         "noOfUnits": 2,
         "crateWeight": 10,
         "crateVolume": 11,
         "crateLength": 12,
         "crateBreadth": 13,
         "crateHeight": 14,
         "shipmentlineitems": [
             {
                 "itemCd": "IT043",
                 "itemName": "Chicken Soup 2X200gm",
                 "itemPrice": 500,
                 "itemQuantity": 1,
                 "itemType": "soup",
                 "itemWeight": 10,
                 "itemVolume": 11,
                 "itemLength": 12,
                 "itemBreadth": 13,
                 "itemHeight": 14
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
    "message": "Shipment Request(s) created successfully",
    "moreResultsExists": false,
    "data": [
        {
            "index": 0,
            "shipmentRequestReferenceId": "2c0dcb93ca494cfc92d5b830c1c8033a",
            "shipmentRequestNo": "SH12432",
            "shipmentRequestType": "PICKUP"
        }
    ],
    "hasError": false
}

```


> Failure Response

```json
{
    "status": 409,
    "message": "Shipment Request Creation Failed",
    "moreResultsExists": false,
    "error": [
        {
            "index": 0,
            "shipmentRequestNo": "SH12432",
            "shipmentRequestType": "DELIVER",
            "errorList": [
                {
                    "key": "deliverAccountCode",
                    "message": [
                        "Address not serviceable"
                    ]
                },
                {
                    "key": "deliveryType",
                    "message": [
                        "DeliveryType is invalid"
                    ]
                }
            ]
        }
    ],
    "hasError": true
}

```

Create deliver Order requests with this API in the LogiNext system. Order requests will be created and assigned a reference ID that can be used at a leter time to identify the order request.

API Type: Tier 1 API

#### Request

<span class="post">POST</span>`https://api.loginextsolutions.com/BookingApp/mile/v1/create`



#### Request Parameters

Param | DataType | Length |  Required | Description
--------- | ------- | ------- | ---------- | ------------
shipmentRequestNo | String | 100 | Optional | Order request Number. If not passed, the system will auto generate an Order request number
awbNumber | String | 1000 | Optional | Airway Bill Number associated with an Order request.
shipmentRequestDispatchDate | | | Optional | The requested Dispatch date for the Order request. The requested dispatch date is the date from which the system looks to start serviceing the order request, either through the service types, or zonal capacities configured. If not passed, the system considers the current date.
shipmentRequestType | String | 40 | Mandatory | The value in this field has to be "PICKUP" always.
distributionCenter | String | 255 | Mandatory | Distribution center name. The Distribution center is the Hub that is responsibile for fulfilling the Order. An Order can have different Pickup and Delivery leg branches, but will require a single Distribution center that is responsible for the fulfillment of the Order.
packageWeight | Double | 10,3 | Optional | Order request weight. The unit of measurement will be based on the unit of measurement selected for your account. For metric system this will be in Kg, and for Imperial system, this will be in pounds.
packageVolume | Double | 10,3 | Optional | Order request  volume. The unit of measurement will be based on the unit of measurement selected for your account. For metric system this will be in cubic centimeters(CC), and for Imperial system, this will be in cubic inches(CBI).
packageLength | Double | 10,3 | Optional | Order request length. The unit of measurement will be based on the unit of measurement selected for your account. For metric system this will be in centimeters(CM), and for Imperial system, this will be in inches.
packageBreadth| Double | 10,3 | Optional | Order request width.  The unit of measurement will be based on the unit of measurement selected for your account. For metric system this will be in centimeters(CM), and for Imperial system, this will be in inches.
packageHeight| Double | 10,3 | Optional | Order request hieght.  The unit of measurement will be based on the unit of measurement selected for your account. For metric system this will be in centimeters(CM), and for Imperial system, this will be in inches.
priority | String | 16 | Optional | Order priority. If you wish to segregate Orders based on certain Order priorities, say you want to Route Plan for Orders based on their priorities, you can set up this field in the settings module and define the values that LogiNext should accept of this field. For example, this could be 'PRIORITY1', 'PRIORITY2', or 'PRIORITY3'.
serviceType | String | 16 | Optional | Order request Service Type.
packageValue | Double | 10 | Optional | Order request value.
paymentType | String | 40 | Optional | Payment mode. Ex: COD - Cash On Delivery, Prepaid. If not passed, this will be defaulted to COD.
numberOfItems | Integer | 20 | Optional | Number of items in the order.
deliveryType | String | 40 | Optional | In certain operations, there are different skill sets / special delivery requirements through which the Delivery has to take place.<br>For e.g. - Groceries / Food items has to be separated with Toiletries<br>Orders for Cake cannot be clubbed with the Order for Flowers while delivering.<br>In such cases, if you want to classify the orders by using Delivery Type such that these orders get assigned to Pickup Associates who are configured in LogiNext system with these special skill-sets or types, then you can use this field.<br>Please note that before you pass orders with certain Delivery Types, you will have to first configure the Delivery Types.<br>Please ask your Account Manager to set these values for you. Note that you can pass multiple Delivery Types in a comma separated manner in this API.
deliverBranch | String | 255 | Mandatory | For Deliver type of order requests, this is the Branch / Distribution Center / Hub to which the Delivery Associate will pickup the Order request from.<br>Note that you will have to first Add your Operation Branch / Distribution Center / Hub either through the Add Branch API or through the Add Branch Screen. <br>If you have any access related issue while creating branch, please reach out to your Account Manager
deliverServiceTime | Integer | 11 | Optional | Deliver service time in mins.
deliverStartTimeWindow | Date |  | Mandatory | Deliver start time window. Format - YYYY-MM-DDTHH:MM:SS.SSSZ e.g. : 2016-07-01T11:18:00.000Z.
deliverEndTimeWindow | Date |  | Mandatory | Deliver end time window. Format - YYYY-MM-DDTHH:MM:SS.SSSZ. For example - 2016-07-01T11:18:00.000Z.
deliveryLocationType | String | 40 | Optional | Type of delivery location. For example - CUSTOMER
deliverAccountCode | String | 255 | Mandatory | This is the customer code of the deliver customer.
deliverAddressId | String |255 | Optional | This is the Address ID of the deliver customer.
deliverAccountName | String | 255 | Conditional Mandatory | This is the deliver account name. This field in Non Mandatory in case Customer Profiling in ON.
deliverEmail | String | 100 | Optional | Delivery Customer email ID.
deliverPhoneNumber | String | 255 | Optional | Delivery Customer phone number.
deliverApartment | String | 512 | Conditional Mandatory | Delivery Address Apartment. This field in Non Mandatory in case Customer Profiling in ON.
deliverStreetName | String | 512 | Conditional Mandatory |Delivery Address street name. This field in Non Mandatory in case Customer Profiling in ON.
deliverLandmark | String | 512 | Optional | Delivery Address landmark.
deliverLocality | String | 512 | Conditional Mandatory | Delivery Address locality. This field in Non Mandatory in case Customer Profiling in ON.
deliverCity | String | 512 | Conditional Mandatory | Delivery Address city.. This field in Non Mandatory in case Customer Profiling in ON.
deliverState| String | 512 | Conditional Mandatory | Delivery Address state code. Please refer to the list of state codes provided in the "State Codes" section. This field in Non Mandatory in case Customer Profiling in ON.
deliverCountry | String | 512 | Conditional Mandatory | Delivery Address country code. Please refer to the list of country codes provided in the "Country Codes" section. This field in Non Mandatory in case Customer Profiling in ON.
deliverPinCode | String | 20 | Conditional Mandatory | Delivery Address postal code. This field in Non Mandatory in case Customer Profiling in ON.
deliverLatitude | Double |  | Optional |  Delivery Address geolocation coordinate (latitude).
deliverLongitude | Double |  | Optional | Delivery Address geolocation coordinate (longitude).
deliverAddressTimezone | String | | Optional | The timezone of the pickup location. Refer to the timezone codes list to get the full list of values you can pass here. If not passed, the timezone associated with the pickup location will be the branch timezone.
pickupNotes | String | 512 | Optional | Additional Pick-up notes associated with the order. For example, This can have details regarding whether the Order is fragile.
deliverNotes | String | 512 | Optional | Additional Delivery notes associated with the order.
clientCode | String | 32 | Optional | This is the identifier for an Account. Account is used to represent LogiNext’s Customer’s Customer. Pass the name of the Account in this field if you wish to create Orders on behalf of one of your Customers.

#### Request Parameters (Crates)

Param | DataType | Length |  Required | Description
--------- | ------- | ------- | ---------- | ------------
shipmentCrateMappings | Array of objects |  | Optional | Shipment crates
shipmentCrateMappings.crateCd | String | 128 | Mandatory | Crate code.
shipmentCrateMappings.crateAmount | Double |  | Optional | Crate amount
shipmentCrateMappings.crateType | String | 100 | Optional | Type of crate. Ex: cake, juice, sweet, furniture etc.
shipmentCrateMappings.noOfUnits | Integer | 10 | Optional | No. of crate units
shipmentCrateMappings.crateVolume | Double | 10,3 | Optional | This is the volume of crate. The unit of measurement will be based on the unit of measurement selected for your account. For metric system this will be in CC, and for Imperial system, this will be in cubic inches.
shipmentCrateMappings.crateWeight | Double | 10,3 | Optional | This is the weight of crate. The unit of measurement will be based on the unit of measurement selected for your account. For metric system this will be in Kg, and for Imperial system, this will be in pounds.
shipmentCrateMappings.crateLength | Double | 10,3 | Optional | This is the length of package. The unit of measurement will be based on the unit of measurement selected for your account. For metric system this will be in centimeters(CM), and for Imperial system, this will be in inches.
shipmentCrateMappings.crateBreadth| Double | 10,3 | Optional | This is the width of package.  The unit of measurement will be based on the unit of measurement selected for your account. For metric system this will be in centimeters(CM), and for Imperial system, this will be in inches.
shipmentCrateMappings.crateHeight| Double | 10,3 | Optional | This is the height of package.  The unit of measurement will be based on the unit of measurement selected for your account. For metric system this will be in centimeters(CM), and for Imperial system, this will be in inches.
shipmentCrateMappings.shipmentlineitems.itemCd | String | 200 | Mandatory | Item code
shipmentCrateMappings.shipmentlineitems.itemName | String | 255 | Optional | Item name
shipmentCrateMappings.shipmentlineitems.itemPrice | Double |  | Mandatory | Item price
shipmentCrateMappings.shipmentlineitems.itemQuantity | Double | 10 | Mandatory | Item quantity
shipmentCrateMappings.shipmentlineitems.itemType | String | 100 | Optional | Item type
shipmentCrateMappings.shipmentlineitems.itemWeight | Double | 10 | Optional | Item weight
shipmentCrateMappings.shipmentlineitems.itemLength | Double | 10,3 | Optional | This is the length of item. The unit of measurement will be based on the unit of measurement selected for your account. For metric system this will be in centimeters(CM), and for Imperial system, this will be in inches.
shipmentCrateMappings.shipmentlineitems.itemBreadth| Double | 10,3 | Optional | This is the width of item.  The unit of measurement will be based on the unit of measurement selected for your account. For metric system this will be in centimeters(CM), and for Imperial system, this will be in inches.
shipmentCrateMappings.shipmentlineitems.itemHeight| Double | 10,3 | Optional | This is the height of item.  The unit of measurement will be based on the unit of measurement selected for your account. For metric system this will be in centimeters(CM), and for Imperial system, this will be in inches.


### Create Pickup and Deliver

> Definition

```json
https://api.loginextsolutions.com/BookingApp/mile/v1/create
```

> Request Body

```json
[
   {
"shipmentRequestNo":"SH12432",
"awbNumber": "435-16685675",
"shipmentRequestDispatchDate": "2020-05-19T10:30:00.000Z",
"shipmentRequestType":"PICKUP",
"packageWeight":"10",
"packageVolume":"10",
"packageValue":"10",
"packageLength":"10",
"packageBreadth":"10",
"packageHeight":"10",
"priority":"Priority 1",
"paymentType":"COD",
"numberOfItems":3,
"deliveryType":"Groceries",
"serviceType":"Express",
"distributionCenter":""New York Main Branch",
"pickupBranch":"mea_allmile_sandbox Main Branch",
"pickupServiceTime": "50",
"pickupStartTimeWindow": "2020-05-19T14:24:00.000Z",
"pickupEndTimeWindow": "2020-05-19T14:24:00.000Z",
"pickupEmail":"james.w@ablogs.com",
"pickupPhoneNumber": "5163063377",
"pickupAccountCode": "jim001",
"pickupAddressId": "Home",
"pickupAddressType":"Home",
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
"deliverBranch":"New York Main Branch",
deliverServiceTime:"10",
deliverStartTimeWindow: "2020-04-10T10:31:00.000Z",
deliverEndTimeWindow: "2020-04-10T10:31:00.000Z",
deliverAccountCode: "Matt001",
deliverAccountName:"Jane Doe",
deliverEmail:"m.richardson@testmail.com",
deliverPhoneNumber:"9891234567",
deliverAddressId: "home",
deliverAddressType:"Home",
deliverApartment: "201",
deliverStreetName: "E Randolph St",
deliverLandmark: "Opp. Chiptole",
deliverLocality: "Down Towm Chicago",
deliverCity: "Chicago",
deliverState: "IL",
deliverCountry: "USA",
deliverPinCode: "60602",
deliverLatitude:41.882702,
deliverLongitude:-87.619392,
deliverAddressTimezone:"America/Chicago",
deliverNotes:"notes for delivery",
"shipmentCrateMappings": [
     {
         "crateCd": "CR041",
         "crateAmount": 100.65,
         "crateType": "case",
         "noOfUnits": 2,
         "crateWeight": 10,
         "crateVolume": 11,
         "crateLength": 12,
         "crateBreadth": 13,
         "crateHeight": 14,
         "shipmentlineitems": [
             {
                 "itemCd": "IT043",
                 "itemName": "Chicken Soup 2X200gm",
                 "itemPrice": 500,
                 "itemQuantity": 1,
                 "itemType": "soup",
                 "itemWeight": 10,
                 "itemVolume": 11,
                 "itemLength": 12,
                 "itemBreadth": 13,
                 "itemHeight": 14
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
    "message": "Shipment Request(s) created successfully",
    "moreResultsExists": false,
    "data": [
        {
            "index": 0,
            "shipmentRequestReferenceId": "2c0dcb93ca494cfc92d5b830c1c8033a",
            "shipmentRequestNo": "SH12432",
            "shipmentRequestType": "BOTH"
        }
    ],
    "hasError": false
}

```


> Failure Response

```json
{
    "status": 409,
    "message": "Shipment Request Creation Failed",
    "moreResultsExists": false,
    "error": [
        {
            "index": 0,
            "shipmentRequestNo": "SH12432",
            "shipmentRequestType": "DELIVER",
            "errorList": [
                {
                    "key": "deliverAccountCode",
                    "message": [
                        "Address not serviceable"
                    ]
                },
                {
                    "key": "deliveryType",
                    "message": [
                        "DeliveryType is invalid"
                    ]
                }
            ]
        }
    ],
    "hasError": true
}

```

Create pickup Oand deliverrder requests with this API in the LogiNext system. Order requests will be created and assigned a reference ID that can be used at a leter time to identify the order request.

API Type: Tier 1 API

#### Request

<span class="post">POST</span>`https://api.loginextsolutions.com/BookingApp/mile/v1/create`



#### Request Parameters

Param | DataType | Length |  Required | Description
--------- | ------- | ------- | ---------- | ------------
shipmentRequestNo | String | 100 | Optional | Order request Number. If not passed, the system will auto generate an Order request number
awbNumber | String | 1000 | Optional | Airway Bill Number associated with an Order request.
shipmentRequestDispatchDate | | | Optional | The requested Dispatch date for the Order request. The requested dispatch date is the date from which the system looks to start serviceing the order request, either through the service types, or zonal capacities configured. If not passed, the system considers the current date.
shipmentRequestType | String | 40 | Mandatory | The value in this field has to be "PICKUP" always.
distributionCenter | String | 255 | Mandatory | Distribution center name. The Distribution center is the Hub that is responsibile for fulfilling the Order. An Order can have different Pickup and Delivery leg branches, but will require a single Distribution center that is responsible for the fulfillment of the Order.
packageWeight | Double | 10,3 | Optional | Order request weight. The unit of measurement will be based on the unit of measurement selected for your account. For metric system this will be in Kg, and for Imperial system, this will be in pounds.
packageVolume | Double | 10,3 | Optional | Order request  volume. The unit of measurement will be based on the unit of measurement selected for your account. For metric system this will be in cubic centimeters(CC), and for Imperial system, this will be in cubic inches(CBI).
packageLength | Double | 10,3 | Optional | Order request length. The unit of measurement will be based on the unit of measurement selected for your account. For metric system this will be in centimeters(CM), and for Imperial system, this will be in inches.
packageBreadth| Double | 10,3 | Optional | Order request width.  The unit of measurement will be based on the unit of measurement selected for your account. For metric system this will be in centimeters(CM), and for Imperial system, this will be in inches.
packageHeight| Double | 10,3 | Optional | Order request hieght.  The unit of measurement will be based on the unit of measurement selected for your account. For metric system this will be in centimeters(CM), and for Imperial system, this will be in inches.
priority | String | 16 | Optional | Order priority. If you wish to segregate Orders based on certain Order priorities, say you want to Route Plan for Orders based on their priorities, you can set up this field in the settings module and define the values that LogiNext should accept of this field. For example, this could be 'PRIORITY1', 'PRIORITY2', or 'PRIORITY3'.
serviceType | String | 16 | Optional | Order request Service Type.
packageValue | Double | 10 | Optional | Order request value.
paymentType | String | 40 | Optional | Payment mode. Ex: COD - Cash On Delivery, Prepaid. If not passed, this will be defaulted to COD.
numberOfItems | Integer | 20 | Optional | Number of items in the order.
deliveryType | String | 40 | Optional | In certain operations, there are different skill sets / special delivery requirements through which the Delivery has to take place.<br>For e.g. - Groceries / Food items has to be separated with Toiletries<br>Orders for Cake cannot be clubbed with the Order for Flowers while delivering.<br>In such cases, if you want to classify the orders by using Delivery Type such that these orders get assigned to Pickup Associates who are configured in LogiNext system with these special skill-sets or types, then you can use this field.<br>Please note that before you pass orders with certain Delivery Types, you will have to first configure the Delivery Types.<br>Please ask your Account Manager to set these values for you. Note that you can pass multiple Delivery Types in a comma separated manner in this API.
deliverBranch | String | 255 | Mandatory | For Deliver type of order requests, this is the Branch / Distribution Center / Hub to which the Delivery Associate will pickup the Order request from.<br>Note that you will have to first Add your Operation Branch / Distribution Center / Hub either through the Add Branch API or through the Add Branch Screen. <br>If you have any access related issue while creating branch, please reach out to your Account Manager
pickupStartTimeWindow | Date |  | Mandatory | This is the start date and time for the time slot of the Pickup.<br>Note that this date and time has to be greater than the Order Creation Date and Time.<br>Note that this date and time has to be in UTC.<br>For example - "2017-07-15T11:30:00.000Z
distributionCenter | String |  | Mandatory | Distribution center's name. The Distribution center is the Hub that is responsibile for fulfilling the Order. An Order can have different Pickup and Delivery leg branches, but will require a single Distribution center that is responsible for the fulfillment of the Order.
pickupEndTimeWindow | Date |  | Mandatory | This is the end date and time for the time slot of the Pickup.<br>Note that this date and time has to be greater than the Pickup Start Date and Time.<br>Note that this date and time has to be in UTC.<br>For example - "2017-07-15T12:30:00.000Z"
pickupAccountCode | String | 255 | Mandatory | Pick-up Customer ID.
pickupAccountName | String | 255 | Conditional Mandatory | Pick-up Customer name. This field in Non Mandatory in case Customer Profiling in ON.
pickupAddressId | String | 255 | Optional | Pick-up Customer Address ID.
pickupEmail | String | 100 | Optional | Pick-up Customer email ID.
pickupPhoneNumber | String | 255 | Optional | Pick-up Customer phone number. This field in Non Mandatory in case Customer Profiling in ON.
pickupApartment | String | 512 | Conditional Mandatory | This is the apartment details of the pickup customer. This field in Non Mandatory in case Customer Profiling in ON.
pickupStreetName | String | 512 | Mandatory | This is the street name of the pickup customer. Standard Address validations that were set while setting up your account in LogiNext will apply for this field. This field in Non Mandatory in case Customer Profiling in ON.
pickupLandmark | String | 512 | Conditional Mandatory | Pick-up Address landmark. This field in Non Mandatory in case Customer Profiling in ON.
pickupLocality | String | 512 | Conditional Mandatory | Pick-up Address locality. This field in Non Mandatory in case Customer Profiling in ON.
pickupCity | String | 512 | Conditional Mandatory | Pick-up Address city. This field in Non Mandatory in case Customer Profiling in ON.
pickupState| String | 512 | Conditional Mandatory | Pick-up Address State. This field in Non Mandatory in case Customer Profiling in ON. Please refer to the list of state codes provided in the "State Codes" section. This field in Non Mandatory in case Customer Profiling in ON.
pickupCountry | String | 512 | Conditional Mandatory | Pick-up Address Country. This field in Non Mandatory in case Customer Profiling in ON. Please refer to the list of country codes provided in the "Country Codes" section.
pickupPinCode | String | 20 | Conditional Mandatory | Pick-up Address postal code. This field in Non Mandatory in case Customer Profiling in ON.
pickupLatitude | Double |  | Optional | This is the geolocation coordinate (latitude) of the pickup customer.
pickupLongitude | Double |  | Optional | The geolocation coordinate (longitude) of the pickup customer.
pickupAddressTimezone | String | | Optional | The timezone of the pickup location. Refer to the timezone codes list to get the full list of values you can pass here. If not passed, the timezone associated with the pickup location will be the branch timezone.
deliverServiceTime | Integer | 11 | Optional | Deliver service time in mins.
deliverStartTimeWindow | Date |  | Mandatory | Deliver start time window. Format - YYYY-MM-DDTHH:MM:SS.SSSZ e.g. : 2016-07-01T11:18:00.000Z.
deliverEndTimeWindow | Date |  | Mandatory | Deliver end time window. Format - YYYY-MM-DDTHH:MM:SS.SSSZ. For example - 2016-07-01T11:18:00.000Z.
deliveryLocationType | String | 40 | Optional | Type of delivery location. For example - CUSTOMER
deliverAccountCode | String | 255 | Mandatory | This is the customer code of the deliver customer.
deliverAddressId | String |255 | Optional | This is the Address ID of the deliver customer.
deliverAccountName | String | 255 | Conditional Mandatory | This is the deliver account name. This field in Non Mandatory in case Customer Profiling in ON.
deliverEmail | String | 100 | Optional | Delivery Customer email ID.
deliverPhoneNumber | String | 255 | Optional | Delivery Customer phone number.
deliverApartment | String | 512 | Conditional Mandatory | Delivery Address Apartment. This field in Non Mandatory in case Customer Profiling in ON.
deliverStreetName | String | 512 | Conditional Mandatory |Delivery Address street name. This field in Non Mandatory in case Customer Profiling in ON.
deliverLandmark | String | 512 | Optional | Delivery Address landmark.
deliverLocality | String | 512 | Conditional Mandatory | Delivery Address locality. This field in Non Mandatory in case Customer Profiling in ON.
deliverCity | String | 512 | Conditional Mandatory | Delivery Address city.. This field in Non Mandatory in case Customer Profiling in ON.
deliverState| String | 512 | Conditional Mandatory | Delivery Address state code. Please refer to the list of state codes provided in the "State Codes" section. This field in Non Mandatory in case Customer Profiling in ON.
deliverCountry | String | 512 | Conditional Mandatory | Delivery Address country code. Please refer to the list of country codes provided in the "Country Codes" section. This field in Non Mandatory in case Customer Profiling in ON.
deliverPinCode | String | 20 | Conditional Mandatory | Delivery Address postal code. This field in Non Mandatory in case Customer Profiling in ON.
deliverLatitude | Double |  | Optional |  Delivery Address geolocation coordinate (latitude).
deliverLongitude | Double |  | Optional | Delivery Address geolocation coordinate (longitude).
deliverAddressTimezone | String | | Optional | The timezone of the pickup location. Refer to the timezone codes list to get the full list of values you can pass here. If not passed, the timezone associated with the pickup location will be the branch timezone.
pickupNotes | String | 512 | Optional | Additional Pick-up notes associated with the order. For example, This can have details regarding whether the Order is fragile.
deliverNotes | String | 512 | Optional | Additional Delivery notes associated with the order.
clientCode | String | 32 | Optional | This is the identifier for an Account. Account is used to represent LogiNext’s Customer’s Customer. Pass the name of the Account in this field if you wish to create Orders on behalf of one of your Customers.

#### Request Parameters (Crates)

Param | DataType | Length |  Required | Description
--------- | ------- | ------- | ---------- | ------------
shipmentCrateMappings | Array of objects |  | Optional | Shipment crates
shipmentCrateMappings.crateCd | String | 128 | Mandatory | Crate code.
shipmentCrateMappings.crateAmount | Double |  | Optional | Crate amount
shipmentCrateMappings.crateType | String | 100 | Optional | Type of crate. Ex: cake, juice, sweet, furniture etc.
shipmentCrateMappings.noOfUnits | Integer | 10 | Optional | No. of crate units
shipmentCrateMappings.crateVolume | Double | 10,3 | Optional | This is the volume of crate. The unit of measurement will be based on the unit of measurement selected for your account. For metric system this will be in CC, and for Imperial system, this will be in cubic inches.
shipmentCrateMappings.crateWeight | Double | 10,3 | Optional | This is the weight of crate. The unit of measurement will be based on the unit of measurement selected for your account. For metric system this will be in Kg, and for Imperial system, this will be in pounds.
shipmentCrateMappings.crateLength | Double | 10,3 | Optional | This is the length of package. The unit of measurement will be based on the unit of measurement selected for your account. For metric system this will be in centimeters(CM), and for Imperial system, this will be in inches.
shipmentCrateMappings.crateBreadth| Double | 10,3 | Optional | This is the width of package.  The unit of measurement will be based on the unit of measurement selected for your account. For metric system this will be in centimeters(CM), and for Imperial system, this will be in inches.
shipmentCrateMappings.crateHeight| Double | 10,3 | Optional | This is the height of package.  The unit of measurement will be based on the unit of measurement selected for your account. For metric system this will be in centimeters(CM), and for Imperial system, this will be in inches.
shipmentCrateMappings.shipmentlineitems.itemCd | String | 200 | Mandatory | Item code
shipmentCrateMappings.shipmentlineitems.itemName | String | 255 | Optional | Item name
shipmentCrateMappings.shipmentlineitems.itemPrice | Double |  | Mandatory | Item price
shipmentCrateMappings.shipmentlineitems.itemQuantity | Double | 10 | Mandatory | Item quantity
shipmentCrateMappings.shipmentlineitems.itemType | String | 100 | Optional | Item type
shipmentCrateMappings.shipmentlineitems.itemWeight | Double | 10 | Optional | Item weight
shipmentCrateMappings.shipmentlineitems.itemLength | Double | 10,3 | Optional | This is the length of item. The unit of measurement will be based on the unit of measurement selected for your account. For metric system this will be in centimeters(CM), and for Imperial system, this will be in inches.
shipmentCrateMappings.shipmentlineitems.itemBreadth| Double | 10,3 | Optional | This is the width of item.  The unit of measurement will be based on the unit of measurement selected for your account. For metric system this will be in centimeters(CM), and for Imperial system, this will be in inches.
shipmentCrateMappings.shipmentlineitems.itemHeight| Double | 10,3 | Optional | This is the height of item.  The unit of measurement will be based on the unit of measurement selected for your account. For metric system this will be in centimeters(CM), and for Imperial system, this will be in inches.


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
    "deliveryType": "Groceries, Reefer",
    "deliveryLocationType":"HOME",
    "pickupBranch": "East Manhatten",
    "distributionCenter": "Brooklyn",
    "partialDeliveryAllowedFl": "Y",
    "cancellationAllowedFl": "N",    
    "returnAllowedFl": "Y",
    "deliveryMediumUsername":"johnc",
    "returnBranch": "Chicago North",
    "numberOfItems": 2,
    "packageWeight":"10",
    "packageVolume": "4500",
    "packageLength": 2.5,
    "packageBreadth": 2.5,
    "packageHeight": 2.5,
    "priority": "PRIORITY1",
    "serviceType":"Premium",
    "paymentType": "COD",
    "packageValue": "5000",
    "shippingCost": "50",
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
        "crateWeight":10,
        "crateVolume":11,
        "crateLength":12,
        "crateBreadth":13,
        "crateHeight":14,
        "shipmentlineitems": [
          {
            "itemCd": "IT038",
            "itemName": "Milk tetra pack small",
            "itemPrice": 100,
            "itemQuantity": 1,
            "itemType": "dairy",
            "itemWeight": 15,
            "itemVolume":16,
            "itemLength":17,
            "itemBreadth":18,
            "itemHeight":19
          },
          {
            "itemCd": "IT043",
            "itemName": "Chicken Soup 2X200gm",
            "itemPrice": 500,
            "itemQuantity": 1,
            "itemType": "soup",
            "itemWeight": 10,
            "itemVolume":16,
            "itemLength":17,
            "itemBreadth":18,
            "itemHeight":19
          },
          {
            "itemCd": "IT030",
            "itemName": "WholeBeanCoffee 6x1kg",
            "itemPrice": 400,
            "itemQuantity": 1,
            "itemType": "coffee",
            "itemWeight": 10,
            "itemVolume":16,
            "itemLength":17,
            "itemBreadth":18,
            "itemHeight":19
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
            "referenceId": "fa7716b25fe5432a96d1a709a28bd6d8",
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

> Partial Success Response

```json
{
    "status": 207,
    "message": "Order(s) created partially",
    "data": [
        {
            "index": 0,
            "referenceId": "fa7716b25fe5432a96d1a709a28bd6d8",
            "orderNumber": "ww1220",
            "shipmentOrderTypeCd": "DELIVER",
            "orderState": "FORWARD"
        },
        {
            "index": 1,
            "referenceId": "af7065ad4f3945a889ec25c323aa7b68",
            "orderNumber": "ww1244",
            "shipmentOrderTypeCd": "DELIVER",
            "orderState": "FORWARD"
        },
        {
            "index": 2,
            "referenceId": "a4e6dc610c854166a7957b9876aa4ce5",
            "orderNumber": "ww1234",
            "shipmentOrderTypeCd": "DELIVER",
            "orderState": "FORWARD"
        }
    ],
    "error": [
        {
            "index": 3,
            "orderNo": "ww1229",
            "orderState": "FORWARD",
            "shipmentOrderTypeCd": "DELIVER",
            "errorList": [
                {
                    "key": "deliverBranch",
                    "message": [
                        "Deliver Branch is invalid"
                    ]
                }
            ]
        }
    ],
    "hasError": true
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

API Type: Tier 1 API

#### Request

<span class="post">POST</span>`https://api.loginextsolutions.com/ShipmentApp/mile/v2/create`



#### Request Parameters

Param | DataType | Length |  Required | Description
--------- | ------- | ------- | ---------- | ------------
orderNo | String | 100 | Mandatory | Order Number.
awbNumber | String | 1000 | Optional | Airway Bill Number associated with an order.
shipmentOrderTypeCd | String | 40 | Mandatory | The value in this field has to be "PICKUP" always.
orderState | String | 512 | Mandatory | If an order is a Forward way (Pickup from Merchant for Customer Delivery), then value here should be "FORWARD"<br>If an order is a Return way (Return from the Customer), then value here should be "REVERSE"
autoAllocateFl| String | 50 | Optional | This can be "Y", "N", or "P". If set to "Y", the Order will be automatially allocated to the nearest Delivery Associate when it is created in the system. The behaviour of the auto assignment will be dependant on the configurations set in the 'Auto Assignment Profile' screen in your LogiNext Account settings screen. If "N", the Order will not be considered for auto assignment at the time of Order Creation<br>Pass this Flag as 'P' if you want to assign the newly created Order to an existing planned trip. This assignment event can impact the sequence of Order previously created for that trip.
shipmentOrderDt | Date |  | Mandatory | Order Date.<br>Note that this date and time has to be in UTC.<br>For example - "2017-07-15T10:30:00.000Z"
distributionCenter | String | 255 | Mandatory | Distribution center name. The Distribution center is the Hub that is responsibile for fulfilling the Order. An Order can have different Pickup and Delivery leg branches, but will require a single Distribution center that is responsible for the fulfillment of the Order.
packageWeight | Double | 10,3 | Optional | Order package weight. The unit of measurement will be based on the unit of measurement selected for your account. For metric system this will be in Kg, and for Imperial system, this will be in pounds.
packageVolume | Double | 10,3 | Optional | Order package volume. The unit of measurement will be based on the unit of measurement selected for your account. For metric system this will be in cubic centimeters(CC), and for Imperial system, this will be in cubic inches(CBI).
packageLength | Double | 10,3 | Optional | Order package length. The unit of measurement will be based on the unit of measurement selected for your account. For metric system this will be in centimeters(CM), and for Imperial system, this will be in inches.
packageBreadth| Double | 10,3 | Optional | Order package width.  The unit of measurement will be based on the unit of measurement selected for your account. For metric system this will be in centimeters(CM), and for Imperial system, this will be in inches.
packageHeight| Double | 10,3 | Optional | Order package hieght.  The unit of measurement will be based on the unit of measurement selected for your account. For metric system this will be in centimeters(CM), and for Imperial system, this will be in inches.
priority | String | 16 | Optional | Order priority. If you wish to segregate Orders based on certain Order priorities, say you want to Route Plan for Orders based on their priorities, you can set up this field in the settings module and define the values that LogiNext should accept of this field. For example, this could be 'PRIORITY1', 'PRIORITY2', or 'PRIORITY3'.
serviceType | String | 16 | Optional | Order Service Type.
packageValue | Double | 10 | Optional | Order value.
shippingCost | Double | 10 | Optional | Shipping cost or delivery Fee for the Order.
paymentType | String | 40 | Optional | Payment mode. Ex: COD - Cash On Delivery, Prepaid. If not passed, this will be defaulted to COD.
numberOfItems | Integer | 20 | Optional | Number of items in the order.
deliveryType | String | 40 | Optional | In certain operations, there are different skill sets / special delivery requirements through which the Delivery has to take place.<br>For e.g. - Groceries / Food items has to be separated with Toiletries<br>Orders for Cake cannot be clubbed with the Order for Flowers while delivering.<br>In such cases, if you want to classify the orders by using Delivery Type such that these orders get assigned to Pickup Associates who are configured in LogiNext system with these special skill-sets or types, then you can use this field.<br>Please note that before you pass orders with certain Delivery Types, you will have to first configure the Delivery Types.<br>Please ask your Account Manager to set these values for you. Note that you can pass multiple Delivery Types in a comma separated manner in this API.
deliveryLocationType | String | 255 | Optional | This parameter if passed helps the Operation Managers / Pickup Associates to know if the Pick location is Residence or Office or Pick-up point, etc.<br>partialDeliveryAllowedFl | String | 50 | Optional | Is Partial Delivery allowed. Ex: Y/N. Default value is N.
returnAllowedFl | String | 1 | Optional | This identifies if order return allowed. Ex: Y/N. Default value is Y.
cancellationAllowedFl | String | 1 | Optional | This identifies if order cancellation is allowed. Ex: Y/N. Default value is Y.
deliveryMediumUsername | STRING | | Optional |  If you know the Delivery Associate who will be fulfilling the Order, pass their usernam in this field.
pickupBranch | String | 255 | Mandatory | For Pick-Up type of orders, this is the Branch / Distribution Center / Hub to which the Delivery Associate will Deliver the order / shipment /parcel to.<br>Note that you will have to first Add your Operation Branch / Distribution Center / Hub either through the Add Branch API or through the Add Branch Screen. <br>If you have any access related issue while creating branch, please reach out to your Account Manager
pickupServiceTime | Integer | 11 | Mandatory | This is the time that the Pickup Associate is going to take at the Pickup location to pickup the orders.
pickupStartTimeWindow | Date |  | Mandatory | This is the start date and time for the time slot of the Pickup.<br>Note that this date and time has to be greater than the Order Creation Date and Time.<br>Note that this date and time has to be in UTC.<br>For example - "2017-07-15T11:30:00.000Z
distributionCenter | String |  | Mandatory | Distribution center's name. The Distribution center is the Hub that is responsibile for fulfilling the Order. An Order can have different Pickup and Delivery leg branches, but will require a single Distribution center that is responsible for the fulfillment of the Order.
pickupEndTimeWindow | Date |  | Mandatory | This is the end date and time for the time slot of the Pickup.<br>Note that this date and time has to be greater than the Pickup Start Date and Time.<br>Note that this date and time has to be in UTC.<br>For example - "2017-07-15T12:30:00.000Z"
pickupAccountCode | String | 255 | Mandatory | Pick-up Customer ID.
pickupAccountName | String | 255 | Conditional Mandatory | Pick-up Customer name. This field in Non Mandatory in case Customer Profiling in ON.
pickupAddressId | String | 255 | Optional | Pick-up Customer Address ID.
pickupEmail | String | 100 | Optional | Pick-up Customer email ID.
pickupPhoneNumber | String | 255 | Optional | Pick-up Customer phone number. This field in Non Mandatory in case Customer Profiling in ON.
pickupApartment | String | 512 | Conditional Mandatory | This is the apartment details of the pickup customer. This field in Non Mandatory in case Customer Profiling in ON.
pickupStreetName | String | 512 | Mandatory | This is the street name of the pickup customer. Standard Address validations that were set while setting up your account in LogiNext will apply for this field. This field in Non Mandatory in case Customer Profiling in ON.
pickupLandmark | String | 512 | Conditional Mandatory | Pick-up Address landmark. This field in Non Mandatory in case Customer Profiling in ON.
pickupLocality | String | 512 | Conditional Mandatory | Pick-up Address locality. This field in Non Mandatory in case Customer Profiling in ON.
pickupCity | String | 512 | Conditional Mandatory | Pick-up Address city. This field in Non Mandatory in case Customer Profiling in ON.
pickupState| String | 512 | Conditional Mandatory | Pick-up Address State. This field in Non Mandatory in case Customer Profiling in ON. Please refer to the list of state codes provided in the "State Codes" section. This field in Non Mandatory in case Customer Profiling in ON.
pickupCountry | String | 512 | Conditional Mandatory | Pick-up Address Country. This field in Non Mandatory in case Customer Profiling in ON. Please refer to the list of country codes provided in the "Country Codes" section.
pickupPinCode | String | 20 | Conditional Mandatory | Pick-up Address postal code. This field in Non Mandatory in case Customer Profiling in ON.
pickupLatitude | Double |  | Optional | This is the geolocation coordinate (latitude) of the pickup customer.
pickupLongitude | Double |  | Optional | The geolocation coordinate (longitude) of the pickup customer.
pickupAddressTimezone | String | | Optional | The timezone of the pickup location. Refer to the timezone codes list to get the full list of values you can pass here. If not passed, the timezone associated with the pickup location will be the branch timezone.
pickupNotes | String | 512 | Optional | Additional Pick-up notes associated with the order. For example, This can have details regarding whether the Order is fragile.
deliverNotes | String | 512 | Optional | Additional Delivery notes associated with the order.
clientCode | String | 32 | Optional | This is the identifier for an Account. Account is used to represent LogiNext’s Customer’s Customer. Pass the name of the Account in this field if you wish to create Orders on behalf of one of your Customers.

#### Request Parameters (Crates)

Param | DataType | Length |  Required | Description
--------- | ------- | ------- | ---------- | ------------
shipmentCrateMappings | Array of objects |  | Optional | Shipment crates
shipmentCrateMappings.crateCd | String | 128 | Mandatory | Crate code.
shipmentCrateMappings.crateAmount | Double |  | Optional | Crate amount
shipmentCrateMappings.crateType | String | 100 | Optional | Type of crate. Ex: cake, juice, sweet, furniture etc.
shipmentCrateMappings.noOfUnits | Integer | 10 | Optional | No. of crate units
shipmentCrateMappings.crateVolume | Double | 10,3 | Optional | This is the volume of crate. The unit of measurement will be based on the unit of measurement selected for your account. For metric system this will be in CC, and for Imperial system, this will be in cubic inches.
shipmentCrateMappings.crateWeight | Double | 10,3 | Optional | This is the weight of crate. The unit of measurement will be based on the unit of measurement selected for your account. For metric system this will be in Kg, and for Imperial system, this will be in pounds.
shipmentCrateMappings.crateLength | Double | 10,3 | Optional | This is the length of package. The unit of measurement will be based on the unit of measurement selected for your account. For metric system this will be in centimeters(CM), and for Imperial system, this will be in inches.
shipmentCrateMappings.crateBreadth| Double | 10,3 | Optional | This is the width of package.  The unit of measurement will be based on the unit of measurement selected for your account. For metric system this will be in centimeters(CM), and for Imperial system, this will be in inches.
shipmentCrateMappings.crateHeight| Double | 10,3 | Optional | This is the height of package.  The unit of measurement will be based on the unit of measurement selected for your account. For metric system this will be in centimeters(CM), and for Imperial system, this will be in inches.
shipmentCrateMappings.shipmentlineitems.itemCd | String | 200 | Mandatory | Item code
shipmentCrateMappings.shipmentlineitems.itemName | String | 255 | Optional | Item name
shipmentCrateMappings.shipmentlineitems.itemPrice | Double |  | Mandatory | Item price
shipmentCrateMappings.shipmentlineitems.itemQuantity | Double | 10 | Mandatory | Item quantity
shipmentCrateMappings.shipmentlineitems.itemType | String | 100 | Optional | Item type
shipmentCrateMappings.shipmentlineitems.itemWeight | Double | 10 | Optional | Item weight
shipmentCrateMappings.shipmentlineitems.itemLength | Double | 10,3 | Optional | This is the length of item. The unit of measurement will be based on the unit of measurement selected for your account. For metric system this will be in centimeters(CM), and for Imperial system, this will be in inches.
shipmentCrateMappings.shipmentlineitems.itemBreadth| Double | 10,3 | Optional | This is the width of item.  The unit of measurement will be based on the unit of measurement selected for your account. For metric system this will be in centimeters(CM), and for Imperial system, this will be in inches.
shipmentCrateMappings.shipmentlineitems.itemHeight| Double | 10,3 | Optional | This is the height of item.  The unit of measurement will be based on the unit of measurement selected for your account. For metric system this will be in centimeters(CM), and for Imperial system, this will be in inches.



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
    "packageLength": 2.5,
    "packageBreadth": 2.5,
    "packageHeight": 2.5,
    "priority": "PRIORITY1",
    "preparationTime":20,
    "serviceType":"Premium",
    "paymentType": "Prepaid",
    "packageValue": "500",
    "shippingCost":"50",
    "numberOfItems": 1,
    "partialDeliveryAllowedFl": "Y",
    "returnAllowedFl": "Y",
    "cancellationAllowedFl": "N",    
    "deliveryMediumUsername":"johnc",
    "deliverBranch": "Boston",
    "deliverServiceTime": "20",
    "deliverEndTimeWindow": "2016-07-18T10:31:00.000Z",
    "deliverStartTimeWindow": "2016-07-16T10:31:00.000Z",
    "deliveryType": "Groceries, Reefer",
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
        "crateWeight":10,
        "crateVolume":11,
        "crateLength":12,
        "crateBreadth":13,
        "crateHeight":14,
        "shipmentlineitems": [
          {
            "itemCd": "IT043",
            "itemName": "Chicken Soup 2X200gm",
            "itemPrice": 500,
            "itemQuantity": 1,
            "itemType": "soup",
            "itemWeight": 10,
            "itemVolume":16,
            "itemLength":17,
            "itemBreadth":18,
            "itemHeight":19
          },
          {
            "itemCd": "IT030",
            "itemName": "WholeBeanCoffee 6x1kg",
            "itemPrice": 400,
            "itemQuantity": 2,
            "itemType": "coffee",
            "itemWeight": 10,
            "itemVolume":16,
            "itemLength":17,
            "itemBreadth":18,
            "itemHeight":19
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
> Partial Success Response

```json
{
    "status": 207,
    "message": "Order(s) created partially",
    "data": [
        {
            "index": 0,
            "referenceId": "b032f3e9397343ba812f96370b92d592",
            "orderNumber": "ww1220",
            "shipmentOrderTypeCd": "DELIVER",
            "orderState": "FORWARD"
        },
        {
            "index": 1,
            "referenceId": "af7065ad4f3945a889ec25c323aa7b68",
            "orderNumber": "ww1244",
            "shipmentOrderTypeCd": "DELIVER",
            "orderState": "FORWARD"
        },
        {
            "index": 2,
            "referenceId": "a4e6dc610c854166a7957b9876aa4ce5",
            "orderNumber": "ww1234",
            "shipmentOrderTypeCd": "DELIVER",
            "orderState": "FORWARD"
        }
    ],
    "error": [
        {
            "index": 3,
            "orderNo": "ww1229",
            "orderState": "FORWARD",
            "shipmentOrderTypeCd": "DELIVER",
            "errorList": [
                {
                    "key": "deliverBranch",
                    "message": [
                        "Deliver Branch is invalid"
                    ]
                }
            ]
        }
    ],
    "hasError": true
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

API Type: Tier 1 API

#### Request

<span class="post">POST</span>`https://api.loginextsolutions.com/ShipmentApp/mile/v2/create`

#### Request Parameters

Param | DataType | Length |  Required | Description
--------- | ------- | ---------- | ---------- | ------------
orderNo | String | 100 | Mandatory |  Order Number.
awbNumber | String  | 1000 | Optional | Airway Bill Number associated with an order.
shipmentOrderTypeCd | String  | 40 | Mandatory | This is the order type code. DELIVER for delivery leg order
orderState | String  | 512 | Mandatory | State of order. Ex: FORWARD
autoAllocateFl| String | 50 | Optional | This can be "Y", "N", or "P". If set to "Y", the Order will be automatially allocated to the nearest Delivery Associate when it is created in the system. The behaviour of the auto assignment will be dependant on the configurations set in the 'Auto Assignment Profile' screen in your LogiNext Account settings screen. If "N", the Order will not be considered for auto assignment at the time of Order Creation<br>Pass this Flag as 'P' if you want to assign the newly created Order to an existing planned trip. This assignment event can impact the sequence of Order previously created for that trip.
shipmentOrderDt | Date |  | Mandatory | Order Date Format - YYYY-MM-DDTHH:MM:SS.SSSZ e.g. : 2016-07-01T11:18:00.000Z.
distributionCenter | String | 255 | Mandatory | Distribution center's name. The Distribution center is the Hub that is responsibile for fulfilling the Order. An Order can have different Pickup and Delivery leg branches, but will require a single Distribution center that is responsible for the fulfillment of the Order.
packageWeight | Double | 10,3 | Optional | Order package weight. The unit of measurement will be based on the unit of measurement selected for your account. For metric system this will be in Kg, and for Imperial system, this will be in pounds.
packageVolume | Double | 10,3 | Optional | Order package volume. The unit of measurement will be based on the unit of measurement selected for your account. For metric system this will be in cubic centimeters(CC), and for Imperial system, this will be in cubic inches(CBI).
packageLength | Double | 10,3 | Optional | Order package length. The unit of measurement will be based on the unit of measurement selected for your account. For metric system this will be in centimeters(CM), and for Imperial system, this will be in inches.
packageBreadth| Double | 10,3 | Optional | Order package breadth.  The unit of measurement will be based on the unit of measurement selected for your account. For metric system this will be in centimeters(CM), and for Imperial system, this will be in inches.
packageHeight| Double | 10,3 | Optional | Order package height. The unit of measurement will be based on the unit of measurement selected for your account. For metric system this will be in centimeters(CM), and for Imperial system, this will be in inches.
priority | String | 16 | Optional | This is the priority of the current Order. If you wish to segregate Orders based on certain Order priorities, say you want to Route Plan for Orders based on their priorities, you can set up this field in the settings module and define the values that LogiNext should accept of this field. For example, this could be 'PRIORITY1', 'PRIORITY2', or 'PRIORITY3'.
preparationTime | Double | 10,3 | Optional | Order preparation time.
serviceType | String | 16 | Optional |This is the service type of the Order.
numberOfItems | Integer | 20 | Optional | This is the number of crates
paymentType | String | 40 | Optional | This is the payment mode. Ex: COD - Cash On Delivery, Prepaid. If not passed, this will be defaulted to COD.
partialDeliveryAllowedFl | String | 50 | Optional | This is the is Partial Delivery allowed. Ex: Y/N. Default value is N.
packageValue | Double | 10 | Optional | Package Value (This will be used when paymentType is Prepaid)
shippingCost | Double | 10 | Optional | Shipping cost or delivery Fee for the Order.
returnAllowedFl | String | 1 | Optional | This field specifies if the order can be returned. Ex: Y/N. Default value is Y.
cancellationAllowedFl | String | 1 | Optional | Is Cancellation allowed. Ex: Y/N. Default value is Y.
deliveryMediumUsername | STRING | | Optional |  If you know the Delivery Associate who will be fulfilling the Order, pass their usernam in this field.
deliverBranch | String | 255 | Mandatory | For Deliver type of orders, this is the Branch / Distribution Center / Hub from which the Delivery Associate will pickup the order / shipment /parcel to.<br>Note that you will have to first Add your Operation Branch / Distribution Center / Hub either through the Add Branch API or through the Add Branch Screen. <br>If you have any access related issue while creating branch, please reach out to your Account Manager.
deliverServiceTime | Integer | 11 | Optional | Deliver service time in mins.
deliverStartTimeWindow | Date |  | Mandatory | Deliver start time window. Format - YYYY-MM-DDTHH:MM:SS.SSSZ e.g. : 2016-07-01T11:18:00.000Z.
deliverEndTimeWindow | Date |  | Mandatory | Deliver end time window. Format - YYYY-MM-DDTHH:MM:SS.SSSZ. For example - 2016-07-01T11:18:00.000Z.
deliveryType | String | 40 | Optional | Order delivery type. For example - ‘Groceries’ for grocery type of Orders. Note that you can pass multiple Delivery Types in a comma separated manner in this API.
deliveryLocationType | String | 40 | Optional | Type of delivery location. For example - CUSTOMER
deliverAccountCode | String | 255 | Mandatory | This is the customer code of the deliver customer.
deliverAddressId | String |255 | Optional | This is the Address ID of the deliver customer.
deliverAccountName | String | 255 | Conditional Mandatory | This is the deliver account name. This field in Non Mandatory in case Customer Profiling in ON.
deliverEmail | String | 100 | Optional | Delivery Customer email ID.
deliverPhoneNumber | String | 255 | Optional | Delivery Customer phone number.
deliverApartment | String | 512 | Conditional Mandatory | Delivery Address Apartment. This field in Non Mandatory in case Customer Profiling in ON.
deliverStreetName | String | 512 | Conditional Mandatory |Delivery Address street name. This field in Non Mandatory in case Customer Profiling in ON.
deliverLandmark | String | 512 | Optional | Delivery Address landmark.
deliverLocality | String | 512 | Conditional Mandatory | Delivery Address locality. This field in Non Mandatory in case Customer Profiling in ON.
deliverCity | String | 512 | Conditional Mandatory | Delivery Address city.. This field in Non Mandatory in case Customer Profiling in ON.
deliverState| String | 512 | Conditional Mandatory | Delivery Address state code. Please refer to the list of state codes provided in the "State Codes" section. This field in Non Mandatory in case Customer Profiling in ON.
deliverCountry | String | 512 | Conditional Mandatory | Delivery Address country code. Please refer to the list of country codes provided in the "Country Codes" section. This field in Non Mandatory in case Customer Profiling in ON.
deliverPinCode | String | 20 | Conditional Mandatory | Delivery Address postal code. This field in Non Mandatory in case Customer Profiling in ON.
deliverLatitude | Double |  | Optional |  Delivery Address geolocation coordinate (latitude).
deliverLongitude | Double |  | Optional | Delivery Address geolocation coordinate (longitude).
deliverAddressTimezone | String | | Optional | The timezone of the pickup location. Refer to the timezone codes list to get the full list of values you can pass here. If not passed, the timezone associated with the pickup location will be the branch timezone.
returnBranch | String | 255 | Mandatory | Name of return branch.
pickupNotes | String | 512 | Optional | Additional pickup comments associated with the order.
deliverNotes | String | 512 | Optional | Additional delivery comments associated with the order.
clientCode | String | 32 | Optional | This is the identifier for an Account. An Account is used to represent LogiNext’s Customer’s Customer. Pass the name of the Account in this field if you wish to create an Order on behalf of one of your Customers.

#### Request Parameters (Crates)

Param | DataType | Length |  Required | Description
--------- | ------- | ------- | ---------- | ------------
shipmentCrateMappings | Array of objects |  | Optional | These are the order crates.
shipmentCrateMappings.crateCd | String | 128 | Mandatory | This is the crate code for a crate.
shipmentCrateMappings.crateAmount | Double |  | Mandatory | This is the crate amount for a crate.
shipmentCrateMappings.crateType | String | 100 | Mandatory | Crate type.
shipmentCrateMappings.noOfUnits | Integer | 10 | Mandatory | This is the Number of items in the crate.
shipmentCrateMappings.crateVolume | Double | 10,3 | Optional | This is the volume of crate. The unit of measurement will be based on the unit of measurement selected for your account. For metric system this will be in CC, and for Imperial system, this will be in cubic inches.
shipmentCrateMappings.crateWeight | Double | 10,3 | Optional | This is the weight of crate. The unit of measurement will be based on the unit of measurement selected for your account. For metric system this will be in Kg, and for Imperial system, this will be in pounds.
shipmentCrateMappings.crateLength | Double | 10,3 | Optional | This is the length of package. The unit of measurement will be based on the unit of measurement selected for your account. For metric system this will be in centimeters(CM), and for Imperial system, this will be in inches.
shipmentCrateMappings.crateBreadth| Double | 10,3 | Optional | This is the width of package.  The unit of measurement will be based on the unit of measurement selected for your account. For metric system this will be in centimeters(CM), and for Imperial system, this will be in inches.
shipmentCrateMappings.crateHeight| Double | 10,3 | Optional | This is the height of package.  The unit of measurement will be based on the unit of measurement selected for your account. For metric system this will be in centimeters(CM), and for Imperial system, this will be in inches.
shipmentCrateMappings.shipmentlineitems.itemCd | String | 200 | Mandatory | This is the crate item code.
shipmentCrateMappings.shipmentlineitems.itemName | String | 255 | Optional | This is the crate item name.
shipmentCrateMappings.shipmentlineitems.itemPrice | Double |  | Mandatory | This is the crate item price.
shipmentCrateMappings.shipmentlineitems.itemQuantity | Double | 10 | Mandatory | This is the crate item quantity.
shipmentCrateMappings.shipmentlineitems.itemType | String | 100 | Optional | This is the crate item type.
shipmentCrateMappings.shipmentlineitems.itemWeight | Double | 10 | Optional | This is the crate item weight.
shipmentCrateMappings.shipmentlineitems.itemLength | Double | 10,3 | Optional | This is the length of item. The unit of measurement will be based on the unit of measurement selected for your account. For metric system this will be in centimeters(CM), and for Imperial system, this will be in inches.
shipmentCrateMappings.shipmentlineitems.itemBreadth| Double | 10,3 | Optional | This is the width of item.  The unit of measurement will be based on the unit of measurement selected for your account. For metric system this will be in centimeters(CM), and for Imperial system, this will be in inches.
shipmentCrateMappings.shipmentlineitems.itemHeight| Double | 10,3 | Optional | This is the height of item.  The unit of measurement will be based on the unit of measurement selected for your account. For metric system this will be in centimeters(CM), and for Imperial system, this will be in inches.


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
    "priority": "PRIORITY3",
    "serviceType":"Premium",
    "paymentType": "Prepaid",
    "packageValue": "5000",
    "shippingCost":"50",
    "numberOfItems": 1,
    "partialDeliveryAllowedFl": "Y",
    "returnAllowedFl": "Y",
    "cancellationAllowedFl": "N",    
    "deliveryMediumUsername":"johnc",
    "deliverBranch": "Boston",
    "deliverServiceTime": "20",
    "deliverEndTimeWindow": "2016-07-18T10:31:00.000Z",
    "deliverStartTimeWindow": "2016-07-16T10:31:00.000Z",
    "deliveryType": "Groceries, Reefer",
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
        "crateCd": "CR041",
        "crateAmount":100.65,
        "crateType":"case",
        "noOfUnits":2,
        "crateWeight":10,
        "crateVolume":11,
        "crateLength":12,
        "crateBreadth":13,
        "crateHeight":14,
        "shipmentlineitems": [
          {
            "itemCd": "IT043",
            "itemName": "Chicken Soup 2X200gm",
            "itemPrice": 500,
            "itemQuantity": 1,
            "itemType": "soup",
            "itemWeight": 10,
            "itemVolume":11,
            "itemLength":12,
            "itemBreadth":13,
            "itemHeight":14
          },
          {
            "itemCd": "IT030",
            "itemName": "WholeBeanCoffee 6x1kg",
            "itemPrice": 400,
            "itemQuantity": 2,
            "itemType": "coffee",
            "itemWeight": 15,
            "itemVolume":16,
            "itemLength":17,
            "itemBreadth":18,
            "itemHeight":19
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
> Partial Success Response

```json
{
    "status": 207,
    "message": "Order(s) created partially",
    "data": [
        {
            "index": 0,
            "referenceId": "b032f3e9397343ba812f96370b92d592",
            "orderNumber": "ww1220",
            "shipmentOrderTypeCd": "DELIVER",
            "orderState": "FORWARD"
        },
        {
            "index": 1,
            "referenceId": "af7065ad4f3945a889ec25c323aa7b68",
            "orderNumber": "ww1244",
            "shipmentOrderTypeCd": "DELIVER",
            "orderState": "FORWARD"
        },
        {
            "index": 2,
            "referenceId": "a4e6dc610c854166a7957b9876aa4ce5",
            "orderNumber": "ww1234",
            "shipmentOrderTypeCd": "DELIVER",
            "orderState": "FORWARD"
        }
    ],
    "error": [
        {
            "index": 3,
            "orderNo": "ww1229",
            "orderState": "FORWARD",
            "shipmentOrderTypeCd": "DELIVER",
            "errorList": [
                {
                    "key": "deliverBranch",
                    "message": [
                        "Deliver Branch is invalid"
                    ]
                }
            ]
        }
    ],
    "hasError": true
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
orderNo | String | 100 | Mandatory |  Order Number.
awbNumber | String | 1000 | Optional | Airway Bill No associated with the Order.
shipmentOrderTypeCd | String | 40 | Mandatory | This is the order type code. BOTH for pickup & delivery leg order
autoAllocateFl| String | 50 | Optional | This can be "Y", "N", or "P". If set to "Y", the Order will be automatially allocated to the nearest Delivery Associate when it is created in the system. The behaviour of the auto assignment will be dependant on the configurations set in the 'Auto Assignment Profile' screen in your LogiNext Account settings screen. If "N", the Order will not be considered for auto assignment at the time of Order Creation<br>Pass this Flag as 'P' if you want to assign the newly created Order to an existing planned trip. This assignment event can impact the sequence of Order previously created for that trip.
orderState | String | 512 | Mandatory | This is the state of order. Ex: FORWARD
shipmentOrderDt | Date |  | Mandatory | This is the order Date. Format - YYYY-MM-DDTHH:MM:SS.SSSZ e.g. : 2016-07-01T11:18:00.000Z.
distributionCenter | String | 255 | Mandatory | Distribution center's name. The Distribution center is the Hub that is responsibile for fulfilling the Order. An Order can have different Pickup and Delivery leg branches, but will require a single Distribution center that is responsible for the fulfillment of the Order.
packageWeight | Double | 10,3 | Optional | Order package Weight. The unit of measurement will be based on the unit of measurement selected for your account. For metric system this will be in Kg, and for Imperial system, this will be in pounds.
packageVolume | Double | 10,3 | Optional | Order package Volume. The unit of measurement will be based on the unit of measurement selected for your account. For metric system this will be in cubic centimeters(CC), and for Imperial system, this will be in cubic inches(CBI).
packageLength | Double | 10,3 | Optional | Order package length. The unit of measurement will be based on the unit of measurement selected for your account. For metric system this will be in centimeters(CM), and for Imperial system, this will be in inches.
packageBreadth| Double | 10,3 | Optional | Order package breadth.  The unit of measurement will be based on the unit of measurement selected for your account. For metric system this will be in centimeters(CM), and for Imperial system, this will be in inches.
packageHeight| Double | 10,3 | Optional | Order package height.  The unit of measurement will be based on the unit of measurement selected for your account. For metric system this will be in centimeters(CM), and for Imperial system, this will be in inches.
priority | String | 16 | Optional | Order priority. If you wish to segregate Orders based on certain Order priorities, say you want to Route Plan for Orders based on their priorities, you can set up this field in the settings module and define the values that LogiNext should accept of this field. For example, this could be 'PRIORITY1', 'PRIORITY2', or 'PRIORITY3'.
serviceType | String | 16 | Optional | Order service type.
packageValue | Double | 10 | Optional | Order value.
shippingCost | Double | 10 | Optional | Shipping cost or delivery Fee for the Order.
numberOfItems | Integer | 20 | Optional | This is the number of crates.
paymentType | String | 40 | Mandatory | This is the mode of payment. Ex: COD - Cash On Delivery, Prepaid. If not passed, this will be defaulted to COD.
partialDeliveryAllowedFl | String | 50 | Optional | This field indicates if partial Delivery allowed. Ex: Y/N
returnAllowedFl | String | 1 | Optional | This field indicates if return is allowed. Ex: Y/N
cancellationAllowedFl | String | 1 | Optional | This field indicates if cancellation is allowed. Ex: Y/N
deliveryMediumUsername | STRING | | Optional |  If you know the Delivery Associate who will be fulfilling the Order, pass their usernam in this field.
deliverBranch | String | 255 | Mandatory | Name of delivery branch
deliverServiceTime | Integer | 11 | Mandatory | Deliver service time in mins.
deliverStartTimeWindow | Date |  | Mandatory | Deliver start time window. Format - YYYY-MM-DDTHH:MM:SS.SSSZ e.g. : 2018-07-01T11:18:00.000Z.
deliverEndTimeWindow | Date |  | Mandatory | Deliver end time window. Format - YYYY-MM-DDTHH:MM:SS.SSSZ. For example - 2018-07-01T11:18:00.000Z.
deliveryType | String | 40 | Optional | Order delivery type. For example - ‘Groceries’ for grocery type of Orders. Note that you can pass multiple Delivery Types in a comma separated manner in this API.
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
returnEmail | String | 100 | Conditional Mandatory | Return email address. This field in Non Mandatory in case Customer Profiling in ON.
returnPhoneNumber | String | 255 | Conditional Mandatory | Return Phone number. This field in Non Mandatory in case Customer Profiling in ON.
returnApartment | String | 512 | Conditional Mandatory | This is the return location's Apartment. This field in Non Mandatory in case Customer Profiling in ON.
returnStreetName | String | 512 | Conditional Mandatory | This is the pickup location's street name. This field in Non Mandatory in case Customer Profiling in ON.
returnLandmark | String | 512 | Optional | This is the pickup location's landmark.
returnLocality | String | 512 | Conditional Mandatory | This is the pickup location's locality. This field in Non Mandatory in case Customer Profiling in ON.
returnCity | String | 512 | Conditional Mandatory | This is the pickup location's city. This field in Non Mandatory in case Customer Profiling in ON.
returnState| String | 512 | Conditional Mandatory | This is the pickup location's state code. Please refer to the list of state codes provided in the "State Codes" section. This field in Non Mandatory in case Customer Profiling in ON.
returnCountry | String | 512 | Conditional Mandatory | This is the pickup location's country code. Please refer to the list of country codes provided in the "Country Codes" section. This field in Non Mandatory in case Customer Profiling in ON.
returnPinCode | String | 20 | Conditional Mandatory | Return Pincode. This field in Non Mandatory in case Customer Profiling in ON.
clientCode | String | 32 | Optional | With this field you can create Orders on behalf of your Customers(accounts) in LogiNext. An account is used to represent LogiNext’s Customer’s Customer.


#### Request Parameters (Crates)

Param | DataType | Length |  Required | Description
--------- | ------- | ------- | ---------- | ------------
shipmentCrateMappings | Array of objects |  | Optional | Order crates.
shipmentCrateMappings.crateCd | String | 128 | Mandatory | Crate code for a crate.
shipmentCrateMappings.crateAmount | Double |  | Mandatory | Crate amount for a crate.
shipmentCrateMappings.crateType | String | 100 | Mandatory | Crate type.
shipmentCrateMappings.noOfUnits | Integer | 10 | Mandatory | Number of items in the crate.
shipmentCrateMappings.crateVolume | Double | 10,3 | Optional | This is the volume of crate. The unit of measurement will be based on the unit of measurement selected for your account. For metric system this will be in CC, and for Imperial system, this will be in cubic inches.
shipmentCrateMappings.crateWeight | Double | 10,3 | Optional | This is the weight of crate. The unit of measurement will be based on the unit of measurement selected for your account. For metric system this will be in Kg, and for Imperial system, this will be in pounds.
shipmentCrateMappings.crateLength | Double | 10,3 | Optional | This is the length of package. The unit of measurement will be based on the unit of measurement selected for your account. For metric system this will be in centimeters(CM), and for Imperial system, this will be in inches.
shipmentCrateMappings.crateBreadth| Double | 10,3 | Optional | This is the width of package.  The unit of measurement will be based on the unit of measurement selected for your account. For metric system this will be in centimeters(CM), and for Imperial system, this will be in inches.
shipmentCrateMappings.crateHeight| Double | 10,3 | Optional | This is the height of package.  The unit of measurement will be based on the unit of measurement selected for your account. For metric system this will be in centimeters(CM), and for Imperial system, this will be in inches.
shipmentCrateMappings.shipmentlineitems.itemCd | String | 200 | Mandatory | Crate item code.
shipmentCrateMappings.shipmentlineitems.itemName | String | 255 | Optional | Crate item name.
shipmentCrateMappings.shipmentlineitems.itemPrice | Double |  | Mandatory | Crate item price.
shipmentCrateMappings.shipmentlineitems.itemQuantity | Double | 10 | Mandatory | Crate item quantity.
shipmentCrateMappings.shipmentlineitems.itemType | String | 100 | Optional | Crate item type.
shipmentCrateMappings.shipmentlineitems.itemWeight | Double | 10 | Optional | Crate item weight.
shipmentCrateMappings.shipmentlineitems.itemLength | Double | 10,3 | Optional | Crate item length. The unit of measurement will be based on the unit of measurement selected for your account. For metric system this will be in centimeters(CM), and for Imperial system, this will be in inches.
shipmentCrateMappings.shipmentlineitems.itemBreadth| Double | 10,3 | Optional | Crate item breadth.  The unit of measurement will be based on the unit of measurement selected for your account. For metric system this will be in centimeters(CM), and for Imperial system, this will be in inches.
shipmentCrateMappings.shipmentlineitems.itemHeight| Double | 10,3 | Optional | Crate item height.  The unit of measurement will be based on the unit of measurement selected for your account. For metric system this will be in centimeters(CM), and for Imperial system, this will be in inches.



### Create Point to Point 

> Definition

```json
https://api.loginextsolutions.com/ShipmentApp/mile/v2/create
```

> Request Body

```json


[
  {
    "orderNo": "PPPL0001",
    "autoAllocateFl":"N",
    "awbNumber": "435-16685675",
    "shipmentOrderDt": "2019-02-05T10:30:00.000Z",
    "shipmentOrderTypeCd": "DELIVER",
    "orderState": "FORWARD",
    "distributionCenter": "Lower Manhattan",
    "packageWeight":"10",
    "packageVolume": "4500",
    "packageLength":5,
    "packageBreadth":5,
    "packageHeight":5,
    "priority": "PRIORITY1",
    "preparationTime":20,
    "serviceType":"Premium",
    "paymentType": "Prepaid",
    "packageValue": "5000",
    "shippingCost":"50",
    "numberOfItems": 1,
    "partialDeliveryAllowedFl": "Y",
    "returnAllowedFl": "N",
    "cancellationAllowedFl": "Y",    
    "deliverServiceTime": "20",
    "deliverEndTimeWindow": "2018-07-18T10:31:00.000Z",
    "deliverStartTimeWindow": "2018-07-16T10:31:00.000Z",
    "deliveryType": "Groceries, Reefer",
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
    "deliverNotes": "Leave it with the neighbour",
    "pickupServiceTime": "50",
    "pickupStartTimeWindow": "2018-07-16T14:24:00.000Z",
    "pickupEndTimeWindow": "2018-07-17T14:24:00.000Z",
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
    "pickupNotes": "Don't ring the doorbell",
    "clientCode": "Salestap",
    "shipmentCrateMappings": [
      {
        "crateCd": "CR041",
        "crateAmount":100.65,
        "crateType":"case",
        "noOfUnits":2,
        "crateWeight":10,
        "crateVolume":11,
        "crateLength":12,
        "crateBreadth":13,
        "crateHeight":14,
        "shipmentlineitems": [
          {
            "itemCd": "IT043",
            "itemName": "Chicken Soup 2X200gm",
            "itemPrice": 500,
            "itemQuantity": 1,
            "itemType": "soup",
            "itemWeight": 10,
            "itemVolume":11,
            "itemLength":12,
            "itemBreadth":13,
            "itemHeight":14
          },
          {
            "itemCd": "IT030",
            "itemName": "WholeBeanCoffee 6x1kg",
            "itemPrice": 400,
            "itemQuantity": 2,
            "itemType": "coffee",
            "itemWeight": 15,
            "itemVolume":16,
            "itemLength":17,
            "itemBreadth":18,
            "itemHeight":19
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
    "message": "",
    "moreResultsExists": false,
    "data": [
        {
            "index": 0,
            "referenceId": "eb7a0e88612c4e888f04b98387099fd1",
            "orderNumber": "PPPL0001",
            "shipmentOrderTypeCd": "DELIVER",
            "orderState": "FORWARD"
        }
    ],
    "hasError": false
}

```
> Partial Success Response

```json
{
    "status": 207,
    "message": "Order(s) created partially",
    "data": [
        {
            "index": 0,
            "referenceId": "b032f3e9397343ba812f96370b92d592",
            "orderNumber": "ww1220",
            "shipmentOrderTypeCd": "DELIVER",
            "orderState": "FORWARD"
        },
        {
            "index": 1,
            "referenceId": "af7065ad4f3945a889ec25c323aa7b68",
            "orderNumber": "ww1244",
            "shipmentOrderTypeCd": "DELIVER",
            "orderState": "FORWARD"
        },
        {
            "index": 2,
            "referenceId": "a4e6dc610c854166a7957b9876aa4ce5",
            "orderNumber": "ww1234",
            "shipmentOrderTypeCd": "DELIVER",
            "orderState": "FORWARD"
        }
    ],
    "error": [
        {
            "index": 3,
            "orderNo": "ww1229",
            "orderState": "FORWARD",
            "shipmentOrderTypeCd": "DELIVER",
            "errorList": [
                {
                    "key": "deliverBranch",
                    "message": [
                        "Deliver Branch is invalid"
                    ]
                }
            ]
        }
    ],
    "hasError": true
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
            "orderNo": "PPPL0001",
            "orderState": "FORWARD",
            "shipmentOrderTypeCd": "DELIVER",
            "errorList": [
                {
                    "key": "deliveryType",
                    "message": [
                        "DeliveryType is invalid"
                    ]
                },
                {
                    "key": "distributionCenter",
                    "message": [
                        "Distribution Center is invalid"
                    ]
                }
            ]
        }
    ],
    "hasError": true
}

```

With This API you can create Orders that have to be Pickedup from and Delivered directly to Customer locations without being dropped of at a branch or Distribution Center in between.

You will have to pass the Pickup and Deliver Customer details in the API to create a Point to Point type of Order.

API Type: Tier 1 API



#### Request

<span class="post">POST</span>`https://api.loginextsolutions.com/ShipmentApp/mile/v2/create`


#### Request Parameters

Param | DataType | Length |  Required | Description
--------- | ------- | ------- | ---------- | ------------
orderNo | String | 100 | Mandatory |  This is the order No.
awbNumber | String | 1000 | Optional | This is the airway Bill No.
shipmentOrderTypeCd | String | 40 | Mandatory | This is the order type code. This will be DELIVER for a point to point type of Order.
autoAllocateFl| String | 50 | Optional |This can be "Y", "N", or "P". If set to "Y", the Order will be automatially allocated to the nearest Delivery Associate when it is created in the system. The behaviour of the auto assignment will be dependant on the configurations set in the 'Auto Assignment Profile' screen in your LogiNext Account settings screen. If "N", the Order will not be considered for auto assignment at the time of Order Creation<br>Pass this Flag as 'P' if you want to assign the newly created Order to an existing planned trip. This assignment event can impact the sequence of Order previously created for that trip.
orderState | String | 512 | Mandatory | This is the state of order. Ex: FORWARD
shipmentOrderDt | Date |  | Mandatory | This is the order Date. Format - YYYY-MM-DDTHH:MM:SS.SSSZ e.g. : 2016-07-01T11:18:00.000Z.
distributionCenter | String | 255 | Mandatory | Distribution center's name. The Distribution center is the Hub that is responsibile for fulfilling the Order. An Order can have different Pickup and Delivery leg branches, but will require a single Distribution center that is responsible for the fulfillment of the Order.
packageWeight | Double | 10,3 | Optional | This is the weight of package. The unit of measurement will be based on the unit of measurement selected for your account. For metric system this will be in Kg, and for Imperial system, this will be in pounds.
packageVolume | Double | 10,3 | Optional | This is the volume of package.The unit of measurement will be based on the unit of measurement selected for your account. For metric system this will be in cubic centimeters(CC), and for Imperial system, this will be in cubic inches(CBI).
packageLength | Double | 10,3 | Optional | This is the length of package. The unit of measurement will be based on the unit of measurement selected for your account. For metric system this will be in centimeters(CM), and for Imperial system, this will be in inches.
packageBreadth| Double | 10,3 | Optional | This is the width of package.  The unit of measurement will be based on the unit of measurement selected for your account. For metric system this will be in centimeters(CM), and for Imperial system, this will be in inches.
packageHeight| Double | 10,3 | Optional | This is the height of package.  The unit of measurement will be based on the unit of measurement selected for your account. For metric system this will be in centimeters(CM), and for Imperial system, this will be in inches.
priority | String | 16 | Optional |This is the priority of the current Order. If you wish to segregate Orders based on certain Order priorities, say you want to Route Plan for Orders based on their priorities, you can set up this field in the settings module and define the values that LogiNext should accept of this field. For example, this could be 'PRIORITY1', 'PRIORITY2', or 'PRIORITY3'.
preparationTime | Double | 10,3 | Optional | Order preparation time.
serviceType | String | 16 | Optional | This is the service type of the Order.
packageValue | Double | 10 | Optional | This is the value of package
shippingCost | Double | 10 | Optional | Shipping cost or delivery Fee for the Order.
numberOfItems | Integer | 20 | Optional | This is the number of crates
paymentType | String | 40 | Mandatory | This is the mode of payment. Ex: COD - Cash On Delivery, Prepaid. If not passed, this will be defaulted to COD.
partialDeliveryAllowedFl | String | 50 | Optional | This field indicates if partial Delivery allowed. Ex: Y/N
returnAllowedFl | String | 1 | Optional | This field indicates if return is allowed. Ex: Y/N
cancellationAllowedFl | String | 1 | Optional | This field indicates if cancellation is allowed. Ex: Y/N
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
deliverServiceTime | Integer | 11 | Mandatory | Deliver service time in mins.
deliverStartTimeWindow | Date |  | Mandatory | Deliver start time window. Format - YYYY-MM-DDTHH:MM:SS.SSSZ e.g. : 2018-07-01T11:18:00.000Z.
deliverEndTimeWindow | Date |  | Mandatory | Deliver end time window. Format - YYYY-MM-DDTHH:MM:SS.SSSZ. For example - 2018-07-01T11:18:00.000Z.
deliveryType | String | 40 | Optional | Order delivery type. For example - ‘Groceries’ for grocery type of Orders. Note that you can pass multiple Delivery Types in a comma separated manner in this API.
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
clientCode | String | 32 | Optional | With this field you can create Orders on behalf of your Customers(accounts) in LogiNext. An account is used to represent LogiNext’s Customer’s Customer.


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
hipmentCrateMappings.shipmentlineitems.itemWeight | Double | 10 | Optional | Item weight
shipmentCrateMappings.shipmentlineitems.itemLength | Double | 10,3 | Optional | This is the length of item. The unit of measurement will be based on the unit of measurement selected for your account. For metric system this will be in centimeters(CM), and for Imperial system, this will be in inches.
shipmentCrateMappings.shipmentlineitems.itemBreadth| Double | 10,3 | Optional | This is the width of item.  The unit of measurement will be based on the unit of measurement selected for your account. For metric system this will be in centimeters(CM), and for Imperial system, this will be in inches.
shipmentCrateMappings.shipmentlineitems.itemHeight| Double | 10,3 | Optional | This is the height of item.  The unit of measurement will be based on the unit of measurement selected for your account. For metric system this will be in centimeters(CM), and for Imperial system, this will be in inches.


### Create Multi Leg E2E Order

> Definition

```json
 https://api.loginextsolutions.com/ShipmentApp/middlemile/shipment/order/api/create
```

> Request Body

```json


[
  {
    "orderNo": "GR432U5",
    "awbNumber": "435-16685675",
    "shipmentOrderTypeCd": "ALLMILE",
    "orderState": "FORWARD",
    "autoAllocateFl": "N",
    "shipmentOrderDt": "2016-07-15T10:30:00.000Z",
    "distributionCenter": "Down Town Chicago",
    "originBranchName" :"Houston",
    "destinationBranchName" : "Boston",
    "routeConfigurationName": "Houston-Boston",
    "nextBranchName":"Cupertino",
    "nextBranchServiceTime": 5,
    "nextBranchStartTimeWindow" : "2016-07-15T10:30:00.000Z",
    "nextBranchEndTimeWindow": "2016-07-15T10:30:00.000Z",
    "deliveryType": "Groceries",
    "serviceTypeCd": "Economy",
    "packageWeight":"10",
    "packageVolume": "4500",
    "paymentType": "Prepaid",
    "packageValue": "5000",
    "shippingCost":"50",
    "numberOfItems": 1,
    "partialDeliveryAllowedFl": "Y",
    "cancellationAllowedFl": "N",    
    "deliverServiceTime": "20",
    "deliverEndTimeWindow": "2016-07-18T10:31:00.000Z",
    "deliverStartTimeWindow": "2016-07-16T10:31:00.000Z",
    "deliveryLocationType":"Home",
    "deliverEmail":"m.richardson@testmail.com",
    "deliverPhoneNumber":"9891234567",
    "deliverAccountCode": "Matt001",
    "deliverAddressId": "home",
    "deliverAccountName": "Mathew Richardson",
    "deliverApartment": "201",
    "deliverStreetName": "E Randolph St",
    "deliverLandmark": "Opp. Chiptole",
    "deliverLocality": "Down Town Chicago",
    "deliverCity": "Chicago",
    "deliverState": "IL",
    "deliverCountry": "USA",
    "deliverPinCode": "60602",
    "deliverLatitude":41.882702,
    "deliverLongitude":-87.619392,   
    "deliverAddressTimezone":"America/Chicago",
    "pickupServiceTime": "50",
    "pickupStartTimeWindow": "2019-07-16T14:24:00.000Z",
    "pickupEndTimeWindow": "2019-07-17T14:24:00.000Z",
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
            "orderNumber": "ww1223"
        }
    ],
    "hasError": false
}

```
> Partial Success Response

```json
{
    "status": 207,
    "message": "Order(s) created partially",
    "data": [
        {
            "index": 0,
            "referenceId": "b032f3e9397343ba812f96370b92d592",
            "orderNumber": "ww1220"
        }
    ],
    "error": [
        {
            "index": 3,
            "orderNo": "ww1229"
            "errorList": [
                {
                    "key": "deliverBranch",
                    "message": [
                        "Deliver Branch is invalid"
                    ]
                }
            ]
        }
    ],
    "hasError": true
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

With This API you can create All MIle type of Orders that can have multiple legs in between the Origin and Destination.


API Type: Tier 1 API



#### Request

<span class="post">POST</span>`https://api.loginextsolutions.com/ShipmentApp/middlemile/shipment/order/api/create`


#### Request Parameters

Param | DataType | Length |  Required | Description
--------- | ------- | ------- | ---------- | ------------
orderNo | String | 100 | Mandatory |  This is the order No.
awbNumber | String | 100 | Optional | This is the airway Bill No.
shipmentOrderTypeCd | String | 40 | Mandatory | This is the order type code. With this API you can create 'FM'(First Mile), 'LM'(Last Mile), or 'ALLMILE' type of Orders. 'ALLMILE' Orders are Orders that have more than one leg of movements.
autoAllocateFl | String | 50 | Optional | This can be "Y", "N", or "P". If set to "Y", the Order will be automatially allocated to the nearest Delivery Associate when it is created in the system. The behaviour of the auto assignment will be dependant on the configurations set in the 'Auto Assignment Profile' screen in your LogiNext Account settings screen. If "N", the Order will not be considered for auto assignment at the time of Order Creation.<br>Pass this Flag as 'P' if you want to assign the newly created Order to an existing planned trip. This assignment event can impact the sequence of Order previously created for that trip.
orderState | String | 512 | Mandatory | This is the state of order. Ex: FORWARD
shipmentOrderDt | Date |  | Mandatory | This is the order Date. Format - YYYY-MM-DDTHH:MM:SS.SSSZ e.g. : 2016-07-01T11:18:00.000Z.
originBranchName |  String | 255 | Optional | This is the Origin branch of the Order
destinationBranchName |  String | 255 | Optional  | This is the Destination branch of the Order
routeConfigurationName |  String | 255 | Optional | This is the route of the Order
deliveryType | String | 40 | Conditional Mandatory | Order delivery type. For example - ‘Groceries’ for grocery type of Orders. This field is Mandatory if you are creating an 'ALLMILE' type of Order.
serviceTypeCd |  String | 255 | Conditional Mandatory | This is the Service type of the Order. You can have different service types depending on your operations. For example - Orders having a 'Premium' service type can have shorter SLAs than Orders having 'Normal' service types. This field is Mandatory if you are creating an 'ALLMILE' type of Order.
distributionCenter | String | 255 | Mandatory | Distribution center's name. The Distribution center is the Hub that is responsibile for fulfilling the Order. An Order can have different Pickup and Delivery leg branches, but will require a single Distribution center that is responsible for the fulfillment of the Order.
packageWeight | Double | 10,3 | Optional | This is the weight of package. The unit of measurement will be based on the unit of measurement selected for your account. For metric system this will be in Kg, and for Imperial system, this will be in pounds.
packageVolume | Double | 10,3 | Optional | This is the volume of package.The unit of measurement will be based on the unit of measurement selected for your account. For metric system this will be in cubic centimeters(CC), and for Imperial system, this will be in cubic inches(CBI).
packageLength | Double | 10,3 | Optional | This is the length of package. The unit of measurement will be based on the unit of measurement selected for your account. For metric system this will be in centimeters(CM), and for Imperial system, this will be in inches.
packageBreadth| Double | 10,3 | Optional | This is the width of package.  The unit of measurement will be based on the unit of measurement selected for your account. For metric system this will be in centimeters(CM), and for Imperial system, this will be in inches.
packageHeight| Double | 10,3 | Optional | This is the height of package.  The unit of measurement will be based on the unit of measurement selected for your account. For metric system this will be in centimeters(CM), and for Imperial system, this will be in inches.
priority | String | 16 | Optional |This is the priority of the current Order. If you wish to segregate Orders based on certain Order priorities, say you want to Route Plan for Orders based on their priorities, you can set up this field in the settings module and define the values that LogiNext should accept of this field. For example, this could be 'PRIORITY1', 'PRIORITY2', or 'PRIORITY3'.
packageValue | Double | 10 | Optional | This is the value of package
shippingCost | Double | 10 | Optional | Shipping cost or delivery Fee for the Order.
numberOfItems | Integer | 20 | Optional | This is the number of crates
paymentType | String | 40 | Mandatory | This is the mode of payment. Ex: COD - Cash On Delivery, Prepaid. If not passed, this will be defaulted to COD.
partialDeliveryAllowedFl | String | 50 | Optional | This field indicates if partial Delivery allowed. Ex: Y/N
returnAllowedFl | String | 1 | Optional | This field indicates if return is allowed. Ex: Y/N
cancellationAllowedFl | String | 1 | Optional | This field indicates if cancellation is allowed. Ex: Y/N
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
deliverServiceTime | Integer | 11 | Mandatory | Deliver service time in mins.
deliverStartTimeWindow | Date |  | Mandatory | Deliver start time window. Format - YYYY-MM-DDTHH:MM:SS.SSSZ e.g. : 2018-07-01T11:18:00.000Z.
deliverEndTimeWindow | Date |  | Mandatory | Deliver end time window. Format - YYYY-MM-DDTHH:MM:SS.SSSZ. For example - 2018-07-01T11:18:00.000Z.
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
clientCode | String | 32 | Optional | With this field you can create Orders on behalf of your Customers(accounts) in LogiNext. An account is used to represent LogiNext’s Customer’s Customer.


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
hipmentCrateMappings.shipmentlineitems.itemWeight | Double | 10 | Optional | Item weight
shipmentCrateMappings.shipmentlineitems.itemLength | Double | 10,3 | Optional | This is the length of item. The unit of measurement will be based on the unit of measurement selected for your account. For metric system this will be in centimeters(CM), and for Imperial system, this will be in inches.
shipmentCrateMappings.shipmentlineitems.itemBreadth| Double | 10,3 | Optional | This is the width of item.  The unit of measurement will be based on the unit of measurement selected for your account. For metric system this will be in centimeters(CM), and for Imperial system, this will be in inches.
shipmentCrateMappings.shipmentlineitems.itemHeight| Double | 10,3 | Optional | This is the height of item.  The unit of measurement will be based on the unit of measurement selected for your account. For metric system this will be in centimeters(CM), and for Imperial system, this will be in inches.




### Create Deliver E2E Order

> Definition

```json
 https://api.loginextsolutions.com/ShipmentApp/middlemile/shipment/order/api/create
```

> Request Body

```json


[
  {
    "orderNo": "GR432U5",
    "awbNumber": "435-16685675",
    "shipmentOrderTypeCd": "LM",
    "orderState": "FORWARD",
    "autoAllocateFl": "N",
    "shipmentOrderDt": "2019-07-15T10:30:00.000Z",
    "distributionCenter": "Down Town Chicago",
    "serviceTypeCd": "Economy",
    "packageWeight":"10",
    "packageVolume": "4500",
    "paymentType": "Prepaid",
    "packageValue": "5000",
    "shippingCost":"50",
    "numberOfItems": 1,
    "partialDeliveryAllowedFl": "Y",
    "cancellationAllowedFl": "N",    
    "deliverBranch":"Boston Main Hub",
    "deliverServiceTime": "20",
    "deliverEndTimeWindow": "2019-07-18T10:31:00.000Z",
    "deliverStartTimeWindow": "2019-07-16T10:31:00.000Z",
    "deliveryType": "Groceries, Reefer",
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
    "deliverNotes": "Leave it with the neighbour",
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
            "orderNumber": "ww1223"
        }
    ],
    "hasError": false
}

```
> Partial Success Response

```json
{
    "status": 207,
    "message": "Order(s) created partially",
    "data": [
        {
            "index": 0,
            "referenceId": "b032f3e9397343ba812f96370b92d592",
            "orderNumber": "ww1220"
        }
    ],
    "error": [
        {
            "index": 3,
            "orderNo": "ww1229"
            "errorList": [
                {
                    "key": "deliverBranch",
                    "message": [
                        "Deliver Branch is invalid"
                    ]
                }
            ]
        }
    ],
    "hasError": true
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
           "errorList": [
               {
                   "key": "returnBranch",
                   "message": [
                       "Deliver Branch name is mandatory."
                   ]
               }
           ]
       }
   ],
   "hasError": true
}

```

With This API you can create a Deliver Order in All MIle that has a single leg between a Hub and a Deliver location.


API Type: Tier 1 API



#### Request

<span class="post">POST</span>`https://api.loginextsolutions.com/ShipmentApp/middlemile/shipment/order/api/create`


#### Request Parameters

Param | DataType | Length |  Required | Description
--------- | ------- | ------- | ---------- | ------------
orderNo | String | 100 | Mandatory |  This is the order No.
awbNumber | String | 100 | Optional | This is the airway Bill No.
shipmentOrderTypeCd | String | 40 | Mandatory | This is the order type code. With this API you can create 'FM'(First Mile), 'LM'(Last Mile), or 'ALLMILE' type of Orders. 'ALLMILE' Orders are Orders that have more than one leg of movements.
autoAllocateFl | String | 50 | Optional | This can be "Y", "N", or "P". If set to "Y", the Order will be automatially allocated to the nearest Delivery Associate when it is created in the system. The behaviour of the auto assignment will be dependant on the configurations set in the 'Auto Assignment Profile' screen in your LogiNext Account settings screen. If "N", the Order will not be considered for auto assignment at the time of Order Creation.<br>Pass this Flag as 'P' if you want to assign the newly created Order to an existing planned trip. This assignment event can impact the sequence of Order previously created for that trip.
orderState | String | 512 | Mandatory | This is the state of order. Ex: FORWARD
shipmentOrderDt | Date |  | Mandatory | This is the order Date. Format - YYYY-MM-DDTHH:MM:SS.SSSZ e.g. : 2016-07-01T11:18:00.000Z.
serviceTypeCd |  String | 255 | Conditional Mandatory | This is the Service type of the Order. You can have different service types depending on your operations. For example - Orders having a 'Premium' service type can have shorter SLAs than Orders having 'Normal' service types. This field is Mandatory if you are creating an 'ALLMILE' type of Order.
distributionCenter | String | 255 | Mandatory | Distribution center's name. The Distribution center is the Hub that is responsibile for fulfilling the Order. An Order can have different Pickup and Delivery leg branches, but will require a single Distribution center that is responsible for the fulfillment of the Order.
packageWeight | Double | 10,3 | Optional | This is the weight of package. The unit of measurement will be based on the unit of measurement selected for your account. For metric system this will be in Kg, and for Imperial system, this will be in pounds.
packageVolume | Double | 10,3 | Optional | This is the volume of package.The unit of measurement will be based on the unit of measurement selected for your account. For metric system this will be in cubic centimeters(CC), and for Imperial system, this will be in cubic inches(CBI).
packageLength | Double | 10,3 | Optional | This is the length of package. The unit of measurement will be based on the unit of measurement selected for your account. For metric system this will be in centimeters(CM), and for Imperial system, this will be in inches.
packageBreadth| Double | 10,3 | Optional | This is the width of package.  The unit of measurement will be based on the unit of measurement selected for your account. For metric system this will be in centimeters(CM), and for Imperial system, this will be in inches.
packageHeight| Double | 10,3 | Optional | This is the height of package.  The unit of measurement will be based on the unit of measurement selected for your account. For metric system this will be in centimeters(CM), and for Imperial system, this will be in inches.
priority | String | 16 | Optional |This is the priority of the current Order. If you wish to segregate Orders based on certain Order priorities, say you want to Route Plan for Orders based on their priorities, you can set up this field in the settings module and define the values that LogiNext should accept of this field. For example, this could be 'PRIORITY1', 'PRIORITY2', or 'PRIORITY3'.
packageValue | Double | 10 | Optional | This is the value of package
shippingCost | Double | 10 | Optional | Shipping cost or delivery Fee for the Order.
numberOfItems | Integer | 20 | Optional | This is the number of crates
paymentType | String | 40 | Mandatory | This is the mode of payment. Ex: COD - Cash On Delivery, Prepaid. If not passed, this will be defaulted to COD.
partialDeliveryAllowedFl | String | 50 | Optional | This field indicates if partial Delivery allowed. Ex: Y/N
returnAllowedFl | String | 1 | Optional | This field indicates if return is allowed. Ex: Y/N
cancellationAllowedFl | String | 1 | Optional | This field indicates if cancellation is allowed. Ex: Y/N
deliverServiceTime | Integer | 11 | Mandatory | Deliver service time in mins.
deliverStartTimeWindow | Date |  | Mandatory | Deliver start time window. Format - YYYY-MM-DDTHH:MM:SS.SSSZ e.g. : 2018-07-01T11:18:00.000Z.
deliverEndTimeWindow | Date |  | Mandatory | Deliver end time window. Format - YYYY-MM-DDTHH:MM:SS.SSSZ. For example - 2018-07-01T11:18:00.000Z.
deliveryType | String | 40 | Optional | Order delivery type. For example - ‘Groceries’ for grocery type of Orders. Note that you can pass multiple Delivery Types in a comma separated manner in this API.
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
deliverNotes | String | 512 | Optional | Additional delivery comments associated with the order.
clientCode | String | 32 | Optional | With this field you can create Orders on behalf of your Customers(accounts) in LogiNext. An account is used to represent LogiNext’s Customer’s Customer.


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
hipmentCrateMappings.shipmentlineitems.itemWeight | Double | 10 | Optional | Item weight
shipmentCrateMappings.shipmentlineitems.itemLength | Double | 10,3 | Optional | This is the length of item. The unit of measurement will be based on the unit of measurement selected for your account. For metric system this will be in centimeters(CM), and for Imperial system, this will be in inches.
shipmentCrateMappings.shipmentlineitems.itemBreadth| Double | 10,3 | Optional | This is the width of item.  The unit of measurement will be based on the unit of measurement selected for your account. For metric system this will be in centimeters(CM), and for Imperial system, this will be in inches.
shipmentCrateMappings.shipmentlineitems.itemHeight| Double | 10,3 | Optional | This is the height of item.  The unit of measurement will be based on the unit of measurement selected for your account. For metric system this will be in centimeters(CM), and for Imperial system, this will be in inches.


### Create Pickup E2E Order

> Definition

```json
 https://api.loginextsolutions.com/ShipmentApp/middlemile/shipment/order/api/create
```

> Request Body

```json


[
  {
    "orderNo": "GR432U5",
    "awbNumber": "435-16685675",
    "shipmentOrderTypeCd": "FM",
    "orderState": "FORWARD",
    "autoAllocateFl": "N",
    "shipmentOrderDt": "2019-07-15T10:30:00.000Z",
    "distributionCenter": "Down Town Chicago",
    "deliveryType": "Groceries",
    "serviceTypeCd": "Economy",
    "packageWeight":"10",
    "packageVolume": "4500",
    "paymentType": "Prepaid",
    "packageValue": "5000",
    "shippingCost":"50",
    "numberOfItems": 1,
    "partialDeliveryAllowedFl": "Y",
    "cancellationAllowedFl": "N",    
    "pickupBranch": "Down Town Chicago",
    "pickupServiceTime": "50",
    "pickupStartTimeWindow": "2019-07-16T14:24:00.000Z",
    "pickupEndTimeWindow": "2019-07-17T14:24:00.000Z",
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
    "pickupNotes": "PickedUp",
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
            "orderNumber": "ww1223"
        }
    ],
    "hasError": false
}

```
> Partial Success Response

```json
{
    "status": 207,
    "message": "Order(s) created partially",
    "data": [
        {
            "index": 0,
            "referenceId": "b032f3e9397343ba812f96370b92d592",
            "orderNumber": "ww1220"
        }
    ],
    "error": [
        {
            "index": 3,
            "orderNo": "ww1229"
            "errorList": [
                {
                    "key": "deliverBranch",
                    "message": [
                        "Deliver Branch is invalid"
                    ]
                }
            ]
        }
    ],
    "hasError": true
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

With This API you can create a Pickup Order in All MIle that has a single leg between a pickup location and a Hub.


API Type: Tier 1 API



#### Request

<span class="post">POST</span>`https://api.loginextsolutions.com/ShipmentApp/middlemile/shipment/order/api/create`


#### Request Parameters

Param | DataType | Length |  Required | Description
--------- | ------- | ------- | ---------- | ------------
orderNo | String | 100 | Mandatory |  This is the order No.
awbNumber | String | 100 | Optional | This is the airway Bill No.
shipmentOrderTypeCd | String | 40 | Mandatory | This is the order type code. With this API you can create 'FM'(First Mile), 'LM'(Last Mile), or 'ALLMILE' type of Orders. 'ALLMILE' Orders are Orders that have more than one leg of movements.
autoAllocateFl | String | 50 | Optional | This can be "Y", "N", or "P". If set to "Y", the Order will be automatially allocated to the nearest Delivery Associate when it is created in the system. The behaviour of the auto assignment will be dependant on the configurations set in the 'Auto Assignment Profile' screen in your LogiNext Account settings screen. If "N", the Order will not be considered for auto assignment at the time of Order Creation.<br>Pass this Flag as 'P' if you want to assign the newly created Order to an existing planned trip. This assignment event can impact the sequence of Order previously created for that trip.
orderState | String | 512 | Mandatory | This is the state of order. Ex: FORWARD
shipmentOrderDt | Date |  | Mandatory | This is the order Date. Format - YYYY-MM-DDTHH:MM:SS.SSSZ e.g. : 2016-07-01T11:18:00.000Z.
serviceTypeCd |  String | 255 | Conditional Mandatory | This is the Service type of the Order. You can have different service types depending on your operations. For example - Orders having a 'Premium' service type can have shorter SLAs than Orders having 'Normal' service types. This field is Mandatory if you are creating an 'ALLMILE' type of Order.
distributionCenter | String | 255 | Mandatory | Distribution center's name. The Distribution center is the Hub that is responsibile for fulfilling the Order. An Order can have different Pickup and Delivery leg branches, but will require a single Distribution center that is responsible for the fulfillment of the Order.
packageWeight | Double | 10,3 | Optional | This is the weight of package. The unit of measurement will be based on the unit of measurement selected for your account. For metric system this will be in Kg, and for Imperial system, this will be in pounds.
packageVolume | Double | 10,3 | Optional | This is the volume of package.The unit of measurement will be based on the unit of measurement selected for your account. For metric system this will be in cubic centimeters(CC), and for Imperial system, this will be in cubic inches(CBI).
packageLength | Double | 10,3 | Optional | This is the length of package. The unit of measurement will be based on the unit of measurement selected for your account. For metric system this will be in centimeters(CM), and for Imperial system, this will be in inches.
packageBreadth| Double | 10,3 | Optional | This is the width of package.  The unit of measurement will be based on the unit of measurement selected for your account. For metric system this will be in centimeters(CM), and for Imperial system, this will be in inches.
packageHeight| Double | 10,3 | Optional | This is the height of package.  The unit of measurement will be based on the unit of measurement selected for your account. For metric system this will be in centimeters(CM), and for Imperial system, this will be in inches.
priority | String | 16 | Optional |This is the priority of the current Order. If you wish to segregate Orders based on certain Order priorities, say you want to Route Plan for Orders based on their priorities, you can set up this field in the settings module and define the values that LogiNext should accept of this field. For example, this could be 'PRIORITY1', 'PRIORITY2', or 'PRIORITY3'.
packageValue | Double | 10 | Optional | This is the value of package
shippingCost | Double | 10 | Optional | Shipping cost or delivery Fee for the Order.
numberOfItems | Integer | 20 | Optional | This is the number of crates
paymentType | String | 40 | Mandatory | This is the mode of payment. Ex: COD - Cash On Delivery, Prepaid. If not passed, this will be defaulted to COD.
partialDeliveryAllowedFl | String | 50 | Optional | This field indicates if partial Delivery allowed. Ex: Y/N
returnAllowedFl | String | 1 | Optional | This field indicates if return is allowed. Ex: Y/N
cancellationAllowedFl | String | 1 | Optional | This field indicates if cancellation is allowed. Ex: Y/N
pickupBranch | String | 255 | Mandatory | Pickup Branch of the Order.
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
clientCode | String | 32 | Optional | With this field you can create Orders on behalf of your Customers(accounts) in LogiNext. An account is used to represent LogiNext’s Customer’s Customer.


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
hipmentCrateMappings.shipmentlineitems.itemWeight | Double | 10 | Optional | Item weight
shipmentCrateMappings.shipmentlineitems.itemLength | Double | 10,3 | Optional | This is the length of item. The unit of measurement will be based on the unit of measurement selected for your account. For metric system this will be in centimeters(CM), and for Imperial system, this will be in inches.
shipmentCrateMappings.shipmentlineitems.itemBreadth| Double | 10,3 | Optional | This is the width of item.  The unit of measurement will be based on the unit of measurement selected for your account. For metric system this will be in centimeters(CM), and for Imperial system, this will be in inches.
shipmentCrateMappings.shipmentlineitems.itemHeight| Double | 10,3 | Optional | This is the height of item.  The unit of measurement will be based on the unit of measurement selected for your account. For metric system this will be in centimeters(CM), and for Imperial system, this will be in inches.


### Create Point to Point E2E Order

> Definition

```json
 https://api.loginextsolutions.com/ShipmentApp/middlemile/shipment/order/api/create
```

> Request Body

```json


[
  {
    "orderNo": "ORD876543456",
    "awbNumber": "AWS-125432",
    "shipmentOrderTypeCd": "LM",
    "orderState": "FORWARD",
    "autoAllocateFl": "Y",
    "shipmentOrderDt": "2020-02-19T09:30:00.000Z",
    "distributionCenter": "Middle Mile Main Hub",
    "serviceTypeCd": "Typgcvb b bjb jjhgkck",
    "packageWeight": "10.5",
    "packageVolume": "450.12",
    "paymentType": "COD",
    "packageValue": "5000",
    "shippingCost":"50",
    "partialDeliveryAllowedFl": "N",
    "cancellationAllowedFl": "N",
    "deliverServiceTime": "20",
    "deliverEndTimeWindow": "2016-07-18T10:31:00.000Z",
    "deliverStartTimeWindow": "2016-07-16T10:31:00.000Z",
    "deliveryLocationType":"Home",
    "deliverEmail":"m.richardson@testmail.com",
    "deliverPhoneNumber":"9891234567",
    "deliverAccountCode": "Matt001",
    "deliverAddressId": "home",
    "deliverAccountName": "Mathew Richardson",
    "deliverApartment": "201",
    "deliverStreetName": "E Randolph St",
    "deliverLandmark": "Opp. Chiptole",
    "deliverLocality": "Down Town Chicago",
    "deliverCity": "Chicago",
    "deliverState": "IL",
    "deliverCountry": "USA",
    "deliverPinCode": "60602",
    "deliverLatitude":41.882702,
    "deliverLongitude":-87.619392,   
    "deliverAddressTimezone":"America/Chicago",  
    "deliverBranch": "East Manhattan",
    "deliverNotes": "Delivered",
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
            "orderNumber": "ww1223"
        }
    ],
    "hasError": false
}

```
> Partial Success Response

```json
{
    "status": 207,
    "message": "Order(s) created partially",
    "data": [
        {
            "index": 0,
            "referenceId": "b032f3e9397343ba812f96370b92d592",
            "orderNumber": "ww1220"
        }
    ],
    "error": [
        {
            "index": 3,
            "orderNo": "ww1229"
            "errorList": [
                {
                    "key": "deliverBranch",
                    "message": [
                        "Deliver Branch is invalid"
                    ]
                }
            ]
        }
    ],
    "hasError": true
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

With This API you can create a Point to Point Order in All MIle that will have a single milestone which will have both Pickup and Deliver Events, without a branch movement between them.


API Type: Tier 1 API



#### Request

<span class="post">POST</span>`https://api.loginextsolutions.com/ShipmentApp/middlemile/shipment/order/api/create`


#### Request Parameters

Param | DataType | Length |  Required | Description
--------- | ------- | ------- | ---------- | ------------
orderNo | String | 100 | Mandatory |  This is the order No.
awbNumber | String | 100 | Optional | This is the airway Bill No.
shipmentOrderTypeCd | String | 40 | Mandatory | This is the order type code. With this API you can create 'FM'(First Mile), 'LM'(Last Mile), or 'ALLMILE' type of Orders. 'ALLMILE' Orders are Orders that have more than one leg of movements.
autoAllocateFl | String | 50 | Optional | This can be "Y", "N", or "P". If set to "Y", the Order will be automatially allocated to the nearest Delivery Associate when it is created in the system. The behaviour of the auto assignment will be dependant on the configurations set in the 'Auto Assignment Profile' screen in your LogiNext Account settings screen. If "N", the Order will not be considered for auto assignment at the time of Order Creation.<br>Pass this Flag as 'P' if you want to assign the newly created Order to an existing planned trip. This assignment event can impact the sequence of Order previously created for that trip.
orderState | String | 512 | Mandatory | This is the state of order. Ex: FORWARD
shipmentOrderDt | Date |  | Mandatory | This is the order Date. Format - YYYY-MM-DDTHH:MM:SS.SSSZ e.g. : 2016-07-01T11:18:00.000Z.
deliveryType | String | 40 | Conditional Mandatory | Order delivery type. For example - ‘Groceries’ for grocery type of Orders. This field is Mandatory if you are creating an 'ALLMILE' type of Order.
serviceTypeCd |  String | 255 | Conditional Mandatory | This is the Service type of the Order. You can have different service types depending on your operations. For example - Orders having a 'Premium' service type can have shorter SLAs than Orders having 'Normal' service types. This field is Mandatory if you are creating an 'ALLMILE' type of Order.
distributionCenter | String | 255 | Mandatory | Distribution center's name. The Distribution center is the Hub that is responsibile for fulfilling the Order. An Order can have different Pickup and Delivery leg branches, but will require a single Distribution center that is responsible for the fulfillment of the Order.
packageWeight | Double | 10,3 | Optional | This is the weight of package. The unit of measurement will be based on the unit of measurement selected for your account. For metric system this will be in Kg, and for Imperial system, this will be in pounds.
packageVolume | Double | 10,3 | Optional | This is the volume of package.The unit of measurement will be based on the unit of measurement selected for your account. For metric system this will be in cubic centimeters(CC), and for Imperial system, this will be in cubic inches(CBI).
packageLength | Double | 10,3 | Optional | This is the length of package. The unit of measurement will be based on the unit of measurement selected for your account. For metric system this will be in centimeters(CM), and for Imperial system, this will be in inches.
packageBreadth| Double | 10,3 | Optional | This is the width of package.  The unit of measurement will be based on the unit of measurement selected for your account. For metric system this will be in centimeters(CM), and for Imperial system, this will be in inches.
packageHeight| Double | 10,3 | Optional | This is the height of package.  The unit of measurement will be based on the unit of measurement selected for your account. For metric system this will be in centimeters(CM), and for Imperial system, this will be in inches.
priority | String | 16 | Optional |This is the priority of the current Order. If you wish to segregate Orders based on certain Order priorities, say you want to Route Plan for Orders based on their priorities, you can set up this field in the settings module and define the values that LogiNext should accept of this field. For example, this could be 'PRIORITY1', 'PRIORITY2', or 'PRIORITY3'.
packageValue | Double | 10 | Optional | This is the value of package
shippingCost | Double | 10 | Optional | Shipping cost or delivery Fee for the Order.
numberOfItems | Integer | 20 | Optional | This is the number of crates
paymentType | String | 40 | Mandatory | This is the mode of payment. Ex: COD - Cash On Delivery, Prepaid. If not passed, this will be defaulted to COD.
partialDeliveryAllowedFl | String | 50 | Optional | This field indicates if partial Delivery allowed. Ex: Y/N
returnAllowedFl | String | 1 | Optional | This field indicates if return is allowed. Ex: Y/N
cancellationAllowedFl | String | 1 | Optional | This field indicates if cancellation is allowed. Ex: Y/N
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
deliverServiceTime | Integer | 11 | Mandatory | Deliver service time in mins.
deliverStartTimeWindow | Date |  | Mandatory | Deliver start time window. Format - YYYY-MM-DDTHH:MM:SS.SSSZ e.g. : 2018-07-01T11:18:00.000Z.
deliverEndTimeWindow | Date |  | Mandatory | Deliver end time window. Format - YYYY-MM-DDTHH:MM:SS.SSSZ. For example - 2018-07-01T11:18:00.000Z.
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
clientCode | String | 32 | Optional | With this field you can create Orders on behalf of your Customers(accounts) in LogiNext. An account is used to represent LogiNext’s Customer’s Customer.


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
hipmentCrateMappings.shipmentlineitems.itemWeight | Double | 10 | Optional | Item weight
shipmentCrateMappings.shipmentlineitems.itemLength | Double | 10,3 | Optional | This is the length of item. The unit of measurement will be based on the unit of measurement selected for your account. For metric system this will be in centimeters(CM), and for Imperial system, this will be in inches.
shipmentCrateMappings.shipmentlineitems.itemBreadth| Double | 10,3 | Optional | This is the width of item.  The unit of measurement will be based on the unit of measurement selected for your account. For metric system this will be in centimeters(CM), and for Imperial system, this will be in inches.
shipmentCrateMappings.shipmentlineitems.itemHeight| Double | 10,3 | Optional | This is the height of item.  The unit of measurement will be based on the unit of measurement selected for your account. For metric system this will be in centimeters(CM), and for Imperial system, this will be in inches.

### Create Recurring E2E Order

> Definition

```json
 https://api.loginextsolutions.com/ShipmentApp/middlemile/v1/shipment/template/create
```

> Request Body

```json


{
"orderTemplateDetails": {
"orderTemplateNumber": "FM_QWA",
"awbNumber": "435-16685675",
"shipmentOrderTypeCd": "ALLMILE",
"orderState": "FORWARD",
"autoAllocateFl": "N",
"shipmentOrderDt": "2016-07-15T10:30:00.000Z",
"distributionCenter": "Down Town Chicago",
"originBranchName" :"Houston",
"destinationBranchName" : "Boston",
"routeConfigurationName": "Houston-Boston",
"nextBranchName":"Cupertino",
"nextBranchServiceTime": 5,
"nextBranchStartTimeWindow" : "2016-07-15T10:30:00.000Z",
"nextBranchEndTimeWindow": "2016-07-15T10:30:00.000Z",
"deliveryType": "Groceries",
"serviceTypeCd": "Economy",
"packageWeight":"10",
"packageVolume": "4500",
"paymentType": "Prepaid",
"packageValue": "5000",
"numberOfItems": 1,
"partialDeliveryAllowedFl": "Y",
"cancellationAllowedFl": "N",    
"deliverServiceTime": "20",
"deliverEndTimeWindow": "2016-07-18T10:31:00.000Z",
"deliverStartTimeWindow": "2016-07-16T10:31:00.000Z",
"deliveryLocationType":"Home",
"deliverEmail":"m.richardson@testmail.com",
"deliverPhoneNumber":"9891234567",
"deliverAccountCode": "Matt001",
"deliverAddressId": "home",
"deliverAccountName": "Mathew Richardson",
"deliverApartment": "201",
"deliverStreetName": "E Randolph St",
"deliverLandmark": "Opp. Chiptole",
"deliverLocality": "Down Town Chicago",
"deliverCity": "Chicago",
"deliverState": "IL",
"deliverCountry": "USA",
"deliverPinCode": "60602",
"deliverLatitude":41.882702,
"deliverLongitude":-87.619392,   
"deliverAddressTimezone":"America/Chicago",  
"deliverBranch": "East Manhattan",
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
"pickupNotes": "PickedUp",
"deliverNotes": "Delivered",
"clientCode": "Salestap",

"shipmentCrateMappings": []
}
,
"schedulerDetails": {
"startDate": "2019-09-23T11:00:00.000Z",
"endDate": "2019-09-25T15:00:00.000Z",
"frequency": "DAILY",
"weekDays":"Tuesday,Thursday",
"interval": 0,
"numberOfOccurrences": 1
}
}

```



> Success Response

```json
{
    "status": 200,
    "message": "Order template created successfully",
    "moreResultsExists": false,
    "data": {
        "orderTemplateReferenceId": "ed7cfd8b400b488babebb68d33f1ddbb",
        "orderTemplateNumber": "FM_QQWA"
    },
    "hasError": false
}

```


> Failure Response

```json
{
    "status": 409,
    "message": "Order template creation failed",
    "moreResultsExists": false,
    "error": [
        {
            "errorList": [
                {
                    "key": "orderTemplateNumber",
                    "message": [
                        "Order template number already exists"
                    ]
                }
            ]
        }
    ],
    "hasError": true
}

```

With This API you can create a Recurring All Mile type of Order. 

Recurring Orders can be used in operations where there are subscriptions or visits to be catered to, where the same Order level parameters are requried to be created in the system at different times depending on the schedule and frequency of these transactions.

The API accepts 2 objects in its request body. The 'orderTemplateDetails' object holds the details of the Orders to be created, and the 'schedulerDetails' objects which defines the frequency and duration of the recurring Order entities.

If the API request is sent for example on a Tuesday, with the first Order occurance for Wednesday, the first Order occurances for that week will be created immediately. Order occurances for subsequent weeks will be created every Sunday.


API Type: Tier 1 API



#### Request

<span class="post">POST</span>`https://api.loginextsolutions.com/ShipmentApp/middlemile/v1/shipment/template/create`


#### Request Parameters

Param | DataType | Length |  Required | Description
--------- | ------- | ------- | ---------- | ------------
orderTemplateNumber | String | 100 | Mandatory |  This is the order Template Number. Orders for this Template will be created by appending the date time to the Order Template number with which the request was passed.
awbNumber | String | 1000 | Optional | This is the airway Bill No.
shipmentOrderTypeCd | String | 40 | Mandatory | This is the order type code. With this API you can create 'FM'(First Mile), 'LM'(Last Mile), or 'ALLMILE' type of Orders. 'ALLMILE' Orders are Orders that have more than one leg of movements.
autoAllocateFl| String | 50 | Optional | This can be "Y", "N", or "P". If set to "Y", the Order will be automatially allocated to the nearest Delivery Associate when it is created in the system. The behaviour of the auto assignment will be dependant on the configurations set in the 'Auto Assignment Profile' screen in your LogiNext Account settings screen. If "N", the Order will not be considered for auto assignment at the time of Order Creation.<br>Pass this Flag as 'P' if you want to assign the newly created Order to an existing planned trip. This assignment event can impact the sequence of Order previously created for that trip.
orderState | String | 512 | Mandatory | This is the state of order. Ex: FORWARD
shipmentOrderDt | Date |  | Mandatory | This is the order Date. Format - YYYY-MM-DDTHH:MM:SS.SSSZ e.g. : 2016-07-01T11:18:00.000Z.
originBranchName |  String | 255 | Optional | This is the Origin branch of the Order
destinationBranchName |  String | 255 | Optional | This is the Destination branch of the Order
routeConfigurationName |  String | 255 | Optional | This is the route of the Order
deliveryType | String | 40 | Conditional Mandatory | Order delivery type. For example - ‘Groceries’ for grocery type of Orders. This field is Mandatory if you are creating an 'ALLMILE' type of Order.
serviceTypeCd |  String | 255 | Conditional Mandatory | This is the Service type of the Order. You can have different service types depending on your operations. For example - Orders having a 'Premium' service type can have shorter SLAs than Orders having 'Normal' service types. This field is Mandatory if you are creating an 'ALLMILE' type of Order.
distributionCenter | String | 255 | Mandatory | Distribution center's name. The Distribution center is the Hub that is responsibile for fulfilling the Order. An Order can have different Pickup and Delivery leg branches, but will require a single Distribution center that is responsible for the fulfillment of the Order.
packageWeight | Double | 10,3 | Optional | This is the weight of package. The unit of measurement will be based on the unit of measurement selected for your account. For metric system this will be in Kg, and for Imperial system, this will be in pounds.
packageVolume | Double | 10,3 | Optional | This is the volume of package.The unit of measurement will be based on the unit of measurement selected for your account. For metric system this will be in cubic centimeters(CC), and for Imperial system, this will be in cubic inches(CBI).
packageLength | Double | 10,3 | Optional | This is the length of package. The unit of measurement will be based on the unit of measurement selected for your account. For metric system this will be in centimeters(CM), and for Imperial system, this will be in inches.
packageBreadth| Double | 10,3 | Optional | This is the width of package.  The unit of measurement will be based on the unit of measurement selected for your account. For metric system this will be in centimeters(CM), and for Imperial system, this will be in inches.
packageHeight| Double | 10,3 | Optional | This is the height of package.  The unit of measurement will be based on the unit of measurement selected for your account. For metric system this will be in centimeters(CM), and for Imperial system, this will be in inches.
priority | String | 16 | Optional |This is the priority of the current Order. If you wish to segregate Orders based on certain Order priorities, say you want to Route Plan for Orders based on their priorities, you can set up this field in the settings module and define the values that LogiNext should accept of this field. For example, this could be 'PRIORITY1', 'PRIORITY2', or 'PRIORITY3'.
packageValue | Double | 10 | Optional | This is the value of package
numberOfItems | Integer | 20 | Optional | This is the number of crates
paymentType | String | 40 | Mandatory | This is the mode of payment. Ex: COD - Cash On Delivery, Prepaid. If not passed, this will be defaulted to COD.
partialDeliveryAllowedFl | String | 50 | Optional | This field indicates if partial Delivery allowed. Ex: Y/N
returnAllowedFl | String | 1 | Optional | This field indicates if return is allowed. Ex: Y/N
cancellationAllowedFl | String | 1 | Optional | This field indicates if cancellation is allowed. Ex: Y/N
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
deliverServiceTime | Integer | 11 | Mandatory | Deliver service time in mins.
deliverStartTimeWindow | Date |  | Mandatory | Deliver start time window. Format - YYYY-MM-DDTHH:MM:SS.SSSZ e.g. : 2018-07-01T11:18:00.000Z.
deliverEndTimeWindow | Date |  | Mandatory | Deliver end time window. Format - YYYY-MM-DDTHH:MM:SS.SSSZ. For example - 2018-07-01T11:18:00.000Z.
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
clientCode | String | 32 | Optional | With this field you can create Orders on behalf of your Customers(accounts) in LogiNext. An account is used to represent LogiNext’s Customer’s Customer.
schedulerDetails | Object | | | The Scheduler Details object has the details for defining the duration and frequency of the Orders to be creatted against this Order Template.
startDate | DateTime | | Mandatory | The start date time from which the Order instances for the Template should be created.
endDate | DateTime |  | Optional | The end date time from which the Order instances for the Template should be created. If not passed, the API will consider only one instance of the Order Template.
frequency | String | | Conditional Mandatory | The frequncy of the occurance of Orders for the Template. This can be 'DAILY' for daily recurrance, 'WEEKLY' for weekly recurrance, 'MONTHLY' for monthly recurrance, or 'CUSTOM', in case a specific recurrance pattern is to be defined, like every alternate day for example. This field is required if weekDays is not passed.
weekDays | String |  | Conditional Mandatory | Comma separated list of day names for which the Order occurances are to be created. This field is required if frequency is 'CUSTOM'.
numberOfOccurrences | Number |  | Optional | Number of occurance of the Order Template.
interval | Number | | Optional | In case you want to create Order occurances once every 2 weeks, you can use this field and a frequency of 'WEEKLY'.

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
            "itemWeight": 10,
            "itemVolume":11,
            "itemLength":12,
            "itemBreadth":13,
            "itemHeight":14
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

API Type: Tier 1 API


#### Request

<span class="post">POST</span>`https://api.loginextsolutions.com/ShipmentApp/mile/v2/multidestination/create`


#### Request Body

Parameter | DataType | Length |  Required | Description
-----------|-------| ------- |------- | ----------
clientCode | String |255 | Optional | With this field you can create Orders on behalf of your Customers(accounts) in LogiNext. An account is used to represent LogiNext’s Customer’s Customer.
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

API Type: Tier 1 API

#### Request

<span class="post">POST</span>`https://api.loginextsolutions.com/ShipmentApp/mile/v1/create/return`

#### Request Body

Parameter | DataType |  Required | Description
-----------|-------|------- | ----------
reference_ids | List | Mandatory | Reference Id associated with the order.



### Get

> Definition

```json
https://api.loginextsolutions.com/ShipmentApp/mile/v1/shipment?end_date=2017-03-07+18:29:59&start_date=2016-02-01+18:30:00&status=ALL&order_no=GKS12567&orderReferenceId=f40cf4493a5949199775499b5750a272&customer_code=123&employee_id=134367&page_no=1&page_size=10
```



> Response

```json

{
    "status": 200,
    "message": "SUCCESS",
    "moreResultsExists": false,
    "data": [
        {
            "referenceId": "f40cf4493a5949199775499b5750a272",
            "orderNo": "GR432U5",
            "parentOrderNo": "GKS12",
            "clientName": "UNY Logistics",
            "branchName": "West Brooklyn Hub",
            "origin": "West Brooklyn Hub",
            "destination": "California Hub",
            "shipmentOrderTypeCd": "DELIVER",
            "orderState": "FORWARD",
            "deliveryType": "TRK",
            "deliveryLocationType": "PUP",
            "shipmentOrderDt": 1485153536000,
            "startTimeWindow": 1485174600000,
            "endTimeWindow": 1485181800000,
            "paymentType": "COD",
            "notes": "Order recieved successfully.Thanks",
            "packageValue": 300.0,
            "shippingCost":50,
            "recalculatedValue": 300.0,
            "status": "DELIVERED",
            "serviceTime": 5,
            "deliveryMediumName": "James",
            "deliverMediumPhoneNumber": "9757282492",
            "assignedThrough": "Manually",
            "tripName": "TRIP-5276",
            "actualStartDt": 1562152130000,
            "actualEndDt": 1562152153000,
            "timeTakenDifferenceInMins": 0,
            "pickupCheckOutTime": 1562152130000,
            "pickupCheckOutLatitude": 40.7520394,
            "pickupCheckOutLongitude": -73.9763424,
            "deliverCheckInTime": 1562152141000,
            "deliverCheckOutTime": 1562152153000,
            "deliverCheckInLatitude": 19.1118182,
            "deliverCheckInLongitude": 72.9094924,
            "deliverCheckOutLatitude": 19.1118182,
            "deliverCheckOutLongitude": 72.9094924,
            "orderSequence": 2,
            "customerCode": "johnsmith",
            "customerName": "John Smith",
            "amountCollected": 300.0,
            "noOfAttempts": 1,
            "isDelayed": false,
            "originLatitude": 40.7520394,
            "originLongitude": -73.9763424,
            "destinationLatitude": 19.1118133,
            "destinationLongitude": 72.9094806,
             "shipmentCrateMappings": [
                {
                    "createdOnDt": 1564757907000,
                    "updatedOnDt": 1564757950000,
                    "createdByUserId": 1535,
                    "updatedByUserId": 1535,
                    "isDeleteFl": "N",
                    "isActiveFl": true,
                    "id": 30310923,
                    "shipmentMappingId": 30310923,
                    "crateCd": "ABG001",
                    "statusCd": "LOADED",
                    "crateAmount": 0.0,
                    "shipmentlineitems": [
                        {
                            "createdOnDt": 1564757907000,
                            "updatedOnDt": 1564757939000,
                            "itemCd": "R445",
                            "itemName": "",
                            "itemPrice": 100.0,
                            "itemQuantity": 10.0,
                            "itemType": "Groceries",
                            "itemWeight": 0.0,
                            "amountToCollect": 1000.0,
                            "statusCd": "LOADED",
                            "loadedQuantity": 10.0,
                            "unloadedQuantity": 0.0
                        }
                    ],
                    "noOfUnits": 1.0,
                    "loadedUnits": 10.0,
                    "unloadedUnits": 0.0,
                    "orderNo": "GR432U5"
                }
            ],
            "employeeId": "ABC345",
            "shipmentOrderDtTZ": "America/New_York",
            "startTimeWindowTZ": "America/New_York",
            "endTimeWindowTZ": "America/Los_Angeles",
            "actualStartDtTZ": "America/New_York",
            "actualEndDtTZ": "America/Los_Angeles",
            "pickupCheckOutTimeTZ": "America/New_York",
            "deliverCheckInTimeTZ": "America/Los_Angeles",
            "deliverCheckOutTimeTZ": "America/Los_Angeles"
        }
    ],
    "hasError": false
}



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
      "shippingCost":50,
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
      "originLatitude": 40.760838,
      "originLongitude": -73.96732299999996,
      “employeeId”: 3224567,
      "pickupCheckInTime": 1485154765000,
      "pickupCheckOutTime": 1485154887000,
      "pickupCheckInLatitude": 40.760838,
      "pickupCheckInLongitude": -73.96732299999996,
      "pickupCheckOutLatitude": 40.760838,
      "pickupCheckOutLongitude": -73.96732299999996,
      "destinationLatitude": 41.882702,
      "destinationLongitude":101.706872,
      "deliverCheckInTime": 1485154905000,
      "deliverCheckOutTime": 1485155021000,
      "deliverCheckInLatitude": 41.882702,
      "deliverCheckInLongitude": -87.61939,
      "deliverCheckOutLatitude": 41.882702,
      "deliverCheckOutLongitude": -87.61939,
      "orderSequence": 5,
      "pickupAccountCode":"PDT_124",
      "customerCode": "CST_ACL1",
      "customerName": "Steven Goods",
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
      "vehicleNumber": "AC2T123",
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

API Type: Tier 1 API

#### Request

<span class="post">GET</span>`https://api.loginextsolutions.com/ShipmentApp/mile/v1/shipment`


#### Request Parameters

Param | DataType | Length |  Required | Description
--------- | ------- | ------- | ---------- | ------------
start_date | Date |  | Conditional Mandatory |  If order_no is not passed in the request, then this field is mandatory. Range of date from which orders can be searched. This will return orders based on the order fulfillment date start time window. <BR>Format 'yyyy-MM-dd HH:mm:ss'
end_date | Date |  | Conditional Mandatory |  If order_no is not passed in the request, then this field is mandatory. Range of date upto which orders can be searched. This will return orders that have fulfillment end times less than the entered time.<BR>Format 'yyyy-MM-dd HH:mm:ss'
status | String | 20 | Optional |  If order_no is passed in the request,then status will not be considered for filtering the orders.Order status. <BR>Ex: NOTDISPATCHED,INTRANSIT,COMPLETED,<BR>NOTCOMPLETED,PICKEDUP(Only for First Mile),CANCELLED
order_no | String | 100 | Optional | Order Number(Only one order number can be passed at a time.If not passed ,all the orders for the specified date range will be fetched)
orderReferenceId | String | 100 | Optional | Order Reference ID(Only one order number can be passed at a time.If not passed, all the orders for the specified date range will be fetched)
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
    "priority": "PRIORITY1",
    "paymentType": "Prepaid",
    "packageValue": "65",
    "shippingCost":"50",
    "numberOfItems": "10",
    "partialDeliveryAllowedFl": "Y",
    "returnAllowedFl": "Y",
    "cancellationAllowedFl": "N",   
    "distributionCenter": "Manhattan Branch"
    "deliverBranch": "test",
    "deliverServiceTime": "20",
    "deliverEndTimeWindow": "2016-07-18T10:31:00.000Z",
    "deliverStartTimeWindow": "2016-07-16T10:31:00.000Z",
    "deliveryType": "RIDER",
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
    "returnAddressId":"JeffOffice",
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



> Success Response

```json
{
    "status": 200,
    "message": "Order updated successfully",
    "moreResultsExists": false,
    "data": [
        17055042
    ],
    "hasError": false
}

```

> Failure Response

```json
{
    "status": 400,
    "message": "Referenceids does not exists",
    "moreResultsExists": false,
    "error": {
        "order_0": [
            {
                "key": "04c1c0c283a34769a5baca01c987b51a",
                "message": [
                    "referenceId.doestnot.exists"
                ],
                "orderReferenceId":"04c1c0c283a34769a5baca01c987b51a"
            }
        ]
    },
    "hasError": true
}

```


With this API, you will be able to update the order information unless and until that order is not delivered and not associated with any Trip.

You can pass multiple order reference IDs and can update one or more parameters.

This API has Custom Field support included. You only need to pass data for the Custom Fields you want to addd or update the values for in the request body. All Custom Fields created at the time of Order creation do not have to be passed here again. For details on how to pass Custom Fields in this API, please refer to the custom fields section of the API documentation.

This API does not support a partial success response. If you pass multiple Orders in a single call of this API, and even one of them fails a validation check, the entire batch of Orders will be considered a failed request.

API Type: Tier 1 API

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
shippingCost | Double | 10 | Optional | Shipping cost or delivery Fee for the Order.
priority | String |100 | Optional |  Order Priority.
numberOfItems | Integer | 20 | Optional | This is the number of crates in the order.
paymentType | String | 40 | Optional | This is the payment mode. Ex: COD - Cash On Delivery, Prepaid. Note that the Payment Type is dependant on the language preference configured for the user account the API token was created from. You can refer to the 'Authenticate' API documentation for more details on this.
partialDeliveryAllowedFl | String | 50 | Optional | This identifies if partial delivery is allowed. Ex: Y/N.
returnAllowedFl | String | 1 | Optional | This identifies if order return allowed. Ex: Y/N. Default value is Y.
cancellationAllowedFl | String | 1 | Optional | This identifies if order cancellation is allowed. Ex: Y/N
distributionCenter | String | 255 | Optional | Distribution center's name. The Distribution center is the Hub that is responsibile for fulfilling the Order. An Order can have different Pickup and Delivery leg branches, but will require a single Distribution center that is responsible for the fulfillment of the Order.
deliverBranch | String | 255 | Optional | Name of delivery branch
deliverServiceTime | Integer | 11 | Optional | Deliver service time in mins.
deliverStartTimeWindow | Date | | Optional | Deliver start time window. Format - YYYY-MM-DDTHH:MM:SS.SSSZ e.g. : 2016-07-01T11:18:00.000Z.
deliverEndTimeWindow | Date | | Optional | Deliver end time window. Format - YYYY-MM-DDTHH:MM:SS.SSSZ e.g. : 2016-07-01T11:18:00.000Z.
deliveryType | String | 40 | Optional | Order delivery type. Ex: TRK - Truck, VAN - Van, RIDER - Delivery Associate
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


### Update Recurring E2E Order

> Definition

```json
 https://demo.loginextsolutions.com/ShipmentApp/middlemile/v1/shipment/template/update
```

> Request Body

```json


{
"orderTemplateDetails": {
"orderTemplateReferenceId":"a8462eb3838d4701bf6182de315c0b14",
"awbNumber": "435-16685675",
"shipmentOrderTypeCd": "ALLMILE",
"orderState": "FORWARD",
"autoAllocateFl": "N",
"shipmentOrderDt": "2016-07-15T10:30:00.000Z",
"distributionCenter": "Down Town Chicago",
"originBranchName" :"Houston",
"destinationBranchName" : "Boston",
"routeConfigurationName": "Houston-Boston",
"nextBranchName":"Cupertino",
"nextBranchServiceTime": 5,
"nextBranchStartTimeWindow" : "2016-07-15T10:30:00.000Z",
"nextBranchEndTimeWindow": "2016-07-15T10:30:00.000Z",
"deliveryType": "Groceries",
"serviceTypeCd": "Economy",
"packageWeight":"10",
"packageVolume": "4500",
"paymentType": "Prepaid",
"packageValue": "5000",
"numberOfItems": 1,
"partialDeliveryAllowedFl": "Y",
"cancellationAllowedFl": "N",    
"deliverServiceTime": "20",
"deliverEndTimeWindow": "2016-07-18T10:31:00.000Z",
"deliverStartTimeWindow": "2016-07-16T10:31:00.000Z",
"deliveryLocationType":"Home",
"deliverEmail":"m.richardson@testmail.com",
"deliverPhoneNumber":"9891234567",
"deliverAccountCode": "Matt001",
"deliverAddressId": "home",
"deliverAccountName": "Mathew Richardson",
"deliverApartment": "201",
"deliverStreetName": "E Randolph St",
"deliverLandmark": "Opp. Chiptole",
"deliverLocality": "Down Town Chicago",
"deliverCity": "Chicago",
"deliverState": "IL",
"deliverCountry": "USA",
"deliverPinCode": "60602",
"deliverLatitude":41.882702,
"deliverLongitude":-87.619392,   
"deliverAddressTimezone":"America/Chicago",  
"deliverBranch": "East Manhattan",
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
"pickupNotes": "Don't ring the doorbell",
"deliverNotes": "Leave it with the neighbour",
"clientCode": "Salestap",

"shipmentCrateMappings": []
}
,
"schedulerDetails": {
"startDate": "2019-09-23T11:00:00.000Z",
"endDate": "2019-09-25T15:00:00.000Z",
"frequency": "DAILY",
"weekDays":"Tuesday,Thursday",
"interval": 0,
"numberOfOccurrences": 1
}
}

```



> Success Response

```json
{
    "status": 200,
    "message": "Order template updated successfully",
    "moreResultsExists": false,
    "data": {
        "orderTemplateReferenceId": "d5c2add00b9146beb8fce30b257c0e9d",
        "orderTemplateNumber": "FM_AQWA"
    },
    "hasError": false
}

```


> Failure Response

```json
{
    "status": 409,
    "message": "Order template update failed",
    "moreResultsExists": false,
    "error": [
        {
            "errorList": [
                {
                    "key": "orderTemplateReferenceId",
                    "message": [
                        "orderTemplateReferenceId is mandatory"
                    ]
                }
            ]
        }
    ],
    "hasError": true
}

```

With This API you can update a recurring Order for All Mile type of Orders. 

Recurring Orders can be used in operations where there are subscriptions or visits to be catered to, where the same Order level parameters are requried to be created in the system at different times depending on the schedule and frequency of these transactions.

The API accepts 2 objects in its request body. The 'orderTemplateDetails' object holds the details of the Orders to be created, and the 'schedulerDetails' objects which defines the frequency and duration of the recurring Order entities.

If the API request is sent for example on a Tuesday, with the first Order occurance for Wednesday, the first Order occurances for that week will be created immediately. Order occurances for subsequent weeks will be created every Sunday.


API Type: Tier 1 API



#### Request

<span class="post">PUT</span>`https://demo.loginextsolutions.com/ShipmentApp/middlemile/v1/shipment/template/update`


#### Request Parameters

Param | DataType | Length |  Required | Description
--------- | ------- | ------- | ---------- | ------------
orderTemplateReferenceId | String | 100 | Mandatory |  This is the order Template Number. Orders for this Template will be created by appending the date time to the Order Template number with which the request was passed.
awbNumber | String | 1000 | Optional | This is the airway Bill No.
shipmentOrderTypeCd | String | 40 | Optional | This is the order type code. With this API you can create 'FM'(First Mile), 'LM'(Last Mile), or 'ALLMILE' type of Orders. 'ALLMILE' Orders are Orders that have more than one leg of movements.
autoAllocateFl| String | 50 | Optional | This can be "Y", "N", or "P". If set to "Y", the Order will be automatially allocated to the nearest Delivery Associate when it is created in the system. The behaviour of the auto assignment will be dependant on the configurations set in the 'Auto Assignment Profile' screen in your LogiNext Account settings screen. If "N", the Order will not be considered for auto assignment at the time of Order Creation.<br>Pass this Flag as 'P' if you want to assign the newly created Order to an existing planned trip. This assignment event can impact the sequence of Order previously created for that trip.
orderState | String | 512 | Optional | This is the state of order. Ex: FORWARD
shipmentOrderDt | Date |  | Optional | This is the order Date. Format - YYYY-MM-DDTHH:MM:SS.SSSZ e.g. : 2016-07-01T11:18:00.000Z.
originBranchName |  String | 255 | Optional | This is the Origin branch of the Order
destinationBranchName |  String | 255 | Optional | This is the Destination branch of the Order
routeConfigurationName |  String | 255 | Optional | This is the route of the Order
deliveryType | String | 40 | Optional | Order delivery type. For example - ‘Groceries’ for grocery type of Orders. This field is Mandatory if you are creating an 'ALLMILE' type of Order.
serviceTypeCd |  String | 255 | Optional | This is the Service type of the Order. You can have different service types depending on your operations. For example - Orders having a 'Premium' service type can have shorter SLAs than Orders having 'Normal' service types. This field is Mandatory if you are creating an 'ALLMILE' type of Order.
distributionCenter | String | 255 | Optional | Distribution center's name. The Distribution center is the Hub that is responsibile for fulfilling the Order. An Order can have different Pickup and Delivery leg branches, but will require a single Distribution center that is responsible for the fulfillment of the Order.
packageWeight | Double | 10,3 | Optional | This is the weight of package. The unit of measurement will be based on the unit of measurement selected for your account. For metric system this will be in Kg, and for Imperial system, this will be in pounds.
packageVolume | Double | 10,3 | Optional | This is the volume of package.The unit of measurement will be based on the unit of measurement selected for your account. For metric system this will be in cubic centimeters(CC), and for Imperial system, this will be in cubic inches(CBI).
packageLength | Double | 10,3 | Optional | This is the length of package. The unit of measurement will be based on the unit of measurement selected for your account. For metric system this will be in centimeters(CM), and for Imperial system, this will be in inches.
packageBreadth| Double | 10,3 | Optional | This is the width of package.  The unit of measurement will be based on the unit of measurement selected for your account. For metric system this will be in centimeters(CM), and for Imperial system, this will be in inches.
packageHeight| Double | 10,3 | Optional | This is the height of package.  The unit of measurement will be based on the unit of measurement selected for your account. For metric system this will be in centimeters(CM), and for Imperial system, this will be in inches.
priority | String | 16 | Optional |This is the priority of the current Order. If you wish to segregate Orders based on certain Order priorities, say you want to Route Plan for Orders based on their priorities, you can set up this field in the settings module and define the values that LogiNext should accept of this field. For example, this could be 'PRIORITY1', 'PRIORITY2', or 'PRIORITY3'.
packageValue | Double | 10 | Optional | This is the value of package
numberOfItems | Integer | 20 | Optional | This is the number of crates
paymentType | String | 40 | Optional | This is the mode of payment. Ex: COD - Cash On Delivery, Prepaid. If not passed, this will be defaulted to COD. Note that the Payment Type is dependant on the language preference configured for the user account the API token was created from. You can refer to the 'Authenticate' API documentation for more details on this.
partialDeliveryAllowedFl | String | 50 | Optional | This field indicates if partial Delivery allowed. Ex: Y/N
returnAllowedFl | String | 1 | Optional | This field indicates if return is allowed. Ex: Y/N
cancellationAllowedFl | String | 1 | Optional | This field indicates if cancellation is allowed. Ex: Y/N
pickupServiceTime | Integer | 11 | Optional | Pickup service time in mins.
pickupStartTimeWindow | Date |  | Optional | Pickup start time window. Format - YYYY-MM-DDTHH:MM:SS.SSSZ e.g. : 2016-07-01T11:18:00.000Z.
pickupEndTimeWindow | Date |  | Optional | Pickup end time window. Format - YYYY-MM-DDTHH:MM:SS.SSSZ e.g. : 2016-07-01T11:18:00.000Z.
pickupAccountCode | String | 255 | Optional | Pickup account code
pickupAccountName | String | 255 | Optional | Pickup account name. This field in Non Mandatory in case Customer Profiling in ON.
pickupEmail| String | 100 | Optional | Email of the merchant
pickupPhoneNumber| String | 255 | Optional | Phone number of the merchant
pickupApartment | String | 512 | Optional | This is the pickup location's apartment. This field in Non Mandatory in case Customer Profiling in ON.
pickupStreetName | String | 512 | Optional | This is the pickup location's street name. This field in Non Mandatory in case Customer Profiling in ON.
pickupLandmark | String | 512 | Optional | This is the pickup location's  landmark.
pickupLocality | String | 512 | Optional | This is the pickup location's locality. This field in Non Mandatory in case Customer Profiling in ON.
pickupCity | String | 512 | Optional | This is the pickup location's city. This field in Non Mandatory in case Customer Profiling in ON.
pickupState| String | 512 | Optional | This is the pickup location's state code. This field in Non Mandatory in case Customer Profiling in ON.
pickupCountry | String | 512 | Optional | This is the pickup location's country code. This field in Non Mandatory in case Customer Profiling in ON.
pickupPinCode | String | 20 | Optional | This is the pickup location's pincode. This field in Non Mandatory in case Customer Profiling in ON.
pickupLatitude | Double |  | Optional | The geolocation coordinate (latitude) of the pickup location.
pickupLongitude | Double |  | Optional | The geolocation coordinate (longitude) of the pickup location.
pickupAddressTimezone | String | | Optional | The timezone of the pickup location. Refer to the timezone codes list to get the full list of values you can pass here. If not passed, the timezone associated with the pickup location will be the branch timezone.
pickupNotes | String | 512 | Optional | Additional pickup comments associated with the order
deliverServiceTime | Integer | 11 | Optional | Deliver service time in mins.
deliverStartTimeWindow | Date |  | Optional | Deliver start time window. Format - YYYY-MM-DDTHH:MM:SS.SSSZ e.g. : 2018-07-01T11:18:00.000Z.
deliverEndTimeWindow | Date |  | Optional | Deliver end time window. Format - YYYY-MM-DDTHH:MM:SS.SSSZ. For example - 2018-07-01T11:18:00.000Z.
deliveryLocationType | String | 40 | Optional | Type of delivery location. For example -  ‘CUSTOMER’.
deliverAccountCode | String | 255 | Optional | Customer ID of the Delivery Customer.
deliverAccountName | String | 255 | Optional | Deliver account name. This field in Non Mandatory in case Customer Profiling in ON.
deliverEmail| String | 100 | Optional | Email of the customer
deliverPhoneNumber| String | 255 | Optional | Phone number of the customer
deliverApartment | String | 512 | Conditional Mandatory | This is the delivery customer location's apartment details. This field in Non Mandatory in case Customer Profiling in ON.
deliverStreetName | String | 512 | Optional | This is the delivery customer location's Street name. This field in Non Mandatory in case Customer Profiling in ON.
deliverLandmark | String | 512 | Optional | This is the delivery customer location's Landmark.
deliverLocality | String | 512 | Optional | This is the delivery customer location's Locality. This field in Non Mandatory in case Customer Profiling in ON.
deliverCity | String | 512 | Optional | This is the delivery customer location's City. This field in Non Mandatory in case Customer Profiling in ON.
deliverState| String | 512 | Optional | This is the delivery customer location's state code. This field in Non Mandatory in case Customer Profiling in ON.
deliverCountry | String | 512 | Optional | This is the delivery customer location's country code. This field in Non Mandatory in case Customer Profiling in ON.
deliverPinCode | String | 20 | This field in Non Mandatory in case Customer Profiling in ON. Mandatory | This is the delivery customer location's Pincode. This field in Non Mandatory in case Customer Profiling in ON.
deliverLatitude | Double | 100 | Optional | The geolocation coordinate (latitude) of the delivery customer.
deliverLongitude | Double | 100 | Optional | The geolocation coordinate (latitude) of the delivery customer.
deliverAddressTimezone | String | | Optional | The timezone of the delivery location. Refer to the timezone codes list to get the full list of values you can pass here. If not passed, the timezone associated with the deliver location will be the branch timezone.
deliverNotes | String | 512 | Optional | Additional delivery comments associated with the order
clientCode | String | 32 | Optional | With this field you can create Orders on behalf of your Customers(accounts) in LogiNext. An account is used to represent LogiNext’s Customer’s Customer.
schedulerDetails | Object | | | The Scheduler Details object has the details for defining the duration and frequency of the Orders to be creatted against this Order Template.
startDate | DateTime | | Optional | The start date time from which the Order instances for the Template should be created.
endDate | DateTime |  | Optional | The end date time from which the Order instances for the Template should be created. If not passed, the API will consider only one instance of the Order Template.
frequency | String | | Optional | The frequncy of the occurance of Orders for the Template. This can be 'DAILY' for daily recurrance, 'WEEKLY' for weekly recurrance, 'MONTHLY' for monthly recurrance, or 'CUSTOM', in case a specific recurrance pattern is to be defined, like every alternate day for example. This field is required if weekDays is not passed.
weekDays | String |  | Optional | Comma separated list of day names for which the Order occurances are to be created. This field is required if frequency is 'CUSTOM'.
numberOfOccurrences | Number |  | Optional | Number of occurance of the Order Template.
interval | Number | | Optional | In case you want to create Order occurances once every 2 weeks, you can use this field and a frequency of 'WEEKLY'.


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
    "latitude": 40.760838,
    "longitude": 74.910214,
    "updateTime":"2016-07-18T10:31:00.000Z"
  },
  {
    "orderReferenceId":"6186d7r5te324c42abb5ea1a32x45f66",
    "reasonCd":"DBUNAVAILABLE",
    "otherReason":"",
    "latitude": 40.760838,
    "longitude": 74.913214,
    "updateTime":"2016-07-18T10:31:00.000Z"

  },
  {
    "orderReferenceId":"6156ty46e324c42abb5ea1a32y45f66",
    "reasonCd":"Other",
    "otherReason":"Technical Issues",
    "latitude": 40.760838,
    "longitude": 74.910321,
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
With this API, you will be able to update the the status of a Order.
You can pass multiple Order reference IDs and can update one or more parameters.


API Type: Tier 1 API

#### Request

<span class="post">PUT</span>`https://api.loginextsolutions.com/ShipmentApp/mile/v1/update/status`


#### Request Parameters

Param | DataType | Length |  Required | Description
--------- | ------- | ---------- | ---------- | ------------
newStatus | String | 20 | Mandatory |  One status for multiple orders.The orders will be updated with this new status<br>Available Values - <br>DELIVERED - When an order has been Delivered by the associate<br>NOTPICKEDUP - When the associate reached the Pick-up location, but could not pick-up the order due to one or the other reason<br>NOTDELIVERED - When the associate reached the delivery location, but could not deliver the order due to one or the other reason
orderReferenceId | String | 100 | Mandatory |  This is the LogiNext Reference ID for the Order<br>This is generated when the order is added in the LogiNext application.
reasonCd | String | 255 | Conditional Mandatory | Mandatory depending upon the status selected : NOTDELIVERED, NOTPICKEDUP, CANCELLED<br>Else Optional.<br>If you have pre-configured the reasons for Order Status Update - NOTDELIVERED, NOTPICKEDUP and CANCELLED in LogiNext application, then it is mandatory to mention that relevant configured reason here.<br>One of the other values here is Other, in case the delivery Associate selects the reason as Others.
otherReason | Date |  | Conditional Mandatory | Mandatory when reasonCd is OTHER
latitude | Double | 15 | Conditional Optional | Geo-location where Order status was updated<br>Sample Value - "17.996"
otherReason | Date | 15 | Conditional Optional | Geo-location where Order status was updated<br>Sample Value - "17.996"
updateTime | Date | 15 | Conditional Optional | This is the timestamp (in UTC format) when the order status was changed. This cannot be greater than the time at which the API is hit. If not passed, the timestamp of the API hit is considered as the timestamp for the status change.


Status | Not Dispatched |  Intransit | Picked Up | Delivered | Attempted | Cancelled
--------- | ------- | ---------- | ---------- | ----------|----------|---------
Not Dispatched | No | No | Yes | Yes | Yes | Yes
Intransit Before Trip Stop | No | No | Yes | Yes | Yes | Yes
Picked Up | No | No | No | Yes | Yes | Yes
Intransit order marked Delivered | Yes | No | No | No | Yes | Yes
NOT DISPTACHED order marked Delivered | Yes | No | No | No | Yes | Yes
Intransit order marked Attempted | Yes | No | No | Yes | No | Yes
NOT DISPTACHED order marked Attempted | Yes | No | No | Yes | No | Yes
Intransit order marked Cancelled | Yes | No | No | Yes | Yes | No
NOT DISPTACHED order marked Cancelled | Yes | No | No | Yes | Yes | No

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

API Type: Tier 1 API

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

The API will take as input the Trip or Delivery Associate details and the list of orders to be added for that trip or Delivery Associate.
The API can be used in 2 ways:
If the trip details are passed (through trip reference id), then Delivery Associate details are not required and the list of orders will be added to that trip, irrespective of the trip being Started or Not Started. Other order and trip validations remain as is.
If the trip details are not passed, then the Delivery Associate details will be required to be passed, either through username, mobile number or employee id (unique identifiers) and a control flag identifying which of these values is being passed. 
The orders will be added to the Default trip (Started or Not Started) of the Delivery Associate.

API Type: Tier 1 API

#### Request

<span class="post">PUT</span>`https://api.loginextsolutions.com/ShipmentApp/mile/v1/manual/assign`


#### Request Parameters

Param | DataType | Length |  Required | Description
--------- | ------- | ---------- | ---------- | ------------
trip.referenceId | String | 32 | Conditional Mandatory | Reference ID of the trip to which the Order has to be assigned. This field has to be passed in case the Delivery Associate details are not passed.
deliveryMedium.identifier | String | 32 | Conditional Mandatory |  This is the control flag field for the Delivery Associate, to identify which details of the Delivery Associate are being passed. Possible values are 'employeeId', 'phoneNumber', 'userName'.
deliveryMedium.identifierValue | String | 32 | Conditional Mandatory | This field will hold the Delivery Associate information to whom the Order is to be assigned, as per the flag set above. For eg - If you wish to assign an Order to a Delivery Associate whose 'employeeId' is 'John1', you would send 'employeeId' in the identifier field and 'John1' in the identifierValue field.
orderReferenceIds | List | |  Mandatory | These are the Reference IDs of the Order to be assigned.


### Unssign

> Definition

```json
https://api.loginextsolutions.com/ShipmentApp/mile/v1/manual/unassign?referenceId=6186d5fc6e324c42abb5ea1a32e05f66
```


> Success Response

```json
{
    "status": 200,
    "message": "Unassignment Successful",
    "moreResultsExists": false,
    "data": {
        "orderReferenceId": "7d7527b351e74159adb05abe9529b0a9",
        "tripReferenceId": "ac4de0a72fa6421e83e00acaeb391d26",
        "deliveryMediumReferenceId": "a2fd9619be204195b8995539e9a946fb",
        "tripStatus": "NOTSTARTED"
    },
    "hasError": false
}

```

> Failure Response

```json
{
    "status": 409,
    "message": "Unassignment Failed",
    "moreResultsExists": false,
    "data": {
        "message": "Order Reference Id is invalid",
        "orderReferenceId": "2d971c78f3f1431c91d9ad76db90202b"
    },
    "hasError": true
}

```

With this API, you can Unassign a Not Delivered Order from a started or Not Started Trip. 

The API accepts a single Order Reference ID in the request and checks if the Order is currently assigned to a trip. If yes, and the Order has not yet been marked Delivered, it will be unassigned from the Trip and put in a Not Dispatced state. This Order can then be assigned to another Trip.

This API will not revise the ETAs of other Orders in the Trip after unassigning the current Order, not will it resequnce the remaining Orders to come up with the new optimised sequnce of Orders in that Trip. You will need to call the LogiNext Replan API in order to revise ETAs and resequnce the Orders in the Trip.

This API accepts only one Order Reference ID in a request

API Type: Tier 1 API

#### Request

<span class="post">PUT</span>`https://api.loginextsolutions.com/ShipmentApp/mile/v1/manual/unassign?referenceId=6186d5fc6e324c42abb5ea1a32e05f66`


#### Request Parameters

Param | DataType | Length |  Required | Description
--------- | ------- | ---------- | ---------- | ------------
referenceId | String | 32 | Mandatory | Reference ID of the Order which is to be unassigned from the Trip.




### Cancel

> Definition

```json
https://api.loginextsolutions.com/ShipmentApp/mile/v1/cancel
```

> Request Body

```json
[
     "c8714df4347911e6829f000d3aa044508"
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

> Failure Response 1

```json
{
   "status": 409,
   "message": "Order(s) couldn't be cancelled",
   "moreResultsExists": false,
   "data": [
        "ac07cbdb9be94d85ac467399117f05fd",
        "b06fe5ef422211e6860c0653055f4dfd" 
    ],
   "hasError": false
}
```

> Failure Response 2

```json
{
   "status": 409,
   "message": "Order(s) are already cancelled",
   "moreResultsExists": false,
   "data": [
        "ac07cbdb9be94d85ac467399117f05fd",
        "b06fe5ef422211e6860c0653055f4dfd" 
    ],
   "hasError": false
}
```


Use this API to cancel an order.

With this API, you can cancel Orders that were created with a 'cancellationAllowedFl' set to 'Y'. If you try to cancel Orders that have a 'cancellationAllowedFl' set to 'N', the API will return an error response.

API Type: Tier 1 API

#### Request

<span class="post">PUT</span>`https://api.loginextsolutions.com/ShipmentApp/mile/v1/cancel`

#### Request Body

Parameter | DataType | Required | Description
-----------|-------|------- | ----------
reference_ids | List  | Mandatory | This is the order reference Id.

### Get EPOD and ESIGN

This endpoint downloads the EPODs and ESIGNs for given order. 

The API responds with a 202 Request received response along with a request ID that uniquely identifies each request of the API. A webhook response is triggered once the images are fetched with the URL to the EPOD/ ESign images. This webhook also has the same request ID to confirm which Order images are being sent.

Calling the URL in the webhook downloads a compressed zip file with the EPOD and ESigns for the Orders sent in the request.

The URL in the webhook has a validity of 1 hour. If you wish to download and save the images in your system, please download these files within one hour of consuming this webhook.

NOTE: The dates accepted are in UTC.

#### Request

<span class="post">GET</span>`https://api.loginextsolutions.com/ShipmentApp/mile/v2/epod/list?orderReferenceId=5e7a0f2804f14cd591a4740dfc7abdf1`

#### Request Parameters

Parameter | DataType | Length |  Required | Description
-----------|-------|------- |------- | ----------
orderNo | String | 40 | Conditional Mandatory | Order Number of the Order for which EPOD/ ESign is required. Mandatory if orderReferenceId is not passed.
orderReferenceId | String | 32 | Conditional Mandatory | Order Number of the Order for which EPOD/ ESign is required Mandatory if orderNo is not passed.


> Success Response

```json
{
     "status": 202,
     "message": "EPOD-ESign request received successfully",
     "requestId": "fb82b48ba4c44370b48c04dc168f0e68",
     "moreResultsExists": false,
     "hasError": false
}

```

> Failure Response

```json

{
   "status": 409,
   "message": "Order referenceId does not exist",
   "moreResultsExists": false,
   "hasError": true
}

```

### Get Custom Forms

> Definition

```json
https://api.loginextsolutions.com/ShipmentApp/mile/v1/customform/list
```

> Request Body

```json
{"orderReferenceId":["ce9e99c4b4924b23b0692fafa26e4d25"]}
```

> Response

```json
{
    "status": 200,
    "message": "success",
    "moreResultsExists": false,
    "data": [
        {
            "referenceId": "ce9e99c4b4924b23b0692fafa26e4d25",
            "tripName": "TRIP-19107",
            "orderNo": "ORD_188",
            "deliveryMediumName": "Bishwajeet",
            "status": "DELIVERED",
            "results": [
                {
                    "moduleId": 8043067,
                    "event": "UNLOAD_AFTER",
                    "moduleName": "ORDERS",
                    "formName": "unloadtesrt",
                    "formStatus": "ACTIVE",
                    "formdata": [
                        {
                            "field": "text",
                            "value": "Test Form"
                        }
                    ],
                    "formSubmissionDt": 1552031091965
                },
                {
                    "moduleId": 8043067,
                    "event": "ESIGN_AFTER",
                    "moduleName": "ORDERS",
                    "formName": "datePicker",
                    "formStatus": "ACTIVE",
                    "formdata": [
                        {
                            "field": "date",
                            "value": "1554834600000",
                            "type": "DATE"
                        },
                        {
                            "field": "text",
                            "value": "test"
                        }
                    ],
                    "formSubmissionDt": 1552031112446
                },
                {
                    "moduleId": 8043067,
                    "event": "PAYMENT_AFTER",
                    "moduleName": "ORDERS",
                    "formName": "Customer Feedback",
                    "formStatus": "ACTIVE",
                    "formdata": [
                        {
                            "field": "orderCollectedBy:",
                            "value": "test"
                        },
                        {
                            "field": "gender",
                            "value": "Male",
                            "type": "RADIO"
                        },
                        {
                            "field": "itemCount",
                            "value": "58"
                        },
                        {
                            "field": "e-Signature",
                            "value": "8043067_PAYMENT_AFTER_e-Signature_2019_03_08_13_15_27.jpg",
                            "type": "IMAGE"
                        },
                        {
                            "field": "image",
                            "value": "ORD_188_PAYMENT_AFTER_image_2019_03_08_13_15_42_211_camera.jpg",
                            "type": "IMAGE"
                        }
                    ],
                    "formSubmissionDt": 1552031146897
                },
                {
                    "moduleId": 8043067,
                    "event": "EPOD_AFTER",
                    "moduleName": "ORDERS",
                    "formName": "Customer Detail",
                    "formStatus": "ACTIVE",
                    "formdata": [
                        {
                            "field": "checkbox",
                            "value": "Options1",
                            "type": "CHECKBOX"
                        }
                    ],
                    "formSubmissionDt": 1552031150616
                }
            ]
        }
    ],
    "hasError": false
}
```

With this API you can fetch the details of Custom Forms associated with your Orders by passing the Order reference IDs of the required Orders.

For example, if you capture the parking or toll charges against an Order using custom forms in the TrackNext application, you can fetch the details of that data with this API. 

The details of the form data filled when submitting a custom form are present inside the formdata object in the API response. 
The 'field' key denotes the field name code that this particular element refers to.
The 'value' key denotes the data that was input when filling this 'field'
The 'type' key denotes the data type of the data captured.

Date fields stored at the custom form level will be returned in EPOCH format.

API Type: Tier 1 API


#### Request

<span class="post">POST</span>`https://api.loginextsolutions.com/ShipmentApp/mile/v1/customform/list`


#### Response Body

Parameter | DataType  |  Description
-----------|-------| ----------
referenceId | String | The reference ID of the Order.
tripName | String |Name of the trip the Order is associated with.
orderNo | String | Order number.
deliveryMediumName | String | Name of the Delivery Associate.
status | String | Order status.
results | List |This contains the results object.
results.event | String | This is the event that the custom form was associated with. The list of poosible events is listed in the table below.
results.moduleName | String | Name of the custom form Module. Will be hardcoded to 'ORDERS' if Order reference IDs are passed in the request body.
results.formName | String | Name of the custom form that was set when creating the template in LogiNext Mile.
results.formStatus | String | This will be hardcoded to 'ACTIVE' if the custom form is currently acitve. If the custom form has been deactivated this will be 'INACTIVE'.
results.formSubmissionDt | String | Form submission date in EPOCH format.
results.formdata | List | This list contains the custom form specific data associated with the order.
results.formdata.field | String | Field name code.
results.formdata.value | String | Field value that was filled when submitting the form.
results.formdata.type | String | Data type of the input field.

Event Key | Description
----------|------------
CHECKIN_AFTER | Custom form filled after the Check In screen on TrackNext.
LOAD_AFTER | Custom form filled after the Loading screen on TrackNext.
UNLOAD_AFTER | Custom form filled after the Unloading screen on TrackNext.
ESIGN_AFTER | Custom form filled after the ESIGN screen on TrackNext.
PAYMENT_AFTER | Custom form filled after the Payment screen on TrackNext.
EPOP_AFTER | Custom form filled after the E Proof of Pickup screen on TrackNext.
EPOD_AFTER | Custom form filled after the E Proof of Delivery on TrackNext.
PICKEDUP_AFTER | Custom form filled after the Pickup is complete for the Order.
NOTPICKED-UP_AFTER | Custom form filled after the Order is marked Not Picked Up.
DELIVERED_AFTER | Custom form filled after the Order is marked Delivered.
NOTDELIVER_AFTER | Custom form filled after the Order is marked Not Delivered.
PARTIALDELIVER_AFTER | Custom form filled after the Order is marked Partial Delivered.

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
If it does not exist, then a new manifest will be created with the provided Manifest ID

API Type: Tier 1 API

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

API Type: Tier 1 API


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

API Type: Tier 1 API

#### Request
<span class="post">GET</span>`https://api.loginextsolutions.com/TripApp/mile/v1/trip/get?referenceId=7f389cfa7ae64d85a915ee6297bd9c3f&tripname=TRIP-26516`

#### Request Parameters

Param | DataType | Length |  Required | Description
--------- | ------- | ------- | ---------- | ------------
referenceId | String |  | Conditional Mandatory |  If tripname is not passed in the request, then this field is mandatory. This is the reference ID of the trip.
tripname | String |  | Conditional Mandatory |  If referenceId is not passed in the request, then this field is mandatory. This is the trip name of the trip for which details are to be fetched.

### Update

> Definition

```json
https://api.loginextsolutions.com/TripApp/mile/v1/trip/update
```

> Request Body

```json
{
"tripReferenceId" : "65ba00dbdcf04fb789311df6aa40e3ba",
"tripName" : "23022020-Trip-Central Chicago",
"deliveryMediumReferenceId" :"96271ec538494ddf8e3ffe234c58b123"
}  
```

> Success Response

```json
{
  "status": 200,
  "message": "Trip Updated Successfully.",
  "data": {
    "tripReferenceId": "65ba00dbdcf04fb789311df6aa40e3ba",
    "deliveryMediumReferenceId": "96271ec538494ddf8e3ffe234c58b123"
  },
  "hasError": false
}

```

> Failure Response

```json
{
  "status": 409,
  "message": "Trip Updation Failed.",
  "error": [
    {
      "key": "tripReferenceId",
      "message": "Trip Reference Id is invalid."
    }
  ],
  "hasError": true
}

```
Update an existing trip  using this API. You can change the Trip Name or the Delivery Associate of this Trip

Type: Tier 1 API

#### Request

<span class="post">POST</span>`https://api.loginextsolutions.com/TripApp/mile/v1/trip/update`

#### Request Body

Parameter | DataType |  Required | Description
-----------|-------|------- | ----------
tripReferenceId | String | Mandatory | Reference Id of the trip.
tripName | String | Optional | New Trip name to be updated in the system.
deliveryMediumReferenceId | String | Optional | The Reference ID of the new Delivery Associate to be tagged to this Trip.


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
With this API, you can find out last tracked location for any order. The API accepts the reference IDs of the Orders you wish to track in the request, and returns the last received geocoordinates of the Order.

API Type: Tier 1 API

#### Request

<span class="post">GET</span>`https://api.loginextsolutions.com/TrackingApp/mile/v1/track/lastlocation`


### iFrame

> Definition

```json
https://api.loginextsolutions.com/track/#/order?ordno=1234&aid=4b41a94b-521b-4986-920d-6e4c1cf15fd0b6
```

The iFrame displays the last tracking for an order, including current location, based on the order no.
You can use this particular feature to display real time Order tracking information to your customers on your UI in Order to provide them great user experience.

You can do so by embedding the URL alongside in your client side application inside a 'frame' tag in the webpage's HTML. For example, this could be in the form of a 'Track' button on your UI that calls the iFrame URL when clicked. The tracking URL can then be opened on your webpage on your webiste's subdomain as an iFrame that will show your customers the live tracking of their Orders.

The Order number will need to be sent in the URL request along with the LogiNext token provided for calling the iFrame. 

Please note that the authentication token provided for the iFrame is different from the one provided to call the LogiNext API. Please reach out to your Account Manager to get this token if you wish to call the iFrame.

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
  "latitude": 40.760838,
  "longitude": 74.9099327
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

API Type: Tier 2 API

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
  "checkinLatitude":40.760838,
  "checkinLongitude":74.11223,
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

API Type: Tier 2 API

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
  "checkinLatitude":"40.760838",
  "checkinLongitude":"74 .11223",
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

API Type: Tier 2 API

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
    "latitude": 40.760838,
    "longitude": 74.9094089,
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
    "lastLatitude": 40.760838,
    "lastLongitude": 74.9094089,
    "isFirstPointFl": "0",
    "currentTime": 1512976899548,
    "previousTime": 1512976899532,
    "signalStrength": 30,
    "appStatus": "100",
    "networkType": "WIFI",
    "dataNetworkType": "Unknown",
    "isGsmFl": false,
    "isActiveNetworkMetered": false,
    "imei": "911380458661315"
  }, {
    "latitude": 40.760838,
    "longitude": 74.9094089,
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
    "lastLatitude": 40.760838,
    "lastLongitude": 74.9094089,
    "isFirstPointFl": "0",
    "currentTime": 1512976879541,
    "previousTime": 1512976879521,
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
    "status": 500,
    "message": "Error occured!",
    "moreResultsExists": false,
    "hasError": true
}

```


With this API, you can send the current position of your Delivery Associates / Field Executives when they are not using LogiNext Mobile App.

API Type: Tier 2 API

#### Request

<span class="post">POST</span>`https://products.loginextsolutions.com/TrackingApp/track/mobile/put`

#### Request Body

Parameter | DataType |  Length | Required | Description
-----------|-------|------- | ----|----------
latitude|Double | 13,10 |Mandatory|The geocoordinate(Latitude) of the Delivery Associate's location. Sample Value - 40.760838
longitude|Double | 13,10 |Mandatory|The geocoordinate(Longitude) of the Delivery Associate's location. Sample Value - 74.9094089
trackingDt|String| | Mandatory|This is the timestamp of the tracking Date and Time in UTC and the mentioned Format. Sample Value - 2018-12-11T07:21:39Z
currentTime|Long| |Mandatory|This is the current timestamp at the time of sending the tracking data to LogiNext. Sample Value - 2018-12-11T07:21:39Z
speed|Number| | Mandatory| The speed of the Delivery Associate at the time of sending the tracking data.Current Speed in meters / second. This can be received from the Android system classes. More information on this can be found in the Android documentation <a href="https://developer.android.com/reference/android/location/Location.html#getSpeed()" target="_top">here
battery|Integer| 3 |Mandatory|This is the pattery percentage on the Delivery Associate's phone at the time of sending the tracking point. Sample Value - 92. MOre details on this can be found here<a href="https://developer.android.com/reference/android/net/ConnectivityManager#TYPE_MOBILE" target="_blank">.
accuracy|Number| 13,10 | Mandatory|Estimated accuracy of the current location in meters Sample Value - 23.878000259
altitude|Number| 10 | Optional|In meters Sample Value - 235
bearing |Number| 10 | Optional|Horizontal distance of travel of the device, in degrees. If the phone has this sensor, then send this value. Sample Value - Any value between 0 to 3600. 0 is North.  Consider Clockwise movement.
locationSource|String| 32 | Optional|Location Provider Values like - “fused” , “wifi”, “gps”
type |String| 40 |Mandatory| The tracking type field is used to identify if the tracking is coming from the Delivery Associate's phone or some other device. This is to be hardcoded to “MOBREG” in case the tracking points will be coming from the phone.
isFirstPointFl|Boolean| 1 | Mandatory| This is used to identify if the current tracking data being sent from the Delivery Associate's device is the first update after every login.|First Point - 0 Then there afterwards - 1 Sample Value -  0 (= False)  1 (= True)
lastLatitude|Double| 13,10 | Mandatory| Last known Latitude Note that if the isFirstPointFl value is “1”, then you can pass zero in this field Sample Value - 40.760838
lastLongitude| Double | 13,10 | Mandatory|  Last known Longitude Note that if the isFirstPointFl value is “1”, then you can pass zero in this field Sample Value - 74.9094089
distanceFromLastLocation| Number|| Mandatory| Distance between last location update in meters. Note that if the isFirstPointFl value is “1”, then you can pass zero as the distance from last location. Sample Value - 23.5
previousTime|Long| | Mandatory|Timestamp of last location update in milliseconds Sample Value - 23.878000259
hasAccuracy|Boolean| 1 |Optional|True, if the current location has an accuracy 0 (= False) / 1 (= True)
hasBearing |Boolean| 1 |Optional|True, if the current location has a bearing 0 (= False) / 1 (= True)
hasSpeed | Boolean| 1 | Optional|True, if the current location has a speed 0 (= False) / 1 (= True)
networkType|String| |Optional|This field is used to identify the network type the Delivery Associate's phone is connected to when the tracking point is sent. This can be received from the Android core Connectivity Manager APIs <a href="https://developer.android.com/reference/android/net/ConnectivityManager#TYPE_MOBILE" target="_blank">here</a>. Sample Value can include WIFI / MOBILE / UNKNOWN
signalStrength|Integer| |Mandatory| This field is to signify the strength of the mobile network on the Delivery Associate's phone at the time when the tracking point is sent. (Wifi, GSM, LTE)|Sample Value - 23. This can be received from the Android core Connectivity Manager <a href="https://developer.android.com/reference/android/telephony/SignalStrength.html#getGsmSignalStrength()" target="_blank">here.
dataNetworkType|String| |Optional|Data Connectivity Type. Sample Values - 1xRTT, EDGE, LTE, CDMA, GPRS, HSPA
isGsmFl|Boolean| 1 | Optional|Current connectivity type. Sample Value - 0 (= False) 1 (= True). This can be received from the Android core Connectivity Manager <a href="https://developer.android.com/reference/android/telephony/SignalStrength.html#isGsm()" target="_blank">here.
isActiveNetworkMetered|Boolean| 1 |Optional| Is the currently active data network is metered. A network is classified as metered when the user is sensitive to heavy data usage on that connection due to monetary costs, data limitations or battery/performance issues. Sample Value -  0 (= False)  1 (= True). This can be received from the Android core Connectivity Manager APIs <a href="https://developer.android.com/reference/android/net/ConnectivityManager#isActiveNetworkMetered()" target="_blank">here.
appStatus| Integer||Optional| Activity status of the app (Foreground, Background, Service, Gone, Sleep, Visible, Unknown). Sample Values - 100 (~ Foreground) 400 (~ Background) 500 (~ Empty) 125 (~ Foreground_Service) 1000 (~ Gone) 200 (~ Visible). More information on this can be found on the Android Activity Manager documentation <a href="https://developer.android.com/reference/android/app/ActivityManager.RunningAppProcessInfo" target="_blank">here.
imei|String|40|Mandatory|IMEI number for device Sample Value - 911380134661315


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
"latitude": 40.760838,
"longitude": 74.9095327
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

### Plan

> Definition

```json
https://api.loginextsolutions.com/TripApp/mile/v1/plan
```

> Request Body

```json
{
  "routeName": "PLAN-1548845037527",
  "startTimeWindow": "2018-12-01T10:43:57.563Z",
  "endTimeWindow": "2018-12-31T10:43:57.560Z",
  "hubReferenceIds": [],
  "orderReferenceIds": ["8dd4e493c715493da182f52eb69d1bcb", "73d57cbe0dc147da8c6b4503b76d5bda"],
  "planningProfile": "1",
  "territoryProfile": "80",
  "mode": "OPTIMIZE_DISTANCE_TIME",
  "deliveryMediumReferenceIds": ["8dd4e493c715493da182f52eb69d1bcb", "73d57cbe0dc147da8c6b4503b76d5bda"],
  "deliveryMediumStartLocation" : "hub"
}


```

> Success Response

```json
{
  "status": 202,
  "data": "Planning request received successfully.",
 "message": “Success!”
}

```

> Failure Response

```json
{
    "status": 409,
    "message": "Bad Request",
    "errors": [
        {
            "key": "routeName",
            "code": "Duplicate Route Name"
        },
        {
            "key": "deliveryMediumReferenceIds",
            "code": "Delivery Medium reference ids are required"
        }
    ]
}

```

The Plan API allows you to create Optimised Route Plans in LogiNext for your Orders.

The API accepts the details of your Owned and Outsourced Fleet and can plan for a single Route Planning operation using details of both fleets.

This is an async API. The response to the API request will have a 202 status code. The results of the replanning operation will be sent back in the form of the Route Planning webhook to the URL configured in your system with new sequence of Orders.

Note that with this API you can plan for upto 2500 orders in one request.

API Type: Special Tier API. The rate Limit for this API is 1 request per minute.

#### Request

<span class="post">POST</span>`https://api.loginextsolutions.com/TripApp/mile/v1/plan`


#### Request Body

Parameter | DataType | Length |  Required | Description
-----------|-------|------- |------- | ----------
routeName | String | 32 | Mandatory | This is the Name of the Route Plan
startTimeWindow | String | 32 | Conditional Mandatory | This is the start time window of the Orders to be considered for route planning. If orderReferenceIds are not passed, this field is Mandatory.
endTimeWindow | String | 32 | Conditional Mandatory | This is the start time window of the Orders to be considered for route planning. If orderReferenceIds are not passed, this field is Mandatory.
hubReferenceIds | List | 32 | Optional | This is a list of Hubs the current Route Plan is to be run for. If not passed, the Route Planning operation will run for the Parent Hub.
orderReferenceIds | List | 32 | Conditional Mandatory |  This is the list of Orders to be considered for Route Planning.If start and end time are not passed, this field is Mandatory.
planningProfile | String | 32 | Optional | This is the name of the Planning Profile you wish to use for the Current Route Planning operation. You can setup multiple Route Planning profiles in your LogiNext account. If not passed, your default Route Planning profile will be considered.
territoryProfile | String | 32 | Optional | This is the name of the Territory Profile you wish to use for the Current Route Planning operation. You can setup multiple Territory profiles in your LogiNext account. If not passed, your default Territory profile will be considered.
mode | String | 32 | Mandatory | The planning objective for the route planning operation. This can be one of - 'CONSIDER_RESOURCE_COST' to optimize Fleet capacity, 'OPTIMIZE_DISTANCE_TIME' to optimize time and distance, 'LOADBALANCING' for balanced optimization, or 'SEQUENCE' for sequence optimization
deliveryMediumReferenceIds | List | 32 | Optional | This is the list of Delivery Associate's to be considered for the current Route Planning Operation. If not passed then All active and present Delivery Associates will be considered.
deliveryMediumStartLocation | List |  | Optional | This is the  Delivery Associate's starting location to be considered in planning. This can be 'hub' or 'home'


###  Optimize

> Definition

```json
https://api.loginextsolutions.com/TripApp/mile/v1/optimize
```

> Request Body

```json
{
"routeName" : "Route237",
"planningProfile":"PlanP1",
"plan" : [{
  "deliveryMediumReferenceId": "f40cf4493a5949199775499b5750a272", 
  "orderReferenceIds":[
    "8dd4e493c715493da182f52eb69d1bcb",
    "f40cf4493a5949199775499b43545656"
  ]},
  {
    "deliveryMediumReferenceId": "f40cf4493a5949199775499b5750a272",
    "orderReferenceIds":[
      "8dd4e493c715493da182f52eb69d1bcb",
      "f40cf4493a5949199775499b5750a272"
    ]
  }]
}

```

> Success Response

```json
{
    "status": 202,
    "message": "Success",
    "data": "Sequencing request received successfully."
}

```

> Failure Response

```json

"status": 409,
    "message": "Bad Request",
    "errors": [
        {
            "key": "plan",
            "message": [
                "f40cf4493a5949199775499b5750a272",
                "f40cf4493a5949199775499b5750a272"
            ],
            "code": "Delivery Associate(s) does not exist"
        },
        {
            "key": "plan",
            "message": [
                "8dd4e493c715493da182f52eb69d1bcb",
                "f40cf4493a5949199775499b43545656",
                "8dd4e493c715493da182f52eb69d1bcb"
            ],
            "code": "Orders do not exist"
        },
        {
            "message": [
                "f40cf4493a5949199775499b5750a272"
            ],
            "code": "Planning allowed only for Not Dispatched Orders"
        },
        {
            "key": "planningProfile",
            "code": "Invalid Planning profile"
        }
    ]
}

```

The Route Optimization API allows you to create Optimised Route Plans in LogiNext for your Orders.

Use this API when you have a list of Orders assigned to a Delivery Associate, and you need an optimizes sequence to deliver those Orders. For example, you you have Orders to be Delivered in the Lower Manhattan area, and you have a Delivery Associate that if familiar with the Lower Manhattan area, this Delivery Associate would be the best person to fulfil those Orders. This API will return the most optimized sequence in which this Delivery Associate can fulfil these Orders.


This API will support maximum of 150 orders per Delivery Associate, and upto 20 Delivery Associates per request.

This is an async API. The response to the API request will have a 202 status code. The results of the replanning operation will be sent back in the form of the Route Planning webhook to the URL configured in your system with new sequence of Orders.

This API will not accept Orders that are in any state besides Not Dispatched. If Orders that are In Transit or Delivered are passed in the API request, the API will return a failure response.

API Type: Special Tier API. The rate Limit for this API is 1 request per 20 seconds.

#### Request

<span class="post">POST</span>`https://api.loginextsolutions.com/TripApp/mile/v1/optimize`


#### Request Body

Parameter | DataType | Length |  Required | Description
-----------|-------|------- |------- | ----------
routeName | String | 32 | Mandatory | This is the Name of the Route Plan
planningProfile | String | 32 | Optional | This is the name of the Planning Profile you wish to use for the Current Route Planning operation. You can setup multiple Route Planning profiles in your LogiNext account. If not passed, your default Route Planning profile will be considered.
plan.deliveryMediumReferenceId | String | 32 | Mandatory | This is the list of Delivery Associate's to be considered for the current Route Planning Operation.
plan.orderReferenceIds | List | 32 | Optional | This is a list of Orders to be optimized for the Delivery Associate




### Replan 

> Definition

```json
https://api.loginextsolutions.com/TripApp/mile/v1/resequence
```

> Request Body

```json
[
"8dd4e493c715493da182f52eb69d1bcb"
]

```

> Success Response

```json
{
    "status": 202,
    "message": "Success",
    "data": "Replanning request received successfully."
}
```

> Failure Response

```json
{
    "status": 400,
    "message": "Bad Request",
    "errors": [
        {
            "key": "",
            "message": [
                "73d57cbe0dc147da8c6b4503b76d5bda"
            ],
            "code": "Trip does not have any pending shipments to be replanned"
        }
    ]
}
```

With this API you can replan Not Started or Started trips by providing the LogiNext reference ID of the trip in the request. The operation will provide an updated seqence in which the remaining Orders of that Trip should be delivered in. The results 

For Not Started Trips, the API considers the Hub location as the starting point. For Started Trips, the API considers the last tracked location of the Delivery Associate whose Trip it is. If no last tracking is received for the Delivery Associate, then the location of the last Delivered Order will be used.

If there are Orders that can no longer be fulfilled within their service windows at the time of replanning, those Orders will get unassigned from the Trip and will be a part of the unallocation reasons object in th Route Planning webhook. These Orders can then be manually assigned to other Trips using the 'Suggest Trips' API and the 'Assign' API.

All Not Delivered Orders will be considered for replanning with this API. For example, if your Delivery Associate delivered Orders #1 and #4 in their Trip, and calls this API, then Orders #2 and #3 in their Trip will also be replanned. The new sequence of Orders after replanning will start from #5 in the above case as Order #4 was already Delviered. Sequence #2 and #3 will remain blank.

This is an async API. The response to the API request will have a 202 status code. The results of the replanning operation will be sent back in the form of the Route Planning webhook to the URL configured in your system with new sequnce of Orders.


API Type: Special Tier API. The rate Limit for this API is 1 request per 20 seconds.

#### Request

<span class="post">POST</span>`https://api.loginextsolutions.com/TripApp/mile/v1/resequence`


#### Request Body

Parameter | DataType | Length |  Required | Description
-----------|-------|------- |------- | ----------
reference ID | String | 32 | Mandatory | Trip Reference ID for the trip you wish to replan.


### Route Planning as a Service

> Definition

```json
https://api.loginextsolutions.com/TripApp/deliveryplanner/v1/plan
```

> Request Body

```json
{
  "routeName":"fas",
  "startLocation": {
    "latitude": 40.760838,
    "longitude": 74.9047021
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
      "latitude": 40.760838,
      "longitude": 74.8925094
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

With this API you can create an optimised Route plan for Orders in the your system. You will need to provide the details of the of your Orders (like weight, volume, geocoordinates and service windows) along with the details of your fleet(weight, volume, and capacity).

The Route Planning operation will provide a list of optimised routes based on the details provided.

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
 "apartment": "611",
 "streetName": "5th Ave",
 "landmark": "near Saks",
 "city": "New York City",
 "country": "United States",
 "state": "NY",
 "pincode": "10022"
}
```

> Get Geocode - Sample Response

```json
{
   "status": 200,
   "message": "Geocodes Fetched Successfully",
   "moreResultsExists": false,
   "data": [
       {
           "lat": 40.75813,
           "lng": -73.9772,
           "geocodingSource": "GOOGLE_GEOCODING",
           "types": "[department_store, establishment, point_of_interest, store]"
       }
   ],
   "hasError": false
}

```

This API gets coordinates for a given location.

#### Request

<span class="post">POST</span>`https://api.loginextsolutions.com//CommonApp/mile/v1/geocode`


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



## Location Serviceability

> Sample Request

```json

{
"latitude" : "40.760838", 
"longitude" : "74.832830",
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
        "geofenceReferenceId": "3e290b46495b482a8e70e1078bd73c3f",
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
    "deliverLatitude":40.760838,
    "deliverLongitude":74.619392,    
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
autoAllocateFl| String | 50 | Optional | This can be "Y", "N", or "P". If set to "Y", the Task will be automatially allocated to the nearest Delivery Associate when it is created in the system. The behaviour of the auto assignment will be dependant on the configurations set in the 'Auto Assignment Profile' screen in your LogiNext Account settings screen. If "N", the Task will not be considered for auto assignment at the time of Task Creation
shipmentTaskDt | Date |  | Mandatory | Task Date Format - YYYY-MM-DDTHH:MM:SS.SSSZ e.g. : 2016-07-01T11:18:00.000Z.
distributionCenter | String | 255 | Mandatory | Distribution center's name. The Distribution center is the Hub that is responsibile for fulfilling the Order. An Order can have different Pickup and Delivery leg branches, but will require a single Distribution center that is responsible for the fulfillment of the Order.
packageWeight | Double | 10 | Optional | This is the weight of package in Kg.
packageVolume | Double | 10 | Optional | This is the volume of package in CC
packageValue | Double | 10 | Optional | This is the value of package
numberOfItems | Integer | 20 | Optional | This is the number of crates
paymentType | String | 40 | Optional | This is the payment mode. Ex: COD - Cash On Delivery, Prepaid. Note that the Payment Type is dependant on the language preference configured for the user account the API token was created from. You can refer to the 'Authenticate' API documentation for more details on this.
partialDeliveryAllowedFl | String | 50 | Optional | This is the is Partial Delivery allowed. Ex: Y/N. Default value is N.
returnAllowedFl | String | 1 | Optional | This field specifies if the task can be returned. Ex: Y/N. Default value is Y.
cancellationAllowedFl | String | 1 | Optional | Is Cancellation allowed. Ex: Y/N. Default value is Y.
deliverBranch | String | 255 | Mandatory | Name of delivery branch
deliverServiceTime | Integer | 11 | Mandatory | Deliver service time in mins.
deliverStartTimeWindow | Date |  | Mandatory | Deliver start time window. Format - YYYY-MM-DDTHH:MM:SS.SSSZ e.g. : 2016-07-01T11:18:00.000Z.
deliverEndTimeWindow | Date |  | Mandatory | Deliver end time window. Format - YYYY-MM-DDTHH:MM:SS.SSSZ e.g. : 2016-07-01T11:18:00.000Z.
deliveryType | String | 40 | Optional | Task delivery type. Ex: TRK - Truck, VAN - Van, RIDER - Delivery Associate
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
            "originLatitude": 40.760838,
            "originLongitude": 74.849
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
    "latitude": 40.760838,
    "longitude": 74.910214,
    "updateTime":"2018-07-18T10:31:00.000Z"
  },
  {
    "taskReferenceId":"6186d7r5te324c42abb5ea1a32x45f66",
    "reasonCd":"DBUNAVAILABLE",
    "otherReason":"",
    "latitude": 40.760838,
    "longitude": 74.913214,
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
With this API, you will be able to update the the status of a Task.
You can pass multiple task reference IDs and can update the status of a task.

#### Request

<span class="post">PUT</span>`https://api.loginextsolutions.com/ShipmentApp/field/v1/update/status`


#### Request Parameters

Param | DataType | Length |  Required | Description
--------- | ------- | ---------- | ---------- | ------------
newStatus | String | 20 | Mandatory |  One status for multiple orders.The orders will be updated with this new status<br>Available Values - <PICKEDUP> - When an Order has been picked up by a Delivery Associate<br>DELIVERED - When an order has been Delivered by the associate<br>NOTPICKEDUP - When the associate reached the Pick-up location, but could not pick-up the order due to one or the other reason<br>NOTDELIVERED - When the associate reached the delivery location, but could not deliver the order due to one or the other reason
orderReferenceId | String | 100 | Mandatory |  This is the LogiNext Reference ID for the Order<br>This is generated when the order is added in the LogiNext application.
reasonCd | String | 255 | Conditional Mandatory | Mandatory depending upon the status selected : NOTDELIVERED, NOTPICKEDUP, CANCELLED<br>Else Optional.<br>If you have pre-configured the reasons for Order Status Update - NOTDELIVERED, NOTPICKEDUP and CANCELLED in LogiNext application, then it is mandatory to mention that relevant configured reason here.<br>One of the other values here is OTHER, in case the delivery Associate selects the reason as Others.
otherReason | Date |  | Conditional Mandatory | Mandatory when reasonCd is OTHER
latitude | Double | 15 | Conditional Optional | Geo-location where Order status was updated<br>Sample Value - "40.760838"
otherReason | Date | 15 | Conditional Optional | Geo-location where Order status was updated<br>Sample Value - "74.996"
updateTime | Date | 15 | Conditional Optional | This is the timestamp (in UTC format) when the order status was changed. This cannot be greater than the time at which the API is hit. If not passed, the timestamp of the API hit is considered as the timestamp for the status change.

# Custom Fields

> Request

```json

"customFields":[
    {

    "field":"cf_cutOffDate",
    "value":"2018-06-25T07:31:39Z.000"
    }
    
    ]
```


If you require certain additional fields to store information regarding your Orders or Resources in LogiNext, you can use our Custom Fields features.

With Custom Fields, you can enter information for reporting and analytics purposes specific to your business use case.

For eg - If you need to look for specific servicability constraints like cut off times within with a certain area/ geofence can be serviced, you can configure a cut off time custom field in LogiNext that will display the availability timelines for that area/ geofence.

To configure Custom Fields for your account, You can do so from the Custom Fields section of your Admin module.

Once configured, you can enter data for the custom fields like any other field in LogiNext. These fields are currently available in the APIs and UI. Please note that when passing a Custom Field name in the API request object, the Custom Field name would have be preceeded by 'cf_' to signify that this is a Custom Field. 

Please Note that if you send these fields in the API without first configuring them in your LogiNext account, the LogiNext API will NOT create a new Custom Field. You will receive a success response from such an API call, but the data sent in the 'customField object will not be considered. The data passed in the API can only be associated with an already existing Custom Field with the identifier specified in the request. 

If using the API, you will need to add the Custom Fields object on the right as part of the API request body to create the new fields in LogiNext.

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

Note that Date and DateTime type of type of Custom Fields will be sent in UTC format in POST API calls, and will be fetched in Epoch format in Get API calls. For example, In the Create Order API, you could pass "shipmentOrderDt": "2016-07-15T10:30:00.000Z". In Custom fields a DateTime field would have the sample value '1485153536000', which will represent a timestamp.

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
6. You can choose to configure an additional security parameter in the LogiNext webhooks Header in the 'x-loginext-signature' header. You can choose to have an APP SECRET configured in LogiNext for this header, and LogiNext will send this APP SECRET in all your configured webhooks. You can validate the value of this header to verify that the webhook request originated from LogiNext. In order to configure this additional security parameter, please reach out to your Account Manager.


## Orders

### Create

> Response

```json
{
  "notificationType": "ORDERCREATIONNOTIFICATION",
  "timestamp": "2018-06-25 07:31:39",
  "orderNo": "CATS487",
  "referenceId": "143b28d87ghf46098de38b0ccce51a5d",
  "awbNumber": "AW234-TG",
  "orderState": "FORWARD",
  "orderLeg": "DELIVER",
  "pickupAccountCode": "JAMES1",
  "pickupAddressId": "HOME",
  "deliverAccountCode": "WAYNE",
  "deliverAddressId": "OFFICE",
  "returnAccountCode": "JAMES1",
  "returnAddressId": "P1947",
  "clientCode":"MyKart"
}
```

This notification is sent when an order is created.

Param | DataType | Description
--------- | ------- | ----------
notificationType | String | This is the notification of the event that triggered the webhook. In case of Order Creation it is hardcoded to 'ORDERCREATIONNOTIFICATION'
timestamp | String | this represents the Order creation timestamp
orderNo | String | This is the Order No.
referenceId | String | Order reference id.
awbNumber | String | AWB Number for the order
orderState | String | State of order. Ex: FORWARD, REVERSE
orderLeg | String | Order leg Ex: PICKUP, DELIVER
pickupAccountCode| String| Custoemr ID of the pickup customer. This field will be sent if the Order has a Pickup leg.
pickupAddressId | String | Address ID of the delivery customer. This field will be sent if the Order has a Pickup leg.
deliverAccountCode| String| Custoemr ID of the deliver customer. This field will be sent if the Order has a Deliver leg.
deliverAddressId | String | Address ID of the delivery customer. This field will be sent if the Order has a Deliver leg
returnAccountCode| String| Custoemr ID of the deliver customer. This field will be sent if the Order has a Return leg i.e the is Return allowed option was selected at the time of Order creation.
returnAddressId | String | Address ID of the delivery customer. This field will be sent if the Order has a Return leg i.e the is Return allowed option was selected at the time of Order creation.
clientCode | String | Account name. This field is sent if the Order was created for a particular Account.

### Update

> Response

```json
{
  "notificationType": "ORDERUPDATENOTIFICATION",
  "orderNo": "CATS487",
  "orderReferenceId": "93780c3292ba4ee4809ad125ef97",
  "vehicleNumber":"MH04DY69",
	"awbNumber": "AWB001",
	"deliveryMediumName": "kumari2",
	"phoneNumber": "6590110114",
	"orderState": "FORWARD",
  "startTimeWindow": "2017-08-17 02:00:00",
  "endTimeWindow": "2017-08-17 03:00:00",
  "tripReferenceId": "c1aa3beae7844b77a90bb6fe0518992c",
  "numberOfItems": 1,
  "packageWeight": 10.0,
  "packageVolume": 4500.0,
  "originAddr": "123,Supreme Business Park,Hiranandani,DMart,Mumbai,400076",
  "destinationAddr": "Destinatioln Address",
  "shipmentOrderTypeCd": "PICKUP",
  "clientNodeName": "Client Node Name",
  "clientNodeCd": "Client Node Code",
  "address": "145 West Coast Road, Singapore, Singapore, Singapore, SINGAPORE, 127367",
  "deliveryType": "RIDER",
  "shipmentNotes": "PickedUp",
  "assignmentMethod": "MANUAL",
  "calculatedStartDt": "2017-08-18 12:53:00",
  "calculatedEndDt": "2017-08-17 02:52:00",
  "orderStatus": "INTRANSIT",
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
  ]
}
```


This notification is sent when an order is updated.

Param | DataType | Description
--------- | ------- | ----------
notificationType | String| This is the notification of the event that triggered the webhook. In case of Order Creation it is hardcoded to 'ORDERUPDATENOTIFICATION' 
orderNo | String | Order No.
orderReferenceId | String | Order reference id.
vehicleNumber | String | Vehicle Number
awbNumber | String | AWB Number
deliveryMediumName | String | Delivery Associate's name
phoneNumber | Integer | Delivery Associate's phone number
orderState | String | eg. FORWARD or REVERSE
shipmentCrateMapping | Array | Array of String of mapped crate
startTimeWindow | String | Order's start time window
endTimeWindow | String  | Order's end time window
tripReferenceId | String | Trip Reference Id. This will be sent if the Order is currently part of a Trip.
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
calculatedStartDt | String  | This is the Calculated start date
calculatedEndDt | String  | Calculated end date
orderStatus | String | The current state of the Order.

### Order Status Update

> Response

```json
{
  "notificationType": "ORDERSTATUSNOTIFICATON",
  "orderNo": "ScanWithAwbOrOrder4",
  "orderReferenceId": "3a2511a92bac464aa001f75f4ba84b7f",
  "scanStatus": "INSCANNED",
  "orderStatus": "NOTDISPATCHED"
  "orderLeg": "DELIVER",
  "awbNumber": "AwbNoOnly",
  "orderState": "FORWARD",
  "branchName": "Powai Vendor",
  "scanTime": "2019-04-26 07:30:55",
  
}

```

This notification is sent when an order Status change occurs. This webhook is triggered at 4 events. When an Order is in scanned, out scanned, handed over or closed.



#### Response Parameters


Param | DataType | Description
--------- | ------- | ----------
notificationType | String | This is the notification of the event that triggered the webhook. In case of Order Creation it is hardcoded to 'ORDERSTATUSNOTIFICATON'.
orderNo | String | Order No.
orderReferenceId | String | Order reference id.
scanStatus | String | Scan Status of the Order. This can be INSCANNED, OUTSCANNED, HANDEDOVER, CLOSED.
branchName | String | Branch Name.
orderLeg | String | Order Leg.
awbNumber | String | AWB Number.
orderState | String | Order State.
branchName | String | Branch Name.
scanTime | String | Order Scan Timestamp.


### Accepted

> Response

```json
{
  "clientShipmentId": "Order_001",
  "status": "ORDER ACCEPTED",
  "awbNumber": "AWB123456789",
  "deliveryMediumName": "Thomas Watson",
  "deliveryMediumUserName": "Thomas",
  "carrierName":"A&C Transporters",
  "carrierBranchName":"Brooklyn",
  "phoneNumber": "9881234567",
  "tripName": "Trip_1227",
  "updatedOn": "2019-06-30 19:43:07",
  "trackUrl": "https://goo.gl/qhZP63",
  "pickupEndDate": "2019-11-20 10:23:20",
  "deliveryEndDate": "2019-11-20 10:23:20",
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
deliveryMediumName | String | Name of Delivery Associate who Accepted the Order. This field will not be sent if Order is assigned to a Carrier.
deliveryMediumUserName | String | Username of Delivery Associate who Accepted the Order. This field will not be sent if Order is assigned to a Carrier.
carrierName | String | Name of the Carrier who Accepted the Order. This field will not be sent if Order is assigned to a Driver.
carrierBranchName | String | Name of the Carrier who Accepted the Order. This field will not be sent if Order is assigned to a Driver.
latitude | Double | The geo-coordinate(latitude) of the Delivery Associate when the Order was accepted
longitude | Double | The geo-coordinate(longitude) of the Delivery Associate when the Order was accepted.
phoneNumber | String | Delivery Associate's phone no.
tripName | String | Trip name
updatedOn | String | Accept order timestamp
trackUrl | String | Url to track Order
deliveryEndDate | String | Delivery end date.
pickupEndDate | String | Planned ETA for the Delivery Associate to complete the Pick-up activity.
orderReferenceId | String | Order Reference Id


### Rejected

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



### Cancel

> Response

```json
{
  "notificationType": "CANCELLEDNOTIFICATION",
  "cancellationTime": "2016-12-05 12:59:16",
  "orderNo": "CATS487",
  "orderReferenceId": "cd81bd6ab1104dc3841e3ae405b",
  "awbNumber": "AWB123456789",
  "orderLeg": "DELIVER",
  "orderState": "FORWARD",
  "tripName": "TRIP-809",
  "deliveryMediumName": "Abhi.P",
  "customerCode": "Cust122435",
  "customerName": "Name",
  "phoneNumber": "9922904337",
  "reason": "Customer Unavailable",
  "reasonCd": "Customer Unavailable Cd",
  "cancelledBy": "M. Smith",
  "isCancelOccurAfterPickupFl": false
}
```

This notification is sent when an order is cancelled.

#### Response Parameters

Param | DataType | Description
--------- | ------- | ----------
notificationType | String | This is the notification of the event that triggered the webhook. In case of Order Creation it is hardcoded to 'CANCELLEDNOTIFICATION'.
cancellationTime | String | Cancellation timestamp. This will have the time in UTC.
orderNo | String | Order No.
orderReferenceId | String | Order Reference Id
awbNumber | String | AWB Number for the order
orderLeg | String | Order leg Ex: PICKUP, DELIVER
orderState | String | State of order. Ex: FORWARD, REVERSE
tripName | String | Name of the Trip the Order is currently in.
deliveryMediumName | String | Name of Delivery Associate. This will be sent if the Order was assigned to a Delivery Associate when it was cancelled.
phoneNumber | Long | Delivery Associate's phone no.
customerName | String | Name of customer
reason | String | Reason for the order being cancelled
reasonCd | String | Reason code
cancelledBy | String | Cancelled by user name
isCancelOccurAfterPickupFl | Boolean | whether order was cancelled after Pickup


### Check In

> Response

```json

{
  "orderNo": "CATS487",
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



### Load Items

```json
{
  "orderNo": "CATS487",  
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
notificationType | String | This is the notification of the event that triggered the webhook. In case of Order Creation it is hardcoded to 'LOADITEMNOTIFICATION'.
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

### Load Complete

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
notificationType | String | This is the notification of the event that triggered the webhook. In case of Order Creation it is hardcoded to 'LOADINGDONENOTIFICATION'.

### Delivered

> Response

```json
{
  "orderNo": "CATS487",
  "latitude":41.882702,
  "longitude":-87.619392,   
  "notificationType": "DELIVEREDNOTIFICATION",
  "orderLeg": "DELIVER",
  "awbNumber": "AWB012345678",
  "customerComment": "User comments",
  "customerRating": 5,
  "deliveryMediumName": "Suresh",
  "phoneNumber": 1234567864,
  "orderState": "FORWARD",
  "customerName": "John Watson",
  "deliverAccountCode": "JohnWatson",
  "deliverAddressId": "Home",
  "pickupAccountCode":"JamesDean", 
  "pickupAddressId": "Office",
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
notificationType | String | This is the notification of the event that triggered the webhook. In case of Order Creation it is hardcoded to 'DELIVEREDNOTIFICATION'.
orderLeg | String | Order leg, Possible values : DELIVER, PICKUP
awbNumber | String | Awb No.
customerComment | String | Customer comments
customerRating | Double | Rating provided by customer
deliveryMediumName | String | Name of Delivery Associate
phoneNumber | Long | Delivery Associate's phone no.
orderState | String | Order state, Possible values : FORWARD, REVERSE
customerName | String | Customer name
pickupAccountCode | String | Pickup Customer ID. This field will be absent for a DELIVER type Order.
pickupAddressId| String | Pickup Customer ID. This field will be absent for a DELIVER type Order.
deliverAccountCode | String | Deliver Customer ID. This field will be absent for a PICKUP type Order.
deliverAddressId | String | Deliver Customer Address ID. This field will be absent for a PICKUP type Order.
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


### Partially Delivered

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
notificationType | String | This is the notification of the event that triggered the webhook. In case of Order Creation it is hardcoded to 'PARTIALDELIVERYNOTIFICATION'.
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

### Not Delivered

> Response

```json
{
  "orderNo": "CATS487",
  "latitude":41.882702,
  "longitude":-87.619392,   
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
notificationType | String | This is the notification of the event that triggered the webhook. In case of Order Creation it is hardcoded to 'NOTDELIVEREDNOTIFICATION'.
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

### Pickedup

> Response

```json
{
  "notificationType": "PICKEDUPNOTIFICATION",
  "orderNo": "CATS487",
  "orderReferenceId": "b7b15a79d6734297a00a93755856e8c8"
  "awbNumber": "AWB001",
  "pickedUpTime": "2016-11-19 06:33:48",
  "latitude":41.882702,
  "longitude":-87.619392,   
  "status": "PICKEDUP",
  "orderLeg": "PICKUP",
  "deliveryMediumName": "James",
  "customerComment": "Test user comments",
  "customerRating": 0,
  "phoneNumber": 1234565435,
  "orderState": "FORWARD",
  "branchName": "1008",
  
}


```

This notification is sent when an order is picked up by a Delivery Associate.



#### Response Parameters

Key | DataType | Description
--------- | ------- |-------
notificationType | String | This is the notification of the event that triggered the webhook. In case of Order Creation it is hardcoded to 'PICKEDUPNOTIFICATION'.
orderNo | String | Order No.
orderReferenceId | String | Order Reference Id
awbNumber | String | AWB Number for the order
pickedUpTime | String | Timestamp of the event when the Order was marked Pickedup by the Delivery Associate.
latitude | Double | Geo coordinates(latitude) of the location where order was marked Pickedup.
longitude | Double | Geo coordinates(longitude) of the location where order was marked Pickedup.
status | String | The new status of the Order. Will be 'PICKEDUP' in case of this webhook.
orderLeg | String | Order leg Ex: PICKUP, DELIVER
customerComments | String | Customer comments provided by the Customer during the Pickup leg of the Order.
customerRating | Double | Rating provided by customer in the Pickup leg of the Order
deliveryMediumName | String | Name of Delivery Associate
phoneNumber | Long | Delivery Associate's phone no.
orderState | String | State of order. Ex: FORWARD, REVERSE
branchName | String | Distribution Center of the Order.



### Not Pickedup

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

### Allocation End

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


### Get E-POD & ESign

> Response

```json

{
  "timestamp": "2019-08-29 14:16:13",
  "notificationType": "GETEPODNOTIFICATION",
  "url": "https://bucketname.s3.ap-southeast-1.amazonaws.com/images/EPOD_ESIGN/EPOD2019_08_29_14_16_12.zip?X-...",
  "requestId": "e5d95546b50e45d2b73f9cdad7dbac18"
}

```

This notification is triggered in response to calling the Get EPOD and ESign API, and has the URL to the EPOD and ESign images for the Orders that were requested in the API. 

This webhook also has the requestId field that is also received in the response of the API request. Use this field to verify which request the webhook has been triggered form.

Calling the URL recevied in the webhook will auomatically trigger a download of a compressed file that has all the images that were uploaded against the Order. This URL is valid for 1 hour from the time at which the request is received. 


#### Response Parameters

Key | DataType | Description
--------- | ------- |-------
timestamp | String | UTC time at which the notification was triggered.
notificationType | String |  GETEPODNOTIFICATION
url | String |  URL of the compressed file that contains the EPOD and ESign images for the Order. This URL is valid for 1 hour from the time of being triggered.
requestId | String |  Unique request identifier to reconcile which API request the webhook was triggered against.s


### Custom Form

> Response

```json

{
  "notificationType": "ORDERCUSTOMFORMNOTIFICATION",
  "event": "EPOD_AFTER",
  "formName": "POD",
  "timestamp": "2019-04-26 02:55:24",
  "orderNo": "26752501_0",
  "orderReferenceId": "d7738ffd9508461e80c5aebad2021ae6",
  "orderStatus": "PICKEDUP",
  "deliveryMediumName": "ATL Dallas Pass_15121",
  "formdata": [
    {
      "key": "recipientName",
      "value": "dallas",
      "type": "text"
    },
    {
      "key": "dept-Floor-Suite-Comments",
      "value": "floor 2",
      "type": "text"
    }
  ]
}
```
This notification is triggered when any Custom form related to an ORder is submitted. This webhook contains the details filled in the custom form.

Custom form data will be sent inside the formData object that contains the key name, value and data type of each field filled in the custom form.

Date and DateTime fields will hold values in the EPOCH format, while Time fields will hold data in HH:MM format.

Editing an existing custom form is likely to impact any integration where there is a check on a specific key name.

#### Response Parameters

Key | DataType | Description
--------- | ------- |-------
notificationType| String | Event Identifier. Hardcoded to 'ORDERCUSTOMFORMNOTIFICATION' for the custom form notification event.
event| String | The event at which the current custom form was triggered. This helps identify at what point in the Order lifecycle was the custom form filled. This can have any one of the values mentioned in the table below.
formName | String | Name of the custom form entered when the custom form was created in the Mile application.
timestamp | String | The timestamp of the event at which the custom form was submitted in 'YYYY-MM-DD HH:MM:SS' format. For example, "2019-04-26 02:55:24".
orderNo | String | Order number against which the custom form was filled. 
orderReferenceId | String | Order Reference ID of the Order against which the custom form was filled.
orderStatus | String | The current Order Status.
deliveryMediumName | String | Delivery Associate name.
formData | List | This list contains the details of the custom form filled.
formData.key | | The key name of the custom form field.
formData.value | | The value of the custom form field.  
formData.type | String | Data type of the custom form field.
 
Event Key | Description
----------|------------
CHECKIN_AFTER | Custom form located after the Check In screen on TrackNext.
LOAD_AFTER | Custom form located after the Loading screen on TrackNext.
UNLOAD_AFTER | Custom form located after the Unloading screen on TrackNext.
ESIGN_AFTER | Custom form located after the ESIGN screen on TrackNext.
PAYMENT_AFTER | Custom form located after the Payment screen on TrackNext.
EPOP_AFTER | Custom form located after the E Proof of Pickup screen on TrackNext.
EPOD_AFTER | Custom form located after the E Proof of Delivery on TrackNext.
PICKEDUP_AFTER | Custom form filled after the Pickup is complete for the Order.
NOTPICKED-UP_AFTER | Custom form filled after the Order is marked Not Picked Up.
DELIVERED_AFTER | Custom form filled after the Order is marked Delivered.
NOTDELIVER_AFTER | Custom form filled after the Order is marked Delivered.
PARTIALDELIVER_AFTER | Custom form filled after the Order is marked Partial Delivered.

### Create E2E Order


> Response

```json

{
  "notificationType": "MILEE2EORDERCREATIONNOTIFICATION",
  "orderDetails": [

    {
      "orderNo": "MM_Excel_WH47",
      "timestamp": "2019-06-07 10:26:49",
      "awbNumber": "MM_Excel_WH",
      "orderState": "FORWARD",
      "orderReferenceId": "adda676c70fa4be3a6c7d6a72eec7ce3",
      "deliveryType": "Small Box",
      "routeConfigurationName": "LA_NY_2",
      "orderType": "ALLMILE",
      "serviceType": "Economy",
      "distributionCenter": "California Main Hub",
      "originBranchName": "California Main Hub",
      "destinationBranchName": "New York Central Hub",
      "nextBranchName": "Boston",
      "milestoneNo": "MM_Excel_WH47_M1",
      "milestoneType": "PICKUP",
      "movementType": "Customer-to-Branch",
      "milestoneReferenceId": "adda676c70fa4be3a6c7d6a72eec7ce3",
      "orderDate": "2019-06-25 12:45:00"
    },
    {
      "orderNo": "MM_Excel_WH48",
      "timestamp": "2019-06-07 10:26:49",
      "awbNumber": "MM_Excel_WH",
      "orderState": "FORWARD",
      "orderReferenceId": "2af1ae80a2424fd8bcc473dd037677bc",
      "deliveryType": "Small Box",
      "routeConfigurationName": "LA_NY_2",
      "orderType": "ALLMILE",
      "serviceType": "Economy",
      "distributionCenter": "California Main Hub",
      "originBranchName": "California Main Hub",
      "destinationBranchName": "New York Main Hub",
      "nextBranchName": "Boston",
      "milestoneNo": "MM_Excel_WH48_M1",
      "milestoneType": "PICKUP",
      "movementType": "Customer-to-Branch",
      "milestoneReferenceId": "2af1ae80a2424fd8bcc473dd037677bc",
      "orderDate": "2019-06-25 12:45:00"
    }
  ]
}
```

A Mile E2E Order is a multi leg Order that can have multiple legs between a pickup and Delivery. If you have an ORder that is to be picked up from a Customer in California and Delivered to a Customer in New York, and has to go through Boston and Chicago on the way there
This notification is triggered when a Mile E2E type of Order is created in LogiNext. The Creation notification can be sent for upto 20 Orders in a single webhook object. For example, if 20 Orders were created in a single call of the Create Order API, the notification for all 20 will be received in a single webhook response.

#### Response Parameters

Param | DataType | Description
--------- | ------- | ----------
notificationType | String | This is the notification of the event that triggered the webhook. In case of Order Creation it is hardcoded to 'MILEE2EORDERCREATIONNOTIFICATION'
orderNo | String | This is the Order No.
timestamp | String | this represents the Order creation timestamp
awbNumber | String | AWB Number for the order
orderState | String | State of order. Ex: FORWARD, REVERSE
orderReferenceId | String | Order reference id
deliveryType | String | Order skill-set type
routeConfigurationName| String| Route name if entered while creating the Order
orderType | String | Will be defaulted to ALLMILE
serviceType| String| The service type entered for the Order at the time of creation
distributionCenter | String | The branch to which the Order is assigned
originBranchName| String| The branch that will fulfill the first leg of the Order
destinationBranchName | String | The branch that will fulfill the last leg of the Order
nextBranchName | String | The branch that will fulfill the next leg of the Order
milestoneNo| String | The milestone number of the first milestone created under the Order
milestoneType| String | can be 'PICKUP' or 'DELIVER' depending on the route configuration defined when creating the route
movementType| String | Can be 'Branch-to-Branch', 'Customer-to-Branch' or 'Branch-to-Customer' depending on the type of movement and Order leg 
milestoneReferenceId| String | Milestone reference ID
orderDate| String | Order creation Date.


### Update E2E Order


> Response

```json

{
  "notificationType": "MILEE2EORDERUPDATESTATUSNOTIFICATION",
  "orderDetails": [
    {


      "orderNo": "LastMile_1",
      "timestamp": "2019-06-24 10:46:57",
      "awbNumber": "LastMile_1",
      "orderState": "FORWARD",
      "orderReferenceId": "91c501c223134022a6708df64bc6a8a8",
      "scanStatus": "INSCANNED",
      "orderStatus": "NOTDISPATCHED",
      "orderType": "LM",
      "distributionCenter": "Main Branch",
      "milestoneNo": "LastMile_1_M1",
      "milestoneType": "DELIVER",
      "milestoneReferenceId": "91c501c223134022a6708df64bc6a8a8",
      "detailedOrderStatus": "NOTDISPATCHED_ASSIGNED",
      "milestoneStatus": "NOTDISPATCHED"    
    },
    {
      "orderNo": "LastMile_2",
      "timestamp": "2019-06-24 10:46:58",
      "awbNumber": "LastMile_1",
      "orderState": "FORWARD",
      "orderReferenceId": "91c501c223134022a6708df64bc6a8a8",
      "scanStatus": "INSCANNED",
      "orderStatus": "NOTDISPATCHED",
      "orderType": "LM",
      "distributionCenter": "Main Branch",
      "milestoneNo": "LastMile_1_M1",
      "milestoneType": "DELIVER",
      "milestoneReferenceId": "91c501c223134022a6708df64bc6a8a8",
      "detailedOrderStatus": "NOTDISPATCHED_ASSIGNED",
      "milestoneStatus": "NOTDISPATCHED"
    }
  ]
}
```
This notification is triggered when an All Mile type of Order is updated in LogiNext. The update notification can be sent for upto 20 Orders in a single webhook object.

#### Response Parameters

Param | DataType | Description
--------- | ------- | ----------
notificationType | String | This is the notification of the event that triggered the webhook. In case of Order Creation it is hardcoded to 'MILEE2EORDERUPDATESTATUSNOTIFICATION'
orderNo | String | This is the Order No.
timestamp | String | this represents the Order creation timestamp
awbNumber | String | AWB Number for the order
orderState | String | State of order. Ex: FORWARD, REVERSE
orderReferenceId | String | Order reference id
deliveryType | String | Order skill-set type
routeConfigurationName| String| Route name if entered while creating the Order
orderType | String | Will be defaulted to ALLMILE
serviceType| String| The service type entered for the Order at the time of creation
distributionCenter | String | The branch to which the Order is assigned
originBranchName| String| The branch that will fulfill the first leg of the Order
destinationBranchName | String | The branch that will fulfill the last leg of the Order
nextBranchName | String | The branch that will fulfill the next leg of the Order
milestoneNo| String | The milestone number of the first milestone created under the Order
milestoneType| String | can be 'PICKUP' or 'DELIVER' depending on the route configuration defined when creating the route
movementType| String | Can be 'Branch-to-Branch', 'Customer-to-Branch' or 'Branch-to-Customer' depending on the type of movement and Order leg 
milestoneReferenceId| String | Milestone reference ID
orderDate| String | Order creation Date.
 

## Trips

### Start

> Response

```json
{
  "notificationType": "STARTTRIP",
  "latitude":41.882702,
  "longitude":-87.619392,   
  "deliveryMediumName": "Suraj Singh",
  "phoneNumber": 1234567546,
  "startTime": "2016-11-19 06:42:44",
  "tripName": "TRIP-84",
  "vehicleNumber":"MH084819",
  "driverName":"Rahul",
  "branchName": "Vikhroli",
  "clientShipmentIds": [
    "Order001",
    "Order002"
  ],
}

```

This notification is sent when a trip is started.

#### Response Parameters

Key | DataType | Description
--------- | ------- |-------
latitude | Long | Geo-coordnates(latitude) of the start trip event,
longitude | Long | Geo-coordnates(longitude) of the start trip event.
clientShipmentIds | List<String> |  Order No.s.
notificationType | String |  STARTTRIP
tripName | String |  Trip name
vehicleNumber | String |  Vehicle no.
driverName | String |  Name of driver
deliveryMediumName | String |  Name of Delivery Associate
phoneNumber | Long | Phone no.
startTime | String |  Trip start time


### Stop

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


### ETA Revision

> Response

```json
{
  "notificationType": "REVISEETANOTIFICATION",
  "eventName": "MANUALASSIGNMENT",
  "tripDetails": [
    {
      "tripName": "TRIP-152",
      "tripReferenceId": "26ba0ccxd3c743a6848e2377aea5c2ef",
      "tripStatus": "STARTED",
      "deliveryMediumName": "trampolin",
      "deliveryMediumReferenceId": "9391fbc28a6b4b12923477fc301334ca",
      "phoneNumber": "93189490",
      "branchName": "California Main Branch",
      "orderDetails": [
        {
          "orderStatusCd": "PICKEDUP",
          "orderTypeCd": "DELIVER",
          "orderNo": "GR432U5",
          "orderReferenceId": "d9a0febe56264bbc8b9d43273c53ge75",
          "paymentType": "COD",
          "pickupDetails": [
            {
              "latitude": 40.319291,
              "longitude": 72.89481899999998,
              "startTimeWindow": "2019-05-20 10:00:00",
              "endTimeWindow": "2019-05-23 00:00:00",
              "plannedStartDate": "2019-05-20 14:22:42",
              "plannedEndDate": "2019-05-20 14:22:42",
              "calculatedStartDate": "2019-05-20 14:23:22",
              "calculatedEndDate": "2019-05-20 14:23:22",
              "plannedDistance": 0,
              "sequence": 2
            }
          ],
          "deliverDetails": [
            {
              "latitude": 40.344959,
              "longitude": 72.963202,
              "startTimeWindow": "2019-05-20 10:00:00",
              "endTimeWindow": "2019-05-23 00:00:00",
              "plannedStartDate": "2019-05-20 14:27:59",
              "plannedEndDate": "2019-05-20 14:32:59",
              "calculatedStartDate": "2019-05-20 16:31:50",
              "calculatedEndDate": "2019-05-20 16:36:50",
              "plannedDistance": 0,
              "sequence": 4
            }
          ]
        },
        {
          "orderStatusCd": "INTRANSIT",
          "orderTypeCd": "DELIVER",
          "orderNo": "GR432U7",
          "orderReferenceId": "1df561c31fd24be621aa816836a90127",
          "paymentType": "COD",
          "pickupDetails": [
            {
              "latitude": 40.319291,
              "longitude": 72.89481899999998,
              "startTimeWindow": "2019-05-20 10:00:00",
              "endTimeWindow": "2019-05-23 00:00:00",
              "calculatedStartDate": "2019-05-20 16:42:28",
              "calculatedEndDate": "2019-05-20 16:42:49",
              "plannedDistance": 0.11,
              "sequence": 7
            }
          ],
          "deliverDetails": [
            {
              "latitude": 40.339693,
              "longitude": 72.954843,
              "startTimeWindow": "2019-05-20 10:00:00",
              "endTimeWindow": "2019-05-23 00:00:00",
              "calculatedStartDate": "2019-05-20 16:42:49",
              "calculatedEndDate": "2019-05-20 16:48:06",
              "plannedDistance": 0.11,
              "sequence": 8
            }
          ]
        }
      ]
    }
  ]
}
```

This webhook is triggered when the ETA for a particular Order is revised. This can happen at 

#### Response Parameters

Key | DataType | Description
--------- | ------- |-------
notificationType | String |  This represents the event that triggered the webhook. In the case of Route Planning it is hardcoded to 'REVISEETANOTIFICATION'
eventName | String | This is the name of the event at which the webhook was triggered. This can be one of 'TRIPSTART', 'ORDERCHECKOUT', 'MANUALASSIGNMENT', 'DELIVERYMEDIUMOFFBREAK', 'SCHEDULED'. 
tripDetails | List | Notification details
tripDetails.tripName | String |  This is the Trip name.
tripDetails.tripReferenceId | String | Reference id of the trip
tripDetails.tripStatus | String | Status of the trip
tripDetails.deliveryMediumName | String | Name of the Delivery Associate who will be fulfilling the Orders in this Trip
tripDetails.deliveryMediumReferenceId | String | Reference ID of the Delivery Associate who will be fulfilling the Orders in this Trip
tripDetails.tripReferenceId | String | Reference id of the trip
notificationDetails.deliveryMediumName | String |  Name of Delivery Associate associated with the current Trip.
tripDetails.phoneNumber | String | Phone no of Delivery Associate.
tripDetails.branchName | String | Branch Name.
tripDetails.orderDetails | List | List of Order details in the Current Trip.
tripDetails.orderDetails.orderTypeCd | String | Order type. Can be 'PICKUP' or 'DELIVER'.
tripDetails.orderDetails.orderNo | String | Order Number
tripDetails.orderDetails.orderReferenceId | String | Order reference ID
tripDetails.orderDetails.paymentType | String | payment type for the Order. 
tripDetails.orderDetails.pickupDetails | List | Details of the pickup leg of the Order
tripDetails.orderDetails.pickupDetails.latitude | Double | Geocoordinates (latitude) of the pickup leg of the Order.
tripDetails.orderDetails.pickupDetails.longitude | Double | Geocoordinates (longitude) pickup leg of the of the Order.
tripDetails.orderDetails.pickupDetails.startTimeWindow | String | Start Time Window of the pickup leg of the of the Order in UTC.
tripDetails.orderDetails.pickupDetails.endTimeWindow | String | End Time Window of the pickup leg of the Order in UTC.
tripDetails.orderDetails.pickupDetails.calculatedStartDate | List | Details of the pickup leg of the pickup leg of the Order
tripDetails.orderDetails.pickupDetails.calculatedEndDate | List | Details of the pickup leg of the pickup leg of the Order
tripDetails.orderDetails.pickupDetails.plannedDistance | List | Details of the pickup leg of the pickup leg of the Order
tripDetails.orderDetails.pickupDetails.sequence | List | Details of the pickup leg of the pickup leg of the Order
tripDetails.orderDetails.deliverDetails.latitude | Double | Geocoordinates (latitude) of the pickup leg of the Order.
tripDetails.orderDetails.deliverDetails.longitude | Double | Geocoordinates (longitude) pickup leg of the of the Order.
tripDetails.orderDetails.deliverDetails.startTimeWindow | String | Start Time Window of the pickup leg of the of the Order in UTC.
tripDetails.orderDetails.deliverDetails.endTimeWindow | String | End Time Window of the pickup leg of the Order in UTC.
tripDetails.orderDetails.deliverDetails.calculatedStartDate | List | Details of the pickup leg of the pickup leg of the Order
tripDetails.orderDetails.deliverDetails.calculatedEndDate | List | Details of the pickup leg of the pickup leg of the Order
tripDetails.orderDetails.deliverDetails.plannedDistance | List | Details of the pickup leg of the pickup leg of the Order
tripDetails.orderDetails.deliverDetails.sequence | List | Details of the pickup leg of the pickup leg of the Order


## Route Planning

### Route Planning v1(Deprecated)

The Route Planning webhook is generated as part of the Route Planning operation. This webhook contains the details of the trips created as a part of the Route Planning operation and the Orders assigned to each trip.

Note that a single Route Planning operation can have multiple Route Planning webhooks generated for it. This will happen in a case where more than 30 Trips are created as part of a Route Planning operation. Each Route Planning webhook will hold the details of not more than 30 trips. 

The Route Planning webhook also provides the details regarding how many total pages of the webhook were generated as part of the Route Planning operation. This can be found from the 'currentPageIndex' and 'totalPages' keys in the webhook. Each page will be sent to the URL configured in LogiNext to receive the webhook.

The list of unassigned Orders will be sent in the 'unassignmentReasons' list in the first page of the webhook. Look for the 'currentPageIndex' key having a value of 1 to find this list. Please note that if all the Orders were assigned and no Orders were left unassigned as part of the Route Planning operation, the 'unassignmentReasons' list will not be sent in the webhook.

> Response

```json
{
  "notificationType": "DELIVERYPLANNING",
  "routeName": "ROUTEP1",
  "totalTripCount": 1,
  "currentTripCount": 1,
  "currentPageIndex": 1,
  "totalPages": 1,
  "totalOrderCount": 100,
  "assignedOrderCount": 50,
  "unassignedOrderCount": 50,
  "notificationDetails": [
    {
      "tripName": "TRIP-7736",
      "referenceId": "225dc58843234f4f80158940d9ed123b",
      "deliveryMediumName": "Hyc_Mld_Superman_12",
      "phoneNumber": "9292929292",
      "orderDetails": [
        {
          "packageStatusCd": "INTRANSIT",
          "originLatitude": 40.760838,
          "originLongitude": 74.835163,
          "destinationLatitude": 40.760838,
          "destinationLongitude": 74.901015,
          "projectDistance": 2.0882,
          "deliveryOrder": 21,
          "shipmentOrderTypeCd": "DELIVER",
          "startTimeWindow": "2019-03-10 14:54:00",
          "endTimeWindow": "2019-03-11 00:54:00",
          "orderNo": "powai",
          "clientName": "Capillary Tech.",
          "clientCity": "mumbai",
          "paymentType": "Prepaid",
          "latitude":40.760838,
          "longitude":74.619392,
          "calculatedStartDate": "2019-03-04 09:36:41",
          "calculatedEndDate": "2019-03-10 10:28:00"
        },
        {
          "packageStatusCd": "INTRANSIT",
          "originLatitude": 40.760838,
          "originLongitude": 74.835163,
          "destinationLatitude": 42.116835,
          "destinationLongitude": 72.910467,
          "projectDistance": 2.4557,
          "deliveryOrder": 20,
          "shipmentOrderTypeCd": "DELIVER",
          "startTimeWindow": "2019-03-10 14:54:00",
          "endTimeWindow": "2019-03-11 00:54:00",
          "orderNo": "dmart",
          "clientName": "Capillary Tech.",
          "clientCity": "mumbai",
          "paymentType": "Prepaid",
          "latitude": 19.116835,
          "longitude": 72.910467,
          "calculatedStartDate": "2019-03-04 09:36:41",
          "calculatedEndDate": "2019-03-10 10:03:00"
        },
        {
          "packageStatusCd": "INTRANSIT",
          "originLatitude": 40.171036,
          "originLongitude": 74.835163,
          "destinationLatitude": 42.132447,
          "destinationLongitude": 72.91286,
          "projectDistance": 27.2243,
          "deliveryOrder": 19,
          "shipmentOrderTypeCd": "DELIVER",
          "startTimeWindow": "2019-03-10 14:54:00",
          "endTimeWindow": "2019-03-11 00:54:00",
          "orderNo": "iit",
          "clientName": "Capillary Tech.",
          "clientCity": "mumbai",
          "paymentType": "Prepaid",
          "latitude": 19.132447,
          "longitude": 72.91286,
          "calculatedStartDate": "2019-03-04 08:10:41",
          "calculatedEndDate": "2019-03-10 09:36:00"
        }
      ],
      "branchName": "1001",
    }
  ],
  
  "unassignmentReasons": [
    {
      "reasonCd": "ORDER_TIMEWINDOW_EXCEEDED",
      "orderCount": 1,
      "orderReferenceIds": [
        "75fe20605f1d4c34b82fcf5df65269ee"
      ]
    }
  ]
}

```





#### Response Parameters

Key | DataType | Description
--------- | ------- |-------
notificationType | String |  This represents the event that triggered the webhook. In the case of Route Planning it is hardcoded to 'DELIVERYPLANNING'
routeName | String | This is the name of the Route 
totalTripCount | Number |  This is the count of the total number of Trips created as part of the route planning operation. This will hold the count of all the trips created across all the webhooks generated for the current route plan.
currentTripCount | Number | This is the count number of trips in the current webhook.
currentPageIndex | Number |  This is the page index of the current route planning webhook.
totalPages | Number | This is the total number of pages geneerated for the current route planning webhook. For example, this will be 4 if 100 trips were created as part of the route planning operation.
totalOrderCount | Number | Total number of Orders considered in the Route planning
assignedOrderCount | Number |  Number of Orders that got assignemd after the current Route Planning operation completed.
unassignedOrderCount | Number |  Number of Orders that remained unassignemd after the current Route Planning operation completed.
notificationDetails | List | Notification details
notificationDetails.tripName | String |  This is the Trip name.
notificationDetails.referenceId | String | Reference id of the trip
notificationDetails.deliveryMediumName | String |  Name of Delivery Associate associated with the current Trip.
notificationDetails.phoneNumber | String | Phone no of Delivery Associate
notificationDetails.orderDetails | List | List of orders present in the trip
originLatitude | Number |  Pickup location geolocation(latitude). 
originLongitude |  Number |  Pickup location geolocation(longitude). 
destinationLatitude |  Number |  Pickup location geolocation(latitude). 
destinationLongitude |  Number |  Delivery location geolocation(latitude). 
projectDistance|  Number |  Delivery location geolocation(latitude). 
shipmentOrderTypeCd | String | Hardcoded to 'DELIVER for Delivery Orders and 'PICKUP' for Pickup Orders.
startTimeWindow | String | Order Start Time Window. Format - "YYYY-MM-DD HH:MM:SS"
endTimeWindow | String | Order End Time Window. Format - "YYYY-MM-DD HH:MM:SS",
orderNo | String | Order Number
paymentType | String | Payment Mode of the Order. Can be "Prepaid" or "COD"
latitude | Double | Order geolocation(latitude). This will be same as the OriginLatitude for Pickup type Orders and the same as destinationLatitude for Deliver type of Orders.
longitude | Double | Order geolocation(longitude). This will be same as the OriginLatitude for Pickup type Orders and the same as destinationLatitude for Deliver type of Orders.
calculatedStartDate | String | The lastest updated ETA to start servicing the current Order. Format - YYYY-MM-DD HH:MM:SS
calculatedEndDate | String | The lastest updated ETA to end servicing the current Order. Format - YYYY-MM-DD HH:MM:SS
unassignmentReasons | List |
unassignmentReasons.reasonCd | String | Reason code of the unassignment reason. This can be one of the following values
unassignmentReasons.orderCount | Number | Number of Orders that were unassigned due to the current unassignment reason
unassignmentReasons.orderReferenceIds | List | List of the ORder Reference IDs that remained unassigned due to the current unassignment reason


Unassignment Key | Description
--------- | -------
REQUIRED_SKILL_NOT_FULLFILLED | No Delivery Associates were found with the required skillset match to fufill these Order
INSUFFICIENT_TIME_WINDOW | The unassigned Orders could not be fulfilled in their given time windows.
INSUFFICIENT_CAPACITY | The fleet capacity was not sufficient to fulfil the Orders
MAX_DISTANCE_NOT_FULFILLED | If a Maximum distance check was applied to the Delivery Associate, then Orders that remained unassigned due to this reason were because they were 
BRANCH_DM_NA | No Delivery Associates of the relevant branch were found to fulfil these Orders
NOT_GEOCODED | The Orders unassigned due to this reason were not geocoded in LogiNext
GEOFENCE_DM_NA | For Orders that were mapped to a particular Geofence, if no Delivery Associates was found to fulfil them, those Orders will remain unassigned due to this reason.
DM_NA | For Orders that are not mapped to any Geofence, if no relevant Delivery Associates were found to fulfil these Orders, those Orders will remain unassigned due to this reason.
ROUTE_MAX_DISTANCE_NOT_FULLFILLED |  Distance constraint between first Order location and last Order location was not met.
PINCODE_MISMATCH | No Delivery Associates were found with the pincode preference of the Orders.
CUSTOMER_BREAK_OVERLAP_TIMEWINDOW | Orders unassigned due to this reason could be delivered to customer locations during the break times for those Customers.
ORDER_TIMEWINDOW_EXCEEDED | Orders unassigned due to this reason could not be serviced in their respective time windows.


### Route Planning v2

The Route Planning webhook is generated as part of the Route Planning operation. This webhook contains the details of the trips created as a part of the Route Planning operation and the Orders assigned to each trip.

Note that a single Route Planning operation can have multiple Route Planning webhooks generated for it. This will happen in a case where more than 30 Trips are created as part of a Route Planning operation. Each Route Planning webhook will hold the details of not more than 30 trips. 

The Route Planning webhook also provides the details regarding how many total pages of the webhook were generated as part of the Route Planning operation. This can be found from the 'currentPageIndex' and 'totalPages' keys in the webhook. Each page will be sent to the URL configured in LogiNext to receive the webhook.

The list of unassigned Orders will be sent in the 'unassignmentReasons' list in the first page of the webhook. Look for the 'currentPageIndex' key having a value of 1 to find this list. Please note that if all the Orders were assigned and no Orders were left unassigned as part of the Route Planning operation, the 'unassignmentReasons' list will not be sent in the webhook.

> Response

```json
{
  "notificationType": "PLANNINGNOTIFICATION",
  "routeName": "AS_2703",
  "unassignmentReasons": [ 
{ 
     "reasonCd": "NOT_GEOCODED", 
     "orderCount": 1, 
     "orderReferenceIds": [ 
          "444820b3361d4e4e8e484060f9b15625"
     ] 
  } 
]
  "totalTripCount": 1,
  "currentTripCount": 1,
  "currentPageIndex": 1,
  "totalPages": 1,
  "totalOrderCount": 4,
  "assignedOrderCount": 4,
  "unassignedOrderCount": 0,
  "tripDetails": [
    {
      "tripName": "TRIP-1550",
      "tripReferenceId": "a24ffe5dcdd94e8c8ca7c2d1b2f6489b",
      "tripStatus": "NOTSTARTED",
      "deliveryMediumName": "James",
      "deliveryMediumReferenceId": "b725204fs5a945ea908abacadd1e352b",
      "phoneNumber": "93462027",
      "branchName": "LB01",
      "orderDetails": [
        {
          "orderStatusCd": "NOTDISPATCHED",
          "orderTypeCd": "DELIVER",
          "orderNo": "NA12070320191",
          "orderReferenceId": "ed9906f4debe4260a4211b801b3b945c",
          "paymentType": "COD",
          "pickupDetails": [
            {
              "latitude": 40.319291,
              "longitude": 72.89481899999998,
              "startTimeWindow": "2019-03-27 00:00:00",
              "endTimeWindow": "2019-03-27 12:00:00",
              "plannedStartDate": "2019-03-26 23:42:53",
              "plannedEndDate": "2019-03-26 23:42:53",
              "calculatedStartDate": "2019-03-26 23:42:53",
              "calculatedEndDate": "2019-03-26 23:42:53",
              "plannedDistance": 0,
              "sequence": 3
            }
          ],
          "deliverDetails": [
            {
              "latitude": 40.344959,
              "longitude": 72.963202,
              "startTimeWindow": "2019-03-27 00:00:00",
              "endTimeWindow": "2019-03-27 12:00:00",
              "plannedStartDate": "2019-03-27 00:15:40",
              "plannedEndDate": "2019-03-27 00:28:36",
              "calculatedStartDate": "2019-03-27 00:15:40",
              "calculatedEndDate": "2019-03-27 00:28:36",
              "plannedDistance": 2.692,
              "sequence": 7
            }
          ]
        },
        {
          "orderStatusCd": "NOTDISPATCHED",
          "orderTypeCd": "DELIVER",
          "orderNo": "NA12070320191",
          "orderReferenceId": "a4592e15a4d44436ae761bc47bf332a0",
          "paymentType": "COD",
          "pickupDetails": [
            {
              "latitude": 40.319291,
              "longitude": 72.89481899999998,
              "startTimeWindow": "2019-03-27 00:00:00",
              "endTimeWindow": "2019-03-27 12:00:00",
              "plannedStartDate": "2019-03-26 23:42:53",
              "plannedEndDate": "2019-03-26 23:42:53",
              "calculatedStartDate": "2019-03-26 23:42:53",
              "calculatedEndDate": "2019-03-26 23:42:53",
              "plannedDistance": 0,
              "sequence": 4
            }
          ],
          "deliverDetails": [
            {
              "latitude": 40.339693,
              "longitude": 72.954843,
              "startTimeWindow": "2019-03-27 00:00:00",
              "endTimeWindow": "2019-03-27 12:00:00",
              "plannedStartDate": "2019-03-27 00:28:36",
              "plannedEndDate": "2019-03-27 00:38:47",
              "calculatedStartDate": "2019-03-27 00:28:36",
              "calculatedEndDate": "2019-03-27 00:38:47",
              "plannedDistance": 2.029,
              "sequence": 8
            }
          ]
        },
        {
          "orderStatusCd": "NOTDISPATCHED",
          "orderTypeCd": "DELIVER",
          "orderNo": "NA12070320191",
          "orderReferenceId": "3d1dc7bdb0c44e63991f112956f37843",
          "paymentType": "COD",
          "pickupDetails": [
            {
              "latitude": 40.319291,
              "longitude": 72.89481899999998,
              "startTimeWindow": "2019-03-27 00:00:00",
              "endTimeWindow": "2019-03-27 12:00:00",
              "plannedStartDate": "2019-03-26 23:42:53",
              "plannedEndDate": "2019-03-26 23:42:53",
              "calculatedStartDate": "2019-03-26 23:42:53",
              "calculatedEndDate": "2019-03-26 23:42:53",
              "plannedDistance": 0,
              "sequence": 1
            }
          ],
          "deliverDetails": [
            {
              "latitude": 40.329154,
              "longitude": 72.967634,
              "startTimeWindow": "2019-03-27 00:00:00",
              "endTimeWindow": "2019-03-27 12:00:00",
              "plannedStartDate": "2019-03-26 23:42:53",
              "plannedEndDate": "2019-03-27 00:05:00",
              "calculatedStartDate": "2019-03-26 23:42:53",
              "calculatedEndDate": "2019-03-27 00:05:00",
              "plannedDistance": 11.397,
              "sequence": 5
            }
          ]
        },
        {
          "orderStatusCd": "NOTDISPATCHED",
          "orderTypeCd": "DELIVER",
          "orderNo": "TestAS_NA12070320191_CNSGS0002704403",
          "orderReferenceId": "7584a114bd3447759898ea8c823045ad",
          "paymentType": "COD",
          "pickupDetails": [
            {
              "latitude": 40.319291,
              "longitude": 72.89481899999998,
              "startTimeWindow": "2019-03-27 00:00:00",
              "endTimeWindow": "2019-03-27 12:00:00",
              "plannedStartDate": "2019-03-26 23:42:53",
              "plannedEndDate": "2019-03-26 23:42:53",
              "calculatedStartDate": "2019-03-26 23:42:53",
              "calculatedEndDate": "2019-03-26 23:42:53",
              "plannedDistance": 0,
              "sequence": 2
            }
          ],
          "deliverDetails": [
            {
              "latitude": 40.3421429,
              "longitude": 72.9641279,
              "startTimeWindow": "2019-03-27 00:00:00",
              "endTimeWindow": "2019-03-27 12:00:00",
              "plannedStartDate": "2019-03-27 00:05:00",
              "plannedEndDate": "2019-03-27 00:15:40",
              "calculatedStartDate": "2019-03-27 00:05:00",
              "calculatedEndDate": "2019-03-27 00:15:40",
              "plannedDistance": 2.023,
              "sequence": 6
            }
          ]
        }
      ]
    }
  ]
}

```

#### Response Parameters

Key | DataType | Description
--------- | ------- |-------
notificationType | String |  This represents the event that triggered the webhook. In the case of Route Planning it is hardcoded to 'DELIVERYPLANNING'
routeName | String | This is the name of the Route 
unassingmentReasons | List  | List of Orders that remained unassigned along with the reason for unassignment
unassignmentReasons.reasonCd | String | Reason code of the unassignment reason. This can be one of the values as mentioned in reason code table
unassignmentReasons.orderCount | Number | Number of Orders that were unassigned due to the current unassignment reason
unassignmentReasons.orderReferenceIds | List | List of the Order Reference IDs that remained unassigned due to the current unassignment reason
totalTripCount | Number |  This is the count of the total number of Trips created as part of the route planning operation. This will hold the count of all the trips created across all the webhooks generated for the current route plan.
currentTripCount | Number | This is the count number of trips in the current webhook.
currentPageIndex | Number |  This is the page index of the current route planning webhook.
totalPages | Number | This is the total number of pages geneerated for the current route planning webhook. For example, this will be 4 if 100 trips were created as part of the route planning operation.
totalOrderCount | Number | Total number of Orders considered in the Route planning
assignedOrderCount | Number |  Number of Orders that got assignemd after the current Route Planning operation completed.
unassignedOrderCount | Number |  Number of Orders that remained unassignemd after the current Route Planning operation completed.
tripDetails | List | Notification details
tripDetails.tripName | String |  This is the Trip name.
tripDetails.tripReferenceId | String | Reference id of the trip
tripDetails.tripStatus | String | Status of the trip
tripDetails.deliveryMediumName | String | Name of the Delivery Associate who will be fulfilling the Orders in this Trip
tripDetails.deliveryMediumReferenceId | String | Reference ID of the Delivery Associate who will be fulfilling the Orders in this Trip
tripDetails.tripReferenceId | String | Reference id of the trip
notificationDetails.deliveryMediumName | String |  Name of Delivery Associate associated with the current Trip.
tripDetails.phoneNumber | String | Phone no of Delivery Associate.
tripDetails.branchName | String | Branch Name.
tripDetails.orderDetails | List | List of Order details in the Current Trip.
tripDetails.orderDetails.orderTypeCd | String | Order type. Can be 'PICKUP' or 'DELIVER'.
tripDetails.orderDetails.orderNo | String | Order Number
tripDetails.orderDetails.orderReferenceId | String | Order reference ID
tripDetails.orderDetails.paymentType | String | payment type for the Order
tripDetails.orderDetails.pickupDetails | List | Details of the pickup leg of the Order
tripDetails.orderDetails.pickupDetails.latitude | Double | Geocoordinates (latitude) of the pickup leg of the Order.
tripDetails.orderDetails.pickupDetails.longitude | Double | Geocoordinates (longitude) pickup leg of the of the Order.
tripDetails.orderDetails.pickupDetails.startTimeWindow | String | Start Time Window of the pickup leg of the of the Order in UTC.
tripDetails.orderDetails.pickupDetails.endTimeWindow | String | End Time Window of the pickup leg of the Order in UTC.
tripDetails.orderDetails.pickupDetails.calculatedStartDate | String | The latest updated ETA to start servicing the pickup leg of the Order
tripDetails.orderDetails.pickupDetails.calculatedEndDate | String | The latest updated ETA to end servicing the pickup leg of the Order
tripDetails.orderDetails.pickupDetails.plannedDistance | List | Details of the pickup leg of the pickup leg of the Order
tripDetails.orderDetails.pickupDetails.sequence | List | Details of the pickup leg of the pickup leg of the Order
tripDetails.orderDetails.deliverDetails | List | Details of the deliver leg of the Order
tripDetails.orderDetails.deliverDetails.latitude | Double | Geocoordinates (latitude) of the deliver leg of the Order.
tripDetails.orderDetails.deliverDetails.longitude | Double | Geocoordinates (longitude) deliver leg of the of the Order.
tripDetails.orderDetails.deliverDetails.startTimeWindow | String | Start Time Window of the deliver leg of the of the Order in UTC.
tripDetails.orderDetails.deliverDetails.endTimeWindow | String | End Time Window of the deliver leg of the Order in UTC.
tripDetails.orderDetails.deliverDetails.calculatedStartDate | String | The latest updated ETA to start servicing the deliver leg of the Order
tripDetails.orderDetails.deliverDetails.calculatedEndDate | String | The latest updated ETA to end servicing the deliver leg of the Order
tripDetails.orderDetails.deliverDetails.plannedDistance | List | Details of the deliver leg of the Order
tripDetails.orderDetails.deliverDetails.sequence | List | Details of the deliver leg of the Order

Unassignment Key | Description
--------- | -------
REQUIRED_SKILL_NOT_FULLFILLED | No Delivery Associates were found with the required skillset match to fufill these Order
INSUFFICIENT_TIME_WINDOW | The unassigned Orders could not be fulfilled in their given time windows.
INSUFFICIENT_CAPACITY | The fleet capacity was not sufficient to fulfil the Orders
MAX_DISTANCE_NOT_FULFILLED | If a Maximum distance check was applied to the Delivery Associate, then Orders that remained unassigned due to this reason were because they were 
BRANCH_DM_NA | No Delivery Associates of the relevant branch were found to fulfil these Orders
NOT_GEOCODED | The Orders unassigned due to this reason were not geocoded in LogiNext
GEOFENCE_DM_NA | For Orders that were mapped to a particular Geofence, if no Delivery Associates was found to fulfil them, those Orders will remain unassigned due to this reason.
DM_NA | For Orders that are not mapped to any Geofence, if no relevant Delivery Associates were found to fulfil these Orders, those Orders will remain unassigned due to this reason.
ROUTE_MAX_DISTANCE_NOT_FULLFILLED |  Distance constraint between first Order location and last Order location was not met.
PINCODE_MISMATCH | No Delivery Associates were found with the pincode preference of the Orders.
CUSTOMER_BREAK_OVERLAP_TIMEWINDOW | Orders unassigned due to this reason could be delivered to customer locations during the break times for those Customers.
ORDER_TIMEWINDOW_EXCEEDED | Orders unassigned due to this reason could not be serviced in their respective time windows.


### Route Planning(API)

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


## Allocation Engine

> Response

```json
{
  "originAddr": "Client Name Main Branch",
  "originLatitude":40.882702,
  "originLongitude":72.619392,
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
       "latitude":40.882702,
       "longitude":74.619392,
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
allocationTimeStamp | String | Mandatory | This is the time at which the allocation engine has identified the nearest  Driver / Associate / Field Executive.<br>Note that this date and time is in UTC.<br>Sample Value - "2017-07-15T10:30:00.000Z"
deliveryMediums | Array Of Object |  | Array - <br>This list would contain list of one or more nearest  Drivery Associate / Field Executive identified for your order.<br>Note that if you have set your account configuration to identify only the nearest driver first, then this array would have only one value.<br>If your account configuration is set to identify X no. of drivers, then this array will have list of the X nearest drivers.
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

## Delivery Associates 

### Active / Inactive

> Response

```json
{
  "referenceId":"6186d5fc6e324c42abb5ea1a32e05f66",
  "deliveryMediumName":"Thomas Walton",
  "employeeId":"133456",
  "phoneNumber":"9881134567",
  "newStatus":"ACTIVE",
  "reasonCd":"DBUNAVAILABLE",
  "updateTime":"2018-07-18T10:31:00.000Z"
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

### Delivery Associate On Break/ Off Break

```json
{
  "latitude":40.882702,
  "longitude":74.619392,
  "timestamp":"2018-07-05 13:22:32",
  "deliveryMediumName":"Sam",
  "tripName":"TRIP-17774",
  "referenceId":"dde5a971e67c4256af48436fe51f23c2",
  "employeeId":"7324567",
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

### Create Delivery Associate 

> Response

```json
{
    "referenceId": "f40cf4493a5949199775499b5750a272",
    "notificationType": "CREATEDELIVERYMEDIUMNOTIFICATION",
    "employeeId":"1001",
    "deliveryMediumName": "James",
    "phoneNumber": "63865471261",
    "imei": "123456789012645",
    "emailId": "james@ablogistics.com",
    "userName": "james003",
    "capacityInUnits": 10,
    "capacityInVolume": 0,
    "capacityInWeight": 0,
    "dob": "2016-12-12",
    "deliveryMediumLanguageList": ["ENGLISH","SPANISH"],
    "gender": "Male",
    "deliveryMediumTypeCd": ["Delivery Associate"],
    "isOwnVehicleFl": "Company",
    "vehicleNumber": "MH034506",
    "dmPreference": ["10035"],
    "cashInHand":"4000",
    "shiftList": [
      {
        "shiftStart": "13:30:00",
        "shiftEnd": "14:30:00"
      }
    ],
    "maxDistance": 100,
    "licenseValidity": "2018-12-12T13:30:00Z",    
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
cashInHand | Double |  cash with delivery Associate.
shiftList | List |  shift details.
shiftList.shiftStart | String |  shift start time
shiftList.shiftEnd | String |  shift end time
maxDistance | Integer |  This is the Maximum Distance in Kms
licenseValidity | String | This is the expiry Date of the Driver's License in UTC format.
reasonCd | String |  When you activate / deactivate the Delivery Associate, you mention the reason for activation / deactivation.<br>The reasons shall be mentioned here
updateTime | String |  This is the time in UTC when the Delivery Associate was marked Active / Inactive
weeklyOffList | List |  List of weekly off's
fixedCost | Integer |  fixed cost associated with delivery Associate.
variableCost | Integer |  variable cost.


## Hubs

### Hub In

> Response

```json
{

  "url" : "endpoint url",
  "data" : "<?xml version=\"1.0\" encoding=\"UTF-8\" standalone=\"yes\"?>\n
          <geofencePushNotificationDTO>\n    
            <hubName>HubName</hubName>\n    
            <latitude>40.018617777777777</latitude>\n    
            <longitude>74.01128</longitude>\n    
            <sightingDate>201603091412</sightingDate>\n    
            <status>HUB IN</status>\n    
            <tripId>TripName</tripId>\n
          </geofencePushNotificationDTO>\n",
  "notificationType" : "HUB IN",
  "updatedDate" : "2016-03-09 07:09:10"
}

```

This notification is sent in LogiNext Haul when a vehicle enters inside a hub.



#### Response Parameters

Key | DataType | Description
--------- | ------- |-------
url | String |  Endpoint URL
data | String |  Data in XML format
notificationType | String |  HUB IN
updatedDate | String | Timestamp


### Hub Out

> Response

```json
{

  "url" : "endpoint url",
  "data" : "<?xml version=\"1.0\" encoding=\"UTF-8\" standalone=\"yes\"?>\n
          <geofencePushNotificationDTO>\n    
            <hubName>HubName</hubName>\n    
            <latitude>40.018617777777777</latitude>\n    
            <longitude>74.01128</longitude>\n    
            <sightingDate>201603091412</sightingDate>\n    
            <status>HUB OUT</status>\n    
            <tripId>TripName</tripId>\n
          </geofencePushNotificationDTO>\n",
  "notificationType" : "HUB OUT",
  "updatedDate" : "2016-03-09 07:09:10"
}

```

This notification is sent in LogiNext Haul when a vehicle enters inside a hub.



#### Response Parameters

Key | DataType | Description
--------- | ------- |-------
url | String |  Endpoint URL
data | String |  Data in XML format
notificationType | String |  HUB IN
updatedDate | String | Timestamp

## Routes

### Create Route

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

This notification is sent in LogiNext Haul when a route is created in LogiNext.

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


### Route Status.

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

This notification is sent in LogiNext Haulwhen a route status is changed in LogiNext.

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


# Country Codes

When creating entities in LogiNext  that require country specific location information associated with them, use the country codes listed below. 
For example, if you want to create an Order that is to be picked up from a Pick-up location in the United States, you would pass USA as the 'pickupCOuntry' in the Create Order API.

If you wish to enter a country code not listed below, please reach out to your Account Manager, write to us at: <a href="mailto:support@loginextsolutions.com?Subject=Postal-Code%20Queries" target="_top">support@loginextsolutions.com</a> 

Country |  Code
--------- | ---------  
AFGHANISTAN | AFG
ALBANIA|ALB
ALGERIA|DZA
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
BRUNEI|BRN
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
ETHIOPIA|ETH
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
IRAN|IRN
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
PALESTINIAN TERRITORIES|PSE
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
SYRIA|SYR
TAIWAN|TWN
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
VIETNAM|VNM
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




## Australia

State | Code
--------- | ---------
New South Wales|New South
Victoria|Victoria
Queensland|Queensland
South Australia|South Aust
Tasmania|Tasmania

## Bangladesh 
State | Code
--------- | ---------

Dhaka | Dhaka
Khulna  | Khulna
Rājshāhi  | Rajshahi
Chattogram | Chittagong
Sylhet | Sylhet
Barisāl | Barisal
Rangpur | GI
Mymensingh | MY

## Canada

State | Code
--------- | ---------
Alberta | CA-AB
British Columbia | CA-BC
Manitoba | CA-MB
New Brunswick | CA-NB
Newfoundland and Labrador | CA-NL
Nova Scotia | CA-NS
Northwest Territory | CA-NT
Nunavut Territory | CA-NU
Ontario | CA-ON
Prince Edward Island | CA-PE
Quebec | CA-QC
Saskatchewan | CA-SK
Yukon | CA-YT

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

## Myanmar
State | Code
--------- | ---------
Mandalay | MA
Irrawaddy | IR
Mon State | MS
Sagaing | SG
Shan State | SS
Pegu | PG
Rakhine State | RS
Kachin State | KCS
Magwe | MG
Kayah State | KYS
Chin State | CS
Karan State | KRS
Rangoon | RN

## Nepal
State | Code
--------- | ---------
Janakpur | JA
Bheri | BH
Dhawalagiri | DH
Gandaki | GA
Karnali | KA
Kosi | KO
Lumbini | LU
Mahakali | MA
Mechi | ME
Narayani | NA
Rapti | RA
Sagarmatha | SA
Bagmati | BA
Seti | SE

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


## Sri Lanka

State | Code
--------- | ---------
Southern | SO
North Central | NC
Uva | UV
Sabaragamuwa | SB
North Western | NW
Jaffna | JF
Kalutara | KL
Kandy | KA
Kegalla | Kegalla
Kurunegala | KU
Mannar | MN
Matale | MT
Amparai | AM,
Moneragala | MO
Mullaittivu | MU
Nuwara Eliya | NE
Polonnaruwa | PO
Puttalam | PU
Ratnapura | RA
Trincomalee | TR
Vavuniya | VA
Matara | MA
Anuradhapura | AN
Badulla | BD
Batticaloa | BT
Colombo | CO
Galle | GL
Gampaha | GM
Hambantota | HA

## Tanzania

State | Code
--------- | ---------
Dar es salaam Tz|Dar es sal
Arusha Tz|Arusha Tz
Mbeya Tz|Mbeya Tz
Mtwara Tz|Mtwara Tz
Dodoma Tz|Dodoma Tz
Other States Tz|Other Stat

## Thailand

State | Code
--------- | ---------
Amnat Charoen | TH-37
Ang Thong | TH-15
Bueng Kan | TH-38
Buri Ram  | TH-31
Chachoengsao  | TH-24
Chai Nat  | TH-18
Chaiyaphum  | TH-36
Chanthaburi | TH-22
Chiang Mai  | TH-50
Chiang Rai  | TH-57
Chon Buri | TH-20
Chumphon  | TH-86
Kalasin | TH-46
Kamphaeng Phet  | TH-62
Kanchanaburi  | TH-71
Khon Kaen | TH-40
Krabi | TH-81
Krung Thep Maha Nakhon  | TH-10
Lampang | TH-52
Lamphun | TH-51
Loei  | TH-42
Lop Buri  | TH-16
Mae Hong Son  | TH-58
Maha Sarakham | TH-44
Mukdahan  | TH-49
Nakhon Nayok  | TH-26
Nakhon Pathom | TH-73
Nakhon Phanom | TH-48
Nakhon Ratchasima | TH-30
Nakhon Sawan  | TH-60
Nakhon Si Thammarat | TH-80
Nan | TH-55
Narathiwat  | TH-96
Nong Bua Lam Phu  | TH-39
Nong Khai | TH-43
Nonthaburi  | TH-12
Pathum Thani  | TH-13
Pattani | TH-94
Phangnga  | TH-82
Phatthalung | TH-93
Phatthaya | TH-S
Phayao  | TH-56
Phetchabun  | TH-67
Phetchaburi | TH-76
Phichit | TH-66
Phitsanulok | TH-65
Phra Nakhon Si Ayutthaya  | TH-14
Phrae | TH-54
Phuket  | TH-83
Prachin Buri  | TH-25
Prachuap Khiri Khan | TH-77
Ranong  | TH-85
Ratchaburi  | TH-70
Rayong  | TH-21
Roi Et  | TH-45
Sa Kaeo | TH-27
Sakon Nakhon  | TH-47
Samut Prakan  | TH-11
Samut Sakhon  | TH-74
Samut Songkhram | TH-75
Saraburi  | TH-19
Satun | TH-91
Si Sa Ket | TH-33
Sing Buri | TH-17
Songkhla  | TH-90
Sukhothai | TH-64
Suphan Buri | TH-72
Surat Thani | TH-84
Surin | TH-32
Tak | TH-63
Trang | TH-92
Trat  | TH-23
Ubon Ratchathani  | TH-34
Udon Thani  | TH-41
Uthai Thani | TH-61
Uttaradit | TH-53
Yala  | TH-95
Yasothon  | TH-35

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



# Timezone Codes

When creating entities in LogiNext for which you want to associate Timezone specific information, use the Timezone codes listed below. 

For example, if you want to create an Order that is to be picked up from a Pick-up location in New York , you would pass 'America/New_York' as the 'pickupAddressTimezone' in the Create Order API.

If you wish to enter a Timezone code not listed below, please reach out to your Account Manager, write to us at: <a href="mailto:support@loginextsolutions.com?Subject=Postal-Code%20Queries" target="_top">support@loginextsolutions.com</a> 

Country Name| Description | Daylight Savings | Timezone Canonical ID
--------- | --------- | -------------- | -------------
AFGHANISTAN|(GMT+04:30) Afghanistan||Asia/Kabul
AFGHANISTAN|(GMT+04:30) Afghanistan||Asia/Kabul
ALBANIA|(GMT+01:00) Albania|ALBANIA(GMT+02:00)|Etc/GMT-1
ALGERIA|(GMT+01:00) Algeria||Etc/GMT-1
AMERICAN SAMOA|(GMT-11:00) American Samoa||Etc/GMT+11
ANDORRA|(GMT+01:00) Andorra|ANDORRA(GMT+02:00)|Europe/Andorra
ANGOLA|(GMT+01:00) Angola||Africa/Luanda
ANGUILLA|(GMT-04:00) Anguilla||America/Anguilla
ANTARCTICA|(GMT-04:00) Antarctica||Antarctica/Palmer
ANTIGUA AND BARBUDA|(GMT-03:00) Antigua And Barbuda||America/St_Johns
ARGENTINA|(GMT+04:00) Argentina||America/Argentina/Buenos_Aires
ARMENIA|(GMT-04:00) Armenia||Asia/Yerevan
ARUBA|(GMT±00:00) Aruba||America/Aruba(-4:00)
AUSTRALIA|(GMT+08:00) Western Australia|-|Australia/Perth
AUSTRALIA|(GMT+09:30) Northern Territory|NULL|Australia/Darwin
AUSTRALIA|(GMT+09:30) South Australia|South Australia(GMT+10:30)|Australia/Adelaide
AUSTRALIA|(GMT+10:00) Australian Capital Territory|Australian Capital Territory(GMT+11:00)|Australia/Sydney
AUSTRALIA|(GMT+10:00) New South Wales|New South Wales(GMT+11:00)|Australia/Sydney
AUSTRALIA|(GMT+10:00) Queensland|NULL|Australia/Brisbane
AUSTRALIA|(GMT+10:00) Tasmania|Tasmania(GMT+11:00)|Australia/Hobart
AUSTRALIA|(GMT+10:00) Victoria|Victoria(GMT+11:00)|Australia/Melbourne
AUSTRALIA|(GMT+10:30) Lord Howe Island|Lord Howe Island(GMT+11:00)|Australia/Lord_Howe
AUSTRALIA|(GMT+11:00) Macquarie Island|NULL|Antarctica/Macquarie
AUSTRIA|(GMT+01:00) Austria|AUSTRIA(GMT+02:00)|Europe/Vienna
AZERBAIJAN|(GMT+04:00) Azerbaijan||Asia/Baku
BAHAMAS.THE|(GMT-05:00) Bahamas.The|BAHAMAS.THE(GMT-04:00)|America/Nassau
BAHAMAS|(GMT-05:00) Bahamas|BAHAMAS(GMT-04:00)|America/Nassau
BAHRAIN|(GMT+03:00) Bahrain||Asia/Bahrain
BANGLADESH|(GMT+06:00) Bangladesh||Asia/Dhaka
BARBADOS|(GMT-04:00) Barbados||America/Barbados
BELARUS|(GMT+03:00) Belarus||Europe/Minsk
BELGIUM|(GMT+01:00) Belgium|BELGIUM(GMT+02:00)|Europe/Brussels
BELIZE|(GMT-06:00) Belize||America/Belize
BENIN|(GMT+01:00) Benin||Africa/Porto-Novo
BERMUDA|(GMT-04:00) Bermuda|BERMUDA(GMT-03:00)|Atlantic/Bermuda
BHUTAN|(GMT+06:00) Bhutan||Asia/Thimphu
BOLIVIA|(GMT-04:00) Bolivia||America/La_Paz
BOSNIA AND HERZEGOVINA|(GMT+01:00) Bosnia And Herzegovina||NULL
BOSNIA AND HERZEGOWINA|(GMT+01:00) Bosnia And Herzegowina|BOSNIA AND HERZEGOWINA(GMT+02:|NULL
BOTSWANA|(GMT-03:30) Newfoundland||Canada/Newfoundland
BOTSWANA|(GMT-04:00) Atlantic||Canada/Atlantic
BOTSWANA|(GMT-05:00) Eastern||Canada/Eastern
BOTSWANA|(GMT-06:00) Central||Canada/Central
BOTSWANA|(GMT-07:00) Mountain||Canada/Mountain
BOTSWANA|(GMT-08:00) Pacific||Canada/Pacific
BOTSWANA|(GMT+02:00) Botswana||Africa/Gaborone
BOUVET ISLAND|(GMT-05:00) Bouvet Island||Etc/GMT+5
BRAZIL|(GMT-03:00) Brasilia Standard Time||America/Sao_Paulo
BRITISH INDIAN OCEAN TERRITORY|(GMT+06:00) British Indian Ocean Territory||NULL
BRUNEI DARUSSALAM|(GMT+08:00) Brunei Darussalam||Asia/Brunei
BRUNEI|(GMT-04:00) Brunei||Asia/Brunei
BULGARIA|(GMT+02:00) Bulgaria|BULGARIA(GMT+03:00)|Europe/Sofia
BURKINA FASO|(GMT±00:00) Burkina Faso||Africa/Ouagadougou
BURUNDI|(GMT+02:00) Burundi||Africa/Bujumbura
CAMBODIA|(GMT+07:00) Cambodia||Asia/Phnom_Penh
CAMEROON|(GMT+01:00) Cameroon||Etc/GMT-1
CANADA | (GMT-03:30) Canada(Newfoundland) || America/St_Johns
CANADA | (GMT-04:00) Canada(Atlantic) || America/Halifax
CANADA | (GMT-04:00) Canada (Atlantic Standard Time) || America/Blanc-Sablon
CANADA | (GMT-05:00) Canada(Eastern) ||  America/Toronto
CANADA | (GMT-05:00) Canada (Eastern Standard Time) || America/Atikokan
CANADA | (GMT-06:00) Canada(Central) || America/Regina
CANADA | (GMT-06:00) Canada (Central Standard Time) || America/Winnipeg
CANADA | (GMT-07:00) Canada(Mountain) ||  America/Edmonton
CANADA | (GMT-07:00) Canada (Mountain Standard Time) || America/Creston
CANADA | (GMT-08:00) Canada(Pacific) || America/Vancouver
CAYMAN ISLANDS|(GMT-05:00) Cayman Islands || America/Cayman
CENTRAL AFRICAN REPUBLIC|(GMT+01:00) Central African Republic||NULL
CENTRAL AFRICAN REPUBLIC|(GMT+01:00) Central African Republic||NULL
CHAD|(GMT+01:00) Chad||Africa/Ndjamena
CHILE|(GMT-04:00) Chile|CHILE(GMT-03:00)|America/Santiago
CHINA|(GMT+08:00) China||Asia/Shanghai
CHRISTMAS ISLAND|(GMT+07:00) Christmas Island||Indian/Christmas
COCOS (KEELING) ISLANDS|(GMT+06:00) Cocos (Keeling) Islands||NULL
COLOMBIA|(GMT-05:00) Colombia||America/Bogota
COMOROS|(GMT+03:00) Comoros||Etc/GMT-3
CONGO| DEMOCRATIC REPUBLIC OF THE|(GMT+01:00) Congo| Democratic Republic Of||NULL
CONGO| THE DRC|(GMT+02:00) Congo| The Drc||Africa/Kinshasa
CONGO|(GMT+01:00) Congo||Africa/Brazzaville
COOK ISLANDS|(GMT-10:00) Cook Islands||Etc/GMT+10
COSTA RICA|(GMT-06:00) Costa Rica||America/Costa_Rica
CROATIA|(GMT+01:00) Croatia|CROATIA(GMT+02:00)|Etc/GMT-1
CUBA|(GMT-05:00) Cuba|CUBA(GMT-04:00)|America/Havana
CYPRUS|(GMT+02:00) Cyprus|CYPRUS(GMT+03:00)|Asia/Nicosia
CZECH REPUBLIC|(GMT+01:00) Czech Republic|CZECH REPUBLIC(GMT+02:00)|Europe/Prague
DENMARK|(GMT+01:00) Denmark|DENMARK(GMT+02:00)|Europe/Copenhagen
DJIBOUTI|(GMT+03:00) Djibouti||Africa/Djibouti
DOMINICA|(GMT-04:00) Dominica||America/Dominica
DOMINICAN REPUBLIC|(GMT-04:00) Dominican Republic||Europe/Copenhagen
ECUADOR|(GMT?05:00) Ecuador||NULL
EGYPT|(GMT+02:00) Egypt||Africa/Cairo
EL SALVADOR|(GMT-06:00) El Salvador||America/El_Salvador
EQUATORIAL GUINEA|(GMT+01:00) Equatorial Guinea||Africa/Malabo
ERITREA|(GMT+03:00) Eritrea||Africa/Asmara
ESTONIA|(GMT+02:00) Estonia|ESTONIA(GMT+03:00)|Europe/Tallinn
ETHIOPIA|(GMT+03:00) Ethiopia||Africa/Addis_Ababa
FALKLAND ISLANDS (MALVINAS)|(GMT-03:00) Falkland Islands (Malvinas)||NULL
FAROE ISLANDS|(GMT±00:00) Faroe Islands|FAROE ISLANDS(GMT+01:00)|Atlantic/Faroe
FIJI|(GMT+12:00) Fiji|FIJI(GMT+13:00)|Pacific/Fiji
FINLAND|(GMT+02:00) Finland|FINLAND(GMT+03:00)|Europe/Helsinki
FRANCE| METROPOLITAN|(GMT+01:00) France| Metropolitan|FRANCE| METROPOLITAN(GMT+02:00|NULL
FRANCE|(GMT+01:00) France|FRANCE(GMT+02:00)|Europe/Paris
FRENCH GUIANA|(GMT-03:00) French Guiana||Etc/GMT+3
FRENCH POLYNESIA|(GMT-10:00) French Polynesia||Etc/GMT+10
FRENCH SOUTHERN TERRITORIES|(GMT+05:00) French Southern Territories|FRENCH SOUTHERN TERRITORIES(GM|NULL
GABON|(GMT+01:00) Gabon||Africa/Libreville
GAMBIA|(GMT±00:00) Gambia||Africa/Banjul
GEORGIA|(GMT+04:00) Georgia||Atlantic/South_Georgia
GERMANY|(GMT+01:00) Germany|GERMANY(GMT+02:00)|Europe/Berlin
GHANA|(GMT±00:00) Ghana||Africa/Accra
GIBRALTAR|(GMT+01:00) Gibraltar|GIBRALTAR(GMT+02:00)|Europe/Gibraltar
GREECE|(GMT+02:00) Greece|GREECE(GMT+03:00)|Europe/Athens
GREENLAND|(GMT-03:00) Greenland|GREENLAND(GMT-02:00)|Etc/GMT+3
GRENADA|(GMT-04:00) Grenada||America/Grenada
GUADELOUPE|(GMT-04:00) Guadeloupe||America/Guadeloupe
GUAM|(GMT+10:00) Guam||Pacific/Guam
GUATEMALA|(GMT-06:00) Guatemala||America/Guatemala
GUINEA|(GMT±00:00) Guinea||Africa/Conakry
GUYANA|(GMT-04:00) Guyana||America/Guyana
HAITI|(GMT-05:00) Haiti||America/Port-au-Prince
HONDURAS|(GMT-06:00) Honduras||America/Tegucigalpa
HONG KONG|(GMT+08:00) Hong Kong||Asia/Hong_Kong
HUNGARY|(GMT+01:00) Hungary|HUNGARY(GMT+02:00)|Europe/Budapest
ICELAND|(GMT±00:00) Iceland||Atlantic/Reykjavik
INDIA|(GMT+05:30) India||Asia/Calcutta
INDONESIA|(GMT+07:00) Indonesia||Asia/Jakarta
IRAN|(GMT+03:30) Iran (Islamic Republic Of)|IRAN (ISLAMIC REPUBLIC OF)(GMT|Asia/Tehran
IRAQ|(GMT+03:00) Iraq||Asia/Baghdad
IRELAND|(GMT±00:00) Ireland|IRELAND(GMT+01:00)|Europe/Dublin
ISRAEL|(GMT+02:00) Israel|ISRAEL(GMT+03:00)|Asia/Jerusalem
ITALY|(GMT+01:00) Italy|ITALY(GMT+02:00)|Europe/Rome
JAMAICA|(GMT-05:00) Jamaica||America/Jamaica
JAPAN|(GMT+09:00) Japan||Asia/Tokyo
JORDAN|(GMT+02:00) Jordan|JORDAN(GMT+03:00)|Asia/Amman
KAZAKHSTAN|(GMT+05:00) Kazakhstan||Etc/GMT-5
KENYA|(GMT+03:00) Kenya||Africa/Nairobi
KIRIBATI|(GMT+05:00) Kiribati||Pacific/Tarawa
KOREA| D.P.R.O.|(GMT+09:00) Korea| D.P.R.O.||Asia/Pyongyang
KOREA| REPUBLIC OF|(GMT+09:00) Korea| Republic Of||Asia/Seoul
KUWAIT|(GMT+03:00) Kuwait||Asia/Kuwait
KYRGYZSTAN|(GMT+06:00) Kyrgyzstan||Asia/Bishkek
LAOS|(GMT+07:00) Laos||Asia/Vientiane
LATVIA|(GMT+02:00) Latvia|LATVIA(GMT+03:00)|Europe/Riga
LEBANON|(GMT+02:00) Lebanon|LEBANON(GMT+03:00)|Asia/Beirut
LESOTHO|(GMT+02:00) Lesotho||Africa/Maseru
LIBERIA|(GMT±00:00) Liberia||Africa/Monrovia
LIECHTENSTEIN|(GMT+01:00) Liechtenstein|LIECHTENSTEIN(GMT+02:00)|Europe/Vaduz
LITHUANIA|(GMT+02:00) Lithuania|LITHUANIA(GMT+03:00)|Europe/Vilnius
LUXEMBOURG|(GMT+01:00) Luxembourg|LUXEMBOURG(GMT+02:00)|Europe/Luxembourg
MACAU|(GMT+08:00) Macau||Asia/Macau
MACEDONIA|(GMT+01:00) Macedonia|MACEDONIA(GMT+02:00)|Etc/GMT-1
MADAGASCAR|(GMT+03:00) Madagascar||Indian/Antananarivo
MALAWI|(GMT+02:00) Malawi||Etc/GMT-2
MALAYSIA|(GMT+08:00) Malaysia||Asia/Kuala_Lumpur
MALDIVES|(GMT+05:00) Maldives||Indian/Maldives
MALI|(GMT±00:00) Mali||Africa/Bamako
MALTA|(GMT+01:00) Malta|MALTA(GMT+02:00)|Europe/Malta
MARSHALL ISLANDS|(GMT+12:00) Marshall Islands||Pacific/Majuro
MARTINIQUE|(GMT-04:00) Martinique||America/Martinique
MAURITANIA|(GMT±00:00) Mauritania||Africa/Nouakchott
MAURITIUS|(GMT+04:00) Mauritius||Indian/Mauritius
MAYOTTE|(GMT+03:00) Mayotte||Indian/Mayotte
MEXICO|(GMT-05:00) Mexico(State Of Quintana Roo)|MEXICO(GMT-05:00)|NULL
MEXICO|(GMT-06:00) Mexico(Baja California Sur (South)| Chihuahua|Nayarit| Sinaloa|Mexico(states of Baja California Sur| Chihuahua| N|America/Mexico_City
MEXICO|(GMT-07:00) Mexico(State Of Sonora)|NULL|Etc/GMT+7
MEXICO|(GMT-08:00) Mexico(State Of Baja California)|Mexico(state of Baja California)(GMT-07:00)|Etc/GMT+7
MICRONESIA| FEDERATED STATES OF|(GMT+10:00) Micronesia| Federated States Of||NULL
MOLDOVA| REPUBLIC OF|(GMT+02:00) Moldova| Republic Of|MOLDOVA| REPUBLIC OF(GMT+03:00|Europe/Chisinau
MONACO|(GMT+01:00) Monaco|MONACO(GMT+02:00)|Europe/Monaco
MONGOLIA|(GMT+08:00) Mongolia|MONGOLIA(GMT+09:00)|Asia/Ulaanbaatar
MONTENEGRO|(GMT+01:00) Montenegro|MONTENEGRO(GMT+02:00)|Etc/GMT-1
MONTSERRAT|(GMT-04:00) Montserrat||America/Montserrat
MOROCCO|(GMT±00:00) Morocco|MOROCCO(GMT+01:00)|Etc/GMT
MOZAMBIQUE|(GMT+02:00) Mozambique||Africa/Maputo
MYANMAR (BURMA)|(GMT+06:30) Myanmar (Burma)||Asia/Rangoon
NAMIBIA|(GMT+01:00) Namibia|NAMIBIA(GMT+02:00)|Africa/Windhoek
NAURU|(GMT+12:00) Nauru||Pacific/Nauru
NEPAL|(GMT+05:45) Nepal||Asia/Kathmandu
NETHERLANDS ANTILLES|(GMT+01:00) Netherlands Antilles|NETHERLANDS ANTILLES(GMT+02:00|NULL
NETHERLANDS|(GMT+01:00) Netherlands|NETHERLANDS(GMT+02:00)|Europe/Amsterdam
NEW CALEDONIA|(GMT+11:00) New Caledonia||Etc/GMT-11
NEW ZEALAND|(GMT+12:00) New Zealand|NEW ZEALAND(GMT+13:00)|Pacific/Auckland
NICARAGUA|(GMT-06:00) Nicaragua||America/Managua
NIGER|(GMT+01:00) Niger||Etc/GMT-1
NIGERIA|(GMT+01:00) Nigeria||Etc/GMT-1
NIUE|(GMT-11:00) Niue||Pacific/Niue
NORFOLK ISLAND|(GMT+11:00) Norfolk Island||Pacific/Norfolk
NORTHERN MARIANA ISLANDS|(GMT+10:00) Northern Mariana Islands||NULL
NORWAY|(GMT+01:00) Norway|NORWAY(GMT+02:00)|Europe/Oslo
OMAN|(GMT+04:00) Oman||Asia/Muscat
PAKISTAN|(GMT+05:00) Pakistan||Asia/Karachi
PALAU|(GMT+09:00) Palau||Pacific/Palau
PANAMA|(GMT-05:00) Panama||America/Panama
PAPUA NEW GUINEA|(GMT+10:00) Papua New Guinea||Pacific/Port_Moresby
PARAGUAY|(GMT-04:00) Paraguay|PARAGUAY(GMT-03:00)|America/Asuncion
PERU|(GMT-05:00) Peru||America/Lima
PHILIPPINES|(GMT+08:00) Philippines||Asia/Manila
PITCAIRN|(GMT-08:00) Pitcairn||Pacific/Pitcairn
POLAND|(GMT+01:00) Poland|POLAND(GMT+02:00)|Europe/Warsaw
PORTUGAL|(GMT±00:00) Portugal|PORTUGAL(GMT+01:00)|Europe/Lisbon
PUERTO RICO|(GMT-04:00) Puerto Rico||America/Puerto_Rico
QATAR|(GMT+03:00) Qatar||Asia/Qatar
REUNION|(GMT+04:00) Reunion||Indian/Reunion
ROMANIA|(GMT+02:00) Romania|ROMANIA(GMT+03:00)|Europe/Bucharest
RUSSIA|(GMT+02:00) Russia(Kaliningrad)|RUSSIA()|Europe/Moscow
RUSSIA|(GMT+03:00) Russia(Moscow)||Europe/Moscow
RUSSIA|(GMT+04:00) Russia(Samara)||Europe/Samara
RUSSIA|(GMT+05:00) Russia(Yekaterinburg)||Asia/Yekaterinburg
RUSSIA|(GMT+06:00) Russia(Omsk)||Asia/Omsk
RUSSIA|(GMT+07:00) Russia(Krasnoyarsk)||Asia/Krasnoyarsk
RUSSIA|(GMT+08:00) Russia(Irkutsk)||Asia/Irkutsk
RUSSIA|(GMT+09:00) Russia(Yakutsk)||Asia/Yakutsk
RUSSIA|(GMT+10:00) Russia(Vladivostok)||Asia/Vladivostok
RUSSIA|(GMT+11:00) Russia(Magadan)||Asia/Magadan
RUSSIA|(GMT+12:00) Russia(Kamchatka)||Asia/Kamchatka
RWANDA|(GMT+02:00) Rwanda||Africa/Kigali
SAINT KITTS AND NEVIS|(GMT-04:00) Saint Kitts And Nevis||NULL
SAINT LUCIA|(GMT-04:00) Saint Lucia||America/St_Lucia
SAINT VINCENT AND THE GRENADINES|(GMT-04:00) Saint Vincent And The Grenadin||NULL
SAMOA|(GMT+13:00) Samoa|SAMOA(GMT+14:00)|Pacific/Apia
SAN MARINO|(GMT+01:00) San Marino|SAN MARINO(GMT+02:00)|Etc/GMT-1
SAO TOME AND PRINCIPE|(GMT±00:00) Sao Tome And Principe||NULL
SAUDI ARABIA|(GMT+03:00) Saudi Arabia||Asia/Riyadh
SENEGAL|(GMT±00:00) Senegal||Africa/Dakar
SERBIA|(GMT+01:00) Serbia|SERBIA(GMT+02:00)|Europe/Belgrade
SEYCHELLES|(GMT+04:00) Seychelles||Etc/GMT-4
SIERRA LEONE|(GMT±00:00) Sierra Leone||Africa/Freetown
SINGAPORE|(GMT+08:00) Singapore||Asia/Singapore
SLOVENIA|(GMT+01:00) Slovenia|SLOVENIA(GMT+02:00)|Etc/GMT-1
SOLOMON ISLANDS|(GMT+11:00) Solomon Islands||Etc/GMT-11
SOMALIA|(GMT+03:00) Somalia||Africa/Mogadishu
SOUTH AFRICA|(GMT+02:00) South Africa||Africa/Blantyre
SOUTH GEORGIA AND SOUTH S.S.|(GMT-02:00) South Georgia And South S.S.||NULL
SOUTH SUDAN|(GMT+03:00) South Sudan||Etc/GMT-3
SPAIN|(GMT+01:00) Spain|SPAIN(GMT+02:00)|Europe/Madrid
SRI LANKA|(GMT+05:30) Sri Lanka||Asia/Colombo
SUDAN|(GMT+03:00) Sudan||Africa/Khartoum
SURINAME|(GMT-03:00) Suriname||America/Paramaribo
SVALBARD AND JAN MAYEN ISLANDS|(GMT+01:00) Svalbard And Jan Mayen Islands|SVALBARD AND JAN MAYEN ISLANDS|NULL
SWAZILAND|(GMT+02:00) Swaziland||Africa/Mbabane
SWEDEN|(GMT+01:00) Sweden|SWEDEN(GMT+02:00)|Europe/Stockholm
SWITZERLAND|(GMT+01:00) Switzerland|SWITZERLAND(GMT+02:00)|Etc/GMT-1
SYRIAN ARAB REPUBLIC|(GMT+02:00) Syrian Arab Republic|SYRIAN ARAB REPUBLIC(GMT+03:00|NULL
TAJIKISTAN|(GMT+05:00) Tajikistan||Asia/Dushanbe
TANZANIA|(GMT+03:00) Tanzania||Africa/Addis_Ababa
THAILAND|(GMT+07:00) Thailand||Asia/Bangkok
TOGO|(GMT±00:00) Togo||Africa/Lome
TOKELAU|(GMT+13:00) Tokelau||Etc/GMT-13
TONGA|(GMT+13:00) Tonga|TONGA(GMT+14:00)|Pacific/Tongatapu
TRINIDAD AND TOBAGO|(GMT-04:00) Trinidad And Tobago||America/Port_of_Spain
TUNISIA|(GMT+01:00) Tunisia||Africa/Tunis
TURKEY|(GMT+03:00) Turkey||Etc/GMT-3
TURKMENISTAN|(GMT+05:00) Turkmenistan||Asia/Ashgabat
TURKS AND CAICOS ISLANDS|(GMT-04:00) Turks And Caicos Islands||NULL
TUVALU|(GMT+12:00) Tuvalu||Pacific/Funafuti
UGANDA|(GMT+03:00) Uganda||Africa/Kampala
UKRAINE|(GMT+02:00) Ukraine|UKRAINE(GMT+03:00)|Etc/GMT-2
UNITED ARAB EMIRATES|(GMT+04:00) United Arab Emirates||Asia/Dubai
UNITED KINGDOM|(GMT±00:00) United Kingdom|UNITED KINGDOM(GMT+01:00)|Europe/London
UNITED STATES|(GMT-05:00) United States(Eastern)|UNITED STATES(GMT-04:00)|America/New_York
UNITED STATES|(GMT-06:00) United Stated(Central)||America/Chicago
UNITED STATES|(GMT-07:00) United Stated(Arizona)||America/Phoenix
UNITED STATES|(GMT-07:00) United States(Mountain)|NULL|America/Denver
UNITED STATES|(GMT-08:00) United States(Pacific)|NULL|America/Los_Angeles
UNITED STATES|(GMT-09:00) United States(Alaska)|NULL|America/Anchorage
UNITED STATES|(GMT-10:00) United States(Hawaii-Aleutian)|NULL|Pacific/Honolulu
URUGUAY|(GMT-03:00) Uruguay||America/Montevideo
UZBEKISTAN|(GMT+05:00) Uzbekistan||Asia/Tashkent
VANUATU|(GMT+11:00) Vanuatu||Etc/GMT-11
VENEZUELA|(GMT-04:00) Venezuela||America/Caracas
VIETNAM|(GMT+07:00) Vietnam|NULL|Etc/GMT-7
WALLIS AND FUTUNA ISLANDS|(GMT+12:00) Wallis And Futuna Islands||NULL
YEMEN|(GMT+03:00) Yemen||Etc/GMT-3
ZAMBIA|(GMT+02:00) Zambia||Africa/Lusaka
ZIMBABWE|(GMT+02:00) Zimbabwe||Africa/Harare


# Postal Codes

If you are looking for a postal code/zip code list for your country, please reach out to your Account Manager to get it configured, or write to us at: <a href="mailto:support@loginextsolutions.com?Subject=Postal-Code%20Queries" target="_top">support@loginextsolutions.com</a> 

# Delivery Associate Status

The current Status of your Delivery Associate. The Status can be updated by calling the Update Status API for the Delivery Associate.

Status | Code | Description
--------- | --------- | -------------
Active | ACTIVE | A Delivery Associate that is Active will be assigned Orders and can Sign In to their TrackNext account. 
Inactive | INACTIVE | A Delivery Associate that is Inactive will not be assigned any orders, or be able to log in to their TrackNext account.
On Break | ONBREAK | The Delivery Associate is not currently fulfilling Orders. New Orders cannot be assigned to an On Break Delivery associate. Only Active Delivery Associates can be On Break.
Off Break | OFFBREAK | Delivery Associate is back from Break and ready to fulfil Orders. Only Active Delivery Associates can be On Break.

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
