---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell  
  - javascript

toc_footers:
  - <a href='#'>Sign Up for a Developer Key</a>
  - <a href='https://github.com/lord/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true
---

# Introduction

The CareRelay API is a RESTful API that is designed to allow one to get, create, update, & delete objects with the HTTP verbs GET, POST, PUT, PATCH, & DELETE.

Making requests to API endpoints gives one everything needed to create new service requests, update/edit, schedule, complete, and bill for services.

# Authentication

> To authorize, use this code:

```ruby
require 'cri'

api = cri::APIClient.authorize!('carecaptain')
```

```python
import cri

api = cri.authorize('carecaptain')
```

```shell
# With shell, you can just pass the correct header with each request
curl "api_endpoint_here"
  -H "Authorization: carecaptain"
```

```javascript
const cri = require('cri');

let api = cri.authorize('carecaptain');
```

> Make sure to replace `carecaptain` with your API key.

CareRelay uses API keys to allow access to the API. You can register a new CareRelay API key at our [developer portal](http://carerelay.com/developers).

CareRelay expects for the API key to be included in all API requests to the server in a header that looks like the following:

`Authorization: carecaptain`

# Query Products/Services

## List Products/Services

```ruby
require 'cri'

api = cri::APIClient.authorize!('carecaptain')
api.kittens.get
```

```python
import cri

api = cri.authorize('carecaptain')
api.kittens.get()
```

```shell
curl "http://carerelay.com/api/carerelay"
  -H "Authorization: carecaptain"
```

```javascript
const cri = require('cri');

let api = cri.authorize('carecaptain');
let kittens = api.kittens.get();
```

> The above command returns JSON structured like this:

```json
{
  "products": [
    {
      "upfront_fare_enabled": true,
      "capacity": 4,
      "product_id": "d4abaae7-f4d6-4152-91cc-77523e8165a4",
      "price_details": {
        "service_fees": [

        ],
        "cost_per_minute": 0.65,
        "distance_unit": "mile",
        "minimum": 15,
        "cost_per_distance": 3.75,
        "base": 8,
        "cancellation_fee": 10,
        "currency_code": "USD"
      },
      "image": "http:\/\/d1a3f4spazzrp4.cloudfront.net\/car-types\/mono\/mono-black.png",
      "cash_enabled": false,
      "shared": false,
      "short_description": "BLACK",
      "display_name": "BLACK",
      "product_group": "uberblack",
      "description": "THE ORIGINAL UBER"
    },
    {
      "upfront_fare_enabled": true,
      "capacity": 2,
      "product_id": "26546650-e557-4a7b-86e7-6a3942445247",
      "price_details": {
        "service_fees": [
          {
            "fee": 2,
            "name": "Booking fee"
          }
        ],
        "cost_per_minute": 0.15,
        "distance_unit": "mile",
        "minimum": 7.45,
        "cost_per_distance": 1.1,
        "base": 2,
        "cancellation_fee": 5,
        "currency_code": "USD"
      },
      "image": "http:\/\/d1a3f4spazzrp4.cloudfront.net\/car-types\/mono\/mono-uberx.png",
      "cash_enabled": false,
      "shared": true,
      "short_description": "POOL",
      "display_name": "POOL",
      "product_group": "rideshare",
      "description": "Share the ride, split the cost."
    },
    {
      "upfront_fare_enabled": false,
      "capacity": 4,
      "product_id": "2d1d002b-d4d0-4411-98e1-673b244878b2",
      "price_details": {
        "service_fees": [
          {
            "fee": 0.55,
            "name": "Booking fee"
          }
        ],
        "cost_per_minute": 0.4,
        "distance_unit": "km",
        "minimum": 9,
        "cost_per_distance": 1.45,
        "base": 2.5,
        "cancellation_fee": 10,
        "currency_code": "AUD"
      },
      "image": "http:\/\/d1a3f4spazzrp4.cloudfront.net\/car-types\/mono\/mono-uberx.png",
      "cash_enabled": false,
      "shared": false,
      "short_description": "uberX",
      "display_name": "uberX",
      "product_group": "uberx",
      "description": "Everyday rides that are always smarter than a taxi"
    },
    {
      "upfront_fare_enabled": false,
      "capacity": 4,
      "product_id": "3ab64887-4842-4c8e-9780-ccecd3a0391d",
      "price_details": {
        "service_fees": [

        ],
        "cost_per_minute": 0.55,
        "distance_unit": "mile",
        "minimum": 3.5,
        "cost_per_distance": 2.75,
        "base": 3.5,
        "cancellation_fee": 5,
        "currency_code": "USD"
      },
```

__This endpoint retrieves all Products/Services__

### HTTP Request

`GET http://carerelay.com/api/products`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
include_services | false | If set to true, the result will also include cats.
available | true | If set to false, the result will include kittens that have already been adopted.

/*<aside class="success">
Remember — a happy customer is an authenticated member!
</aside>*/

## Get a Product/Service Details

```ruby
require 'cri'

api = cri::APIClient.authorize!('carecaptain')
api.kittens.get(2)
```

```python
import cri

api = cri.authorize('carecaptain')
api.kittens.get(2)
```

```shell
curl "http://carerelay.com/api/carerelay/2"
  -H "Authorization: carecaptain"
```

```javascript
const cri = require('cri');

let api = cri.authorize('carecaptain');
let max = api.kittens.get(2);
```

> The above command returns JSON structured like this:

```json
{
  "upfront_fare_enabled": false,
  "capacity": 4,
  "product_id": "a1111c8c-c720-46c3-8534-2fcdd730040d",
  "price_details": {
    "service_fees": [
      {
        "fee": 1.55,
        "name": "Booking fee"
      }
    ],
    "cost_per_minute": 0.22,
    "distance_unit": "mile",
    "minimum": 6.55,
    "cost_per_distance": 1.15,
    "base": 2,
    "cancellation_fee": 5,
    "currency_code": "USD"
  },
  "image": "http://d1a3f4spazzrp4.cloudfront.net/car-types/mono/mono-uberx.png",
  "cash_enabled": false,
  "shared": false,
  "short_description": "uberX",
  "display_name": "uberX",
  "product_group": "uberx",
  "description": "THE LOW-COST UBER"
}
```

__This endpoint retrieves a specific Product/Service__

### HTTP Request

`GET http://example.com/api//{product_id}`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the Product/Service to retrieve

# Query Price/Time

## Get Quotes/Price Estimates

```ruby
require 'cri'

api = cri::APIClient.authorize!('carecaptain')
api.kittens.delete(2)
```

```python
import cri

api = cri.authorize('carecaptain')
api.kittens.delete(2)
```

```shell
curl "http://carerelay.com/api/carerelay/2"
  -X DELETE
  -H "Authorization: carecaptain"
```

```javascript
const cri = require('cri');

let api = cri.authorize('carecaptain');
let max = api.kittens.delete(2);
```

> The above command returns JSON structured like this:

```json
{
  "prices": [
    {
      "localized_display_name": "POOL",
      "distance": 6.17,
      "display_name": "POOL",
      "product_id": "26546650-e557-4a7b-86e7-6a3942445247",
      "high_estimate": 15,
      "low_estimate": 13,
      "duration": 1080,
      "estimate": "$13-14",
      "currency_code": "USD"
    },
    {
      "localized_display_name": "uberX",
      "distance": 6.17,
      "display_name": "uberX",
      "product_id": "a1111c8c-c720-46c3-8534-2fcdd730040d",
      "high_estimate": 17,
      "low_estimate": 13,
      "duration": 1080,
      "estimate": "$13-17",
      "currency_code": "USD"
    },
    {
      "localized_display_name": "uberXL",
      "distance": 6.17,
      "display_name": "uberXL",
      "product_id": "821415d8-3bd5-4e27-9604-194e4359a449",
      "high_estimate": 26,
      "low_estimate": 20,
      "duration": 1080,
      "estimate": "$20-26",
      "currency_code": "USD"
    },
    {
      "localized_display_name": "SELECT",
      "distance": 6.17,
      "display_name": "SELECT",
      "product_id": "57c0ff4e-1493-4ef9-a4df-6b961525cf92",
      "high_estimate": 38,
      "low_estimate": 30,
      "duration": 1080,
      "estimate": "$30-38",
      "currency_code": "USD"
    },
    {
      "localized_display_name": "BLACK",
      "distance": 6.17,
      "display_name": "BLACK",
      "product_id": "d4abaae7-f4d6-4152-91cc-77523e8165a4",
      "high_estimate": 43,
      "low_estimate": 43,
      "duration": 1080,
      "estimate": "$43.10",
      "currency_code": "USD"
    },
    {
      "localized_display_name": "SUV",
      "distance": 6.17,
      "display_name": "SUV",
      "product_id": "8920cb5e-51a4-4fa4-acdf-dd86c5e18ae0",
      "high_estimate": 63,
      "low_estimate": 50,
      "duration": 1080,
      "estimate": "$50-63",
      "currency_code": "USD"
    },
    {
      "localized_display_name": "ASSIST",
      "distance": 6.17,
      "display_name": "ASSIST",
      "product_id": "ff5ed8fe-6585-4803-be13-3ca541235de3",
      "high_estimate": 17,
      "low_estimate": 13,
      "duration": 1080,
      "estimate": "$13-17",
      "currency_code": "USD"
    },
    {
      "localized_display_name": "WAV",
      "distance": 6.17,
      "display_name": "WAV",
      "product_id": "2832a1f5-cfc0-48bb-ab76-7ea7a62060e7",
      "high_estimate": 33,
      "low_estimate": 25,
      "duration": 1080,
      "estimate": "$25-33",
      "currency_code": "USD"
    },
    {
      "localized_display_name": "TAXI",
      "distance": 6.17,
      "display_name": "TAXI",
      "product_id": "3ab64887-4842-4c8e-9780-ccecd3a0391d",
      "high_estimate": null,
      "low_estimate": null,
      "duration": 1080,
      "estimate": "Metered",
      "currency_code": null
    }
  ]
}
```

This endpoint retrieves a specific Quote/Price

### HTTP Request

`GET http://carerelay.com/api/estimates/price`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the kitten to delete

## Get Date/Time Estimates

```ruby
require 'cri'

api = cri::APIClient.authorize!('carecaptain')
api.kittens.delete(2)
```

```python
import cri

api = cri.authorize('carecaptain')
api.kittens.delete(2)
```

```shell
curl "http://carerelay.com/api/carerelay/2"
  -X DELETE
  -H "Authorization: carecaptain"
```

```javascript
const cri = require('cri');

let api = cri.authorize('carecaptain');
let max = api.kittens.delete(2);
```

> The above command returns JSON structured like this:

```json
{
  "times": [
    {
      "localized_display_name": "POOL",
      "estimate": 60,
      "display_name": "POOL",
      "product_id": "26546650-e557-4a7b-86e7-6a3942445247"
    },
    {
      "localized_display_name": "uberX",
      "estimate": 60,
      "display_name": "uberX",
      "product_id": "a1111c8c-c720-46c3-8534-2fcdd730040d"
    },
    {
      "localized_display_name": "uberXL",
      "estimate": 240,
      "display_name": "uberXL",
      "product_id": "821415d8-3bd5-4e27-9604-194e4359a449"
    },
    {
      "localized_display_name": "SELECT",
      "estimate": 240,
      "display_name": "SELECT",
      "product_id": "57c0ff4e-1493-4ef9-a4df-6b961525cf92"
    },
    {
      "localized_display_name": "BLACK",
      "estimate": 240,
      "display_name": "BLACK",
      "product_id": "d4abaae7-f4d6-4152-91cc-77523e8165a4"
    },
    {
      "localized_display_name": "SUV",
      "estimate": 240,
      "display_name": "SUV",
      "product_id": "8920cb5e-51a4-4fa4-acdf-dd86c5e18ae0"
    },
    {
      "localized_display_name": "ASSIST",
      "estimate": 300,
      "display_name": "ASSIST",
      "product_id": "ff5ed8fe-6585-4803-be13-3ca541235de3"
    },
    {
      "localized_display_name": "TAXI",
      "estimate": 480,
      "display_name": "TAXI",
      "product_id": "3ab64887-4842-4c8e-9780-ccecd3a0391d"
    }
  ]
}
```

This endpoint retrieves a specific Time/Date Estimate.

### HTTP Request

`GET http://carerelay.com/api/estimates/time`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of carerelay to delete


# Create Service Requests

## POST Service Requests

```ruby
require 'cri'

api = cri::APIClient.authorize!('carecaptain')
api.kittens.get
```

```python
import cri

api = cri.authorize('carecaptain')
api.kittens.get()
```

```shell
curl "http://carerelay.com/api/carerelay"
  -H "Authorization: carecaptain"
```

```javascript
const cri = require('cri');

let api = cri.authorize('carecaptain');
let kittens = api.kittens.get();
```

> The above command returns JSON structured like this:

```json
[
  {
    "id": 1,
    "name": "Fluffums",
    "breed": "calico",
    "fluffiness": 6,
    "cuteness": 7
  },
  {
    "id": 2,
    "name": "Max",
    "breed": "unknown",
    "fluffiness": 5,
    "cuteness": 10
  }
]
```

This endpoint retrieves all Products/Services

### HTTP Request

`GET http://carerelay.com/api/requests`

### POST Service Request Details
Parameter | Default | Description
--------- | ------- | -----------
include_services | false | If set to true, the result will also include cats.
available | true | If set to false, the result will include kittens that have already been adopted.

<aside class="success">
Remember — a happy customer is an authenticated kitten!
</aside>

## GET Service Request Details by ID

```ruby
require 'cri'

api = cri::APIClient.authorize!('carecaptain')
api.kittens.get(2)
```

```python
import cri

api = cri.authorize('carecaptain')
api.kittens.get(2)
```

```shell
curl "http://carerelay.com/api/carerelay/2"
  -H "Authorization: carecaptain"
```

```javascript
const cri = require('cri');

let api = cri.authorize('carecaptain');
let max = api.kittens.get(2);
```

> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "name": "Max",
  "breed": "unknown",
  "fluffiness": 5,
  "cuteness": 10
}
```

This endpoint retrieves a specific Product/Service

<aside class="warning">Inside HTML code blocks like this one, you can't use Markdown, so use <code>&lt;code&gt;</code> blocks to denote code.</aside>

### HTTP Request

`GET http://carerelay.com/api/requests/{request_id}`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the Product/Service to retrieve

# Update/Edit or Cancel Service Requests

## Update Service Request

```ruby
require 'cri'

api = cri::APIClient.authorize!('carecaptain')
api.kittens.get
```

```python
import cri

api = cri.authorize('carecaptain')
api.kittens.get()
```

```shell
curl "http://carerelay.com/api/carerelay"
  -H "Authorization: carecaptain"
```

```javascript
const cri = require('cri');

let api = cri.authorize('carecaptain');
let kittens = api.kittens.get();
```

> The above command returns JSON structured like this:

```json
{
  "picture": "https://d1w2poirtb3as9.cloudfront.net/f3be498cb0bbf570aa3d.jpeg",
  "first_name": "Uber",
  "last_name": "Developer",
  "uuid": "f4a416e3-6016-4623-8ec9-d5ee105a6e27",
  "rider_id": "8OlTlUG1TyeAQf1JiBZZdkKxuSSOUwu2IkO0Hf9d2HV52Pm25A0NvsbmbnZr85tLVi-s8CckpBK8Eq0Nke4X-no3AcSHfeVh6J5O6LiQt5LsBZDSi4qyVUdSLeYDnTtirw==",
  "email": "uberdevelopers@gmail.com",
  "mobile_verified": true,
  "promo_code": "uberd340ue"
}
```

This endpoint retrieves all Products/Services

### HTTP Request

`PATCH http://carerelay.com/api/requests/{request_id}`

### POST Service Request Details
Parameter | Default | Description
--------- | ------- | -----------
include_services | false | If set to true, the result will also include cats.
available | true | If set to false, the result will include kittens that have already been adopted.

<aside class="success">
Remember — a happy customer is an authenticated kitten!
</aside>

## Cancel Service Request

```ruby
require 'cri'

api = cri::APIClient.authorize!('carecaptain')
api.kittens.get(2)
```

```python
import cri

api = cri.authorize('carecaptain')
api.kittens.get(2)
```

```shell
curl "http://carerelay.com/api/carerelay/2"
  -H "Authorization: carecaptain"
```

```javascript
const cri = require('cri');

let api = cri.authorize('carecaptain');
let max = api.kittens.get(2);
```

> The above command returns JSON structured like this:

```json
{
  "picture": "https://d1w2poirtb3as9.cloudfront.net/f3be498cb0bbf570aa3d.jpeg",
  "first_name": "Uber",
  "last_name": "Developer",
  "uuid": "f4a416e3-6016-4623-8ec9-d5ee105a6e27",
  "rider_id": "8OlTlUG1TyeAQf1JiBZZdkKxuSSOUwu2IkO0Hf9d2HV52Pm25A0NvsbmbnZr85tLVi-s8CckpBK8Eq0Nke4X-no3AcSHfeVh6J5O6LiQt5LsBZDSi4qyVUdSLeYDnTtirw==",
  "email": "uberdevelopers@gmail.com",
  "mobile_verified": true,
  "promo_code": "uberd340ue"
}
```

This endpoint retrieves a specific Product/Service

<aside class="warning">Inside HTML code blocks like this one, you can't use Markdown, so use <code>&lt;code&gt;</code> blocks to denote code.</aside>

### HTTP Request

`DELETE http://carerelay.com/api/requests/{request_id}`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the Product/Service to retrieve