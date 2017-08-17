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

<b><u>The validity of this session token is 1 day (24 hours).</u></b>

Please ensure that you add the token and secret key as part of every Loginext API call.

> Definition

```json
https://api.loginextsolutions.com/LoginApp/login/authenticate
```
> Request Body

```json
{
        "userName":"demouser",
        "password":"Admin#1!"
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

Parameter | DataType |  Required | Description
-----------|-------|------- | ----------
userName | String | Mandatory | Username provided by LogiNext
password | String | Mandatory | Password provided by LogiNext

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

Parameter | DataType |  Required | Description
-----------|-------|------- | ----------
vehicleNumber | String | Mandatory | Unique name to identify the vehicle
vehicleMake | String | Optional | Make of the vehicle like Mazda, Volvo, etc.
vehicleModel | String |Optional | Model of the vehicle as specified by manufacturer like FH series, MethaneDiesel, etc.
typeOfBody | String |Optional | Body Type of the vehicle. This is static field and can have only one of the below values - 4 wheeler, 2 wheeler, 24FT, 20FT, 32FT, 19FT, TATA 407, 14 FT CANTER, 17FT, TRLR, TRUCK
unladdenWeight | Integer |Optional | Unladen weight of the vehicle in Kg.
capacityInWeight | Integer |Optional | Capacity of vehicle in Kg.
capacityInUnits | Integer |Optional | Capacity of the vehicle in Units
capacityInVolume | Integer |Optional | Capacity of the vehicle on cubic centimeters
chasisNumber | String |Optional | Chassis / VIN number of the vehicle
engineNumber | String |Optional | Engine Number of the vehicle
markerName | String |Optional | Name of the Sub-ordinate who is driving along with the driver
registrationNumber | String |Optional | Registered Number provided by the local transportation authority
pucValidity | Date |Optional | Date till which PUC certificate is valid.Format - YYYY-MM-DDTHH:MM:SS.SSSZ e.g. : 2016-07-01T11:18:00.000Z. This date always needs to be later than the current date.
insuranceValidity | Date |Optional | Date till which insurance of the vehicle is valid. Format - YYYY-MM-DDTHH:MM:SS.000Z e.g. : 2016-07-01T11:18:00.SSSZ.This date always needs to be later than the current date.
vehiclePermit | String |Optional | Full name of the states of India in which the vehicle is permitted to travel
ownership | String |Optional | Entity that owns the vehicle. This field can have only below two values - Company , Vendor
ownerName | String |Optional | Name of the Company / Vendor who owns the vehicle
transporter | String |Optional | Name of the transporter / carrier / 3PL provider responsible for the delivery.
financer | String |Optional | If the vehicle is on loan, then name of the financer
accidentHistory | String |Optional | If vehicle has any accident records against it, then please document the details through this field
rentStartDate | Date |Optional | This input is valid only if the vehicle’s owner is a vendor. Format - YYYY-MM-DDTHH:MM:SS.000Z e.g. : 2016-07-01T11:18:00.SSSZ. Rent start Date should be earlier than the Rent End Date.
rentEndDate  | Date |Optional | This input is valid only if the vehicle’s owner is a vendor. Format - YYYY-MM-DDTHH:MM:SS.000Z e.g. : 2016-07-01T11:18:00.SSSZ. Rent End Date should be later than the Rent Start Date.
deviceId.barcode | String |Optional | This input should be the barcode of the tracker in order to map the Vehicle with the tracker.In order to get the list of tracker that you can attach to a vehicle, you will need to either access the Loginext portal with your login or contact our CSA and get the list. On LogiNext portal, you can access the tracker list - LogiNext → Resource → Tracker.

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

Parameter | DataType |  Required | Description
-----------|-------|------- | ----------
reference_id | String | Mandatory | Reference Id associated with the vehicle.


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

<span class="post">POST</span>`https://api.loginextsolutions.com/VehicleApp/haul/v1`


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

Parameter | DataType |  Required | Description
-----------|-------|------- | ----------
vehicleNumber | String | Mandatory | Unique name to identify the vehicle
vehicleMake | String | Optional | Make of the vehicle like Mazda, Volvo, etc.
vehicleModel | String |Optional | Model of the vehicle as specified by manufacturer like FH series, MethaneDiesel, etc.
typeOfBody | String |Optional | Body Type of the vehicle. This is static field and can have only one of the below values - 4 wheeler, 2 wheeler, 24FT, 20FT, 32FT, 19FT, TATA 407, 14 FT CANTER, 17FT, TRLR, TRUCK
unladdenWeight | Integer |Optional | Unladen weight of the vehicle in Kg.
capacityInWeight | Integer |Optional | Capacity of vehicle in Kg.
capacityInUnits | Integer |Optional | Capacity of the vehicle in Units
capacityInVolume | Integer |Optional | Capacity of the vehicle on cubic centimeters
chasisNumber | String |Optional | Chassis / VIN number of the vehicle
engineNumber | String |Optional | Engine Number of the vehicle
markerName | String |Optional | Name of the Sub-ordinate who is driving along with the driver
registrationNumber | String |Optional | Registered Number provided by the local transportation authority
pucValidity | Date |Optional | Date till which PUC certificate is valid.Format - YYYY-MM-DDTHH:MM:SS.SSSZ e.g. : 2016-07-01T11:18:00.000Z. This date always needs to be later than the current date.
insuranceValidity | Date |Optional | Date till which insurance of the vehicle is valid. Format - YYYY-MM-DDTHH:MM:SS.000Z e.g. : 2016-07-01T11:18:00.SSSZ.This date always needs to be later than the current date.
vehiclePermit | String |Optional | Full name of the states of India in which the vehicle is permitted to travel
ownership | String |Optional | Entity that owns the vehicle. This field can have only below two values - Company , Vendor
ownerName | String |Optional | Name of the Company / Vendor who owns the vehicle
transporter | String |Optional | Name of the transporter / carrier / 3PL provider responsible for the delivery.
financer | String |Optional | If the vehicle is on loan, then name of the financer
accidentHistory | String |Optional | If vehicle has any accident records against it, then please document the details through this field
rentStartDate | Date |Optional | This input is valid only if the vehicle’s owner is a vendor. Format - YYYY-MM-DDTHH:MM:SS.000Z e.g. : 2016-07-01T11:18:00.SSSZ. Rent start Date should be earlier than the Rent End Date.
rentEndDate  | Date |Optional | This input is valid only if the vehicle’s owner is a vendor. Format - YYYY-MM-DDTHH:MM:SS.000Z e.g. : 2016-07-01T11:18:00.SSSZ. Rent End Date should be later than the Rent Start Date.
deviceId.barcode | String |Optional | This input should be the barcode of the tracker in order to map the Vehicle with the tracker.In order to get the list of tracker that you can attach to a vehicle, you will need to either access the Loginext portal with your login or contact our CSA and get the list. On LogiNext portal, you can access the tracker list - LogiNext → Resource → Tracker.
deviceId.barcode | String |Optional | Barcode of the tracker.


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

Param | DataType |  Required | Description
--------- | ------- | ---------- | ------------
driverName | String | Mandatory |  Driver's full name
phoneNumber | String | Mandatory | Phone No
emailId | String | Optional | EmailId
dateOfBirth | String | Optional | Date of Birth
languageList | List of Objects | Optional | Language(s) known to the driver
languageList.name | String | Optional | Name of language
salary | String | Optional | Current salary of Driver
maritalStatus | String | Optional | Marital Status. Ex: married, unmarried.
gender | String | Optional | Gender. Ex - male,female.
experience | Integer | Optional | No of yrs. of driving experience
licenseValidity | String | Optional | License validity date
licenseNumber | String | Mandatory | License No
licenseType | String | Optional | License Type. Ex: 2 wheeler, 4 wheeler
licenseIssueBy | String | Optional | License Issuing Authority Name
addressList.apartment | String | Mandatory | Apartment name/no
addressList.streetName | String | Mandatory | Society/Street name
addressList.landmark | String | Mandatory | Landmark
addressList.areaName | String | Optional | Locality/Area name
addressList.countryShortCode | String | Mandatory | Country code.Please refer to the list of country codes provided in the "Country Codes" section.
addressList.stateShortCode | String | Mandatory | State short code.Please refer to the list of state codes provided in the "State Codes" section.
addressList.city | String | Mandatory | City
addressList.pincode | Integer | Mandatory | Pincode
addressList.isCurrentAddress | Boolean | Mandatory | Indicates whether this is current address of driver or not. Ex: true - Current Address, false - Permanent Address
driverEmployeeId | String | Optional | EmployeeId
shiftList.startTime | String | Mandatory | Shift start date
shiftList.endTime | String | Mandatory | Shift end date
shiftList.shiftStartTime | String | Mandatory | Shift start time
shiftList.shiftEndTime | String | Mandatory | Shift end time
previousCompanyName | String | Optional | Driver's last company name
reportingManager | String | Optional | Driver's last company's reporting manager's name
managerPhoneNumber | String | Optional | Driver's last company'smanager's phone no
managerEmailId | String | Optional | Driver's last company's manager's email id






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
          "shiftStartTime": "01, Jan 1970 07:03 PM",
          "shiftEndTime": "01, Jan 1970 07:10 AM",
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

Param | DataType |  Required | Description
--------- | ------- | ---------- | ------------
referenceId | String | Mandatory |  ReferenceId of the record
driverName | String | Mandatory |  Driver's full name
phoneNumber | String | Mandatory | Phone No
emailId | String | Optional | EmailId
dateOfBirth | String | Optional | Date of Birth
languageList | List of Objects | Optional | Language(s) known to the driver
languageList.name | String | Optional | Name of language
salary | String | Optional | Current salary of Driver
maritalStatus | String | Optional | Marital Status. Ex: married, unmarried.
gender | String | Optional | Gender. Ex - male,female.
experience | Integer | Optional | No of yrs. of driving experience
licenseValidity | String | Optional | License validity date
licenseNumber | String | Mandatory | License No
licenseType | String | Optional | License Type. Ex: 2 wheeler, 4 wheeler
licenseIssueBy | String | Optional | License Issuing Authority Name
addressList.apartment | String | Mandatory | Apartment name/no
addressList.streetName | String | Mandatory | Society/Street name
addressList.landmark | String | Mandatory | Landmark
addressList.areaName | String | Optional | Locality/Area name
addressList.countryShortCode | String | Mandatory | Country short code.Please refer to the list of country codes provided in the "Country Codes" section.
addressList.stateShortCode | String | Mandatory | State short code.Please refer to the list of state codes provided in the "State Codes" section.
addressList.city | String | Mandatory | City
addressList.pincode | Integer | Mandatory | Pincode
addressList.isCurrentAddress | Boolean | Mandatory | Indicates whether this is current address of driver or not. Ex: true - Current Address, false - Permanent Address
driverEmployeeId | String | Optional | EmployeeId
shiftList.startTime | String | Mandatory | Shift start date
shiftList.endTime | String | Mandatory | Shift end date
shiftList.shiftStartTime | String | Mandatory | Shift start time
shiftList.shiftEndTime | String | Mandatory | Shift end time
previousCompanyName | String | Optional | Driver's last company name
reportingManager | String | Optional | Driver's last company's reporting manager's name
managerPhoneNumber | String | Optional | Driver's last company'smanager's phone no
managerEmailId | String | Optional | Driver's last company's manager's email id

=======

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

Parameter | DataType |  Required | Description
-----------|-------|------- | ----------
shipmentType | String | Mandatory | Type of the Shipment being created.Examples:"Bag","Package","Manifest"
originAddr | String |Mandatory | Origin point of the trip.Examples:-AMDD,BLRX
destinationAddr | String |Mandatory | Destination point of the trip.Examples:-CNND,BOMX
name | String |Mandatory | Name of the trip.Has to be unique.Example:-CNND-BOMX-123_456
packageWeight | Integer |Optional | Capacity of the shipment in terms of Kgs
packageValue | Integer |Optional | Capacity of the shipment in terms of the number of units present in it
packageVolume | Integer |Optional | Capacity of the shipment in terms of cc
vehicleReportingDate | Date |Mandatory | Reporting date of the vehicle at the origin hub
modeOfTransport | String |Mandatory | Mode of transit for the trip.Examples:-ROAD,AIR,RAIL
lrNumber | String | Mandatory(Conditional) | Lorry Receipt Number if modeOfTransport selected as ROAD.
flightNum| String |Mandatory(Conditional) | Flight Number if modeOfTransport selected as AIR.
trainNum| String |Mandatory(Conditional) | Rail Number if modeOfTransport selected as RAIL.
driverName | String |Optional | Name of the driver
vehicleNumber | String |Optional | Vehicle Number.
barcode | String |Mandatory | Barcode of the tracker used for attaching to vehicle during trip


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
["ca7fbf96a133461aadce8f94678084ee"]
{
    "tripReferenceIds":["ca7fbf96a133461aadce8f94678084ee"]
}
```

> Response

```json
{
  "status": 200,
  "message": "Trips started successfully",
  "data": null,
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
["ca7fbf96a133461aadce8f94678084ee"]
{
    "tripReferenceIds":["ca7fbf96a133461aadce8f94678084ee"]
}
```

> Response

```json
{
  "status": 200,
  "message": "Trips ended successfully",
  "data": null,
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


### HTTP Request Parameters

Parameter | Type |  Required | Description
-----------|-------|------- | ----------
tripReferenceIds | List of Strings | Mandatory | Reference Ids of the trip

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

Param | DataType |  Required | Description
--------- | ------- | ---------- | ------------
trackerId | String | Mandatory |  Device's unique ID
latitude | Double | Mandatory | Latitude
longitude | Double | Mandatory | Longitude
time | Date | Mandatory | Tracking time in UTC
batteryPerc | Double | Mandatory | Battery Percentage of device
speed | Double | Optional | Speed with which consignment is moving
messageType | String | Mandatory | Message type. Ex: REG
temperature | Double | Optional | Consignment's temperature


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
  "data": null,
  "hasError": false
}

```
Place a new delivery leg order with this API.

### Request

<span class="post">POST</span>`https://api.loginextsolutions.com/ShipmentApp/mile/v1/create`

### Request Parameters

Param | DataType |  Required | Description
--------- | ------- | ---------- | ------------
orderNo | String | Mandatory |  Order No.
awbNumber | String | Optional | Airway Bill No.
shipmentOrderTypeCd | String | Mandatory | Order type code. DELIVER for delivery leg order
orderState | String | Mandatory | State of order. Ex: FORWARD
shipmentOrderDt | Date | Mandatory | Order Date
distributionCenter | String | Mandatory | Distribution center's name
packageWeight | Double | Optional | Weight of package in Kg.
packageVolume | Double | Optional | Volume of package in CC
packageValue | Double | Optional | Value of package
numberOfItems | Integer | Optional | Number of crates
paymentType | String | Optional | Payment mode. Ex: COD - Cash On Delivery, Prepaid
partialDeliveryAllowedFl | String | Optional | Is Partial Delivery allowed. Ex: Y/N. Default value is N.
returnAllowedFl | String | Optional | Is Return allowed. Ex: Y/N. Default value is Y.
cancellationAllowedFl | String | Optional | Is Cancellation allowed. Ex: Y/N. Default value is Y.
deliverBranch | String | Mandatory | Name of delivery branch
deliverServiceTime | Integer | Mandatory | Deliver service time in mins.
deliverStartTimeWindow | Date | Mandatory | Deliver start time window
deliverEndTimeWindow | Date | Mandatory | Deliver end time window
deliveryType | String | Optional | Order delivery type. Ex: TRK - Truck, VAN - Van, DLBOY - Delivery Boy
deliveryLocationType | String | Optional | Type of delivery location. Ex: CUSTOMER, PUP
deliverAccountCode | String | Mandatory | Deliver account code
deliverAccountName | String | Mandatory | Deliver account name
deliverEmail | String | Optional | Deliver email
deliverPhoneNumber | String | Optional | Deliver phone number
deliverApartment | String | Mandatory | Apartment
deliverStreetName | String | Mandatory | Street name
deliverLandmark | String | Optional | Landmark
deliverLocality | String | Mandatory | Locality
deliverCity | String | Mandatory | City
deliverState| String | Mandatory | State code. Please refer to the list of state codes provided in the "State Codes" section.
deliverCountry | String | Mandatory | Country code. Please refer to the list of country codes provided in the "Country Codes" section.
deliverPinCode | String | Mandatory | Pincode
deliverLatitude | Double | Optional | Delivery address Latitude
deliverLongitude | Double | Optional | Delivery address Longitude
returnBranch | String | Mandatory | Name of return branch
pickupNotes | String | Optional | Additional pickup comments associated with the order
deliverNotes | String | Optional | Additional delivery comments associated with the order

### Request Parameters (Crates)

Param | DataType |  Required | Description
--------- | ------- | ---------- | ------------
shipmentCrateMappings | Array of objects | Optional | Shipment crates
shipmentCrateMappings.crateCd | String | Mandatory | Crate code
shipmentCrateMappings.crateAmount | Double | Mandatory | Crate amount
shipmentCrateMappings.crateType | String | Mandatory | Crate type. Ex - ??
shipmentCrateMappings.noOfUnits | Integer | Mandatory | No. of items in crate
shipmentCrateMappings.shipmentlineitems.itemCd | String | Mandatory | Item code
shipmentCrateMappings.shipmentlineitems.itemName | String | Optional | Item name
shipmentCrateMappings.shipmentlineitems.itemPrice | Double | Mandatory | Item price
shipmentCrateMappings.shipmentlineitems.itemQuantity | Double | Mandatory | Item quantity
shipmentCrateMappings.shipmentlineitems.itemType | String | Optional | Item type
shipmentCrateMappings.shipmentlineitems.itemWeight | Double | Optional | Item weight

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
  "data": null,
  "hasError": false
}

```
Place a new pickup leg order with this API.

### Request

<span class="post">POST</span>`https://api.loginextsolutions.com/ShipmentApp/mile/v1/create`



### Request Parameters

Param | DataType |  Required | Description
--------- | ------- | ---------- | ------------
orderNo | String | Mandatory |  Order No.
awbNumber | String | Optional | Airway Bill No.
shipmentOrderTypeCd | String | Mandatory | Order type code. DELIVER for delivery leg order
orderState | String | Mandatory | State of order. Ex: FORWARD
shipmentOrderDt | Date | Mandatory | Order Date
distributionCenter | String | Mandatory | Distribution center's name
packageWeight | Double | Optional | Weight of package in Kg.
packageVolume | Double | Optional | Volume of package in CC
packageValue | Double | Optional | Value of package
paymentType | String | Mandatory | Payment mode. Ex: COD - Cash On Delivery, Prepaid
numberOfItems | Integer | Optional | Number of crates
deliveryType | String | Optional | Order delivery type. Ex: TRK - Truck, VAN - Van, DLBOY - Delivery Boy
partialDeliveryAllowedFl | String | Optional | Is Partial Delivery allowed. Ex: Y/N. Default value is N.
returnAllowedFl | String | Optional | Is Return allowed. Ex: Y/N. Default value is Y.
cancellationAllowedFl | String | Optional | Is Cancellation allowed. Ex: Y/N. Default value is Y.
pickupBranch | String | Mandatory | Name of pickup branch
pickupServiceTime | Integer | Mandatory | Pickup service time in mins.
pickupStartTimeWindow | Date | Mandatory | Pickup start time window
pickupEndTimeWindow | Date | Mandatory | Pickup end time window
pickupAccountCode | String | Mandatory | Pickup account code
pickupAccountName | String | Mandatory | Pickup account name
pickupEmail | String | Optional | Pickup email id
pickupPhoneNumber | Optional | Mandatory | Pickup phone no
pickupApartment | String | Mandatory | Pickup Apartment
pickupStreetName | String | Mandatory | Pickup Street name
pickupLandmark | String | Optional | Pickup Landmark
pickupLocality | String | Mandatory | Pickup Locality
pickupCity | String | Mandatory | Pickup City
pickupState| String | Mandatory | Pickup State. Please refer to the list of state codes provided in the "State Codes" section.
pickupCountry | String | Mandatory | Pickup Country. Please refer to the list of country codes provided in the "Country Codes" section.
pickupPinCode | String | Mandatory | Pickup Pincode
pickupLatitude | Double | Optional | Pickup address Latitude
pickupLongitude | Double | Optional | Pickup address Longitude
pickupNotes | String | Optional | Additional pickup comments associated with the order
deliverNotes | String | Optional | Additional delivery comments associated with the order


### Request Parameters (Crates)

Param | DataType |  Required | Description
--------- | ------- | ---------- | ------------
shipmentCrateMappings | Array of objects | Optional | Shipment crates
shipmentCrateMappings.crateCd | String | Mandatory | CRATE001
shipmentCrateMappings.crateAmount | Double | Optional | Crate amount
shipmentCrateMappings.crateType | String | Optional | Type of crate. Ex: cake, juice, sweet, furniture etc.
shipmentCrateMappings.noOfUnits | Integer | Optional | No. of crate units
shipmentCrateMappings.shipmentlineitems.itemCd | String | Mandatory | Item code
shipmentCrateMappings.shipmentlineitems.itemName | String | Optional | Item name
shipmentCrateMappings.shipmentlineitems.itemPrice | Double | Mandatory | Item price
shipmentCrateMappings.shipmentlineitems.itemQuantity | Double | Mandatory | Item quantity
shipmentCrateMappings.shipmentlineitems.itemType | String | Optional | Item type
shipmentCrateMappings.shipmentlineitems.itemWeight | Double | Optional | Item weight





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
  "data": null,
  "hasError": false
}

```
Place a new delivery leg order with this API.

### Request

<span class="post">POST</span>`https://api.loginextsolutions.com/ShipmentApp/mile/v1/create`


### Request Parameters

Param | DataType |  Required | Description
--------- | ------- | ---------- | ------------
orderNo | String | Mandatory |  Order No.
awbNumber | String | Optional | Airway Bill No.
shipmentOrderTypeCd | String | Mandatory | Order type code. BOTH for pickup & delivery leg order
orderState | String | Mandatory | State of order. Ex: FORWARD
shipmentOrderDt | Date | Mandatory | Order Date
distributionCenter | String | Mandatory | Distribution center's name
packageWeight | Double | Optional | Weight of package in Kg.
packageVolume | Double | Optional | Volume of package in CC
packageValue | Double | Optional | Value of package
numberOfItems | Integer | Optional | Number of crates
paymentType | String | Mandatory | Payment mode. Ex: COD - Cash On Delivery, Prepaid
partialDeliveryAllowedFl | String | Optional | Is Partial Delivery allowed. Ex: Y/N
returnAllowedFl | String | Optional | Is Return allowed. Ex: Y/N
cancellationAllowedFl | String | Optional | Is Cancellation allowed. Ex: Y/N
deliverBranch | String | Mandatory | Name of delivery branch
deliverServiceTime | Integer | Mandatory | Deliver service time in mins.
deliverStartTimeWindow | Date | Mandatory | Deliver start time window
deliverEndTimeWindow | Date | Mandatory | Deliver end time window
deliveryType | String | Optional | Order delivery type. Ex: TRK - Truck, VAN - Van, DLBOY - Delivery Boy
deliveryLocationType | String | Optional | Type of delivery location. Ex: CUSTOMER, PUP
deliverAccountCode | String | Mandatory | Deliver account code
deliverAccountName | String | Mandatory | Deliver account name
deliverApartment | String | Mandatory | Apartment
deliverStreetName | String | Mandatory | Street name
deliverLandmark | String | Optional | Landmark
deliverLocality | String | Mandatory | Locality
deliverCity | String | Mandatory | City
deliverState| String | Mandatory | State code
deliverCountry | String | Mandatory | Country code
deliverPinCode | String | Mandatory | Pincode
deliverLatitude | Double | Optional | Delivery address Latitude
deliverLongitude | Double | Optional | Delivery address Longitude
pickupBranch | String | Mandatory | Name of pickup branch
pickupServiceTime | Integer | Mandatory | Pickup service time in mins.
pickupStartTimeWindow | Date | Mandatory | Pickup start time window
pickupEndTimeWindow | Date | Mandatory | Pickup end time window
pickupAccountCode | String | Mandatory | Pickup account code
pickupAccountName | String | Mandatory | Pickup account name
pickupApartment | String | Mandatory | Pickup Apartment
pickupStreetName | String | Mandatory | Pickup Street name
pickupLandmark | String | Optional | Pickup Landmark
pickupLocality | String | Mandatory | Pickup Locality
pickupCity | String | Mandatory | Pickup City
pickupState| String | Mandatory | Pickup State code
pickupCountry | String | Mandatory | Pickup Country code
pickupPinCode | String | Mandatory | Pickup Pincode
pickupLatitude | Double | Optional | Pickup address Latitude
pickupLongitude | Double | Optional | Pickup address Longitude
returnBranch | String | Mandatory | Name of return branch
returnStartTimeWindow | Date | Mandatory | Return start time window
returnEndTimeWindow | Date | Mandatory | Return end time window
returnAccountCode | String | Mandatory | Return account code
returnAccountName | String | Mandatory | Return account name
returnEmail | String | Mandatory | Return account code
returnPhoneNumber | String | Mandatory | Return account name
returnApartment | String | Mandatory | Return Apartment
returnStreetName | String | Mandatory | Return Street name
returnLandmark | String | Optional | Return Landmark
returnLocality | String | Mandatory | Return Locality
returnCity | String | Mandatory | Return City
returnState| String | Mandatory | Return State code. Please refer to the list of state codes provided in the "State Codes" section.
returnCountry | String | Mandatory | Return Country code. Please refer to the list of country codes provided in the "Country Codes" section.
returnPinCode | String | Mandatory | Return Pincode
deliverEmail| String | Optional | Email of the customer
deliverPhoneNumber| String | Optional | Phone number of the customer
pickupEmail| String | Optional | Email of the merchant
pickupPhoneNumber| String | Optional | Phone number of the merchant
pickupNotes | String | Optional | Additional pickup comments associated with the order
deliverNotes | String | Optional | Additional delivery comments associated with the order



### Request Parameters (Crates)

Param | DataType |  Required | Description
--------- | ------- | ---------- | ------------
shipmentCrateMappings | Array of objects | Optional | Shipment crates
shipmentCrateMappings.crateCd | String | Mandatory | CRATE001
shipmentCrateMappings.crateAmount | Double | Optional | Crate amount
shipmentCrateMappings.crateType | String | Optional | Type of crate. Ex: cake, juice, sweet, furniture etc.
shipmentCrateMappings.noOfUnits | Integer | Optional | No. of crate units
shipmentCrateMappings.shipmentlineitems.itemCd | String | Mandatory | Item code
shipmentCrateMappings.shipmentlineitems.itemName | String | Optional | Item name
shipmentCrateMappings.shipmentlineitems.itemPrice | Double | Mandatory | Item price
shipmentCrateMappings.shipmentlineitems.itemQuantity | Double | Mandatory | Item quantity
shipmentCrateMappings.shipmentlineitems.itemType | String | Optional | Item type
shipmentCrateMappings.shipmentlineitems.itemWeight | Double | Optional | Item weight

## Create Return Order

> Definition

```json
https://api.loginextsolutions.com/ShipmentApp/mile/v1/create/return
```

> Request Body

```json
["863fe69239bc4f738ca275a809c3b2e2"]
```

> Response

```json
{
  "status": 201,
  "message": "success",
  "referenceId": [
    "d7b0f3f8e1174742bd6a8ae451866cb1"
  ],
  "data":null,
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
      "clientName": "Asia Commerce Logistics SDN BHD",
      "branchName": "ACL_CENTER_WHSE",
      "origin": "ACL_CENTER_WHSE",
      "destination": "Mid Valley Megamall,Lingkaran Syed Putra, Mid Valley City,Kuala Lumpur",
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
      "clientName": "Asia Commerce Logistics SDN BHD",
      "branchName": "ACL_CENTER_WHSE",
      "origin": "No. 1,Jalan Taylors,,,,Subang Jaya,47500",
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
  "referenceId": null,
  "data": null,
  "hasError": false
}

```
With this API, you will be able to update the order information unless and until that order is not dispatched and not associated with any Trip.
You can pass multiple order reference IDs and can update one or more parameters.

### Request

<span class="post">POST</span>`https://api.loginextsolutions.com/ShipmentApp/mile/v1/update`


### Request Parameters

Param | DataType |  Required | Description
--------- | ------- | ---------- | ------------
referenceId | String | Mandatory |  Order Reference id
orderNo | String | Optional |  Order No.
awbNumber | String | Optional | Airway Bill No.
shipmentOrderDt | Date | Optional | Order Date
packageWeight | Double | Optional | Weight of package in Kg.
packageVolume | Double | Optional | Volume of package in CC
packageValue | Double | Optional | Value of package
numberOfItems | Integer | Optional | Number of crates
paymentType | String | Optional | Payment mode. Ex: COD - Cash On Delivery, Prepaid
partialDeliveryAllowedFl | String | Optional | Is Partial Delivery allowed. Ex: Y/N
returnAllowedFl | String | Optional | Is Return allowed. Ex: Y/N
cancellationAllowedFl | String | Optional | Is Cancellation allowed. Ex: Y/N
deliverBranch | String | Optional | Name of delivery branch
deliverServiceTime | Integer | Optional | Deliver service time in mins.
deliverStartTimeWindow | Date | Optional | Deliver start time window
deliverEndTimeWindow | Date | Optional | Deliver end time window
deliveryType | String | Optional | Order delivery type. Ex: TRK - Truck, VAN - Van, DLBOY - Delivery Boy
deliveryLocationType | String | Optional | Type of delivery location. Ex: CUSTOMER, PUP
deliverAccountCode | String | Optional | Deliver account code
deliverAccountName | String | Optional | Deliver account name
deliverApartment | String | Optional | Apartment
deliverStreetName | String | Optional | Street name
deliverLandmark | String | Optional | Landmark
deliverLocality | String | Optional | Locality
deliverCity | String | Optional | City
deliverState| String | Optional | State code
deliverCountry | String | Optional | Country code
deliverPinCode | String | Optional | Pincode
pickupBranch | String | Optional | Name of pickup branch
pickupServiceTime | Integer | Optional | Pickup service time in mins.
pickupStartTimeWindow | Date | Optional | Pickup start time window
pickupEndTimeWindow | Date | Optional | Pickup end time window
pickupAccountCode | String | Optional | Pickup account code
pickupAccountName | String | Optional | Pickup account name
pickupApartment | String | Optional | Pickup Apartment
pickupStreetName | String | Optional | Pickup Street name
pickupLandmark | String | Optional | Pickup Landmark
pickupLocality | String | Optional | Pickup Locality
pickupCity | String | Optional | Pickup City
pickupState| String | Optional | Pickup State code. Please refer to the list of state codes provided in the "State Codes" section.
pickupCountry | String | Optional | Pickup Country code. Please refer to the list of country codes provided in the "Country Codes" section.
pickupPinCode | String | Optional | Pickup Pincode
returnBranch | String | Optional | Name of return branch
returnStartTimeWindow | Date | Optional | Return start time window
returnEndTimeWindow | Date | Optional | Return end time window
returnAccountCode | String | Optional | Return account code
returnAccountName | String | Optional | Return account name
returnEmail | String | Optional | Return account code
returnPhoneNumber | String | Optional | Return account name
returnApartment | String | Optional | Return Apartment
returnStreetName | String | Optional | Return Street name
returnLandmark | String | Optional | Return Landmark
returnLocality | String | Optional | Return Locality
returnCity | String | Optional | Return City
returnState| String | Optional | Return State code. Please refer to the list of state codes provided in the "State Codes" section.
returnCountry | String | Optional | Return Country code. Please refer to the list of country codes provided in the "Country Codes" section.
returnPinCode | String | Optional | Return Pincode

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
    "reasonCd":"DBUNAVAILABLE",
    "otherReason":""

  },
  {
    "orderReferenceId":"6186d7r5te324c42abb5ea1a32x45f66",
    "reasonCd":"DBUNAVAILABLE",
    "otherReason":""

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
  "data": null,
  "message": "Shipment updated successfully",
  "hasError": false
}

```
With this API, you will be able to update the order information unless and until that order is not dispatched and not associated with any Trip.
You can pass multiple order reference IDs and can update one or more parameters.

### Request

<span class="post">PUT</span>`https://api.loginextsolutions.com/ShipmentApp/mile/v1/update/status


### Request Parameters

Param | DataType |  Required | Description
--------- | ------- | ---------- | ------------
newStatus | String | Mandatory |  One status for multiple orders.The orders will be updated with this new status
orderReferenceId | String | Mandatory |  LogiNext provided order/shipment referenceId
reasonCd | String | Conditional Mandatory | Can pass only set values or any value can be sent as OTHER.Mandatory depending upon the status selected : NOTDELIVERED, NOTPICKEDUP, CANCELLED
otherReason | Date | Conditional Mandatory | Mandatory when reasonCd is OTHER

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
  "referenceId": null,
  "data": null,
  "hasError": false
}

```
With this API, you will be able to update the crate and line items information for one order at a time until that order is not dispatched and not associated with any Trip.
You can pass multiple crate and line items.

### Request

<span class="post">POST</span>`https://api.loginextsolutions.com/ShipmentApp/mile/v1/updateCrates`

### Request Parameters (Crates)

Param | DataType |  Required | Description
--------- | ------- | ---------- | ------------
shipmentCrates | Array of objects | Optional | Shipment crates
shipmentCrates.crateCd | String | Mandatory | Crate Code
shipmentCrates.crateAmount | Double | Optional | Crate amount
shipmentCrates.crateType | String | Optional | Type of crate. Ex: cake, juice, sweet, furniture etc.
shipmentCrates.noOfUnits | Integer | Optional | No. of crate units
shipmentCrates.shipmentlineitems.itemCd | String | Mandatory | Item code
shipmentCrates.shipmentlineitems.itemName | String | Optional | Item name
shipmentCrates.shipmentlineitems.itemPrice | Double | Mandatory | Item price
shipmentCrates.shipmentlineitems.itemQuantity | Double | Mandatory | Item quantity
shipmentCrates.shipmentlineitems.itemType | String | Optional | Item type
shipmentCrates.shipmentlineitems.itemWeight | Double | Optional | Item weight


## Cancel Order

> Definition

```json
https://api.loginextsolutions.com/ShipmentApp/mile/v1/cancel
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
  "message": null,
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

Parameter | DataType |  Required | Description
-----------|-------|------- | ----------
orderstartdt | String | Mandatory | Order start date
orderenddt | String | Mandatory | Order end date
deliverystartdt | String | Mandatory | Delivery start date
deliveryenddt | String | Mandatory | Delivery end date
status | String | Optional | Order status. <BR>Ex: NOTDISPATCHED,INTRANSIT,DELIVERED,<BR>NOTDELIVERED,PICKEDUP,NOTPICKEDUP,CANCELLED

## Start Trip

> Definition

```json
https://api.loginextsolutions.com/TripApp/mile/v1/trip/start
```

> Request Body

```json
["a9be39b9347911e6829f000d3aa04450"]
```

> Response

```json
{
  "status": 200,
  "message": "1 trip(s) started",
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

Parameter | DataType |  Required | Description
-----------|-------|------- | ----------
tripReferenceId | String  | Mandatory | Reference Id associated with the trip.
notDispatchedOrders | List  | Mandatory | Reference Id associated with the non-dispatched order.
deliveredOrders | List | Mandatory | Reference Id associated with the delivered order.

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

Parameter | DataType |  Required | Description
-----------|-------|------- | ----------
employeeId | String | Mandatory | Employee Id
userGroupName | String | Mandatory | User group name
branchName | String | Mandatory | Client branch name
deliveryMediumMasterName | String |Mandatory | Full name of Delivery medium
phoneNumber | String | Mandatory | Mobile no
imei | String |Optional | IMEI no
emailId | String | Optional | Email id
userName | String | Mandatory | Username
password | String | Mandatory | Password
capacityInUnits | Integer | Mandatory | Capacity of Delivery medium in units
capacityInVolume | Integer | Optional | Capacity of Delivery medium in volume
capacityInWeight | Integer |Optional | Capacity of Delivery medium in weight
dob | String | Optional | Date of birth
gender | String |Optional | Gender. Ex - Male,Female
deliveryMediumMasterTypeCd | String |Optional | Delivery medium type. Ex - Truck, Delivery Boy
isOwnVehicleFl | String |Optional | Owner of vehicle. Ex - Owned, Company
vehicleNumber | String | Optional | Vehicle number to be assigned to the delivery medium
weeklyOffList  | String |Optional | Array of week's off days. Ex - Monday, Tuesday etc.
maxDistance | Integer |Optional | Max. allowed distance
licenseValidity | String |Optional | License validity date
deliveryMediumMapList.name | String | Optional | Name of language
shiftList.shiftStartTime  | String |Optional | Shift start time
shiftList.shiftEndTime  | String |Optional | Shift end time
dmPreference  | String | Optional | Preferred Pincode of Delivery medium

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
 "referenceId": null,
 "data": [
   {
     "lat": 19.11736939999999,
     "lng": 72.9103214,
     "shipmentReference": null,
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
"referenceId": null,
"data": null,
"hasError": false
}
```

### Request

<span class="post">POST</span>`https://api.loginextsolutions.com/TripApp/deliveryplanner/v1/plan`


### Request Body

Parameter | DataType |  Required | Description
-----------|-------|------- | ----------
routeName | String | Mandatory | Route name
startLocation.latitude | Double | Mandatory | Latitude of start location
startLocation.longitude | Double | Mandatory | Longitude of start location
vehicles | List | Mandatory | List of delivery medium
vehicles.name | String | Mandatory | Delivery medium name
vehicles.capacity.weight | Integer | Optional | Capacity of delivery medium
vehicles.capacity.volume | Integer | Optional | Volume of delivery medium
vehicles.type | List | Optional | Type of delivery medium
shipments | List | Mandatory | List of orders
shipments.name | String | Mandatory | Order no.
shipments.location.latitude | Double | Mandatory | Order Latitude
shipments.location.longitude | Double | Mandatory | Order Longitude
shipments.start | String | Mandatory | Order start time window
shipments.end | String | Mandatory | Order end time window
shipments.serviceTime | Integer | Optional | Order service time in mins.
shipments.weight | Integer | Optional | Weight of order in Kg.
shipments.volume | Integer | Optional | Volume of order in cc.
shipments.type | List | Mandatory | Type of orders



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
    "customerName" : "TestName",
    "locality" : "Andheri East",
    "subLocality" : "JVLR",
    "address" : "JVLR Powai",
    "deliverPhoneNumber" : "8888889999",
    "orderNo" : "35629171418620161809",
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

Param | DataType |  Required | Description
--------- | ------- | ---------- | ------------
orderNo | String | Mandatory |  Order No.
distributionCenter | String | Mandatory | Distribution center's name
paymentType | String | Mandatory | Payment mode. Ex: COD, Prepaid
packageValue | Double | Optional | Package Value (This will be used when paymentType is Prepaid)
cashOnDelivery | Double | Mandatory(if paymentType is COD) | Cash to be collected on delivery
cashOnPickup | Double | Optional | Cash to be given on pickup
locality | String | Mandatory | Locality name
subLocality | String | Mandatory | Sub-locality name
address | String | Optional | Address where delivery should be done
deliverPhoneNumber | String | Mandatory | End customer contact number
customerName | String | Mandatory | End customer name



## Create Order (Variable Pickup)

> Definition

```json
https://api.loginextsolutions.com/ShipmentApp/ondemand/v1/create
```

> Request Body

```json
[
  {
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

Param | DataType |  Required | Description
--------- | ------- | ---------- | ------------
orderNo | String | Mandatory |  Order No.
distributionCenter | String | Mandatory | Distribution center's name
shipmentOrderDt | Double | Mandatory | Order Date
deliverCapacityInVolume | Double | Optional | Weight of package in Kg.
deliverCapacityInUnits | Double | Optional | Volume of package in CC
paymentType | String | Optional | Payment mode. Ex: COD, Prepaid
packageValue | Double | Optional | Package Value (This will be used when paymentType is Prepaid)
cashOnDelivery | Double | Mandatory(if paymentType is Delivery) | Cash to be collected on delivery
cashOnPickup | Double | Optional | Cash to be given on pickup
isPartialDeliveryAllowedFl | String | Optional | Is Partial Delivery allowed. Ex: Y/N
pickupAccountCode | String | Mandatory | Pickup customer-id
pickupAccountName | String | Mandatory | Pickup customer name
pickupEmail | String | Optional | Pickup customer email-id
pickupPhoneNumber | String | Mandatory | Pickup customer contact number
pickupApartment | String | Mandatory | Pickup customer apartment
pickupStreetName | String | Mandatory | Pickup customer street name
pickupLandmark | String | Optional | Pickup customer landmark
pickupLocality | String | Mandatory | Pickup area name
pickupCountry | String | Mandatory | Pickup country code
pickupState | String | Mandatory | Pickup state code
pickupCity | String | Mandatory | Pickup city
pickupPincode | String | Mandatory | Pickup pincode
pickupStartTimeWindow | Date | Mandatory | Pickup Start time window of order
pickupEndTimeWindow | Date | Mandatory | Pickup End time window of order
pickupLatitude | Double | Optional | Latitude of pickup location
pickupLongitude | Double | Optional | Longitude of pickup location
pickupNotes | String | Optional | Pickup notes
deliverAccountCode | String | Mandatory | Deliver customer-id
deliverAccountName | String | Mandatory | Deliver customer name
deliverEmail | String | Optional | Deliver customer email-id
deliverPhoneNumber | String | Mandatory | Deliver customer contact number
deliverApartment | String | Mandatory | Deliver customer apartment
deliverStreetName | String | Mandatory | Deliver customer street name
deliverLandmark | String | Optional | Deliver customer landmark
deliverLocality | String | Mandatory | Deliver area name
deliverCountry | String | Mandatory | Deliver country code
deliverState | String | Mandatory | Deliver state code
deliverCity | String | Mandatory | Deliver city
deliverPincode | String | Mandatory | Deliver pincode
deliverStartTimeWindow | Date | Mandatory | Deliver Start time window of order
deliverEndTimeWindow | Date | Mandatory | Deliver End time window of order
deliverLatitude | Double | Optional | Latitude of deliver location
deliverLongitude | Double | Optional | Longitude of deliver location
deliverNotes | String | Optional | Deliver notes

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
  "timestamp":"2016-07-01 03:05:08"
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

## Update Order

> Response

```json
{
  "clientShipmentId": "RE0012",
  "orderState": "FORWARD",
  "shipmentCrateMapping": [],
  "startTimeWindow": "2017-08-16 16:45:00",
  "endTimeWindow": "2017-08-18 21:15:00",
  "orderReferenceId": "03ff479b970c47dcae0439323711fce1",
  "originAddr": "South Avenue,m,Mumbai,400076",
  "destinationAddr": "Capillary_Hypercity_PreProd Main Branch",
  "shipmentOrderTypeCd": "PICKUP",
  "clientNodeName": "Capillary_Hypercity_PreProd Main Branch",
  "clientNodeCd": "Capillary_Hypercity_PreProd Main Branch",
  "address": "314 - The Summit Business Bay, Opp. Cinemax Theatre, Off Andheri Kurla Road, Near Western Express Highway,Andheri East,  , ,, ,, ,, Mumbai, Maharashtra, INDIA, 400069",
  "deliveryType": ""
}
```


This notification is sent when an order is updated.

Param | DataType | Description
--------- | ------- | ----------
clientShipmentId | String | Order No.
orderState | String | FORWARD
shipmentCrateMapping | Array | Array of String of mapped crates
orderReferenceId | String | Order Reference Id
startTimeWindow | String | Order's start time window
endTimeWindow | String  | Order's end time window
originAddr | String  | Origin Address
destinationAddr | String  | Destination Address
shipmentOrderTypeCd | String  | Order type e.g. PICKUP or DELIVER
clientNodeName | String  | Node name Mapped for the client order
clientNodeCd | String  |  Code Mapped for the client order node
address | String  | Destination Address
deliveryType | String  | Delivery type

## Accept Order

> Response

```json
{
  "clientShipmentId": "TestOrder",
  "status": "ORDER ACCEPTED",
  "deliveryMediumName": "TestDM",
  "phoneNumber": 1234567890,
  "tripName": "TestTrip",
  "updatedOn": "2016-06-30 19:43:07",
  "deliveryMediumName": "Sandeep",
  "phoneNumber": 1234567890
}

```

This notification is sent when an order is accepted by a delivery boy.



### Response Parameters


Param | DataType | Description
--------- | ------- | ----------
clientShipmentId | String | Order No.
status | String | Status of the order
deliveryMediumName | String | Name of delivery medium
phoneNumber | Long | Delivery medium's phone no.
tripName | String | Trip name
updatedOn | String | Accept order timestamp
deliveryMediumName | String | Name of delivery medium
phoneNumber | Long | Delivery medium's phone no.

## Reject Order

> Response

```json
{
  "clientShipmentId": "TestOrder",
  "status": "ORDER REJECTED",
  "tripName": "TestTrip",
  "updatedOn": "2016-06-30 20:47:20",
  "reasonOfRejection": "Cannot reach on ETA"
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


## Cancel Order

> Response

```json
{
  "orderNo": "Order001",
  "notificationType": "CANCELLEDNOTIFICATION",
  "orderLeg": "DELIVER",
  "awbNumber": "AWB001",
  "deliveryMediumName": "Abhi.P",
  "phoneNumber": "9922904337",
  "orderState": "FORWARD",
  "customerName": "Name",
  "reason": "Customer Unavailable",
  "reasonCd": "Customer Unavailable Cd",
  "tripName": "TRIP-809",
  "customerCode": "TestCId",
  "cancellationTime": "2016-12-05 12:59:16",
  "cancelledBy": "Last Mile Demo User"
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

## Load Items

```json
{
  "orderNo": "TestOrderNo",  
  "orderState":"FORWARD",
  "orderLeg":"PICKUP",
  "awbNumber":"AWB001",
  "notificationType": "LOADITEMNOTIFICATION",
   "shipmentCrateMapping": [
      {
        "crateCd": "CRATE001",
        "crateType": "CRATE001",
        "statusCd": "CRATE001",
        "crateAmount": 100.30,
        "crateQuantity":3,
        "shipmentlineitems": [
          {
            "itemCd": "CODE001",
            "statusCd":"StatusCd",
            "itemName": "ITEM1",
            "itemPrice": 100,
            "itemQuantity": 1
          }
        ]
      }
    ]
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
  "vehicleNumber":"MH 03992"
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
  "orderNo": "Order001",
  "latitude": 19.1118589,
  "longitude": 72.9095639,
  "notificationType": "DELIVEREDNOTIFICATION",
  "orderLeg": "DELIVER",
  "awbNumber": "AWB001",
  "customerComment": "Test user comments",
  "customerRating": 5,
  "deliveryMediumName": "Suresh",
  "phoneNumber": 1234567864,
  "orderState": "FORWARD",
  "customerName": "Customer123",
  "deliveryTime": "2016-11-19 06:11:27",
  "cashAmount": 0,
  "deliveryLocationType": "",
  "transactionId": "12456",
  "paymentMode": "PREPAID",
  "actualCashAmount": 120,
  "recipientName": "Rahul"
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
orderLeg | String | Order leg Ex: PICKUP, DELIVER
awbNumber | String | AWB Number for the order
customerComment | String | Customer comments
customerRating | Integer | Rating provided by customer
deliveryMediumName | String | Name of delivery medium
phoneNumber | Long | Delivery medium's phone no.
orderState | String | State of order. Ex: FORWARD, REVERSE
customerName | String | Customer name
deliveryTime | String | Delivery timestamp
cashAmount | Double | Cash amount to collect
deliveryLocationType | String | Delivery Location
transactionId | String | Transaction id
actualCashAmount | Double | Cash amount actually collected
recipientName | String | Name of recipient


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
        "shipmentLineItemsList": [
          {
            "itemCd": "CODE001",
            "itemType":"Type1",
            "statusCd":"StatusCd",
            "itemName": "ITEM1",
            "itemPrice": 100,
            "itemQuantity": 1,
            "itemWeight": 100,
            "actualItemQuantity": 5
          }
        ]
      }
  ]
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
shipmentCrateMappingList.shipmentlineitems.itemCd | String | Item code
shipmentCrateMappingList.shipmentlineitems.itemType | String | Item type
shipmentCrateMappingList.shipmentlineitems.statusCd | String | Item status. It will be LOADED.
shipmentCrateMappingList.shipmentlineitems.itemName | String | Name of item
shipmentCrateMappingList.shipmentlineitems.itemPrice | Double | Item price
shipmentCrateMappingList.shipmentlineitems.itemQuantity | Integer | Item quantity
shipmentCrateMappingList.shipmentlineitems.itemWeight | Integer | Item weight
shipmentCrateMappingList.shipmentlineitems.actualItemQuantity | Integer | Unloaded Item quantity


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
  "recipientName": ""
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
  "orderState": "FORWARD"
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
  "reasonCd": ""
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
  "notificationType": "STARTTRIP",
  "deliveryMediumName": "TestDM",
  "phoneNumber": 1234567546,
  "startTime": "2016-11-19 06:42:44",
  "tripName": "TRIP-84",
  "vehicleNumber":"MH084819",
  "driverName":"Rahul",
  "clientShipmentIds": [
    "Order001",
    "Order002"
  ]
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
UNITED ARAB EMIRATES|AE
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
