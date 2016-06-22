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

Welcome to the Loginext API! You can use our API to access Kittn API endpoints, which can get information on various cats, kittens, and breeds in our database.

We have language bindings in Shell, Ruby, and Python! You can view code examples in the dark area to the right, and you can switch the programming language of the examples with the tabs in the top right.

This example API documentation page was created with [Slate](https://github.com/tripit/slate). Feel free to edit it and use it as a base for your own API's documentation.

# Authentication

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


> Sample Response

```json
{
  "status": 200,
  "message": "success",
  "data": null,
  "hasError": false
}

```


# OnDemand


# Mile

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



# Haul

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
                            "shiftStartTime"  :"07:03pm",
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

`POST http://endpoint.loginextsolutions.com/TripApp/haul/v1/trip/start`

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
