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

LogiNext welcomes you to the world of organised logistics.

Using the LogiNext API, you can integrate all the segments of your logistics and supply chain network into our product platform to create seamless experience for your operations and executive team.

The LogiNext API is designed to allow our client partners to add resources, shipments, plan a route, start the trip, track and follow the updates till the trip is completed and shipment is pickedup/delivered at the desired location.

Below are few important steps that would explain what it takes for you, as our Client partner, to link your system with LogiNext’s.

<b><u>Step 1</u></b> –  Please read carefully the Request, Responses and Authentication section so that you can configure things on your end to integrate with LogiNext APIs.

<b><u>Step 2</u></b> – You will need to get the username and password which will be provided to you either by our system (in case of auto sign-up) or by our assigned CSAs(Customer Service Associate)

<b><u>Step 3</u></b> – (Optional) If you are planning to consume any of the LogiNext notifications, you will need to share the end-point URL on your system to consume the Webhook.

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
CLIENT_SECRET_KEY | $2a$08$LQEqG3s.LF2jBt7Baq| Authentication key

### Versioning

Versioning allows us to provide developers a consistent experience. All endpoints are prefixed with a version such as /v1. This version refers to the overall layout of the endpoints and response standards.

# Responses

The LogiNext API uses HTTP status codes to indicate the status of your requests. This includes Success and Error codes.

Dates in API responses like 2016-07-01T11:18:00.000Z are sent in Coordinated Universal Time (UTC) format.

Code | Message | Description
---------- | ------- | -------
200 | Success | This message means that the request is successfully processed.
201 | Created  | This message means that the resource is successfully created.
400 | Bad Request  | This message means that the request is syntactically incorrect.
401 | Invalid username or password  | This message means that invalid credentials are passed.
404 | Not Found  | This message means that the resource could not be found.
405 | Method Not Allowed  | This message means that the method used to access the resource is invalid.
409 | Conflict  | This message means that the request could not be completed due to a conflict with the current state of the target resource.
415 | Unsupported Media Type  |  This message means that the request is not in the format accepted by this method of target resource.
429 | Too Many Requests  |  This message means that too many resources are requested.
500 | Internal Server Error  | This message means that there is an issue with the LogiNext server.Please try accessing the request later.
503 | Service Unavailable  | This message means that the LogiNext applications are down for scheduled maintanance. Please try accessing the request later.

# Authentication

##Authenticate

LogiNext API uses Basic Authentication to provide you an authorized access. Please use the the below URL Endpoint to authenticate yourself as a user of this API.

You will have to pass the username and password which is provided to you either by our system (in case of auto sign-up) or by our assigned CSAs(Customer Service Associate).

The response will contain a session token and a Client Secret key, which is unique in relation to every specific customer.

If you want session to be valid for 1 Hour, then the "sessionExpiryTimeout" should be 1.<br>
Similarly for - <br>
24 Hours, it should be 24 <br>
6 months, it should be  180* 24 = 4320<br>
12 Months, it should be 365*24= 8760<br>
5 Years, it should be 365*5*24 = 43800<br>
10 Years, it should be 365*10*24= 87600<br>

<b><u>If you do not provide 'sessionExpiryTimeout', the validity of this session token will be 1 day (24 hours).</u></b>

Please ensure that you add the token and secret key as part of every Loginext API call.

> Definition

```json
https://api.loginextsolutions.com/LoginApp/login/authenticate
```
> Request Body

```json
{
        "userName":"demouser",
        "password":"Admin#1!",
        "sessionExpiryTimeout":72
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

### Request

<span class="post">POST</span>`https://api.loginextsolutions.com/LoginApp/login/authenticate`

### Request Headers

Header | Sample Value | Description
--------- | ------- | -------------
Content-Type | application/json | JSON request

### Request Parameters

Parameter | DataType | Length | Required | Description
-----------|-------|---|---------------|--------
userName | String | 255 | Mandatory | Username provided by LogiNext
password | String | 255 | Mandatory | Password provided by LogiNext
sessionExpiryTimeout | Integer | 10 | Optional | Number of hours till which you want the session to be valid

### Response
The response will consist of parameters as mentioned in the "Responses" section based on the request parameters passed.For example,the response can contain 200 - Success or 401 - Invalid username or password, etc.

### Response Headers

The response header will consist of Authentication Token and Client Secret Key. Please note that the validity of this token and key is 24 hours only.

Header | Sample Value
--------- | -------
WWW-Authenticate | BASIC 075b8961-bd02-454c-83eb-259f965f313f
CLIENT_SECRET_KEY | $2a$08$bCi0ja4B5S02BKQt3VdxNuReERpSV8SiAbwVrHNyhC7mD

##Invalidate

You can fetch a fresh session token and a key by calling the below API. This call will invalidate the existing token and key and then you will be provided with a new token and a key which you will have to pass everytime in every other API call.

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

### Request

<span class="post">GET</span>`https://api.loginextsolutions.com/LoginApp/login/token/refresh`


### Request Headers

Header | Sample Value
--------- | ------- | -------------
Content-Type | application/json | Json request
WWW-Authenticate | BASIC 8bce7b1b-9762-4de7-b9cd-976ecf38b6a0 | Authentication token
CLIENT_SECRET_KEY | $2a$08$npX3e6RD6zJFHcvFV469D.XtRpCwCQwZ3YlsEpERDcd.c2jmabLsG| Authentication key

### Response Headers

Header | Sample Value
--------- | -------
WWW-Authenticate | BASIC 075b8961-bd02-454c-83eb-259f965f313f
CLIENT_SECRET_KEY | $2a$08$bCi0ja4B5S02BKQt3VdxNuReERpSV8SiAbwVrHNyhC7mD


# LogiNext Haul <sup>TM</sup>


1. Once the resources are created, then you can create trips by calling Create Trips API. You need to provide the Unique trip name along with the Origin and Destination Address details and the Journey date. The acknowledgement consists of the Reference ID for each of the trips created which needs to be stored in your system for future references.
Please check with our assigned CSAs on the address format based on the model type configured for you as either the Pin Code or Hub to Hub.

2. Further you can mark the trip as started by calling the Start Trip API and mark the same trip as stopped by calling Stop Trip API. In both these API you will have to pass the trip reference ID.

3. Finally you can track your vehicle in transit through the Track Last Location API. in this case also you need to pass the Trip Reference ID.

## Create Vehicle

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
        "vehiclePermit":"Andhra Pradesh,Delhi",
        "ownership":"company",
        "ownerName":"ABC",
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
        "vehicleNumber":"MH-111",
        "referenceId":"a9be39b9347911e6829f000d3aa04450"
      }
     ],
  "hasError": false
}
```

Create a new vehicle by passing form data through json.

The acknowledgement will provide the vehicle number and reference ID.

### Request

<span class="post">POST</span>`https://api.loginextsolutions.com/VehicleApp/haul/v1/create`


### Request Parameters

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

## Get Vehicle (Single)

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
    "vehicleNumber": "VH-00-1122",
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
    "clientBranchName": "Mahindra Logistics Ltd"
  },
  "hasError": false
}

```

Use this API to read all data for a particular vehicle using its reference ID.


### Request

<span class="post">GET</span>`https://api.loginextsolutions.com/VehicleApp/haul/v1/:reference_id`


### Request Parameters

Parameter | DataType | Length | Required | Description
-----------|-------|-------|------|----------
reference_id | String | 32 | Mandatory | Reference Id associated with the vehicle.


## Get Vehicle

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

### Request

<span class="get">GET</span>`https://api.loginextsolutions.com/VehicleApp/haul/v1`


## Update Vehicle

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
          "vehicleModel":"OMNI",
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
        "vehiclePermit":"Andhra Pradesh,Delhi",
        "ownership":"company",
        "ownerName":"ABC",
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

### Request

<span class="post">PUT</span>`https://api.loginextsolutions.com/VehicleApp/haul/v1`


### Request Parameters

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


## Delete Vehicle

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

### Request

<span class="post">DELETE</span>`https://api.loginextsolutions.com/VehicleApp/haul/v1`



### Request Body

Parameter | DataType |  Required | Description
-----------|-------|------- | ----------
reference_ids | List | Mandatory | Reference Id associated with the vehicle.


## Create Driver
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
        "languageList":[{"name":"English"},{"name":"Hindi"}],
        "salary":"10000",
        "maritalStatus":"married",
        "gender":"male",
        "experience":10,

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
        "managerPhoneNumber":1234567890,
        "managerEmailId":"test@test.com"
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

### Request

<span class="post">POST</span> `https://api.loginextsolutions.com/DriverApp/haul/v1/driver/create`



### Request Parameters

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






## Get Driver

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

### Request

<span class="post">POST</span>` https://api.loginextsolutions.com/DriverApp/haul/v1/driver/list`

### Request Body

Parameter | DataType |  Required | Description
-----------|-------|------- | ----------
reference_ids | List | Mandatory | Reference Id associated with the driver.


## Update Driver

> Definition

```json
https://api.loginextsolutions.com/DriverApp/haul/v1/driver/update
```

> Request Body

```json
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

### Request

<span class="post">PUT</span>`https://api.loginextsolutions.com/DriverApp/haul/v1/driver/update`



### Request Parameters

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

## Delete Driver

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

### Request

<span class="post">DELETE</span>`https://api.loginextsolutions.com/DriverApp/haul/v1/driver/delete`

### Request Body

Parameter | DataType |  Required | Description
-----------|-------|------- | ----------
reference_ids | List | Mandatory | Reference Id associated with the driver.


## Create Trip

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
  "destinationAddr": "NAGD",
  "name": "CNN-NAG-12221",
  "packageWeight": 6,
  "packageValue": 8,
  "packageVolume": 10,
  "vehicleReportingDate": "2016-02-27T18:30:00.000Z",
  "modeOfTransport": "ROAD",
  "vehicleNumber": "MH40AK0175",
  "barcode": "LN00590915",
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

### Request

<span class="post">POST</span>`https://api.loginextsolutions.com/TripApp/haul/v1/trip/create`



### Request Parameters

Parameter | DataType |  Length | Required | Description
-----------|-------|-------|---------|----------
shipmentType | String | 45 | Mandatory | Type of the Shipment being created.Examples:"Bag","Package","Manifest"
originAddr | String | 1000 |  Mandatory | Origin point of the trip.Examples:-AMDD,BLRX
destinationAddr | String | 1000 | Mandatory | Destination point of the trip.Examples:-CNND,BOMX
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


## Get Trip

> Definition

```json
https://api.loginextsolutions.com/TripApp/haul/v1/trip/get
```

> Request Body

```json
[
 "842b0dd8422211e6860c0653055f4dfd", "sfygv54g",
 "842b0c25422211e6860c0653055f4dfd", "842c59b0422211e6860c0653055f4dfd",
 "842ce089422211e6860c0653055f4dfd", "842d9d2d422211e6860c0653055f4dfd",
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
      "batteryPerc": 40
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
      "batteryPerc": 40
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
      "batteryPerc": 40
    },
    {
      "referenceId": "842fc7eb422211e6860c0653055f4dfd",
      "tripName": "Mum-DEL",
      "origin": "Mumbai",
      "destination": "BLRH",
      "tripStatus": "ENDED",
      "tripStartDt": null,
      "tripEndDt": null,
      "eta": "2016-04-05 11:49:00",
      "calculatedStartDt": null,
      "calculatedEndDt": null,
      "actualDistance": 0.0038,
      "packageWeight": 0,
      "packageVolume": 0,
      "packageValue": 0,
      "goodType": null,
      "phoneNumber": "8600900689",
      "isStuckFl": null,
      "lastStuckDt": null,
      "notesDescription": null,
      "barcode": null,
      "lrNumber": "MHHGJHGJ",
      "awbNumber": null,
      "sealNumber": null,
      "challanNumber": null,
      "flightNum": null,
      "trainNum": null,
      "vehicle": "MH02CB829",
      "vehicleType": null,
      "driver": "Paresh",
      "vehicleReportingTime": "2016-04-04 09:30:00",
      "tracking": "2016-04-04 07:46:47",
      "lastHub": null,
      "lastTrackedLatitude": 19.1118,
      "lastTrackedLongitude": 72.909683,
      "batteryPerc": 40
    },
    {
      "referenceId": "842fd22a422211e6860c0653055f4dfd",
      "tripName": "Mum-DEL",
      "origin": "Mumbai",
      "destination": "DELU",
      "tripStatus": "ENDED",
      "tripStartDt": null,
      "tripEndDt": null,
      "eta": "2016-04-05 21:04:00",
      "calculatedStartDt": null,
      "calculatedEndDt": null,
      "actualDistance": 0,
      "packageWeight": 0,
      "packageVolume": 0,
      "packageValue": 0,
      "goodType": null,
      "phoneNumber": "9020405010",
      "isStuckFl": null,
      "lastStuckDt": null,
      "notesDescription": null,
      "barcode": "LN00840216",
      "lrNumber": "jhdgfasjdgfk",
      "awbNumber": null,
      "sealNumber": null,
      "challanNumber": null,
      "flightNum": null,
      "trainNum": null,
      "vehicle": "MH02CB829",
      "vehicleType": null,
      "driver": "Ajay",
      "vehicleReportingTime": "2016-04-04 18:45:00",
      "tracking": "2016-04-04 07:48:56",
      "lastHub": null,
      "lastTrackedLatitude": 19.1118,
      "lastTrackedLongitude": 72.909683,
      "batteryPerc": 40
    },
    {
      "referenceId": "842fd2a3422211e6860c0653055f4dfd",
      "tripName": "Mum-DEL",
      "origin": "Mumbai",
      "destination": "DELU",
      "tripStatus": "ENDED",
      "tripStartDt": null,
      "tripEndDt": null,
      "eta": "2016-04-06 03:49:00",
      "calculatedStartDt": null,
      "calculatedEndDt": null,
      "actualDistance": null,
      "packageWeight": 0,
      "packageVolume": 0,
      "packageValue": 0,
      "goodType": null,
      "phoneNumber": "8600900689",
      "isStuckFl": null,
      "lastStuckDt": null,
      "notesDescription": null,
      "barcode": "LN00840216",
      "lrNumber": "ssdghaj",
      "awbNumber": null,
      "sealNumber": null,
      "challanNumber": null,
      "flightNum": null,
      "trainNum": null,
      "vehicle": "MH02CB829",
      "vehicleType": null,
      "driver": "Paresh",
      "vehicleReportingTime": "2016-04-05 01:30:00",
      "tracking": null,
      "lastHub": null,
      "lastTrackedLatitude": null,
      "lastTrackedLongitude": null,
      "batteryPerc": null
    },
    {
      "referenceId": "842fd390422211e6860c0653055f4dfd",
      "tripName": "Mum-DEL",
      "origin": "Mumbai",
      "destination": "DELU",
      "tripStatus": "ENDED",
      "tripStartDt": null,
      "tripEndDt": null,
      "eta": "2016-04-05 14:49:00",
      "calculatedStartDt": null,
      "calculatedEndDt": null,
      "actualDistance": 0.0242,
      "packageWeight": 0,
      "packageVolume": 0,
      "packageValue": 0,
      "goodType": null,
      "phoneNumber": "8600900689",
      "isStuckFl": null,
      "lastStuckDt": null,
      "notesDescription": null,
      "barcode": "LN00840216",
      "lrNumber": "aGHDFKAYDG",
      "awbNumber": null,
      "sealNumber": null,
      "challanNumber": null,
      "flightNum": null,
      "trainNum": null,
      "vehicle": "MH02CB829",
      "vehicleType": null,
      "driver": "Paresh",
      "vehicleReportingTime": "2016-04-04 12:30:00",
      "tracking": "2016-04-04 09:43:40",
      "lastHub": null,
      "lastTrackedLatitude": 19.1118,
      "lastTrackedLongitude": 72.909683,
      "batteryPerc": 40
    },
    {
      "referenceId": "843e51d3422211e6860c0653055f4dfd",
      "tripName": "Mum-DEL",
      "origin": "Mumbai",
      "destination": "DELU",
      "tripStatus": "ENDED",
      "tripStartDt": null,
      "tripEndDt": null,
      "eta": "2016-04-15 23:51:00",
      "calculatedStartDt": null,
      "calculatedEndDt": null,
      "actualDistance": 13.7874,
      "packageWeight": 0,
      "packageVolume": 0,
      "packageValue": 0,
      "goodType": null,
      "phoneNumber": "9028811556",
      "isStuckFl": null,
      "lastStuckDt": null,
      "notesDescription": null,
      "barcode": "LN01130216",
      "lrNumber": "iu878",
      "awbNumber": null,
      "sealNumber": null,
      "challanNumber": null,
      "flightNum": null,
      "trainNum": null,
      "vehicle": "TN02-GG-2012",
      "vehicleType": null,
      "driver": "Sagnik Sen",
      "vehicleReportingTime": "2016-04-14 21:30:00",
      "tracking": "2016-04-15 14:16:58",
      "lastHub": null,
      "lastTrackedLatitude": 19.02425,
      "lastTrackedLongitude": 72.836267,
      "batteryPerc": 40
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

### Request

<span class="post">POST</span>`https://api.loginextsolutions.com/TripApp/haul/v1/trip/get`



### Request Parameters

Parameter | DataType |  Required | Description
-----------|-------|------- | ----------
reference_ids<br>OR<br>trip names | List | Mandatory | Either the list of Reference Ids or the list of Trip Names is required to fetch list of trip information



## Start Trip

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

### Request

<span class="post">PUT</span>`https://api.loginextsolutions.com/TripApp/haul/v1/trip/start`

### Request Body

Parameter | DataType |  Required | Description
-----------|-------|------- | ----------
referenceIds | List | Mandatory | Reference Ids associated with trips

## Stop Trip


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

### Request

<span class="post">POST</span>`https://api.loginextsolutions.com/TripApp/haul/v1/trip/stop`

### Request Body

Parameter | DataType |  Required | Description
-----------|-------|------- | ----------
referenceIds | List | Mandatory | Reference Ids associated with trips



## Trip iFrame

> Definition

```json
https://api.loginextsolutions.com/track/#/order?tripname=Trip-123&aid=4b41a94b-521b-4986-920d-6e4c1cf15fd0b6&key=$2a$08$dfVg6jJLhrHEsqOUfD1EJHyuelHeIgcUyvgTfGaeRmnzN5jGVi86k
```

The iFrame displays the last tracking for a trip, including current location and trip history, based on the trip name.

### Request


<span class="post">GET</span>` https://api.loginextsolutions.com/track/#/order?tripname=<tripname>&aid=<aid>&key=<key>`

### Request Parameters

Parameter | Sample Value | Description
--------- | ------- | -------------
aid | f522631c-490c-46fd-9f79-ca8d14a704d7 | Value of authentication token without 'BASIC' keyword
key | $2a$08$Vg6jJLhrHEsqOUfD1EJHyuelHeIgcUyvgT | Client Secret Key
tripname | TestTripName| Trip name

## Get Location

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
      "eta": "2016-08-18 06:43:00",
      "lastTrackedAt": "2016-08-17 16:26:01",
    },
    {
      "lat": 23.484535,
      "lng": 79.460987,
      "eta": "2016-08-18 06:43:00",
      "lastTrackedAt": "2016-08-17 16:26:01",
    }
  ],
  "hasError": false
}
```

This API fetches the latest location and the reverse geocoded address for a trip.

### Request

<span class="post">POST</span>`https://api.loginextsolutions.com/TrackingApp/haul/v1/track/lastlocation?address=false`

### Request Parameters

Parameter | DataType |  Required | Description
-----------|-------|------- | ----------
address | Boolean | Optional | To be passed as "true" if reverse geocoded address is needed,else "false"

### Request Body

Parameter | DataType |  Required | Description
-----------|-------|------- | ----------
- | List of Strings | Mandatory | List of Trip names

### Response Body

Parameter | DataType | Description
-----------|-------| ----------
lat | Double | Specifies the latitude of the last tracked location
lng | Double | Specifies the longitude of the last tracked location
eta | Date   | Estimated time of arrival at the destination
lastTrackedAt | Date | The last tracked date and time in UTC of the GPS device
address | String | The reverse geocoded address will be fetched if the "address" parameter is passed as true

## Create Tracking Record

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

### Request

<span class="post">POST</span>`http://api.loginextsolutions.com/TrackingApp/track/put`


### Request Parameters

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


## Get Tracker (List)

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

### Request

<span class="post">GET</span>`https://api.loginextsolutions.com/DeviceApp/device/v1/haul`






# LogiNext Mile <sup>TM</sup>

Mile Product refers to the first mile and last mile shipment deliveries. Mile product will help you create -  

Pick-up orders thereby catering to your first leg of logistics, wherein shipments are ‘picked’ from your customer / merchants / suppliers / vendors and transported to the hub for aggregation.

Delivery orders by loading the items for different orders from a Single Point of Pick Up (Hub) and deliver the same to your customers (Multiple Drop Points).


1. Once the resources are created, then you can add shipments or orders in the LogiNext database by calling Create Order API. You need to provide the Order Number, Date and time window on which order should be picked-up / delivered and the pick-up / delivery address details. Additionally you can also specify the Crate level and line item level details contained in that order.The response consists of the Reference ID against each Order ID which needs to be stored in your system for future references.

2. Once the optimization for capacity and route planning is completed, trips will be created by the LogiNext system and you can mark the trip as started by calling the Start Trip API and mark the same trip as stopped by calling Stop Trip API. In both these API you will have to pass the order reference ID.

3. Finally you can track your pick-up / delivery executive in transit through the Track Last Location API. In this case also you need to pass the Trip Reference Id.

4. You can also mark a particular order as cancelled by calling the Cancel Order API and passing the order reference ID.

5. In case, your account is being configured into the LogiNext system as a pick-up and delivery both, the you can also create the return shipment for the order thereby optimizing you reverse logistics and return planning.

## Create Order (Delivery)

> Definition

```json
https://api.loginextsolutions.com/ShipmentApp/mile/v1/create
```

> Request Body

```json
[
  {
    "orderNo": "DummyOrderNo",
    "awbNumber": "AWB001",
    "shipmentOrderTypeCd": "DELIVER",
    "orderState": "FORWARD",
    "shipmentOrderDt": "2016-07-15T10:30:00.000Z",
    "distributionCenter": "Gurgaon",
    "packageWeight":"10",
    "packageVolume": "4500",
    "paymentType": "Prepaid",
    "packageValue": "5000",
    "numberOfItems": "10",
    "partialDeliveryAllowedFl": "Y",
    "returnAllowedFl": "Y",
    "cancellationAllowedFl": "N",    
    "deliverBranch": "Gurgaon",
    "deliverServiceTime": "20",
    "deliverEndTimeWindow": "2016-07-18T10:31:00.000Z",
    "deliverStartTimeWindow": "2016-07-16T10:31:00.000Z",
    "deliveryType": "DLBOY",
    "deliveryLocationType":"PUP",
    "deliverAccountCode": "Customer001",
    "deliverAccountName": "TestUser",
    "deliverEmail":"test@test.com",
    "deliverPhoneNumber":"1234567890",
    "deliverApartment": "123",
    "deliverStreetName": "Powai",
    "deliverLandmark": "Dmart",
    "deliverLocality": "Hiranandani",
    "deliverCity": "Mumbai",
    "deliverState": "MH",
    "deliverCountry": "IND",
    "deliverPinCode": "400076",
    "deliverLatitude":"19.124497",
    "deliverLongitude":"72.893675",    
    "returnBranch": "Gurgaon",
    "pickupNotes": "PickedUp",
    "deliverNotes": "Delivered"
    "shipmentCrateMappings": [
      {
        "crateCd": "CRATE001",
        "crateAmount":100.65,
        "crateType":"case",
        "noOfUnits":10,
        "shipmentlineitems": [
          {
            "itemCd": "CODE001",
            "itemName": "ITEM1",
            "itemPrice": 100,
            "itemQuantity": 2,
            "itemType": "TYPE1",
            "itemWeight": 10
          },
          {
            "itemCd": "CODE002",
            "itemName": "ITEM2",
            "itemPrice": 50,
            "itemQuantity": 3,
            "itemType": "TYPE2",
            "itemWeight": 10
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
  "message": "Order created successfully",
  "referenceId": [
    "dcd883efcccc4d2299da962a72b01f23"
  ],
  "hasError": false
}

```
Place a new delivery leg order with this API.

### Request

<span class="post">POST</span>`https://api.loginextsolutions.com/ShipmentApp/mile/v1/create`

### Request Parameters

Param | DataType | Length |  Required | Description
--------- | ------- | ---------- | ---------- | ------------
orderNo | String | 100 | Mandatory |  Order No.
awbNumber | String  | 1000 | Optional | Airway Bill No.
shipmentOrderTypeCd | String  | 40 | Mandatory | Order type code. DELIVER for delivery leg order
orderState | String  | 512 | Mandatory | State of order. Ex: FORWARD
shipmentOrderDt | Date |  | Mandatory | Order Date Format - YYYY-MM-DDTHH:MM:SS.SSSZ e.g. : 2016-07-01T11:18:00.000Z.
distributionCenter | String | 255 | Mandatory | Distribution center's name
packageWeight | Double | 10 | Optional | Weight of package in Kg.
packageVolume | Double | 10 | Optional | Volume of package in CC
packageValue | Double | 10 | Optional | Value of package
numberOfItems | Integer | 20 | Optional | Number of crates
paymentType | String | 40 | Optional | Payment mode. Ex: COD - Cash On Delivery, Prepaid
partialDeliveryAllowedFl | String | 50 | Optional | Is Partial Delivery allowed. Ex: Y/N. Default value is N.
returnAllowedFl | String | 1 | Optional | Is Return allowed. Ex: Y/N. Default value is Y.
cancellationAllowedFl | String | 1 | Optional | Is Cancellation allowed. Ex: Y/N. Default value is Y.
deliverBranch | String | 255 | Mandatory | Name of delivery branch
deliverServiceTime | Integer | 11 | Mandatory | Deliver service time in mins.
deliverStartTimeWindow | Date |  | Mandatory | Deliver start time window. Format - YYYY-MM-DDTHH:MM:SS.SSSZ e.g. : 2016-07-01T11:18:00.000Z.
deliverEndTimeWindow | Date |  | Mandatory | Deliver end time window. Format - YYYY-MM-DDTHH:MM:SS.SSSZ e.g. : 2016-07-01T11:18:00.000Z.
deliveryType | String | 40 | Optional | Order delivery type. Ex: TRK - Truck, VAN - Van, DLBOY - Delivery Boy
deliveryLocationType | String | 40 | Optional | Type of delivery location. Ex: CUSTOMER, PUP
deliverAccountCode | String | 255 | Mandatory | Deliver account code
deliverAccountName | String | 255 | Mandatory | Deliver account name
deliverEmail | String | 100 | Optional | Deliver email
deliverPhoneNumber | String | 255 | Optional | Deliver phone number
deliverApartment | String | 512 | Mandatory | Apartment
deliverStreetName | String | 512 | Mandatory | Street name
deliverLandmark | String | 512 | Optional | Landmark
deliverLocality | String | 512 | Mandatory | Locality
deliverCity | String | 512 | Mandatory | City
deliverState| String | 512 | Mandatory | State code. Please refer to the list of state codes provided in the "State Codes" section.
deliverCountry | String | 512 | Mandatory | Country code. Please refer to the list of country codes provided in the "Country Codes" section.
deliverPinCode | String | 20 | Mandatory | Pincode
deliverLatitude | Double |  | Optional | Delivery address Latitude
deliverLongitude | Double |  | Optional | Delivery address Longitude
returnBranch | String | 255 | Mandatory | Name of return branch
pickupNotes | String | 512 | Optional | Additional pickup comments associated with the order
deliverNotes | String | 512 | Optional | Additional delivery comments associated with the order

### Request Parameters (Crates)

Param | DataType | Length |  Required | Description
--------- | ------- | ------- | ---------- | ------------
shipmentCrateMappings | Array of objects |  | Optional | Shipment crates
shipmentCrateMappings.crateCd | String | 128 | Mandatory | Crate code
shipmentCrateMappings.crateAmount | Double |  | Mandatory | Crate amount
shipmentCrateMappings.crateType | String | 100 | Mandatory | Crate type. Ex - ??
shipmentCrateMappings.noOfUnits | Integer | 10 | Mandatory | No. of items in crate
shipmentCrateMappings.shipmentlineitems.itemCd | String | 200 | Mandatory | Item code
shipmentCrateMappings.shipmentlineitems.itemName | String | 255 | Optional | Item name
shipmentCrateMappings.shipmentlineitems.itemPrice | Double |  | Mandatory | Item price
shipmentCrateMappings.shipmentlineitems.itemQuantity | Double | 10 | Mandatory | Item quantity
shipmentCrateMappings.shipmentlineitems.itemType | String | 100 | Optional | Item type
shipmentCrateMappings.shipmentlineitems.itemWeight | Double | 10 | Optional | Item weight

## Create Order (Pickup)

> Definition

```json
https://api.loginextsolutions.com/ShipmentApp/mile/v1/create
```

> Request Body

```json
[
  {
    "orderNo": "DummyOrderNo1",
    "awbNumber": "AWB001",
    "shipmentOrderTypeCd": "PICKUP",
    "orderState": "FORWARD",
    "shipmentOrderDt": "2016-07-15T10:30:00.000Z",
    "distributionCenter": "test",
    "packageWeight":"10",
    "packageVolume": "4500",
    "packageValue": "5000",
    "paymentType": "Prepaid",
    "numberOfItems": "1",
    "deliveryType":"DLBOY",
    "partialDeliveryAllowedFl": "Y",
    "returnAllowedFl": "Y",
    "cancellationAllowedFl": "N",
    "pickupBranch":"testbranch",
    "pickupServiceTime": "50",
    "pickupStartTimeWindow": "2016-07-16T14:24:00.000Z",
    "pickupEndTimeWindow": "2016-07-17T14:24:00.000Z",
    "pickupAccountCode": "Customer123",
    "pickupAccountName": "Customer001",
    "pickupEmail": "test@test.com",
    "pickupPhoneNumber": "9090909090",
    "pickupApartment": "123",
    "pickupStreetName": "Supreme Business Park",
    "pickupLandmark": "DMart",
    "pickupLocality": "Hiranandani",
    "pickupCity": "Mumbai",
    "pickupState": "MH",
    "pickupCountry": "IND",
    "pickupPinCode": "400076",
    "pickupLatitude":"19.116854",
    "pickupLongitude":"72.910455",
    "pickupNotes": "PickedUp",
    "deliverNotes": "Delivered"
    "shipmentCrateMappings": [
      {
        "crateCd": "CRATE001",
        "crateAmount":100.65,
        "crateType":"case",
        "noOfUnits":10,
        "shipmentlineitems": [
          {
            "itemCd": "CODE001",
            "itemName": "ITEM1",
            "itemPrice": 100,
            "itemQuantity": 2,
            "itemType": "TYPE1",
            "itemWeight": 10
          },
          {
            "itemCd": "CODE002",
            "itemName": "ITEM2",
            "itemPrice": 50,
            "itemQuantity": 3,
            "itemType": "TYPE2",
            "itemWeight": 10
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
  "message": "Order created successfully",
  "referenceId": [
    "dcd883efcccc4d2299da962a72b01f23"
  ],
  "hasError": false
}

```
Place a new pickup leg order with this API.

### Request

<span class="post">POST</span>`https://api.loginextsolutions.com/ShipmentApp/mile/v1/create`



### Request Parameters

Param | DataType | Length |  Required | Description
--------- | ------- | ------- | ---------- | ------------
orderNo | String | 100 | Mandatory |  Order No.
awbNumber | String | 1000 | Optional | Airway Bill No.
shipmentOrderTypeCd | String | 40 | Mandatory | Order type code. DELIVER for delivery leg order
orderState | String | 512 | Mandatory | State of order. Ex: FORWARD
shipmentOrderDt | Date |  | Mandatory | Order Date. Format - YYYY-MM-DDTHH:MM:SS.SSSZ e.g. : 2016-07-01T11:18:00.000Z.
distributionCenter | String | 255 | Mandatory | Distribution center's name
packageWeight | Double | 10 | Optional | Weight of package in Kg.
packageVolume | Double | 10 | Optional | Volume of package in CC
packageValue | Double | 10 | Optional | Value of package
paymentType | String | 40 | Mandatory | Payment mode. Ex: COD - Cash On Delivery, Prepaid
numberOfItems | Integer | 20 | Optional | Number of crates
deliveryType | String | 40 | Optional | Order delivery type. Ex: TRK - Truck, VAN - Van, DLBOY - Delivery Boy
partialDeliveryAllowedFl | String | 50 | Optional | Is Partial Delivery allowed. Ex: Y/N. Default value is N.
returnAllowedFl | String | 1 | Optional | Is Return allowed. Ex: Y/N. Default value is Y.
cancellationAllowedFl | String | 1 | Optional | Is Cancellation allowed. Ex: Y/N. Default value is Y.
pickupBranch | String | 255 | Mandatory | Name of pickup branch
pickupServiceTime | Integer | 11 | Mandatory | Pickup service time in mins.
pickupStartTimeWindow | Date |  | Mandatory | Pickup start time window. Format - YYYY-MM-DDTHH:MM:SS.SSSZ e.g. : 2016-07-01T11:18:00.000Z.
pickupEndTimeWindow | Date |  | Mandatory | Pickup end time window. Format - YYYY-MM-DDTHH:MM:SS.SSSZ e.g. : 2016-07-01T11:18:00.000Z.
pickupAccountCode | String | 255 | Mandatory | Pickup account code
pickupAccountName | String | 255 | Mandatory | Pickup account name
pickupEmail | String | 100 | Optional | Pickup email id
pickupPhoneNumber | String | 255 | Mandatory | Pickup phone no
pickupApartment | String | 512 | Mandatory | Pickup Apartment
pickupStreetName | String | 512 | Mandatory | Pickup Street name
pickupLandmark | String | 512 | Optional | Pickup Landmark
pickupLocality | String | 512 | Mandatory | Pickup Locality
pickupCity | String | 512 | Mandatory | Pickup City
pickupState| String | 512 | Mandatory | Pickup State. Please refer to the list of state codes provided in the "State Codes" section.
pickupCountry | String | 512 | Mandatory | Pickup Country. Please refer to the list of country codes provided in the "Country Codes" section.
pickupPinCode | String | 20 | Mandatory | Pickup Pincode
pickupLatitude | Double |  | Optional | Pickup address Latitude
pickupLongitude | Double |  | Optional | Pickup address Longitude
pickupNotes | String | 512 | Optional | Additional pickup comments associated with the order
deliverNotes | String | 512 | Optional | Additional delivery comments associated with the order


### Request Parameters (Crates)

Param | DataType | Length |  Required | Description
--------- | ------- | ------- | ---------- | ------------
shipmentCrateMappings | Array of objects |  | Optional | Shipment crates
shipmentCrateMappings.crateCd | String | 128 | Mandatory | CRATE001
shipmentCrateMappings.crateAmount | Double |  | Optional | Crate amount
shipmentCrateMappings.crateType | String | 100 | Optional | Type of crate. Ex: cake, juice, sweet, furniture etc.
shipmentCrateMappings.noOfUnits | Integer | 10 | Optional | No. of crate units
shipmentCrateMappings.shipmentlineitems.itemCd | String | 200 | Mandatory | Item code
shipmentCrateMappings.shipmentlineitems.itemName | String | 255 | Optional | Item name
shipmentCrateMappings.shipmentlineitems.itemPrice | Double |  | Mandatory | Item price
shipmentCrateMappings.shipmentlineitems.itemQuantity | Double | 10 | Mandatory | Item quantity
shipmentCrateMappings.shipmentlineitems.itemType | String | 100 | Optional | Item type
shipmentCrateMappings.shipmentlineitems.itemWeight | Double | 10 | Optional | Item weight





## Create Order (Pickup & Delivery)

> Definition

```json
https://api.loginextsolutions.com/ShipmentApp/mile/v1/create
```

> Request Body

```json
[
  {
    "orderNo": "DummyOrderNo13",
    "awbNumber": "AWB001",
    "shipmentOrderTypeCd": "BOTH",
    "orderState": "FORWARD",
    "shipmentOrderDt": "2016-07-15T10:30:00.000Z",
    "distributionCenter": "test",
    "packageWeight":"10",
    "packageVolume": "4500",
    "paymentType": "Prepaid",
    "packageValue": "5000",
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
    "deliverAccountCode": "Customer001",
    "deliverAccountName": "TestUser",
    "deliverApartment": "123",
    "deliverStreetName": "Powai",
    "deliverLandmark": "Dmart",
    "deliverLocality": "Hiranandani",
    "deliverCity": "Mumbai",
    "deliverState": "MH",
    "deliverCountry": "IND",
    "deliverPinCode": "400076",
    "deliverLatitude":"19.125497",
    "deliverLongitude":"72.836675",    
    "pickupBranch":"Gurgaon",
    "pickupServiceTime": "50",
    "pickupStartTimeWindow": "2016-07-16T14:24:00.000Z",
    "pickupEndTimeWindow": "2016-07-17T14:24:00.000Z",
    "pickupAccountCode": "Customer123",
    "pickupAccountName": "Customer001",
    "pickupApartment": "123",
    "pickupStreetName": "Supreme Business Park",
    "pickupLandmark": "DMart",
    "pickupLocality": "Hiranandani",
    "pickupCity": "Mumbai",
    "pickupState": "MH",
    "pickupCountry": "IND",
    "pickupPinCode": "400076",
    "pickupLatitude":"19.116854",
    "pickupLongitude":"72.910455",   
    "returnBranch": "test",
    "returnStartTimeWindow": "2016-05-18T03:00:00.000Z",
    "returnEndTimeWindow": "2016-05-18T16:00:00.000Z",
    "returnAccountCode": "retAcc123",
    "returnAccountName": "retAcc1234",
    "returnEmail": "test@test.com",
    "returnPhoneNumber": "9090909090",
    "returnApartment": "sjlkd CHS",
    "returnStreetName": "kljsdl Road",
    "returnLandmark": "skjdlk Nagar",
    "returnLocality": "kldlk West",
    "returnCity": "Mumbai",
    "returnState": "MH",
    "returnCountry": "IND",
    "returnPinCode": "400104",
    "deliverEmail":"z@z.zzz",
    "deliverPhoneNumber":"9876543210",
    "pickupEmail":"z@z.zzz",
    "pickupPhoneNumber":"9876543210",
    "pickupNotes": "PickedUp",
    "deliverNotes": "Delivered"
    "shipmentCrateMappings": [
      {
        "crateCd": "CRATE001",
        "crateAmount":100.65,
        "crateType":"case",
        "noOfUnits":10,
        "shipmentlineitems": [
          {
            "itemCd": "CODE001",
            "itemName": "ITEM1",
            "itemPrice": 100,
            "itemQuantity": 2,
            "itemType": "TYPE1",
            "itemWeight": 10
          },
          {
            "itemCd": "CODE002",
            "itemName": "ITEM2",
            "itemPrice": 50,
            "itemQuantity": 3,
            "itemType": "TYPE2",
            "itemWeight": 10
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
  "message": "Order created successfully",
  "referenceId": [
    "dcd883efcccc4d2299da962a72b01f23"
  ],
  "hasError": false
}

```
Place a new delivery leg order with this API.

### Request

<span class="post">POST</span>`https://api.loginextsolutions.com/ShipmentApp/mile/v1/create`


### Request Parameters

Param | DataType | Length |  Required | Description
--------- | ------- | ------- | ---------- | ------------
orderNo | String | 100 | Mandatory |  Order No.
awbNumber | String | 1000 | Optional | Airway Bill No.
shipmentOrderTypeCd | String | 40 | Mandatory | Order type code. BOTH for pickup & delivery leg order
orderState | String | 512 | Mandatory | State of order. Ex: FORWARD
shipmentOrderDt | Date |  | Mandatory | Order Date. Format - YYYY-MM-DDTHH:MM:SS.SSSZ e.g. : 2016-07-01T11:18:00.000Z.
distributionCenter | String | 255 | Mandatory | Distribution center's name
packageWeight | Double | 10 | Optional | Weight of package in Kg.
packageVolume | Double | 10 | Optional | Volume of package in CC
packageValue | Double | 10 | Optional | Value of package
numberOfItems | Integer | 20 | Optional | Number of crates
paymentType | String | 40 | Mandatory | Payment mode. Ex: COD - Cash On Delivery, Prepaid
partialDeliveryAllowedFl | String | 50 | Optional | Is Partial Delivery allowed. Ex: Y/N
returnAllowedFl | String | 1 | Optional | Is Return allowed. Ex: Y/N
cancellationAllowedFl | String | 1 | Optional | Is Cancellation allowed. Ex: Y/N
deliverBranch | String | 255 | Mandatory | Name of delivery branch
deliverServiceTime | Integer | 11 | Mandatory | Deliver service time in mins.
deliverStartTimeWindow | Date |  | Mandatory | Deliver start time window. Format - YYYY-MM-DDTHH:MM:SS.SSSZ e.g. : 2016-07-01T11:18:00.000Z.
deliverEndTimeWindow | Date |  | Mandatory | Deliver end time window. Format - YYYY-MM-DDTHH:MM:SS.SSSZ e.g. : 2016-07-01T11:18:00.000Z.
deliveryType | String | 40 | Optional | Order delivery type. Ex: TRK - Truck, VAN - Van, DLBOY - Delivery Boy
deliveryLocationType | String | 40 | Optional | Type of delivery location. Ex: CUSTOMER, PUP
deliverAccountCode | String | 255 | Mandatory | Deliver account code
deliverAccountName | String | 255 | Mandatory | Deliver account name
deliverApartment | String | 512 | Mandatory | Apartment
deliverStreetName | String | 512 | Mandatory | Street name
deliverLandmark | String | 512 | Optional | Landmark
deliverLocality | String | 512 | Mandatory | Locality
deliverCity | String | 512 | Mandatory | City
deliverState| String | 512 | Mandatory | State code
deliverCountry | String | 512 | Mandatory | Country code
deliverPinCode | String | 20 | Mandatory | Pincode
deliverLatitude | Double | 100 | Optional | Delivery address Latitude
deliverLongitude | Double | 100 | Optional | Delivery address Longitude
pickupBranch | String | 255 | Mandatory | Name of pickup branch
pickupServiceTime | Integer | 11 | Mandatory | Pickup service time in mins.
pickupStartTimeWindow | Date |  | Mandatory | Pickup start time window. Format - YYYY-MM-DDTHH:MM:SS.SSSZ e.g. : 2016-07-01T11:18:00.000Z.
pickupEndTimeWindow | Date |  | Mandatory | Pickup end time window. Format - YYYY-MM-DDTHH:MM:SS.SSSZ e.g. : 2016-07-01T11:18:00.000Z.
pickupAccountCode | String | 255 | Mandatory | Pickup account code
pickupAccountName | String | 255 | Mandatory | Pickup account name
pickupApartment | String | 512 | Mandatory | Pickup Apartment
pickupStreetName | String | 512 | Mandatory | Pickup Street name
pickupLandmark | String | 512 | Optional | Pickup Landmark
pickupLocality | String | 512 | Mandatory | Pickup Locality
pickupCity | String | 512 | Mandatory | Pickup City
pickupState| String | 512 | Mandatory | Pickup State code
pickupCountry | String | 512 | Mandatory | Pickup Country code
pickupPinCode | String | 20 | Mandatory | Pickup Pincode
pickupLatitude | Double |  | Optional | Pickup address Latitude
pickupLongitude | Double |  | Optional | Pickup address Longitude
returnBranch | String | 255 | Mandatory | Name of return branch
returnStartTimeWindow | Date |  | Mandatory | Return start time window. Format - YYYY-MM-DDTHH:MM:SS.SSSZ e.g. : 2016-07-01T11:18:00.000Z.
returnEndTimeWindow | Date |  | Mandatory | Return end time window. Format - YYYY-MM-DDTHH:MM:SS.SSSZ e.g. : 2016-07-01T11:18:00.000Z.
returnAccountCode | String | 255 | Mandatory | Return account code
returnAccountName | String | 255 | Mandatory | Return account name
returnEmail | String | 100 | Mandatory | Return account code
returnPhoneNumber | String | 255 | Mandatory | Return account name
returnApartment | String | 512 | Mandatory | Return Apartment
returnStreetName | String | 512 | Mandatory | Return Street name
returnLandmark | String | 512 | Optional | Return Landmark
returnLocality | String | 512 | Mandatory | Return Locality
returnCity | String | 512 | Mandatory | Return City
returnState| String | 512 | Mandatory | Return State code. Please refer to the list of state codes provided in the "State Codes" section.
returnCountry | String | 512 | Mandatory | Return Country code. Please refer to the list of country codes provided in the "Country Codes" section.
returnPinCode | String | 20 | Mandatory | Return Pincode
deliverEmail| String | 100 | Optional | Email of the customer
deliverPhoneNumber| String | 255 | Optional | Phone number of the customer
pickupEmail| String | 100 | Optional | Email of the merchant
pickupPhoneNumber| String | 255 | Optional | Phone number of the merchant
pickupNotes | String | 512 | Optional | Additional pickup comments associated with the order
deliverNotes | String | 512 | Optional | Additional delivery comments associated with the order



### Request Parameters (Crates)

Param | DataType | Length |  Required | Description
--------- | ------- | ------- | ---------- | ------------
shipmentCrateMappings | Array of objects |  | Optional | Shipment crates
shipmentCrateMappings.crateCd | String | 128 | Mandatory | CRATE001
shipmentCrateMappings.crateAmount | Double |  | Optional | Crate amount
shipmentCrateMappings.crateType | String | 100 | Optional | Type of crate. Ex: cake, juice, sweet, furniture etc.
shipmentCrateMappings.noOfUnits | Integer | 10 | Optional | No. of crate units
shipmentCrateMappings.shipmentlineitems.itemCd | String | 200 | Mandatory | Item code
shipmentCrateMappings.shipmentlineitems.itemName | String | 255 | Optional | Item name
shipmentCrateMappings.shipmentlineitems.itemPrice | Double |  | Mandatory | Item price
shipmentCrateMappings.shipmentlineitems.itemQuantity | Double | 10 | Mandatory | Item quantity
shipmentCrateMappings.shipmentlineitems.itemType | String | 100 | Optional | Item type
shipmentCrateMappings.shipmentlineitems.itemWeight | Double | 10 | Optional | Item weight

## Create Return Order

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


Place a new return order with this API.

### Request

<span class="post">POST</span>`https://api.loginextsolutions.com/ShipmentApp/mile/v1/create/return`

### Request Body

Parameter | DataType |  Required | Description
-----------|-------|------- | ----------
reference_ids | List | Mandatory | Reference Id associated with the order.

## Create Order Multi Stop

> Definition

```json
https://api.loginextsolutions.com/ShipmentApp/mile/v2/multidestination/create
```

> Request Body

```json
{
  "parentOrderNo": "GGLPAR98761234",
  "awbNumber": "AWB001",
  "shipmentOrderDt": "2016-07-15T10:30:00.000Z",
  "autoAllocateFl": "Y",
  "shipmentOrderTypeCd": "DELIVER",
  "orderState": "FORWARD",
  "deliverStartTimeWindow": "2016-07-16T10:31:00.000Z",
  "deliverEndTimeWindow": "2016-07-18T10:31:00.000Z",
  "deliveryType": "DLBOY",
  "shipmentBranch": "Gurgaon",
  "returnAllowedFl": "Y",
  "cancellationAllowedFl": "N",
  "returnBranch": "Gurgaon",
  "pickupNotes": "PickedUp",
  "optimiseOrderSequenceFl": "Y",
  "backToOrigin": "Y",
  "orders": [
    {
      "orderNo": "DEST1-98765123",
      "deliverySequence": 1,      
      "packageWeight": "10",
      "packageVolume": "4500",
      "paymentType": "Prepaid",
      "packageValue": "5000",
      "numberOfItems": "1",
      "deliverServiceTime": "20",
      "deliveryLocationType": "PUP",
      "partialDeliveryAllowedFl": "Y",
      "deliverAccountCode": "Customer001",
      "deliverAccountName": "Mathew Richardson",
      "deliverEmail": "m.richardson@testmail.com",
      "deliverPhoneNumber": "9891234567",
      "deliverApartment": "10 Suite No. A1901",
      "deliverStreetName": "Walton Avenue",
      "deliverLandmark": "Opp. Chiptole",
      "deliverLocality": "Down Towm Chicago",
      "deliverCity": "Chicago",
      "deliverState": "IL",
      "deliverCountry": "USA",
      "deliverPinCode": "72712",
      "deliverLatitude": "19.124497",
      "deliverLongitude": "72.893675",
      "deliverNotes": "Delivered",
      "shipmentCrateMappings": [
        {
          "crateCd": "CRATE001",
          "crateAmount": 100.65,
          "crateType": "case",
          "noOfUnits": 2,
          "shipmentlineitems": [
            {
              "itemCd": "CODE001",
              "itemName": "ITEM1",
              "itemPrice": 100,
              "itemQuantity": 2,
              "itemType": "TYPE1",
              "itemWeight": 10
            },
            {
              "itemCd": "CODE002",
              "itemName": "ITEM2",
              "itemPrice": 50,
              "itemQuantity": 3,
              "itemType": "TYPE2",
              "itemWeight": 10
            }
          ]
        }
      ]
    },  
  ]
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

With this API, you can add orders with Single Pickup and Multiple destination.
This API can also be used for Single Pick-up and Single Destinaton.


### Request

<span class="post">POST</span>`https://api.loginextsolutions.com/ShipmentApp/mile/v2/multidestination/create`


### Request Body

Parameter | DataType | Length |  Required | Description
-----------|-------| ------- |------- | ----------
parentOrderNo | String | 255 | Mandatory | This is the Order No.
awbNumber | String | 1000 | Optional | If you want a AWB no. to be associated with an order, you can pass the same here.
shipmentOrderDt | String | | Mandatory | The date and time on which the order is created.<br>Note that this date and time has to be in UTC.<br>Sample Value - "2017-07-15T10:30:00.000Z"
shipmentOrderTypeCd| String | 10 | Mandatory | The value in this field has to be "DELIVER" always.
orderState| String | 10 | Mandatory | If an order is a Forward way (Delivery to the Customer), then value here should be "FORWARD"<br>If an order is a Retrun way (Return from the Customer), then value here should be "REVERSE"
deliverStartTimeWindow| String | | Mandatory | This is the start date and time for the time slot of the Delivery.<br>Note that this date and time has to be greater than the Order Creation Date and Time.<br>Note that this date and time has to be in UTC.<br>Sample Value - "2017-07-15T11:30:00.000Z<br><br>If the you set the auto allocation flag  "autoAllocateFl" as "Y", then the Pick-up start Date and Time is also taken as the  same.<br>If the you set the auto allocation flag  "autoAllocateFl" as "N", then the Pick-up Date and Time is NOT set.
deliverEndTimeWindow| String | | Mandatory | This is the end date and time for the time slot of the Delivery.<br>Note that this date and time has to be greater than the Delivery Start Date and Time.<br>Note that this date and time has to be in UTC.<br>Sample Value - "2017-07-15T12:30:00.000Z"<br><br>If you set the auto allocation flag  "autoAllocateFl" as "Y", then the Pick-up end Date and Time is also taken as the  same.<br>If you set the auto allocation flag  "autoAllocateFl" as "N", then the Pick-up Date and Time is NOT set.
deliveryType| String | 40 | Mandatory | This Optional Field. You can choose to leave it blank.<br>In certain operations, there are different skill sets / special delivery requirements through which the Delivery has to take place.<br>For e.g. - Groceries / Food items has to be seperated with Toileteries<br>Orders for Cake cannot be clubbed with the Order for Flowers while delivering.<br><br>In such cases, if you want to classify the orders by using Delivery Type such that these orders get assigned to Delivery Mediums who are configured in LogiNext system with these special skill-sets or types, then you can use this field.<br>Please note that before you pass orders with certain Delivery Types, you will have to first configure the Delivery Types.<br>Please ask your Account Manager to set these values for you.
shipmentBranch| String | 255 | Mandatory | For Pick-Up type of orders, this is the Branch / Distribution Center / Hub to which the Delivery Medium will Deliver the order / shipment /parcel to.<br>For Delivery type of orders, this is the Branch / Distribution Center / Hub from where the Delivery Medium will pick-up the order / shipment / parcel and deliver it to the end customer.<br><br>Note that you will have to first Add your Operation Branch / Distribution Center / Hub either through the Add Branch API or through the Add Branch Screen.<br>If you have any access related issue while creating branch, please reach out to your Account Manager
returnAllowedFl| String | 1 | Optional | If your Business process allows the customer to return the orders back to you, then you will have to mark this Flag as  "Y". This way your OMS / WMS / ERP system(integrated with LogiNext system) or you Operations Manager will be able to create a return request for an order.<br>If you mark this flag as "N", LogiNext system will not allow you to create a return request referencing to this order.<br><br>You will always have any option to create a new order all-together for Returns by passing "REVERSE" in the "orderState" field.<br>If you have not set this Flag, it will be defaulted to "N"
cancellationAllowedFl| String | 1 | Optional | If your Business process allows the customer to cancel the orders before it is delivered to their doorstep, then you will have to mark this Flag as "Y". This way your OMS / WMS / ERP system(integrated with LogiNext system) or you Operations Manager will be able to cancel an order.<br>If you mark this flag as "N", LogiNext system will not allow you to cancel an order.<br><br>If you have not set this Flag, it will be defaulted to "N"
returnBranch| String | 255 | Conditional Mandatory | If the "returnAllowedFl" is marked as "Y", then this is mandatory.<br>Else this this optional and you can choose to leave it blank.<br>For Pick-Up type of orders, this is the Branch / Distribution Center / Hub to which the Delivery Medium will return the orders to. This is generally the Merchant's / Seller's Branch / Hub form where the shipment / parcel was picked up.<br>For Delivery type of orders, this is the Branch / Distribution Center / Hub where the Delivery Medium will have to bring back the shipment / parcel to.  <br>Note that you will have to first Add your Operation Branch / Distribution Center / Hub either through the Add Branch API or through the Add Branch Screen. <br>If you have any access related issue while creating branch, please reach out to your Account Manager
pickupNotes| String | 100 | Optional | You can enter instructions (if any) for the Delivery Associate while picking-up the order.
autoAllocateFl| String | 1 | Mandatory | Pass this Flag as "Y", if - If you add any order which needs to be allocated automatically to the logged-in Delivery Medium.<br>Pass this Flag as "N", if - If you add any order which you want to allocate manually to the Delivery Medium OR<br>If you want to run the Route optimization on the set of orders and want system to identify the Delivery Mediums.
optimiseOrderSequenceFl| String | 1 | Mandatory | This flag is to be used only if you have Multi- Destination Orders.<br>If you set this Flag as "N", system would plan the Delivery routes by keeping the sequence of the Orders same as what you have supplied.<br>If you set this Flag as "Y", system would optimize the route and re-arrange the sequence in which Order needs to be delivered.
backToOrigin| String | 1 | Mandatory | If you want the Pick-up Branch from where the Delivery Medium has picked-up the order / shipment / parcel to be the last Destination, then set this Flag as "Y" else set this flag as "N"
orders| List | | Mandatory | Array - This is the list of orders and its information.
orders.orderNo| String | 255 | Conditional Mandatory | This is the Order No.<br>In case of Single Destination, this Order No. is same as the Parent Order No. It is mandatory.<br>In case of Multi -Destination, this Order No. should not be same as the Parent Order No.<br>In this case, it is order no. for each destination.<br>If you do not have a separate order for each destination, you can leave it blank.<br>LogiNext will generate Order No. with the format - Parent_Order_No_1, Parent_Order_No_2, etc.
orders.deliverySequence| String | 1 | Mandatory | In case of Single Destination, this is to be "1" always.<br>In case of Multi-destination, this is the sequence that you want the order to be delivered in.
orders.packageWeight| String | 10 | Optional | This is an optional field. You can choose to leave it blank.<br>If you have any package weight that needs to be specified to the Delivery Associate, you can pass the value here as a FYI.<br>Also, LogiNext system allows you to configure the capacity (weight) of Delivery Medium. If particular capacity (weight) of an order is specified in this field, then the order will get assigned to the Delivery Associate whose capacity is greater than or equal to this capacity.
orders.packageVolume| String | 10 | Optional | This is an optional field. You can choose to leave it blank.<br>If you have any package volume that needs to be specified to the Delivery Associate, you can pass the value here as a FYI.<br>Also, LogiNext system allows you to configure the capacity (volume) of Delivery Medium. If particular capacity (volume) of an order is specified in this field, then the order will get assigned to the Delivery Associate whose capacity is greater than or equal to this capacity.<br>Note that volume here is overall cubic volume (L*B*H)
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
orders.deliverApartment| String | 512 | Conditional Mandatory | If you have the Customer Profiling set to allow the LogiNext to select the Address based on the Account Code passed, then this field is optional.<br>If you have the Lat. and Long of the Customer, then this fields is optional.<br><br>If you are passing the value in this field, then - <br>This is Address Line 1.<br>This is the Apartment Name / House Name / Building Name / Suite No.<br>Sample Value - A 901 Supreme Business Center
orders.deliverStreetName| String | 512 | Conditional Mandatory | If you have the Customer Profiling set to allow the LogiNext to select the Address based on the Account Code passed, then this field is optional.<br>If you have the Lat. and Long of the Customer, then this fields is optional.<br>If you are passing the value in this field, then - <br>This is Address Line 2.<br>This is the name of the Street where the Customer's / Delivery location is present.<br>Sample Value - Walton Boulevard
orders.deliverLandmark| String | 512 | Optional | Any nearby landmark to identify your Customer Address<br>Sample Value - Opp. McDonalds or Behind Mercy Hospital<br>Orders.deliverLocality| String | 255 | Conditional Mandatory | If you have the Customer Profiling set to allow the LogiNext to select the Address based on the Account Code passed, then this field is optional.<br>If you have the Lat. and Long of the Customer, then this fields is optional.<br>If you are passing the value in this field, then -<br>This is area or locality in which the is Customer's address is located<br>Sample Value - Southern Industry Park or Dubai Downtown<br>If you think that your specific region in which you operate does not have localities, then please raise the support request with your Account Manager to make this non-mandatory
orders.deliverCity| String | 512 | Conditional Mandatory | If you have the Customer Profiling set to allow the LogiNext to select the Address based on the Account Code passed, then this field is optional.<br>If you have the Lat. and Long of the Customer, then this fields is optional.<br>If you are passing the value in this field, then - <br>This is name of the city.<br>Sample Value - Atlanta or Kuala Lampur
orders.deliverState| String | 3 | Conditional Mandatory | If you have the Customer Profiling set to allow the LogiNext to select the Address based on the Account Code passed, then this field is optional.<br>If you have the Lat. and Long of the Customer, then this fields is optional.<br>If you are passing the value in this field, then - <br>This is code of State / Province.<br>Sample Value - For Georgia use GA ; For Jawa Barat use JB<br><br>Please refer to the section where we have listed down state codes for each country.<br>If you think that your specific region in which you operate does not have States / Provinces, then please raise the support request with your Account Manager to make this non-mandatory.
orders.deliverCountry| String | 3 | Conditional Mandatory | If you have the Customer Profiling set to allow the LogiNext to select the Address based on the Account Code passed, then this field is optional.<br>If you have the Lat. and Long of the Customer, then this fields is optional.<br>If you are passing the value in this field, then - <br>This is code of Country.<br>Sample Value - For India use IND; For China use CHN<br>Please refer to the section where we have listed down country codes.
orders.deliverPinCode| String | 255 | Conditional Mandatory | If you have the Customer Profiling set to allow the LogiNext to select the Address based n the Account code passed, then this field is optional<br>If you have the Lat. and Long of the Customer, then this fields is optional.<br>This is the postal code / zip code of the area.<br>Sample Value - 72712 ; 400076<br>If you think that your specific region in which you operate does not have postal codes, then please raise the support request with your Account Manager to make this non-mandatory.
orders.deliverLatitude| String |  | Conditional Mandatory | If you are passing the Customer Address, then this field is optional or <br>If you have the Customer Profiling set to allow the LogiNext to select the Address based on the Account Code passed, then this field is optional.
orders.deliverLongitude| String |  | Conditional Mandatory | If you are passing the Customer Address, then this field is optional or <br>If you have the Customer Profiling set to allow the LogiNext to select the Address based on the Account Code passed, then this field is optional.
orders.deliverNotes| String | 255 | Optional | You can enter instructions (if any) for the Delivery Associate while delivering the order.
shipmentCrateMappings| Array of objects | |  | Array - <br>Note that if your account is configured to have Order &  Crates Hierarchy or Order, Crates * Line Items Hierarchy, then it is mandatory for you pass the details of the Crates / Line Items in this field.


### Request Parameters (Crates)

Param | DataType | Length |  Required | Description
--------- | ------- | ------- | ---------- | ------------
crateCd | String | 128 | Mandatory | This is the unique Crate ID / Code
crateAmount | Double |  | Mandatory | This is the amount / value of the items in the Crate.<br>If you allow partial delivery, then this amount helps in recalculating the amount of the order.
crateType | String | 100 | Optional | This Optional Field. You can choose to leave it blank.
noOfUnits | Integer | 10 | Conditional Mandatory | If your account is configured to have  Order, Crates & Line Items Hierarchy, then it is mandatory for you pass the number of items and it should be equal to the number of Line Items in that Crate.
shipmentlineitems | Array of objects |  | Optional | Array - <br>Note that if your account is configured to have  Order, Crates & Line Items Hierarchy, then it is mandatory for you pass the details of the Crates / Line Items in this field.

### Request Parameters (LineItems)

Param | DataType | Length |  Required | Description
--------- | ------- | ------- | ---------- | ------------
itemCd | String | 200 | Mandatory | This is the unique Item Code
itemName | String | 255 | Mandatory | This is the Item Name
itemPrice | Double |  | Mandatory | This is the amount / value of the item.<br>If you allow partial delivery, then this amount helps in recalculating the amount of the order.
itemQuantity | Double | 10 | Optional | Quantity of the Items
itemType | String | 100 | Optional | Any description in addition to Item name that you want to pass. For e.g. - Discounted Item, etc.
itemWeight | Double | 10 | Optional | Weight of Item


## Get Order

> Definition

```json
https://api.loginextsolutions.com/ShipmentApp/mile/v1/shipment?end_date=2017-03-07+18:29:59&start_date=2016-02-01+18:30:00&status=ALL&order_no=TEST_ORDER
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
      "orderNo": "TEST_ORDER1",
      "awbNumber": "12345",
      "clientName": "KL Logistics",
      "branchName": "KL CENTER",
      "origin": "LK CENTER",
      "destination": "KL Valley, Mid Valley City,Kuala Lumpur",
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
      "tripName": "TRIP-3",
      "eta": 1485155640000,
      "actualStartDt": 1485154380000,
      "actualEndDt": 1485155021000,
      "plannedDistance": 16.708,
      "actualDistance": 6430.184,
      "distanceFromHub": null,
      "plannedStartDt": 1485154380000,
      "plannedEndDt": 1485155640000,
      "timeTakenDifferenceInMins": 10,
      "pickupCheckInTime": 1485154765000,
      "pickupCheckOutTime": 1485154887000,
      "pickupCheckInLatitude": 19.1117636,
      "pickupCheckInLongitude": 72.9093743,
      "pickupCheckOutLatitude": 19.1117636,
      "pickupCheckOutLongitude": 72.9093743,
      "deliverCheckInTime": 1485154905000,
      "deliverCheckOutTime": 1485155021000,
      "deliverCheckInLatitude": 19.1117636,
      "deliverCheckInLongitude": 72.9093743,
      "deliverCheckOutLatitude": 19.1117548,
      "deliverCheckOutLongitude": 72.909282,
      "orderSequence": 5,
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
      "customerPhoneNumber": "9988776655",
      "deliveryMediumPhoneNumber":"9977776644",
      "reason": null,
      "vehicleNumber": "MH 02 T 123",
      "noOfAttempts": 1,
      "deliveryGeofenceEnterTime": 1484727378000,
      "deliveryGeofenceExitTime": 1484727387000,
      "isDelayed": false,
      "delayedBy": null,
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
    },
    {
      "referenceId": "bf5b17d7f4a449a7a4612754899615a0",
      "orderNo": "TEST_ORDER2",
      "awbNumber": "",
      "clientName": "KL Logistics",
      "branchName": "KL CENTER",
      "origin": "KL, Adress",
      "destination": "SubangJaya_Mile",
      "shipmentOrderTypeCd": "PICKUP",
      "orderState": "FORWARD",
      "deliveryType": "TRK",
      "deliveryLocationType": null,
      "shipmentOrderDt": 1484618400000,
      "startTimeWindow": 1484791200000,
      "endTimeWindow": 1484827200000,
      "paymentType": "COD",
      "notes": "Order recieved successfully.Thanks",
      "packageValue": 0,
      "recalculatedValue": 0,
      "status": "DELIVERED",
      "plannedServiceTime": 0,
      "serviceTime": 0,
      "deliveryMediumName": "5T-ACOM2",
      "assignedThrough": "Manually",
      "tripName": "TRIP-8",
      "eta": 1484727307000,
      "actualStartDt": 1484727307000,
      "actualEndDt": 1484727397000,
      "plannedDistance": 7.55,
      "actualDistance": 6429.382,
      "distanceFromHub": 7.054,
      "plannedStartDt": 1484728567000,
      "plannedEndDt": 1484727307000,
      "timeTakenDifferenceInMins": 1,
      "pickupCheckInTime": 1484727378000,
      "pickupCheckOutTime": 1484727387000,
      "pickupCheckInLatitude": 19.1118447,
      "pickupCheckInLongitude": 72.909282,
      "pickupCheckOutLatitude": 19.1118447,
      "pickupCheckOutLongitude": 72.909282,
      "deliverCheckInTime": null,
      "deliverCheckOutTime": 1484727378000,
      "deliverCheckInLatitude": null,
      "deliverCheckInLongitude": null,
      "deliverCheckOutLatitude": 19.1118447,
      "deliverCheckOutLongitude": 72.909282,
      "orderSequence": 1,
      "customerCode": "Cha1",
      "customerName": "Jacob",
      "customerPhoneNumber": "9988776665",
      "deliveryMediumPhoneNumber":"9977775544",
      "reason": null,
      "vehicleNumber": "MH 02 T 153",
      "amountCollected": null,
      "podCount": null,
      "noOfCrates": 1,
      "packageWeight": 0,
      "packageVolume": 0,
      "customerComments": "",
      "deliveryNotes": "",
      "customerRatings": 5,
      "noOfAttempts": 1,
      "deliveryGeofenceEnterTime": 1484727378000,
      "deliveryGeofenceExitTime": 1484727378000,
      "isDelayed": false,
      "delayedBy": null,
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
          "orderNo": "ODT012",
          "crateQuantity": null,
          "amountToCollect": 0,
        }
      ]
    }
  ],
  "hasError": false
}

```
With this API you can fetch the list of your orders and the associated order information.

### Request

<span class="post">GET</span>`https://api.loginextsolutions.com/ShipmentApp/mile/v1/shipment`


### Request Parameters

Param | DataType | Length |  Required | Description
--------- | ------- | ------- | ---------- | ------------
start_date | Date |  | Conditional Mandatory |  If order_no is not passed in the request,then this field is mandatory.Range of date from which orders can be searched.<BR>Format 'yyyy-MM-dd HH:mm:ss'
end_date | Date |  | Conditional Mandatory |  If order_no is not passed in the request,then this field is mandatory.Range of date upto which orders can be searched.<BR>Format 'yyyy-MM-dd HH:mm:ss'
status | String | 20 | Optional |  If order_no is passed in the request,then status will not be considered for filtering the orders.Order status. <BR>Ex: NOTDISPATCHED,INTRANSIT,COMPLETED,<BR>NOTCOMPLETED,PICKEDUP(Only for First Mile),CANCELLED
order_no | String | 100 | Optional | Order Number(Only one order number can be passed at a time.If not passed ,all the orders for the specified date range will be fetched)

Status | Filter applied on orders
--------- | -------
NOTDISPATCHED | Orders will be fetched for which either the Order Start Date & Time Window or the Order End Date & Time Window lies within the range specified.
INTRANSIT | Orders will be fetched for which the Actual Delivery Start Date & Time lies within the range specified.
COMPLETED | For First Mile, an order is marked COMPLETED when it is PICKEDUP and DELIVERED at the hub. For Last Mile, an order is marked COMPLETED once it is DELIVERED to the end customer.<BR>Orders will be fetched for which the Actual Delivery End Date & Time lies within the range specified.
NOTCOMPLETED | For First Mile, when the order is  NOTPICKEDUP,it is marked as NOTCOMPLETED. For Last Mile, when the order is PICKEDUP but  NOTDELIVERED, it is marked as NOTCOMPLETED. <BR>Orders will be fetched for which the Actual Delivery End Date & Time lies within the range specified.
CANCELLED | Orders will be fetched for which the Cancellation Date & Time lies within the range specified.
ALL | Superset of all the filters mentioned for the above statuses will be considered.

## Update Order

> Definition

```json
https://api.loginextsolutions.com/ShipmentApp/mile/v1/update
```

> Request Body

```json
[
  {
    "referenceId":"04c1c0c283a34769a5baca01c987b51a",
    "orderNo": "DummyOrderNo13",
    "awbNumber": "AWB001",
    "shipmentOrderDt": "2016-07-15T10:30:00.000Z",
    "packageWeight":"10",
    "packageVolume": "4500",
    "paymentType": "Prepaid",
    "packageValue": "5000",
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
    "deliverAccountCode": "Customer001",
    "deliverAccountName": "TestUser",
    "deliverApartment": "123",
    "deliverStreetName": "Powai",
    "deliverLandmark": "Dmart",
    "deliverLocality": "Hiranandani",
    "deliverCity": "Mumbai",
    "deliverState": "MH",
    "deliverCountry": "IND",
    "deliverPinCode": "400076",    
    "pickupBranch":"Gurgaon",
    "pickupServiceTime": "50",
    "pickupStartTimeWindow": "2016-07-16T14:24:00.000Z",
    "pickupEndTimeWindow": "2016-07-17T14:24:00.000Z",
    "pickupAccountCode": "Customer123",
    "pickupAccountName": "Customer001",
    "pickupApartment": "123",
    "pickupStreetName": "Supreme Business Park",
    "pickupLandmark": "DMart",
    "pickupLocality": "Hiranandani",
    "pickupCity": "Mumbai",
    "pickupState": "MH",
    "pickupCountry": "IND",
    "pickupPinCode": "400076",    
    "returnBranch": "test",
    "returnStartTimeWindow": "2016-05-18T03:00:00.000Z",
    "returnEndTimeWindow": "2016-05-18T16:00:00.000Z",
    "returnAccountCode": "retAcc123",
    "returnAccountName": "retAcc1234",
    "returnEmail": "test@test.com",
    "returnPhoneNumber": "9090909090",
    "returnApartment": "sjlkd CHS",
    "returnStreetName": "kljsdl Road",
    "returnLandmark": "skjdlk Nagar",
    "returnLocality": "kldlk West",
    "returnCity": "Mumbai",
    "returnState": "MH",
    "returnCountry": "IND",
    "returnPinCode": "400104"
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
With this API, you will be able to update the order information unless and until that order is not dispatched and not associated with any Trip.
You can pass multiple order reference IDs and can update one or more parameters.

### Request

<span class="post">POST</span>`https://api.loginextsolutions.com/ShipmentApp/mile/v1/update`


### Request Parameters

Param | DataType | Length |  Required | Description
--------- | ------- | ------- | ---------- | ------------
referenceId | String | 32 | Mandatory |  Order Reference id
orderNo | String | 100 | Optional |  Order No.
awbNumber | String | 1000 | Optional | Airway Bill No.
shipmentOrderDt | Date | | Optional | Order Date. Format - YYYY-MM-DDTHH:MM:SS.SSSZ e.g. : 2016-07-01T11:18:00.000Z.
packageWeight | Double | 10 | Optional | Weight of package in Kg.
packageVolume | Double | 10 | Optional | Volume of package in CC
packageValue | Double | 10 | Optional | Value of package
numberOfItems | Integer | 20 | Optional | Number of crates
paymentType | String | 40 | Optional | Payment mode. Ex: COD - Cash On Delivery, Prepaid
partialDeliveryAllowedFl | String | 50 | Optional | Is Partial Delivery allowed. Ex: Y/N
returnAllowedFl | String | 1 | Optional | Is Return allowed. Ex: Y/N
cancellationAllowedFl | String | 1 | Optional | Is Cancellation allowed. Ex: Y/N
deliverBranch | String | 255 | Optional | Name of delivery branch
deliverServiceTime | Integer | 11 | Optional | Deliver service time in mins.
deliverStartTimeWindow | Date | | Optional | Deliver start time window. Format - YYYY-MM-DDTHH:MM:SS.SSSZ e.g. : 2016-07-01T11:18:00.000Z.
deliverEndTimeWindow | Date | | Optional | Deliver end time window. Format - YYYY-MM-DDTHH:MM:SS.SSSZ e.g. : 2016-07-01T11:18:00.000Z.
deliveryType | String | 40 | Optional | Order delivery type. Ex: TRK - Truck, VAN - Van, DLBOY - Delivery Boy
deliveryLocationType | String | 40 | Optional | Type of delivery location. Ex: CUSTOMER, PUP
deliverAccountCode | String | 255 | Optional | Deliver account code
deliverAccountName | String| 255  | Optional | Deliver account name
deliverApartment | String | 512 | Optional | Apartment
deliverStreetName | String | 512 | Optional | Street name
deliverLandmark | String | 512 | Optional | Landmark
deliverLocality | String | 512 | Optional | Locality
deliverCity | String | 512 | Optional | City
deliverState| String | 512 | Optional | State code
deliverCountry | String | 512 | Optional | Country code
deliverPinCode | String | 20 | Optional | Pincode
pickupBranch | String | 255 | Optional | Name of pickup branch
pickupServiceTime | Integer | 11 | Optional | Pickup service time in mins.
pickupStartTimeWindow | Date | | Optional | Pickup start time window. Format - YYYY-MM-DDTHH:MM:SS.SSSZ e.g. : 2016-07-01T11:18:00.000Z.
pickupEndTimeWindow | Date | | Optional | Pickup end time window. Format - YYYY-MM-DDTHH:MM:SS.SSSZ e.g. : 2016-07-01T11:18:00.000Z.
pickupAccountCode | String | 255 | Optional | Pickup account code
pickupAccountName | String | 255 | Optional | Pickup account name
pickupApartment | String | 512 | Optional | Pickup Apartment
pickupStreetName | String | 512 | Optional | Pickup Street name
pickupLandmark | String | 512 | Optional | Pickup Landmark
pickupLocality | String | 512 | Optional | Pickup Locality
pickupCity | String | 512 | Optional | Pickup City
pickupState| String | 512 | Optional | Pickup State code. Please refer to the list of state codes provided in the "State Codes" section.
pickupCountry | String | 512 | Optional | Pickup Country code. Please refer to the list of country codes provided in the "Country Codes" section.
pickupPinCode | String | 20 | Optional | Pickup Pincode
returnBranch | String | 255 | Optional | Name of return branch
returnStartTimeWindow | Date | | Optional | Return start time window. Format - YYYY-MM-DDTHH:MM:SS.SSSZ e.g. : 2016-07-01T11:18:00.000Z.
returnEndTimeWindow | Date | | Optional | Return end time window. Format - YYYY-MM-DDTHH:MM:SS.SSSZ e.g. : 2016-07-01T11:18:00.000Z.
returnAccountCode | String | 255 | Optional | Return account code
returnAccountName | String | 255 | Optional | Return account name
returnEmail | String | 500 | Optional | Return account code
returnPhoneNumber | String | 255 | Optional | Return account name
returnApartment | String | 512 | Optional | Return Apartment
returnStreetName | String | 512 | Optional | Return Street name
returnLandmark | String | 512 | Optional | Return Landmark
returnLocality | String | 512 | Optional | Return Locality
returnCity | String | 512 | Optional | Return City
returnState| String | 512 | Optional | Return State code. Please refer to the list of state codes provided in the "State Codes" section.
returnCountry | String | 512 | Optional | Return Country code. Please refer to the list of country codes provided in the "Country Codes" section.
returnPinCode | String | 20 | Optional | Return Pincode

## Update Order Status

> Definition

```json
https://api.loginextsolutions.com/ShipmentApp/mile/v1/update/status
```

> Request Body

```json
{
  "newStatus":"CANCELLED",
  "orderDetails":
  [{
    "orderReferenceId":"6186d5fc6e324c42abb5ea1a32e05f66",
    "reasonCd":"DBUNAVAILABLE"
  },
  {
    "orderReferenceId":"6186d7r5te324c42abb5ea1a32x45f66",
    "reasonCd":"DBUNAVAILABLE"
  },
  {
    "orderReferenceId":"6156ty46e324c42abb5ea1a32y45f66",
    "reasonCd":"OTHER",
    "otherReason":"Technical Issues"

  }]

}
```



> Response

```json
{
  "status": 200,
  "message": "Shipment updated successfully",
  "hasError": false
}

```
With this API, you will be able to update the order information unless and until that order is not dispatched and not associated with any Trip.
You can pass multiple order reference IDs and can update one or more parameters.

### Request

<span class="post">PUT</span>`https://api.loginextsolutions.com/ShipmentApp/mile/v1/update/status


### Request Parameters

Param | DataType | Length |  Required | Description
--------- | ------- | ---------- | ---------- | ------------
newStatus | String | 20 | Mandatory |  One status for multiple orders.The orders will be updated with this new status
orderReferenceId | String | 100 | Mandatory |  LogiNext provided order/shipment referenceId
reasonCd | String | 255 | Conditional Mandatory | Can pass only set values or any value can be sent as OTHER.Mandatory depending upon the status selected : NOTDELIVERED, NOTPICKEDUP, CANCELLED
otherReason | Date |  | Conditional Mandatory | Mandatory when reasonCd is OTHER

## Update Crates and Line Items in Order

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
With this API, you will be able to update the crate and line items information for one order at a time until that order is not dispatched and not associated with any Trip.
You can pass multiple crate and line items.

### Request

<span class="post">POST</span>`https://api.loginextsolutions.com/ShipmentApp/mile/v1/updateCrates`

### Request Parameters (Crates)

Param | DataType | Length |  Required | Description
--------- | ------- | ------- | ---------- | ------------
shipmentCrates | Array of objects | | Optional | Shipment crates
shipmentCrates.crateCd | String | 128 | Mandatory | Crate Code
shipmentCrates.crateAmount | Double | | Optional | Crate amount
shipmentCrates.crateType | String | 100 | Optional | Type of crate. Ex: cake, juice, sweet, furniture etc.
shipmentCrates.noOfUnits | Integer | 10 | Optional | No. of crate units
shipmentCrates.shipmentlineitems.itemCd | String | 200 | Mandatory | Item code
shipmentCrates.shipmentlineitems.itemName | String | 255 | Optional | Item name
shipmentCrates.shipmentlineitems.itemPrice | Double | | Mandatory | Item price
shipmentCrates.shipmentlineitems.itemQuantity | Double | 10 | Mandatory | Item quantity
shipmentCrates.shipmentlineitems.itemType | String | 100 | Optional | Item type
shipmentCrates.shipmentlineitems.itemWeight | Double | 10 | Optional | Item weight



## Cancel Order

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

> Response

```json
{
  "status": 200,
  "message": "success",
  "hasError": false
}
```

Use this API to cancel an order.

### Request

<span class="post">PUT</span>`https://api.loginextsolutions.com/ShipmentApp/mile/v1/cancel`

### Request Body

Parameter | DataType |  Required | Description
-----------|-------|------- | ----------
reference_ids | List  | Mandatory | Reference Id associated with the order.

## Get Status of Order

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

### Request

<span class="post">POST</span>`https://api.loginextsolutions.com/ShipmentApp/mile/v1/status`

### Request Body

Parameter | DataType |  Required | Description
-----------|-------|------- | ----------
reference_ids | List | Mandatory | Reference Id associated with the order.

## Download EPOD

This endpoint downloads the EPODs for given order, delivery dates and status of order. The response is in form of a zip file. NOTE: The dates accepted are in UTC.

### Request

<span class="post">GET</span>`http://api.loginextsolutions.com/ShipmentApp/shipment/fmlm/epod/list?orderstartdt=2015-06-16 00:00:00&orderenddt=2016-06-16 00:30:00&deliverystartdt=2015-06-15 00:00:00&deliveryenddt=2016-06-15 00:00:00&status=NOTDISPATCHED`

### Request Parameters

Parameter | DataType | Length |  Required | Description
-----------|-------|------- |------- | ----------
orderstartdt | String |  | Mandatory | Order start date
orderenddt | String |  | Mandatory | Order end date
deliverystartdt | String |  | Mandatory | Delivery start date
deliveryenddt | String |  | Mandatory | Delivery end date
status | String | 20 | Optional | Order status. <BR>Ex: NOTDISPATCHED,INTRANSIT,DELIVERED,<BR>NOTDELIVERED,PICKEDUP,NOTPICKEDUP,CANCELLED

### Response

Response is a binary zip file.<br>
In any browser just hit the url and zip file download will start automatically.<br>
In tools like POSTMAN instead of clicking 'Send' button click on 'Send & Download' button, which will save the zip file.

## Start Trip

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
Start the trip for a delivery medium using this API.

### Request

<span class="post">POST</span>`https://api.loginextsolutions.com/TripApp/mile/v1/trip/start`

### Request Body

Parameter | DataType |  Required | Description
-----------|-------|------- | ----------
reference_ids | List | Mandatory | Reference Id associated with the trip.

## Stop Trip

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
Stop the trip for a delivery medium using this API.

### Request

<span class="post">POST</span>`https://api.loginextsolutions.com/TripApp/mile/v1/trip/stop`

### Request Body

Parameter | DataType | Length |  Required | Description
-----------|-------|-------|------- | ----------
tripReferenceId | String  | 32 | Mandatory | Reference Id associated with the trip.
notDispatchedOrders | List  |  | Mandatory | Reference Id associated with the non-dispatched order.
deliveredOrders | List |  | Mandatory | Reference Id associated with the delivered order.

## Track Last Location

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
Use this to find out last tracked location for any order/ delivery medium.

### Request

<span class="post">GET</span>`https://api.loginextsolutions.com/TrackingApp/mile/v1/track/lastlocation`

## Create Delivery Medium

> Create Delivery Medium - Sample Request

```json
[
  {
    "employeeId": "1001",
    "userGroupName": "lastmile",
    "branchName": "LMDMumbai",
    "deliveryMediumMasterName": "Amit",
    "phoneNumber": "63865471261",
    "imei": "123456789012645",
    "emailId": "test@test.com",
    "userName": "test003",
    "password": "admin",
    "capacityInUnits": 10,
    "capacityInVolume": 0,
    "capacityInWeight": 0,
    "dob": "2016-12-12",
    "gender": "Male",
    "deliveryMediumMasterTypeCd": "Delivery Boy",
    "isOwnVehicleFl": "Company",
    "vehicleNumber": "MH034506",
    "weeklyOffList": [
      "Thursday",
      "Monday"
    ],
    "maxDistance": 100,
    "licenseValidity": "2016-12-13",
    "deliveryMediumMapList": [
      {
        "name": "HINDI"

      },
      {
        "name": "ENGLISH"

      }
    ],
    "shiftList": [
      {
        "shiftStartTime": "2016-12-12T13:30:00Z",
        "shiftEndTime": "2016-12-12T14:30:00Z"
      }
    ],
    "dmPreference": "400001"
  }
]
```

> Create Delivery Medium - Sample Response

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

This endpoint creates a new delivery medium.

### Request

<span class="post">POST</span>`http://api.loginextsolutions.com/DeliveryMediumApp/mile/v1/create`


### Request Parameters

Parameter | DataType | Length |  Required | Description
-----------|-------|------- |------- | ----------
employeeId | String | 50 | Mandatory | Employee Id
userGroupName | String | 255 | Mandatory | User group name
branchName | String | 255 | Mandatory | Client branch name
deliveryMediumMasterName | String | 255 |Mandatory | Full name of Delivery medium
phoneNumber | String | 255 | Mandatory | Mobile no
imei | String | 40 |Optional | IMEI no
emailId | String | 100 | Optional | Email id
userName | String | 255 | Mandatory | Username
password | String | 255 | Mandatory | Password
capacityInUnits | Integer | 20 | Mandatory | Capacity of Delivery medium in units
capacityInVolume | Integer | 20 | Optional | Capacity of Delivery medium in volume
capacityInWeight | Integer | 20 |Optional | Capacity of Delivery medium in weight
dob | String |  | Optional | Date of birth
gender | String | 12 |Optional | Gender. Ex - Male,Female
deliveryMediumMasterTypeCd | String | 255 |Optional | Delivery medium type. Ex - Truck, Delivery Boy
isOwnVehicleFl | String | 1 |Optional | Owner of vehicle. Ex - Owned, Company
vehicleNumber | String | 255 | Optional | Vehicle number to be assigned to the delivery medium
weeklyOffList  | String | 255 |Optional | Array of week's off days. Ex - Monday, Tuesday etc.
maxDistance | Integer | 20 |Optional | Max. allowed distance
licenseValidity | String |  |Optional | License validity date
deliveryMediumMapList.name | String | 255 | Optional | Name of language
shiftList.shiftStartTime  | String |  |Optional | Shift start time
shiftList.shiftEndTime  | String |  |Optional | Shift end time
dmPreference  | String | 255 | Optional | Preferred Pincode of Delivery medium

## Get Geocode

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

### Request

<span class="post">POST</span>`http://api.loginextsolutions.com/CommonApp/mile/v1/geocode`


### Request Parameters

Parameter | DataType |  Required | Description
-----------|-------|------- | ----------
apartment | String | Optional | Apartment
streetName | String | Optional | Street name
landmark | String | Optional | Landmark
locality | String | Optional | Locality
city | String | Optional | City
country | String | Optional | Country
state | String |Optional | State
pincode | String | Mandatory | Pincode

## iFrame

> Definition

```json
https://api.loginextsolutions.com/track/#/order?ordno=1234&aid=4b41a94b-521b-4986-920d-6e4c1cf15fd0b6&key=$2a$08$dfVg6jJLhrHEsqOUfD1EJHyuelHeIgcUyvgTfGaeRmnzN5jGVi86k
```

The iFrame displays the last tracking for an order, including current location, based on the order no.

### Request


<span class="post">GET</span>` https://api.loginextsolutions.com/track/#/order?ordno=<ordno>&aid=<aid>&key=<key>`

### Request Parameters

Parameter | Sample Value | Description
--------- | ------- | -------------
aid | f522631c-490c-46fd-9f79-ca8d14a704d7 | Value of authentication token without 'BASIC' keyword
key | $2a$08$Vg6jJLhrHEsqOUfD1EJHyuelHeIgcUyvgT | Client Secret Key
ordno | 1234| Order no

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

### Request

<span class="post">POST</span>`https://api.loginextsolutions.com/TripApp/deliveryplanner/v1/plan`


### Request Body

Parameter | DataType | Length |  Required | Description
-----------|-------|------- |------- | ----------
routeName | String | 150 | Mandatory | Route name
startLocation.latitude | Double | 20 | Mandatory | Latitude of start location
startLocation.longitude | Double | 20 | Mandatory | Longitude of start location
vehicles | List |  | Mandatory | List of delivery medium
vehicles.name | String | 255 | Mandatory | Delivery medium name
vehicles.capacity.weight | Integer | 20 | Optional | Capacity of delivery medium
vehicles.capacity.volume | Integer | 20 | Optional | Volume of delivery medium
vehicles.type | List |  | Optional | Type of delivery medium
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


## Create / Update Manifest

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

With this API you can create Manifests for your shipments.​ ​The Scan status​ ​of an order​ ​will get updated to
"​Out-scanned"​ ​if the Manifest is created successfully.​

​You will have to pass the LogiNext​ ​Order Reference ID in this API.
LogiNext Reference ID is generated when you add order in the LogiNext system.
If you do not store the Reference ID for orders, then you will have to fetch the same through the Get Order API.

You can also manifest Cancelled Orders (by turning this flag to "true") in case you have to return (out-scan) the cancelled orders back to the merchant / origin.

If you pass the manifestId, there would be a check if that Manifest ID exists in LogiNext application.
If it exists, then the orders (through order reference ID) will be updated in the LogiNext application.
If it does not exist, then a new manifest will be created with the provided Manifest ID.


### Request

<span class="post">POST</span>`https://api.loginextsolutions.com/ShipmentApp/mile/v1/scan/manifest/addshipment`


### Request Body

Parameter | DataType | Length |  Required | Description
-----------|-------| ------- |------- | ----------
manifestId | String | 11 | Optional | You can pass the Manifest ID as one of the Request parameters​ ​if your system​ ​generates such​ ​ID. If Not​ ​passed, then LogiNext​ ​will create the Manifest ID. This Manifest ID will also be passed as one of the response parameters. You can store the same for any future reference.
manifestType | String | 25 | Optional | Default manifestType is ORDER
cancelledOrderAllowedFl | String | 1 | Optional | By default the value will be taken as  "false". If you would like to OutScan Cancelled orders, then please pass "true"
orderReferenceIds | List |  | Mandatory | LogiNext Order Reference ID

## Create Hub

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
"adminContactName":"Suraj K.",
"mobileNumber":"9033977123",
"emailAddress":"superjames@gmails.com",
"longitude": 19.111755,
"latitude": 72.9095327
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

With this API, you can create your hubs / branches / distribution centers in the LogiNext application.

### Request

<span class="post">POST</span>`https://api.loginextsolutions.com/ClientApp/v1/branch/create`


### Request Body

Parameter | DataType | Length |  Required | Description
-----------|-------| ------- |------- | ----------
clientParentBranchName | String | 255 | Mandatory | This is name of the Parent Branch under which you want to create the new branch.<br>Please note that you cannot crate the Main Parent branch for your account through this API.<br>The Main Parent Branch gets created automatically when your account is configured in LogiNext system.<br>If you want to know the name of the Main Parent Branch Name, please get in touch with your assigned Account Manager
branchName | String | 255 | Mandatory | This is the name of the branch / hub / distribution center/ that you want to add.
Address.apartment | String | 512 | Mandatory | This is Address Line 1. This is the Apartment Name / House Name / Building Name / Suite No.<br>Sample Value - A 901 Suprement Business Center
Address.streetName | String | 512 | Mandatory | This is Address Line 2.This is the name of the Street where the Hub is situated.<br>Sample Value - Off Highway I96 or Walton Boulevard
Address.landmark | String | 512 | Mandatory | Any nearby landmark to identify your Hub quickly.<br>Sample Value - Opp. McDonalds or Behind Mercy Hospital
branchName | String | 255 | Optional | Any nearby landmark to identify your Hub quickly.<br>Sample Value - Opp. McDonalds or Behind Mercy Hospital
Address.locality | String | 512 | Mandatory | This is area in which the Hub is located<br>Sample Value - Southern Industry Park or Dubai Downtown<br><br>If you think that your specific region in which you operate does not have localities, then please raise the support request with your Account Manager to make this non-mandatory
Address.city | String | 512 | Mandatory | This is name of the city in which your Hub is situated<br>Sample Value - Atlanta or Kuala Lampur
Address.stateShortCode | String | 11 | Mandatory | This is code of State / Province.<br>Sample Value - For Georgia use GA ; For Jawa Barat use JB<br><br>Please refer to the section where we have listed down state codes for each country.<br>If you think that your specific region in which you operate does not have States / Provinces, then please raise the support request with your Account Manager to make this non-mandatory.
Address.countryShortCode | String | 11 | Mandatory | This is code of Country.<br>Sample Value - For India use IND; For China use CHN<br><br>Please refer to the section where we have listed down country codes.
Address.pincode | String | 20 | Mandatory | This is the postal code / zip code of the area in which your Hub is situated<br>Sample Value - 72712 ; 400076<br><br>If you think that your specific region in which you operate does not have postal codes, then please raise the support request with your Account Manager to make this non-mandatory.
division | String | 255 | Mandatory | Ex. ADIV
isOwnBranchFl | String | 1 | Mandatory | There can be two values here -  In Mile Hardcode this to N
isHubFl | String | 1 | Mandatory | There can be two values here -  In Mile Hardcode this to Y
geoFenceRadius | String | 255 | Optional | This is the radius in KMs that you have to enter if you want to create a geofence for your hub.<br>If no value is passed, then the default value of 2 Kms is taken.<br>Ideally a geofence radius should range between - 200 meters to 2 KMs
branchDescription | String | 500 | Optional | If you would like add a brief description name for the hub, use this field.
billingContactName | String | 500 | Mandatory | Name of the Contact Person at this Branch / Hub
officeNumber | String | 255 | Mandatory | Fixed Line Number of the Branch  / Hub
adminContactName | String | 255 | Mandatory | Name of the Supervisor / Alternate Contact for this Hub
mobileNumber | String | 255 | Mandatory | Mobile Phone No. of the contact person
emailAddress | String | 255 | Mandatory | Email Address of the contact person



# LogiNext OnDemand <sup>TM</sup>


## Create Order (Fixed Pickup)

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
    "locality" : "Andheri East",
    "subLocality" : "JVLR",
    "address" : "JVLR Powai",
    "deliverPhoneNumber" : "8888889999",
    "orderNo" : "ORder_18620161809",
    "distributionCenter" : "Mumbai",
    "paymentType" : "COD"
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

### Request

<span class="post">POST</span>`https://api.loginextsolutions.com/ShipmentApp/ondemand/v1/create`

### Request Parameters

Param | DataType |  Length | Required | Description
--------- | ------- | -------|------- | ------------
orderNo | String | 100 | Mandatory |  Order No.
distributionCenter | String | 255 | Mandatory | Distribution center's name
paymentType | String | 40 | Mandatory | Payment mode. Ex: COD, Prepaid
packageValue | Double | 10 | Optional | Package Value (This will be used when paymentType is Prepaid)
cashOnDelivery | Double | 10 | Mandatory(if paymentType is COD) | Cash to be collected on delivery
cashOnPickup | Double | 10 | Optional | Cash to be given on pickup
locality | String | 512 | Mandatory | Locality name
subLocality | String | 512 | Mandatory | Sub-locality name
address | String | 512 | Optional | Address where delivery should be done
deliverPhoneNumber | String | 255 | Mandatory | End customer contact number
customerName | String | 255 | Mandatory | End customer name



## Create Order (Variable Pickup)

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
    "deliverCapacityInWeight":15.2
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

### Request

<span class="post">POST</span>`https://api.loginextsolutions.com/ShipmentApp/ondemand/v1/create`

### Request Parameters

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


## Get Order

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

### Request

<span class="post">PUT</span>` https://api.loginextsolutions.com/ShipmentApp/ondemand/v1/shipment?end_date=2017-03-07+18:29:59&start_date=2016-02-01+18:30:00&status=ALL&order_no=LN01234567`

### Request Body

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


## Cancel Order

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

### Request

<span class="post">PUT</span>`https://api.loginextsolutions.com/ShipmentApp/ondemand/v1/cancel`

### Request Body

Parameter | DataType |  Required | Description
-----------|-------|------- | ----------
reference_ids | List  | Mandatory | Reference Id associated with the order.


# Webhooks

Webhooks allow you to build or set up integrations which subscribe to certain events like Order Creation, Route Planning, Trip Start, etc. on LogiNext System. When one of those events is triggered, we'll send a HTTP POST request to the webhook's configured URL (end point).

Note -

1. LogiNext Webhooks are sent via HTTP REST protocol.
2. The default content type for all the LogiNext Webhooks is "application/ json".
3. If you have a request to support the other content types like "application/xml " or "application/x-www-form-urlencoded", then please get in touch with your assigned CSA (Customer Service Associate) and request the same.
4. All the dates and timestamps that are represented in the Webhooks are in the UTC timezones.
5. Please share the end-point on your system to consume the Webhooks with your assigned CSAs.

## Create Order

> Response

```json
{
  "orderNo": "TestOrder",
  "orderState":"FORWARD",
  "orderLeg":"PICKUP",
  "awbNumber":"AWB001",
  "notificationType": "ORDERCREATIONNOTIFICATION",
  "timestamp":"2016-07-01 03:05:08",
  "orderReferenceId":"3daeaf418c59421319b1307e632b327da"
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
orderReferenceId | String | Order reference id.

## Update Order

> Response

```json
{
  "orderNo": "P_Aetos1",
	"notificationType": "ORDERUPDATENOTIFICATION",
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
}
```


This notification is sent when an order is updated.

Param | DataType | Description
--------- | ------- | ----------
orderNo | String | Order No.
notificationType | String| eg. ORDERUPDATENOTIFICATION
vehicleNumber | String | Vehicle Number
awbNumber | String | AWB Number
deliveryMediumName | String | Delivery boy name
phoneNumber | Integer | Delivery boy phone number
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


## Accept Order

> Response

```json
{
  "clientShipmentId": "Order_001",
  "status": "ORDER ACCEPTED",
  "awbNumber": "AWB123456789",
  "deliveryMediumName": "Thomas Watson",
  "phoneNumber": 9881234567,
  "tripName": "Trip_1227",
  "updatedOn": "2016-06-30 19:43:07",
  "trackUrl": "https://goo.gl/qhZP63",
  "deliveryEndDate": "2017-11-20 10:23:20",
  "orderReferenceId": "b7b15a79d6734297a00a93755856e8c8"
}

```

This notification is sent when an order is accepted by a delivery boy.



### Response Parameters


Param | DataType | Description
--------- | ------- | ----------
clientShipmentId | String | Order No.
status | String | Status of the order
awbNumber | String | AWB No.
deliveryMediumName | String | Name of delivery medium
phoneNumber | Long | Delivery medium's phone no.
tripName | String | Trip name
updatedOn | String | Accept order timestamp
trackUrl | String | Url to track Order
deliveryEndDate | String | Delivery end date.
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

This notification is sent when an order is rejected by a delivery boy.

### Response Parameters

Param | DataType | Description
--------- | ------- | ----------
clientShipmentId | String | Order No.
status | String | Status of the order
tripName | String | Trip name
updatedOn | String | Reject order timestamp
reasonOfRejection | String | Reason provided by Delivery medium while rejecting the order
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

### Response Parameters

Param | DataType | Description
--------- | ------- | ----------
orderNo | String | Order No.
notificationType | String | CANCELLEDNOTIFICATION
orderLeg | String | Order leg Ex: PICKUP, DELIVER
awbNumber | String | AWB Number for the order
deliveryMediumName | String | Name of delivery medium
phoneNumber | Long | Delivery medium's phone no.
orderState | String | State of order. Ex: FORWARD, REVERSE
customerName | String | Name of customer
reason | String | Reason for the order being cancelled
reasonCd | String | Reason code
cancellationTime | String | Cancellation timestamp
cancelledBy | String | Cancelled by user name
isCancelOccurAfterPickupFl | Boolean | whether order was cancelled after Pickup


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

### Response Parameters

Param | DataType | Description
--------- | ------- | ----------
clientShipmentIds | String | Order Nos.
deliveryMediumName | String | Name of delivery medium
tripName | String | Trip name
startTime | Date | Time when loading is completed.
phoneNumber | Long | Delivery medium's phone no.
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
  "deliveryTime": "2016-11-19 06:11:27",
  "cashAmount": 0,
  "deliveryLocationType": "",
  "transactionId": "12456",
  "actualCashAmount": 120,
  "paymentMode": "COD",
  "recipientName": "Rahul",
  "branchName": "AAA0",
  "paymentSubType": "",
  "orderReferenceId": "b7b15a79d6734297a00a93755856e8c8"
}

```

This notification is sent when an order is delivered by a delivery boy to customer.



### Response Parameters

Key | DataType | Description
--------- | ------- |-------
orderNo | String | Order No.
latitude | Double | Latitude where order was delivered
longitude | Double | Longitude where order was delivered
notificationType | String | DELIVEREDNOTIFICATION
orderLeg | String | Order leg, Possible values : DELIVER, PICKUP
awbNumber | String | Awb No.
customerComment | String | Customer comments
customerRating | Integer | Rating provided by customer
deliveryMediumName | String | Name of delivery medium
phoneNumber | Long | Delivery medium's phone no.
orderState | String | Order state, Possible values : FORWARD, REVERSE
customerName | String | Customer name
deliveryTime | String | Delivery timestamp
cashAmount | Double | Cash amount to collect
deliveryLocationType | String | Delivery Location
transactionId | String | Transaction id
paymentMode | String | Paymode mode, Possible values : PREPAID, COD
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

This notification is sent when an order is partially delivered by a delivery boy to customer.



### Response Parameters

Key | DataType | Description
--------- | ------- |-------
orderNo | String | Order No.
statusCd | String | PARTIALLYDELIVERED
notificationType | String | PARTIALDELIVERYNOTIFICATION
orderLeg | String | Order leg Ex: PICKUP, DELIVER
awbNumber | String | AWB Number for the order
customerComments | String | Customer comments
customerRating | Integer | Rating provided by customer
deliveryMediumName | String | Name of delivery medium
phoneNumber | Long | Delivery medium's phone no.
orderState | String | State of order. Ex: FORWARD, REVERSE
customerName | String | Customer name
reason | String | Reason for the order being partially delivered
reasonCd | String | Reason code
deliveryTime | String | Delivery timestamp
cashAmount | Double | Cash amount to be collected
deliveryLocationType | String | Delivery Location
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
  "notificationType": "NOTDELIVEREDNOTIFICATION",
  "orderLeg": "DELIVER",
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

This notification is sent when an order is not delivered by a delivery boy.



### Response Parameters

Key | DataType | Description
--------- | ------- | -------
orderNo | String | Order No.
notificationType | String | NOTDELIVEREDNOTIFICATION
orderLeg | String | Order leg Ex: PICKUP, DELIVER
awbNumber | String | AWB Number for the order
customerComments | String | Customer comments
customerRating | Integer | Rating provided by customer
deliveryMediumName | String | Name of delivery medium
phoneNumber | Long | Delivery medium's phone no.
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

This notification is sent when an order is picked up by a delivery boy.



### Response Parameters

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
customerRating | Integer | Rating provided by customer
deliveryMediumName | String | Name of delivery medium
phoneNumber | Long | Delivery medium's phone no.
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

This notification is sent when an order is picked up by a delivery boy.



### Response Parameters

Key | DataType | Description
--------- | ------- |-------
orderNo | String |  Order No.
notificationType | String |  NOTPICKEDUPNOTIFICATION
orderLeg | String |  Order leg
awbNumber | String | Airway Bill Number
customerComment | String |  Customer comments
customerRating | Integer | Rating provided by customer
deliveryMediumName | String |  Name of delivery medium
phoneNumber | Long | Phone no of delivery medium
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
      "driverName": "TestDriver1",
      "vehicleNumber": "MH-13213",
      "orderDetails": [
        {
          "orderNo": "DummyOrder345",
          "startTimeWindow": "2016-10-13 11:18:00",
          "endTimeWindow": "2016-10-13 17:45:00",
          "deliveryOrder":1,
          "latitude": 19.1239285,
          "longitude": 72.90944069999999
        }
      ]
    }
  ]
}

```

This notification is sent when route planning is done to assign orders to delivery boys for a particular window of time.



### Response Parameters

Key | DataType | Description
--------- | ------- |-------
notificationType | String |  DELIVERYPLANNING
notificationDetails | List | Notification details
tripName | String |  Trip name
deliveryMediumName | String |  Name of delivery medium
referenceId | String | Reference id of the trip
phoneNumber | String | Phone no of delivery medium
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
You will have to consume this webhook in case your system is integrated with LogiNext through Route Planning API.


### Response Parameters

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

### Response Parameters

Key | DataType | Description
--------- | ------- |-------
clientShipmentIds | List<String> |  Order No.s.
notificationType | String |  STARTTRIP
tripName | String |  Trip name
vehicleNumber | String |  Vehicle no.
driverName | String |  Name of driver
deliveryMediumName | String |  Name of delivery medium
phoneNumber | Long | Phone no.
startTime | String |  Trip start time


## Stop Trip

> Response

```json
{
  "notificationType": "DELIVEREDNOTIFICATION",
  "deliveryMediumName": "Rajesh",
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

### Response Parameters

Key | DataType | Description
--------- | ------- |-------
clientShipmentIds | List<String> |  Order Nos.
notificationType | String |  DELIVEREDNOTIFICATION
tripName | String |  Trip name
vehicleNumber | String |  Vehicle no.
driverName | String |  Name of driver
deliveryMediumName | String |  Name of delivery medium
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



### Response Parameters

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



### Response Parameters

Key | DataType | Description
--------- | ------- |-------
url | String |  Endpoint URL
data | String |  Data in XML format
notificationType | String |  HUB IN
updatedDate | String | Timestamp

## Allocation Engine Webhook

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

With this webhook, you can get the list of one or more nearest Drivers / Delivery Boys / Field Executives that the LogiNext Delivery Medium Allocation Engine has identified to deliver your On Demand (point to point) Orders.

### Response Parameters

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
deliveryMediums.userGroupName | String | Mandatory | This is the name of the User Group which the Driver / Delivery Medium / Field Executive belongs to in the LogiNext application.<br>Each user that is created in the LN system is associated to a user group. <br>This user groups is used to provide relevant access to the users.<br>Sample Value - "Platinum User Group"
deliveryMediums.employeeId | String | Mandatory | This the Employee ID set for the Driver / Delivery Medium / Field Executive in the LogiNext application.<br>Sample Value - "133478"
deliveryMediums.userName | String | Mandatory | This the Use rName set for the Driver / Delivery Medium / Field Executive in the LogiNext application.<br>Sample Value - "Joshua.Anderson"
deliveryMediums.phoneNumber | String | Mandatory | This the Phone No. set for the Driver / Delivery Medium / Field Executive in the LogiNext application.<br>Sample Value - "9894965656"
deliveryMediums.latitude | Double | Optional | This the current geo-location of the Driver / Delivery Medium / Field Executive.<br>Sample Value - "17.897"
deliveryMediums.longitude | Double | Optional | This the current geo-location of the Driver / Delivery Medium / Field Executive.<br>Sample Value - "85.897"
deliveryMediums.pickupEta | String | Mandatory | This the time at which the Driver / Delivery Medium / Field Executive will reach the Pick-Up Location<br>Sample Value - "2016-07-15T10:47:00.000Z"
deliveryMediums.distanceInKms | Double | Mandatory | This the distance in KM that the Driver / Delivery Medium / Field Executive is away from the Pick-Up Location
deliveryMediums.timeInMin | Integer | Mandatory | This the time in Minutes which the Driver / Delivery Medium / Field Executive will take to reach the Pick-up Location.
deliveryMediums.expiryTime | String | Mandatory | This the time before which the Driver / Delivery Medium / Field Executive will have to "accept" the order  on his / her mobile app. If not accepted, the order will be removed and allocated to next available Delivery Medium.<br>Sample Value - "2016-07-15T10:30:00.000Z"<br><br>Note that the time till which you want the order to remain displayed in the Delivery Medium's app. is configurable through the Settings screen on the LogiNext application.
deliveryMediums.statusCd | String | Mandatory | This is the current Status of the Delivery Medium.<br>This will have either of the two values depending on the configuration you have set.<br>If you want the Delivery Medium to cater to only one order at a time, then this Status code will be AVAILABLE.<br>If you want an order to be allocated to the Delivery Medium to cater to multiple orders at any given time i.e. even when is catering another order, then the Status Code will be DISPATCHED in case he is delivering another order.
deliveryMediums.tripStatus | String | Mandatory | This is the current Status of the Trip of the Delivery Medium.<br>This will have either of the two values depending on the configuration you have set.<br>If you want the Delivery Medium to cater to only one order at a time, then this Status code will be NOT STARTED .<br>If you want an order to be allocated to the Delivery Medium to cater to multiple orders at any given time i.e. even when is catering another order, then the Status Code will be DISPATCHED in case he is delivering another order.
deliveryMediums.referenceId | String | Mandatory | This is the LogiNext reference ID of the Delivery Medium / Driver / Field Executive.

# Country Codes

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
    });
  }, 50);
</script>
