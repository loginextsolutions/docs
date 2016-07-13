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

Welcome to the Loginext API

# Authentication

This endpoint authenticates a user.

## Authenticate

This endpoint authenticates a user. 

### HTTP Request

`POST http://endpoint.loginextsolutions.com/LoginApp/login/authenticate`

LogiNext uses tokens to allow access to the API. You can register a new LogiNext token using our auth api. 

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

`POST http://endpoint.loginextsolutions.com/LoginApp/token/refresh`


### HTTP Request Headers

Header | Sample Value 
--------- | ------- | -------------
WWW-Authenticate | BASIC 075b8961-bd02-454c-83eb-259f965f313f
CLIENT_SECRET_KEY | $2a$08$bCi0ja4B5S02BKQt3VdxNuReERpSV8SiAbwVrHNyhC7mD

<aside class="success">Response headers will contain new session token and authentication key.</aside>

# OnDemand 2.0


# Mile

## Create Order

> Create Order - Sample Request

```json

```

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

`POST http://endpoint.loginextsolutions.com/ShipmentApp/mile/v1/create`

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

`POST http://endpoint.loginextsolutions.com/ShipmentApp/mile/v1/create/return`

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

`POST http://endpoint.loginextsolutions.com/ShipmentApp/mile/v1/crate`

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

`POST http://endpoint.loginextsolutions.com/ShipmentApp/mile/v1/cancel`

### HTTP Request Headers

Header | Sample Value | Brief Info
--------- | ------- | -------------
Content-Type | application/json | Json request
WWW-Authenticate | BASIC 51bbe3f7-1671-476c-818a-e7fbbca10202 | Authentication token
CLIENT_SECRET_KEY | $2a$08$LQEqG3s.LF2jBt7Baq| Authentication key

## Get Status

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

`POST http://endpoint.loginextsolutions.com/ShipmentApp/mile/v1/status`

### HTTP Request Headers

Header | Sample Value | Brief Info
--------- | ------- | -------------
Content-Type | application/json | Json request
WWW-Authenticate | BASIC 51bbe3f7-1671-476c-818a-e7fbbca10202 | Authentication token
CLIENT_SECRET_KEY | $2a$08$LQEqG3s.LF2jBt7Baq| Authentication key



## Trip Start

> Trip Start - Sample Request

```json
[
    "a9be39b9347911e6829f000d3aa04450"    
]
```

> Trip Start - Sample Response

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

`POST http://endpoint.loginextsolutions.com/TripApp/mile/v1/trip/start`

### HTTP Request Headers

Header | Sample Value | Brief Info
--------- | ------- | -------------
Content-Type | application/json | Json request
WWW-Authenticate | BASIC 8bce7b1b-9762-4de7-b9cd-976ecf38b6a0 | Authentication token
CLIENT_SECRET_KEY | $2a$08$npX3e6RD6zJFHcvFV469D.XtRpCwCQwZ3YlsEpERDcd.c2jmabLsG| Authentication key

## Trip Stop

> Trip Stop - Sample Request

```json
[{
    "tripReferenceId":"a9be39b9347911e6829f000d3aa04450",
    "notDispatchedOrders":["c8714df4347911e6829f000d3aa04450"],
    "deliveredOrders":["c8714cac347911e6829f000d3aa04450"]
}
]
```

> Trip Stop - Sample Response

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

`POST http://endpoint.loginextsolutions.com/TripApp/mile/v1/trip/stop`
  
### HTTP Request Headers

Header | Sample Value | Brief Info
--------- | ------- | -------------
Content-Type | application/json | Json request
WWW-Authenticate | BASIC 8bce7b1b-9762-4de7-b9cd-976ecf38b6a0 | Authentication token
CLIENT_SECRET_KEY | $2a$08$npX3e6RD6zJFHcvFV469D.XtRpCwCQwZ3YlsEpERDcd.c2jmabLsG| Authentication key

## Track Last Location

> Track Last Location - Sample Request

```json
http://endpoint.loginextsolutions.com/TrackingApp/mile/v1/track/lastlocation?shipmentReferences=25a565a9c9d540cd9e6c02fae890cb67,c7afc8b1b97b48468c3417aa425eff81,27121903f4f047bcb378a6457bee2fec,21b538edf7f047028334480036179c70
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

`GET http://endpoint.loginextsolutions.com/TrackingApp/mile/v1/track/lastlocation`
  
### HTTP Request Headers

Header | Sample Value | Brief Info
--------- | ------- | -------------
Content-Type | application/json | Json request
WWW-Authenticate | BASIC 8bce7b1b-9762-4de7-b9cd-976ecf38b6a0 | Authentication token
CLIENT_SECRET_KEY | $2a$08$npX3e6RD6zJFHcvFV469D.XtRpCwCQwZ3YlsEpERDcd.c2jmabLsG| Authentication key



# Haul

## Vehicle Create

> Vehicle Create - Sample Request

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

> Vehicle Create - Sample Response

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

`POST http://endpoint.loginextsolutions.com/VehicleApp/v1/vehicle/create`

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

## Vehicle Read (Single)


> Vehicle Read - Sample Response

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

`POST http://endpoint.loginextsolutions.com/VehicleApp/v1/vehicle/:reference_id`

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


## Vehicle Read


> Vehicle Read - Sample Response

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

`POST http://endpoint.loginextsolutions.com/VehicleApp/v1/vehicle`

### HTTP Request Headers

Header | Sample Value | Brief Info
--------- | ------- | -------------
Content-Type | application/json | Json request
WWW-Authenticate | BASIC 51bbe3f7-1671-476c-818a-e7fbbca10202 | Authentication token
CLIENT_SECRET_KEY | $2a$08$LQEqG3s.LF2jBt7Baq| Authentication key

## Vehicle Update

> Vehicle Update - Sample Request

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

> Vehicle Update - Sample Response

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

`PUT http://endpoint.loginextsolutions.com/VehicleApp/v1/vehicle`

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


## Vehicle Delete

> Vehicle Delete - Sample Request

```json
["a9be39b9347911e6829f000d3aa04450"]
```

> Vehicle Delete - Sample Response

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

`DELETE http://endpoint.loginextsolutions.com/VehicleApp/v1/vehicle`

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


## Driver Create

> Driver Create - Sample Request

```json
[
    {
        "driverEmployeeId":"D0011",
        "licenseNumber":"LN110090",
        
        "driverName":"Test001",
        "phoneNumber":1234567890,
        "addressList":[ {
                                "apartment":"Loginext",
                                "city":"Mumbai",
                                "country":10,
                                "state":20,
                                "isCurrentAddress":true,
                                "guid":"bd53"
                                
                        }],
        "shiftList":[{
                            "shiftStartTime" :"07:03pm",
                            "shiftEndTime":"07:10am",
                            "startTime":"2016-06-13",
                            "endTime":"2016-06-15"
                            
        }]
        
        
    }    
]
```

> Driver Create - Sample Response

```json
{
  "status": 200,
  "message": "success",
  "data": null,
  "hasError": false
}

```

This endpoint creates a new driver.

### HTTP Request

`POST http://endpoint.loginextsolutions.com/DriverApp/haul/driver/v1/create`

### HTTP Request Headers

Header | Sample Value | Brief Info
--------- | ------- | -------------
Content-Type | application/json | Json request
WWW-Authenticate | BASIC 51bbe3f7-1671-476c-818a-e7fbbca10202 | Authentication token
CLIENT_SECRET_KEY | $2a$08$LQEqG3s.LF2jBt7Baq| Authentication key

### HTTP Request Parameters

Param | DataType |  Required | Brief Info
--------- | ------- | ---------- | ------------ 
driverEmployeeId | String | Mandatory | Driver EmployeeID


## Driver Read

> Driver Read - Sample Request

```json
["863fe69239bc4f738ca275a809c3b2e2"]
```

> Driver Read - Sample Response

```json
{
  "status": 200,
  "message": "success",
  "data": null,
  "hasError": false
}

```

This endpoint lists an existing driver.

### HTTP Request

`POST http://endpoint.loginextsolutions.com/DriverApp/haul/driver/v1/list`

### HTTP Request Headers

Header | Sample Value | Brief Info
--------- | ------- | -------------
Content-Type | application/json | Json request
WWW-Authenticate | BASIC 51bbe3f7-1671-476c-818a-e7fbbca10202 | Authentication token
CLIENT_SECRET_KEY | $2a$08$LQEqG3s.LF2jBt7Baq| Authentication key

## Driver Update

> Driver Update - Sample Request

```json
[
    {
        "driverEmployeeId":"D0011",
        "licenseNumber":"LN110090",
        "referenceId": "863fe69239bc4f738ca275a809c3b2e2",
        "driverName":"test_shiv",
        "phoneNumber":1234567890,
        "addressList":[ {
                                "apartment":"Loginext",
                                "city":"Mumbai",
                                "country":10,
                                "state":20,
                                "isCurrentAddress":true,
                                 "guid":"bd53"
                                
                        }],
        "shiftList":[{
                            "shiftStartTime"  :"07:03pm",
                            "shiftEndTime":"07:10am",
                            "startTime":"2016-06-13",
                            "endTime":"2016-06-15"
                            
        }]
        
        
    }    
]
```

> Driver Update - Sample Response

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

`PUT http://endpoint.loginextsolutions.com/DriverApp/haul/driver/v1/update`

### HTTP Request Headers

Header | Sample Value | Brief Info
--------- | ------- | -------------
Content-Type | application/json | Json request
WWW-Authenticate | BASIC 51bbe3f7-1671-476c-818a-e7fbbca10202 | Authentication token
CLIENT_SECRET_KEY | $2a$08$LQEqG3s.LF2jBt7Baq| Authentication key

=======

## Driver Delete

> Driver Delete - Sample Request

```json
["e0eaebdd84ac4c40af72d827ab610090"]
```

> Driver Delete - Sample Response

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

`DELETE http://endpoint.loginextsolutions.com/DriverApp/haul/driver/v1/delete`

### HTTP Request Headers

Header | Sample Value | Brief Info
--------- | ------- | -------------
Content-Type | application/json | Json request
WWW-Authenticate | BASIC 51bbe3f7-1671-476c-818a-e7fbbca10202 | Authentication token
CLIENT_SECRET_KEY | $2a$08$LQEqG3s.LF2jBt7Baq| Authentication key

## Trip Create

> Trip Create - Sample Request

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

> Trip Create - Sample Response

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

`POST http://endpoint.loginextsolutions.com/TripApp/haul/v1/trip/create`

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



## Trip Start

> Trip Start - Sample Request

```json
[
    "1880d6906e9d426995b815a83aa3927f"
]
```

> Trip Start - Sample Response

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

`PUT http://endpoint.loginextsolutions.com/TripApp/haul/v1/trip/start`

### HTTP Request Headers

Header | Sample Value | Brief Info
--------- | ------- | -------------
Content-Type | application/json | Json request
WWW-Authenticate | BASIC f522631c-490c-46fd-9f79-ca8d14a704d7 | Authentication token
CLIENT_SECRET_KEY | $2a$08$V4u/aPJrPq/AxqQM6myUYON/gdLw4KfnRPBPZvvHAyW37UGiwakX6| Authentication key

## Trip Stop

> Trip Stop - Sample Request

```json
[
    "1880d6906e9d426995b815a83aa3927f"
]
```

> Trip Stop - Sample Response

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

`POST http://endpoint.loginextsolutions.com/TripApp/haul/v1/trip/stop`

### HTTP Request Headers

Header | Sample Value | Brief Info
--------- | ------- | -------------
Content-Type | application/json | Json request
WWW-Authenticate | BASIC f522631c-490c-46fd-9f79-ca8d14a704d7 | Authentication token
CLIENT_SECRET_KEY | $2a$08$V4u/aPJrPq/AxqQM6myUYON/gdLw4KfnRPBPZvvHAyW37UGiwakX6| Authentication key

## Trip iFrame

This endpoint is to get iFrame view of a trip.

### HTTP Request

`GET https://endpoint.loginextsolutions.com/haul/track/#/?aid=f522631c-490c-46fd-9f79-ca8d14a704d7&key=$2a$08$Vg6jJLhrHEsqOUfD1EJHyuelHeIgcUyvgTfGaeRmnzNr5jGVi86k3&tripname=TestTripName`

### HTTP Request Parameters

Parameter | Sample Value | Brief Info
--------- | ------- | -------------
aid | f522631c-490c-46fd-9f79-ca8d14a704d7 | Value of authentication token without 'BASIC' keyword
key | $2a$08$Vg6jJLhrHEsqOUfD1EJHyuelHeIgcUyvgT | Client Secret Key
tripname | TestTripName| Trip name 

## Track Last Location

> Track Last Location - Sample Request

```json
http://endpoint.loginextsolutions.com/TrackingApp/haul/v1/track/lastlocation?shipmentReferences=25a565a9c9d540cd9e6c02fae890cb67,c7afc8b1b97b48468c3417aa425eff81,27121903f4f047bcb378a6457bee2fec,21b538edf7f047028334480036179c70
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

`GET http://endpoint.loginextsolutions.com/TrackingApp/haul/v1/track/lastlocation`
  
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

> Order pickup - Sample Response

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

