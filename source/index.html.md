---
title: API Reference

language_tabs:
  - json

toc_footers:
  - <a href='#'>Sign Up for a Developer Key</a>
  - <a href='https://github.com/tripit/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true
---

# Introduction

Loginext welcomes you to the world of organised logistics. 

This API documentation will help you, intergrate your software platform with loginext's for end to end logistics management. 

# Authentication

##Authenticate

Loginext uses Basic Authentication to provide authorized access to its API.

Use the following URL endpoint to authenticate userself as a user of this API.

### HTTP Request

`POST http://api.loginextsolutions.com/LoginApp/login/authenticate`

### HTTP Request Headers

Header | Sample Value | Brief Info
--------- | ------- | -------------
Content-Type | application/json | Json request

### HTTP Request Body

Header | Sample Value 
--------- | ------- 
Content-Type | application/x-www-form-urlencoded

### HTTP Request Parameters

Param Name | Value 
--------- | ------- 
username | your username
password | your password 

### HTTP Response Headers

Header | Sample Value 
--------- | ------- 
WWW-Authenticate | BASIC 075b8961-bd02-454c-83eb-259f965f313f
CLIENT_SECRET_KEY | $2a$08$bCi0ja4B5S02BKQt3VdxNuReERpSV8SiAbwVrHNyhC7mD

##Invalidate

This endpoint invalidates a user. 

### HTTP Request

`POST http://api.loginextsolutions.com/LoginApp/token/refresh`


### HTTP Request Headers

Header | Sample Value 
--------- | ------- | -------------
WWW-Authenticate | BASIC 075b8961-bd02-454c-83eb-259f965f313f
CLIENT_SECRET_KEY | $2a$08$bCi0ja4B5S02BKQt3VdxNuReERpSV8SiAbwVrHNyhC7mD

<aside class="success">Response headers will contain new session token and authentication key.</aside>


# Mile 2.0

## Create Order

> Create Order - Sample Request

```json

```
> Defination

> Create Order - Sample Response

```json
{
  "status": 200,
  "message": "success",
  "data": null,
  "hasError": false
}

```

This endpoint creates a new order.

### HTTP Request

`POST http://api.loginextsolutions.com/ShipmentApp/mile/v1/create`

### HTTP Request Headers

Header | Sample Value | Brief Info
--------- | ------- | -------------
Content-Type | application/json | Json request
WWW-Authenticate | BASIC 51bbe3f7-1671-476c-818a-e7fbbca10202 | Authentication token
CLIENT_SECRET_KEY | $2a$08$LQEqG3s.LF2jBt7Baq| Authentication key


## Create Return Order

> Create Return Order - Sample Request

```json
["863fe69239bc4f738ca275a809c3b2e2"]
```

> Create Return Order - Sample Response

```json
{
  "status": 200,
  "message": "success",
  "data": null,
  "hasError": false
}

```

This endpoint creates a return order.

### HTTP Request

`POST http://api.loginextsolutions.com/ShipmentApp/mile/v1/create/return`

### HTTP Request Headers

Header | Sample Value | Brief Info
--------- | ------- | -------------
Content-Type | application/json | Json request
WWW-Authenticate | BASIC 51bbe3f7-1671-476c-818a-e7fbbca10202 | Authentication token
CLIENT_SECRET_KEY | $2a$08$LQEqG3s.LF2jBt7Baq| Authentication key

## Cancel Order

> Cancel Order - Sample Request

```json
["e0eaebdd84ac4c40af72d827ab610090"]
```

> Cancel Order - Sample Response

```json
{
  "status": 200,
  "message": "success",
  "data": "No of orders cancelled:1",
  "hasError": false
}

```

This endpoint cancels an order.

### HTTP Request

`POST http://api.loginextsolutions.com/ShipmentApp/mile/v1/cancel`

### HTTP Request Headers

Header | Sample Value | Brief Info
--------- | ------- | -------------
Content-Type | application/json | Json request
WWW-Authenticate | BASIC 51bbe3f7-1671-476c-818a-e7fbbca10202 | Authentication token
CLIENT_SECRET_KEY | $2a$08$LQEqG3s.LF2jBt7Baq| Authentication key

## Get Status of Order

> Get Status - Sample Request

```json
["c8714df4347911e6829f000d3aa04450"]
```

> Get Status - Sample Response

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

This endpoint gets an order status.

### HTTP Request

`POST http://api.loginextsolutions.com/ShipmentApp/mile/v1/status`

### HTTP Request Headers

Header | Sample Value | Brief Info
--------- | ------- | -------------
Content-Type | application/json | Json request
WWW-Authenticate | BASIC 51bbe3f7-1671-476c-818a-e7fbbca10202 | Authentication token
CLIENT_SECRET_KEY | $2a$08$LQEqG3s.LF2jBt7Baq| Authentication key


## Add Crates

> Add Crates - Sample Request

```json
[
  {
    "shipmentCrates": [
      {
        "crateCd": "Crate1",
        "shipmentlineitems": [
          {
            "itemCd": "Item1",
            "itemName": "",
            "itemPrice": 33,
            "itemQuantity": 10,
            "itemType": "",
            "itemWeight": 0,
            "isDeleteFl": "N"
          }
        ],
        "isDeleteFl": "N"
      },
      {
        "crateCd": "Crate2",
        "shipmentlineitems": [
          {
            "itemCd": "Item2",
            "itemName": "",
            "itemPrice": 33,
            "itemQuantity": 10,
            "itemType": "",
            "itemWeight": 0,
            "isDeleteFl": "N"
          }
        ],
        "isDeleteFl": "N"
      }
    ],
    "referenceId": "c8714df4347911e6829f000d3aa04450"
  }
]
```

> Add Crates - Sample Response

```json
{
  "status": 200,
  "message": "success",
  "data": null,
  "hasError": false
}

```

This endpoint adds crates to an existing order.

### HTTP Request

`POST http://api.loginextsolutions.com/ShipmentApp/mile/v1/crate`

### HTTP Request Headers

Header | Sample Value | Brief Info
--------- | ------- | -------------
Content-Type | application/json | Json request
WWW-Authenticate | BASIC 51bbe3f7-1671-476c-818a-e7fbbca10202 | Authentication token
CLIENT_SECRET_KEY | $2a$08$LQEqG3s.LF2jBt7Baq| Authentication key


## Start Trip 

> Start Trip - Sample Request

```json
[
    "a9be39b9347911e6829f000d3aa04450"    
]
```

> Start Trip - Sample Response

```json
{
  "status": 200,
  "message": "1 trip(s) started",
  "data": true,
  "hasError": false
}

```

This endpoint starts a trip.

### HTTP Request

`POST http://api.loginextsolutions.com/TripApp/mile/v1/trip/start`

### HTTP Request Headers

Header | Sample Value | Brief Info
--------- | ------- | -------------
Content-Type | application/json | Json request
WWW-Authenticate | BASIC 8bce7b1b-9762-4de7-b9cd-976ecf38b6a0 | Authentication token
CLIENT_SECRET_KEY | $2a$08$npX3e6RD6zJFHcvFV469D.XtRpCwCQwZ3YlsEpERDcd.c2jmabLsG| Authentication key

## Stop Trip 

> Stop Trip - Sample Request

```json
[{
    "tripReferenceId":"a9be39b9347911e6829f000d3aa04450",
    "notDispatchedOrders":["c8714df4347911e6829f000d3aa04450"],
    "deliveredOrders":["c8714cac347911e6829f000d3aa04450"]
}
]
```

> Stop Trip - Sample Response

```json
{
  "status": 200,
  "message": "Trips ended successfully",
  "data": true,
  "hasError": false
}

```

This endpoint stops a trip.

### HTTP Request

`POST http://api.loginextsolutions.com/TripApp/mile/v1/trip/stop`
  
### HTTP Request Headers

Header | Sample Value | Brief Info
--------- | ------- | -------------
Content-Type | application/json | Json request
WWW-Authenticate | BASIC 8bce7b1b-9762-4de7-b9cd-976ecf38b6a0 | Authentication token
CLIENT_SECRET_KEY | $2a$08$npX3e6RD6zJFHcvFV469D.XtRpCwCQwZ3YlsEpERDcd.c2jmabLsG| Authentication key

## Track Last Location

> Track Last Location - Sample Request

```json
http://api.loginextsolutions.com/TrackingApp/mile/v1/track/lastlocation?shipmentReferences=25a565a9c9d540cd9e6c02fae890cb67,c7afc8b1b97b48468c3417aa425eff81,27121903f4f047bcb378a6457bee2fec,21b538edf7f047028334480036179c70
```

> Track Last Location - Sample Response

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

This endpoint fetches the latest location for the requested shipments

### HTTP Request

`GET http://api.loginextsolutions.com/TrackingApp/mile/v1/track/lastlocation`
  
### HTTP Request Headers

Header | Sample Value | Brief Info
--------- | ------- | -------------
Content-Type | application/json | Json request
WWW-Authenticate | BASIC 8bce7b1b-9762-4de7-b9cd-976ecf38b6a0 | Authentication token
CLIENT_SECRET_KEY | $2a$08$npX3e6RD6zJFHcvFV469D.XtRpCwCQwZ3YlsEpERDcd.c2jmabLsG| Authentication key



# Haul 2.0

## Create Vehicle 

> Create Vehicle - Sample Request

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
        		"barcode”:”LN12345678”
    		}
    }
]  
```

> Create Vehicle - Sample Response

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

This endpoint creates a new Vehicle.

### HTTP Request

`POST http://api.loginextsolutions.com/VehicleApp/v1/vehicle/create`

### HTTP Request Headers

Header | Sample Value | Brief Info
--------- | ------- | -------------
Content-Type | application/json | Json request
WWW-Authenticate | BASIC 51bbe3f7-1671-476c-818a-e7fbbca10202 | Authentication token
CLIENT_SECRET_KEY | $2a$08$LQEqG3s.LF2jBt7Baq| Authentication key


### HTTP Request Parameters

Parameter | Type |  Required | Description
-----------|-------|------- | ---------- 
vehicleNumber | String | Mandatory | Vehicle Number.
vehicleMake | String | Optional | Make of the vehicle.
vehicleModel | String |Optional | Model of the vehicle.
typeOfBody | String |Optional | Type of Body.
unladdenWeight | Integer |Optional | Unladen weight of the vehicle.
capacityInWeight | Integer |Optional | Capacity of vehicle in (Kgs).
capacityInUnits | Integer |Optional | Capacity of vehicle in (Units).
capacityInVolume | Integer |Optional | Capacity of vehicle in (Cc).
chasisNumber | String |Optional | Chasis number.
engineNumber | String |Optional | Engine number.
markerName | String |Optional | 
registrationNumber | String |Optional | Registration Number of the vehicle.
pucValidity | Date |Optional | PUC Validity Date
insuranceValidity | Date |Optional | Insurance Validity Date
vehiclePermit | String |Optional | Comma separated list of states within which vehicle is permitted to travel.
ownership | String |Optional | Vehicle owned by. Possible values (company OR vendor)
ownerName | String |Optional | Name of the owner of the vehicle.
transporter | String |Optional |
financer | String |Optional |
accidentHistory | String |Optional | Previous accident history associated with the vehicle.
rentStartDate | Date |Optional | If ownership is “vendor” then only this field is valid.
rentEndDate  | Date |Optional | If ownership is “vendor” then only this field is valid.
deviceId.barcode | String |Optional | Barcode of the tracker.

## Read Vehicle (Single)


> Read Vehicle - Sample Response

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

This endpoint returns the vehicle details for the client with the given Reference ID.

### HTTP Request

`POST http://api.loginextsolutions.com/VehicleApp/v1/vehicle/:reference_id`

### HTTP Request Headers

Header | Sample Value | Brief Info
--------- | ------- | -------------
Content-Type | application/json | Json request
WWW-Authenticate | BASIC 51bbe3f7-1671-476c-818a-e7fbbca10202 | Authentication token
CLIENT_SECRET_KEY | $2a$08$LQEqG3s.LF2jBt7Baq| Authentication key

### HTTP Request Parameters

Parameter | Type |  Required | Description
-----------|-------|------- | ---------- 
reference_id | String | Mandatory | Reference Id associated with the vehicle.


## Read Vehicle 


> Read Vehicle - Sample Response

```json
{
  "status": 200,
  "message": "success",
  "data": {
    "totalCount": 119,
    "otherCount": 0,
    "results": [
      {
        "createdOnDt": null,
        "updatedOnDt": null,
        "createdByUserId": null,
        "updatedByUserId": null,
        "isDeleteFl": null,
        "isActiveFl": true,
        "vehicleId": 1182,
        "vehicleName": null,
        "guid": null,
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
        "clientBranchId": null,
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
        "removedRegistrationMediaId": null,
        "removedInsuranceMediaId": null,
        "removedPucMediaId": null,
        "deviceId": {
          "deviceId": null,
          "barcode": "Not Assigned",
          "statusCd": null,
          "trackeeId": null
        },
        "clientId": null,
        "tripDetail": null,
        "insuranceAlertWindow": null,
        "pucAlertWindow": null,
        "lastInsuranceAlertSentDt": null,
        "lastPUCAlertSentDt": null,
        "client_Id": null,
        "gpsStatus": null,
        "speed": null,
        "branchName": null,
        "referenceId": "538649a7b9fc45be8d75b5932cc8ab60"
      },
      {
        "createdOnDt": null,
        "updatedOnDt": null,
        "createdByUserId": null,
        "updatedByUserId": null,
        "isDeleteFl": null,
        "isActiveFl": true,
        "vehicleId": 1170,
        "vehicleName": null,
        "guid": null,
        "vehicleNumber": "Mh04HD1531",
        "vehicleMake": null,
        "vehicleModel": null,
        "vehicleType": null,
        "typeOfBody": "",
        "previousVehiclenumber": null,
        "unladdenWeight": null,
        "capacityInUnits": 7500,
        "capacityInVolume": null,
        "capacityInWeight": null,
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
        "clientBranchId": null,
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
        "removedRegistrationMediaId": null,
        "removedInsuranceMediaId": null,
        "removedPucMediaId": null,
        "deviceId": {
          "deviceId": 3182,
          "barcode": "LN00700416",
          "statusCd": null,
          "trackeeId": "358899057353677"
        },
        "clientId": null,
        "tripDetail": null,
        "insuranceAlertWindow": null,
        "pucAlertWindow": null,
        "lastInsuranceAlertSentDt": null,
        "lastPUCAlertSentDt": null,
        "client_Id": null,
        "gpsStatus": null,
        "speed": null,
        "branchName": null,
        "referenceId": "f9d77411a3f94f58910e241019a0ee4e"
      }
    ]
  },
  "hasError": false
}

```

This endpoint lists an existing Vehicles for the client.

### HTTP Request

`POST http://api.loginextsolutions.com/VehicleApp/v1/vehicle`

### HTTP Request Headers

Header | Sample Value | Brief Info
--------- | ------- | -------------
Content-Type | application/json | Json request
WWW-Authenticate | BASIC 51bbe3f7-1671-476c-818a-e7fbbca10202 | Authentication token
CLIENT_SECRET_KEY | $2a$08$LQEqG3s.LF2jBt7Baq| Authentication key

## Update Vehicle

> Update Vehicle - Sample Request

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

> Update Vehicle - Sample Response

```json
{
  "status": 200,
  "message": "success",
  "data": null,
  "hasError": false
}

```

This endpoint updates the vehicle details with given reference id.

### HTTP Request

`PUT http://api.loginextsolutions.com/VehicleApp/v1/vehicle`

### HTTP Request Headers

Header | Sample Value | Brief Info
--------- | ------- | -------------
Content-Type | application/json | Json request
WWW-Authenticate | BASIC 51bbe3f7-1671-476c-818a-e7fbbca10202 | Authentication token
CLIENT_SECRET_KEY | $2a$08$LQEqG3s.LF2jBt7Baq| Authentication key

### HTTP Request Parameters

Parameter | Type |  Required | Description
-----------|-------|------- | ---------- 
reference_id | String | Mandatory | Reference Id associated with the vehicle.
vehicleNumber | String | Mandatory | Vehicle Number.
vehicleMake | String | Optional | Make of the vehicle.
vehicleModel | String |Optional | Model of the vehicle.
typeOfBody | String |Optional | Type of Body.
unladdenWeight | Integer |Optional | Unladen weight of the vehicle.
capacityInWeight | Integer |Optional | Capacity of vehicle in (Kgs).
capacityInUnits | Integer |Optional | Capacity of vehicle in (Units).
capacityInVolume | Integer |Optional | Capacity of vehicle in (Cc).
chasisNumber | String |Optional | Chasis number.
engineNumber | String |Optional | Engine number.
markerName | String |Optional | 
registrationNumber | String |Optional | Registration Number of the vehicle.
pucValidity | Date |Optional | PUC Validity Date
insuranceValidity | Date |Optional | Insurance Validity Date
vehiclePermit | String |Optional | Comma separated list of states within which vehicle is permitted to travel.
ownership | String |Optional | Vehicle owned by. Possible values (company OR vendor)
ownerName | String |Optional | Name of the owner of the vehicle.
transporter | String |Optional |
financer | String |Optional |
accidentHistory | String |Optional | Previous accident history associated with the vehicle.
rentStartDate | Date |Optional | If ownership is “vendor” then only this field is valid.
rentEndDate  | Date |Optional | If ownership is “vendor” then only this field is valid.
deviceId.barcode | String |Optional | Barcode of the tracker.


## Delete Vehicle

> Delete Vehicle - Sample Request

```json
["a9be39b9347911e6829f000d3aa04450"]
```

> Delete Vehicle - Sample Response

```json
{
  "status": 200,
  "message": "success",
  "data": null,
  "hasError": false
}

```

This endpoint deletes the Vehicle with given list of reference IDs.

### HTTP Request

`DELETE http://api.loginextsolutions.com/VehicleApp/v1/vehicle`

### HTTP Request Headers

Header | Sample Value | Brief Info
--------- | ------- | -------------
Content-Type | application/json | Json request
WWW-Authenticate | BASIC 51bbe3f7-1671-476c-818a-e7fbbca10202 | Authentication token
CLIENT_SECRET_KEY | $2a$08$LQEqG3s.LF2jBt7Baq| Authentication key

### HTTP Request Parameters

Parameter | Type |  Required | Description
-----------|-------|------- | ---------- 
reference_ids | List (String) | Mandatory | Reference Id associated with the vehicle.


## Create Driver

> Create Driver - Sample Request

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

>  Create Driver - Sample Response

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

This endpoint creates a new driver.

### HTTP Request

`POST http://api.loginextsolutions.com/DriverApp/haul/v1/driver/create`

### HTTP Request Headers

Header | Sample Value | Brief Info
--------- | ------- | -------------
Content-Type | application/json | Json request
WWW-Authenticate | BASIC 51bbe3f7-1671-476c-818a-e7fbbca10202 | Authentication token
CLIENT_SECRET_KEY | $2a$08$LQEqG3s.LF2jBt7Baq| Authentication key

### HTTP Request Parameters

### HTTP Request Parameters

Param | DataType |  Required | Brief Info
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
addressList.countryShortCode | String | Mandatory | Country short code
addressList.stateShortCode | String | Mandatory | State short code
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






## Read Driver

> Read Driver - Sample Request

```json
["1c3a551f47534b98a29d916b0405fd6d"]
```

> Read Driver - Sample Response

```json
{
  "status": 200,
  "message": "success",
  "data": [
    {
      "createdOnDt": null,
      "updatedOnDt": null,
      "createdByUserId": null,
      "updatedByUserId": null,
      "isDeleteFl": null,
      "isActiveFl": true,
      "driverId": 772,
      "driverName": "Test_Driver",
      "clientId": null,
      "phoneNumber": "1234565632",
      "emailId": "test@testing.com",
      "idProof": null,
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
      "clientBranchId": 1402,
      "defaultVehicle": null,
      "vehicleNumber": null,
      "licenseAlertWindow": null,
      "mediaLocation": null,
      "fileName": null,
      "mediaPurposeCode": null,
      "entity": null,
      "attendance": null,
      "workHour": null,
      "status": null,
      "dateOfBirth": 1465776000000,
      "experience": "11",
      "maritalStatus": "married",
      "gender": "female",
      "languageList": [
        {
          "createdOnDt": null,
          "updatedOnDt": null,
          "createdByUserId": null,
          "updatedByUserId": null,
          "isDeleteFl": null,
          "isActiveFl": true,
          "id": 90,
          "guid": null,
          "name": "English",
          "code": null,
          "driverId": null,
          "deliveryMediumMasterId": null
        },
        {
          "createdOnDt": null,
          "updatedOnDt": null,
          "createdByUserId": null,
          "updatedByUserId": null,
          "isDeleteFl": null,
          "isActiveFl": true,
          "id": 91,
          "guid": null,
          "name": "Hindi",
          "code": null,
          "driverId": null,
          "deliveryMediumMasterId": null
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
          "driverId": 772,
          "createdByUserId": null,
          "startTime": null,
          "endTime": null,
          "deliveryMediumMasterId": null
        }
      ],
      "addressList": [],
      "tripId": null,
      "lat": null,
      "lng": null,
      "isPresent": null,
      "tripStatus": null,
      "batteryPerc": null,
      "mediaList": null,
      "addressProofId": null,
      "removeAddressProofId": null,
      "removeLicenseProof": null,
      "lastLicenseAlertSentDt": null,
      "clientBranchName": null,
      "previousPhoneNumber": null,
      "referenceId": "1c3a551f47534b98a29d916b0405fd6d",
      "guid": null,
      "licenseProof": null
    }
  ],
  "hasError": false
}

```

This endpoint lists an existing driver.

### HTTP Request

`POST http://api.loginextsolutions.com/DriverApp/haul/v1/driver/list`

### HTTP Request Headers

Header | Sample Value | Brief Info
--------- | ------- | -------------
Content-Type | application/json | Json request
WWW-Authenticate | BASIC 51bbe3f7-1671-476c-818a-e7fbbca10202 | Authentication token
CLIENT_SECRET_KEY | $2a$08$LQEqG3s.LF2jBt7Baq| Authentication key

## Update Driver

> Update Driver - Sample Request

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

> Update Driver - Sample Response

```json
{
  "status": 200,
  "message": "success",
  "data": null,
  "hasError": false
}

```

This endpoint updates an existing driver.

### HTTP Request

`PUT http://api.loginextsolutions.com/DriverApp/haul/v1/driver/update`

### HTTP Request Headers

Header | Sample Value | Brief Info
--------- | ------- | -------------
Content-Type | application/json | Json request
WWW-Authenticate | BASIC 51bbe3f7-1671-476c-818a-e7fbbca10202 | Authentication token
CLIENT_SECRET_KEY | $2a$08$LQEqG3s.LF2jBt7Baq| Authentication key

### HTTP Request Parameters

Param | DataType |  Required | Brief Info
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
addressList.countryShortCode | String | Mandatory | Country short code
addressList.stateShortCode | String | Mandatory | State short code
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

> Delete Driver - Sample Request

```json
["e0eaebdd84ac4c40af72d827ab610090"]
```

> Delete Driver - Sample Response

```json
{
  "status": 200,
  "message": "success",
  "data": null,
  "hasError": false
}

```

This endpoint deletes an existing driver.

### HTTP Request

`DELETE http://api.loginextsolutions.com/DriverApp/haul/v1/driver/delete`

### HTTP Request Headers

Header | Sample Value | Brief Info
--------- | ------- | -------------
Content-Type | application/json | Json request
WWW-Authenticate | BASIC 51bbe3f7-1671-476c-818a-e7fbbca10202 | Authentication token
CLIENT_SECRET_KEY | $2a$08$LQEqG3s.LF2jBt7Baq| Authentication key


## Create Trip

> Create Trip - Sample Request

```json
{
  "shipmentType": "Bag",
  sealNumber:"SN-123",
  "lrNumber":"LR123",
  "originAddr": "CNND",
  "destinationAddr": "NAGD",
  "name": "CNN-NAG-12221",
  "packageWeight": 6,
  "packageValue": 8,
  "packageVolume": 10,
  "vehicleReportingDate": "2016-02-27T18:30:00.000Z",
  "vehicleReportingTime": "1970-02-01T07:30:00.000Z",
  "modeOfTransport": "ROAD",
  "vehicleNumber": "MH40AK0175",
  "barcode": "LN00590915",
  "startNow":false
}
```

> Create Trip - Sample Response

```json
{
  "status": 200,
  "message": "Trip created successfully.Reference Id for future access:1880d6906e9d426995b815a83aa3927f",
  "data": null,
  "hasError": false
}

```

This endpoint creates a new trip.

### HTTP Request

`POST http://api.loginextsolutions.com/TripApp/haul/v1/trip/create`

### HTTP Request Headers

Header | Sample Value | Brief Info
--------- | ------- | -------------
Content-Type | application/json | Json request
WWW-Authenticate | BASIC f522631c-490c-46fd-9f79-ca8d14a704d7 | Authentication token
CLIENT_SECRET_KEY | $2a$08$V4u/aPJrPq/AxqQM6myUYON/gdLw4KfnRPBPZvvHAyW37UGiwakX6| Authentication key

### HTTP Request Parameters

Parameter | Type |  Required | Description
-----------|-------|------- | ---------- 
shipmentType | String | Mandatory | Type of the Shipment being created.Examples:"Bag","Package","Manifest"
originAddr | String |Mandatory | Origin point of the trip.Examples:-AMDD,BLRX
destinationAddr | String |Mandatory | Destination point of the trip.Examples:-CNND,BOMX
name | String |Mandatory | Name of the trip.Has to be unique.Example:-CNND-BOMX-123_456
packageWeight | Integer |Optional | Capacity of the shipment in terms of Kgs
packageValue | Integer |Optional | Capacity of the shipment in terms of the number of units present in it
packageVolume | Integer |Optional | Capacity of the shipment in terms of cc
vehicleReportingDate | Date |Mandatory | Reporting date of the vehicle at the origin hub
vehicleReportingTime | Date |Mandatory | Reporting time of the vehicle at the origin hub
modeOfTransport | String |Mandatory | Mode of transit for the trip.Examples:-ROAD,AIR,RAIL
lrNumber | String | Mandatory(Conditional) | Lorry Receipt Number if modeOfTransport selected as ROAD.
flightNum| String |Mandatory(Conditional) | Flight Number if modeOfTransport selected as AIR.
trainNum| String |Mandatory(Conditional) | Rail Number if modeOfTransport selected as RAIL.
driverName | String |Optional | Name of the driver
vehicleNumber | String |Optional | Vehicle Number.
barcode | String |Mandatory | Barcode of the tracker used for attaching to vehicle during trip



## Start Trip

> Start Trip - Sample Request

```json
[
    "1880d6906e9d426995b815a83aa3927f"
]
```

> Start Trip - Sample Response

```json
{
  "status": 200,
  "message": "Trips started successfully",
  "data": null,
  "hasError": false
}

```

This endpoint starts a trip.

### HTTP Request

`PUT http://api.loginextsolutions.com/TripApp/haul/v1/trip/start`

### HTTP Request Headers

Header | Sample Value | Brief Info
--------- | ------- | -------------
Content-Type | application/json | Json request
WWW-Authenticate | BASIC f522631c-490c-46fd-9f79-ca8d14a704d7 | Authentication token
CLIENT_SECRET_KEY | $2a$08$V4u/aPJrPq/AxqQM6myUYON/gdLw4KfnRPBPZvvHAyW37UGiwakX6| Authentication key

## Stop Trip

> Stop Trip - Sample Request

```json
[
    "1880d6906e9d426995b815a83aa3927f"
]
```

> Stop Trip - Sample Response

```json
{
  "status": 200,
  "message": "Trips ended successfully",
  "data": null,
  "hasError": false
}

```

This endpoint stops a trip.

### HTTP Request

`POST http://api.loginextsolutions.com/TripApp/haul/v1/trip/stop`

### HTTP Request Headers

Header | Sample Value | Brief Info
--------- | ------- | -------------
Content-Type | application/json | Json request
WWW-Authenticate | BASIC f522631c-490c-46fd-9f79-ca8d14a704d7 | Authentication token
CLIENT_SECRET_KEY | $2a$08$V4u/aPJrPq/AxqQM6myUYON/gdLw4KfnRPBPZvvHAyW37UGiwakX6| Authentication key

## Trip iFrame

This endpoint is to get iFrame view of a trip.

### HTTP Request

`GET https://api.loginextsolutions.com/haul/track/#/?aid=f522631c-490c-46fd-9f79-ca8d14a704d7&key=$2a$08$Vg6jJLhrHEsqOUfD1EJHyuelHeIgcUyvgTfGaeRmnzNr5jGVi86k3&tripname=TestTripName`

### HTTP Request Parameters

Parameter | Sample Value | Brief Info
--------- | ------- | -------------
aid | f522631c-490c-46fd-9f79-ca8d14a704d7 | Value of authentication token without 'BASIC' keyword
key | $2a$08$Vg6jJLhrHEsqOUfD1EJHyuelHeIgcUyvgT | Client Secret Key
tripname | TestTripName| Trip name 

## Track Last Location

> Track Last Location - Sample Request

```json
http://api.loginextsolutions.com/TrackingApp/haul/v1/track/lastlocation?shipmentReferences=25a565a9c9d540cd9e6c02fae890cb67,c7afc8b1b97b48468c3417aa425eff81,27121903f4f047bcb378a6457bee2fec,21b538edf7f047028334480036179c70
```

> Track Last Location - Sample Response

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

This endpoint fetches the latest location for the requested shipments

### HTTP Request

`GET http://api.loginextsolutions.com/TrackingApp/haul/v1/track/lastlocation`
  
### HTTP Request Headers

Header | Sample Value | Brief Info
--------- | ------- | -------------
Content-Type | application/json | Json request
WWW-Authenticate | BASIC 8bce7b1b-9762-4de7-b9cd-976ecf38b6a0 | Authentication token
CLIENT_SECRET_KEY | $2a$08$npX3e6RD6zJFHcvFV469D.XtRpCwCQwZ3YlsEpERDcd.c2jmabLsG| Authentication key

# Webhooks

## Accept Order

> Accept Order - Sample Response

```json
{
  "clientShipmentId": "TestOrder",
  "status": "ORDER ACCEPTED",
  "deliveryMediumName": "TestDM",
  "phoneNumber": 1234567890,
  "tripName": "TestTrip",
  "updatedOn": "2016-06-30 19:43:07"
}

```

This notification is sent when an order is accepted by a delivery boy.



### HTTP Response Parameters

Key | Brief Info
--------- | -------
clientShipmentId | Order no.
status | Status of the order
deliveryMediumName | Name of delivery medium who accepted the order
phoneNumber | Phone no. of delivery medium
tripName | Trip name
updatedOn | Accept order timestamp

## Reject Order

> Reject Order - Sample Response

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



### HTTP Response Parameters

Key | Brief Info
--------- | -------
clientShipmentId | Order no.
status | Status of the order
tripName | Trip name
updatedOn | Accept order timestamp
reasonOfRejection | Reason provided by Delivery medium while rejecting the order

## Delivered

> Delivery - Sample Response

```json
{
  "clientShipmentId": "TestOrder",
  "latitude": 28.283528,
  "longitude": 76.921535,
  "notificationType": "DELIVEREDNOTIFICATION",
  "customerComment": "Test comments",
  "customerRating": 5,
  "deliveryTime": "2016-06-30 19:12:49",
  "cashAmount": 100,
  "deliveryLocationType": "Customer",
  "transactionId": "0",
  "actualCashAmount": 100,
  "recipientName": "RecipientName"
}

```

This notification is sent when an order is delivered by a delivery boy to customer.



### HTTP Response Parameters

Key | Brief Info
--------- | -------
clientShipmentId | Order no.
latitude | Latitude where order was delivered
longitude | Longitude where order was delivered
notificationType | DELIVEREDNOTIFICATION
customerComment | Customer comments 
customerRating | Rating provided by customer
deliveryTime | Delivery timestamp
cashAmount | Cash amount to collect
deliveryLocationType | Delivery Location
transactionId | Transaction id
actualCashAmount | Cash amount actually collected
recipientName | Name of recipient


## Partially Delivered

> Partial Delivery - Sample Response

```json
{
  "clientShipmentId": "TestOrder",
  "statusCd": "PARTIALLYDELIVERED",
  "notificationType": "PARTIALDELIVERYNOTIFICATION",
  "customerComments": "",
  "customerRating": 4,
  "reason": "Customer not accepting",
  "reasonCd": "",
  "cashAmount": 1,
  "transactionId": "",
  "actualCashAmount": 100,
  "shipmentCrateMappingList": [],
  "recipientName": "John2"
}

```

This notification is sent when an order is partially delivered by a delivery boy to customer.



### HTTP Response Parameters

Key | Brief Info
--------- | -------
clientShipmentId | Order no.
statusCd | PARTIALLYDELIVERED
notificationType | PARTIALDELIVERYNOTIFICATION
customerComments | Customer comments 
customerRating | Rating provided by customer
reason | Reason for the order being partially delivered
reasonCd | Reason code
cashAmount | Cash amount to be collected
transactionId | Transaction id
actualCashAmount | Cash amount actually collected
shipmentCrateMappingList | Shipment crates
recipientName | Name of recipient

## Not Delivered

> Not Delivered - Sample Response

```json
{
  "clientShipmentId": "TestOrder",
  "notificationType": "NOTDELIVEREDNOTIFICATION",
  "customerComments": "Test comments",
  "customerRating": 5,
  "reason": "Product damaged in transit",
  "reasonCd": "",
  "deliveryTime": "2016-06-30 19:12:49",
  "deliveryLocationType": "Customer",
  "recipientName": "RecipientName"
}

```

This notification is sent when an order is not delivered by a delivery boy.



### HTTP Response Parameters

Key | Brief Info
--------- | -------
clientShipmentId | Order no.
notificationType | NOTDELIVEREDNOTIFICATION
customerComments | Customer comments 
customerRating | Rating provided by customer
reason | Reason for the order not delivered
reasonCd | Reason code
deliveryTime | Undelivered timestamp
deliveryLocationType | Delivery location
recipientName | Name of recipient

## Pickedup

> Pickup Order - Sample Response

```json
{
  "clientShipmentId": "TestOrder",
  "latitude": 28.283528,
  "longitude": 76.921535,
  "pickedUpTime": "2016-06-30 19:10:56",
  "status": "PICKEDUPNOTIFICATION"
}

```

This notification is sent when an order is picked up by a delivery boy.



### HTTP Response Parameters

Key | Brief Info
--------- | -------
clientShipmentId | Order no.
latitude | Latitude where order was pickedup
longitude | Longitude where order was pickedup
pickedUpTime | Pickup order timestamp
status | PICKEDUPNOTIFICATION

## Not Pickedup

> Order not pickup - Sample Response

```json
{
  "clientShipmentId": "TestOrder",
  "notificationType": "NOTPICKEDUPNOTIFICATION",
  "orderLeg": "DELIVER",
  "awbNumber": "",
  "customerComments": "",
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



### HTTP Response Parameters

Key | Brief Info
--------- | -------
clientShipmentId | Order no.
notificationType | NOTPICKEDUPNOTIFICATION
orderLeg | Order leg
awbNumber | Airway Bill Number
customerComments | Customer comments
customerRating | Rating provided by customer
deliveryMediumName | Name of delivery medium
phoneNumber | Phone no of delivery medium
orderState | State of the order
customerName | Name of customer
reason | Reason for order not pickedup
reasonCd | Reason code

