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

## What is REST?

REST is acronym for REpresentational State Transfer. It is architectural style for distributed hypermedia systems and was first presented by Roy Fielding in 2000 in his famous dissertation.

Like any other architectural style, REST also does have it’s own 6 guiding constraints which must be satisfied if an interface needs to be referred as RESTful. These principles are listed below.

## Guiding Principles of REST

Client–server – By separating the user interface concerns from the data storage concerns, we improve the portability of the user interface across multiple platforms and improve scalability by simplifying the server components.

Stateless – Each request from client to server must contain all of the information necessary to understand the request, and cannot take advantage of any stored context on the server. Session state is therefore kept entirely on the client.

Cacheable – Cache constraints require that the data within a response to a request be implicitly or explicitly labeled as cacheable or non-cacheable. If a response is cacheable, then a client cache is given the right to reuse that response data for later, equivalent requests.

Uniform interface – By applying the software engineering principle of generality to the component interface, the overall system architecture is simplified and the visibility of interactions is improved. In order to obtain a uniform interface, multiple architectural constraints are needed to guide the behavior of components. REST is defined by four interface constraints: identification of resources; manipulation of resources through representations; self-descriptive messages; and, hypermedia as the engine of application state.

Layered system – The layered system style allows an architecture to be composed of hierarchical layers by constraining component behavior such that each component cannot “see” beyond the immediate layer with which they are interacting.

Code on demand (optional) – REST allows client functionality to be extended by downloading and executing code in the form of applets or scripts. This simplifies clients by reducing the number of features required to be pre-implemented.

### Resource

The key abstraction of information in REST is a resource. Any information that can be named can be a resource: a document or image, a temporal service, a collection of other resources, a non-virtual object (e.g. a person), and so on. REST uses a resource identifier to identify the particular resource involved in an interaction between components.

The state of resource at any particular timestamp is known as resource representation. A representation consists of data, metadata describing the data and hypermedia links which can help the clients in transition to next desired state.

The data format of a representation is known as a media type. The media type identifies a specification that defines how a representation is to be processed. A truly RESTful API looks like hypertext. Every addressable unit of information carries an address, either explicitly (e.g., link and id attributes) or implicitly (e.g., derived from the media type definition and representation structure).

According to Roy Fielding:

<aside class="success">

Hypertext (or hypermedia) mean the simultaneous presentation of information and controls such that the information becomes the affordance through which the user (or automaton) obtains choices and selects actions. Remember that hypertext does not need to be HTML (or XML or JSON) on a browser. Machines can follow links when they understand the data format and relationship types.

</aside>

Further, resource representations shall be self-descriptive: the client does not need to know if a resource is employee or device. It should act on basis of media-type associated with resource. So in practice, you will end up creating lots of custom media-types – normally one media-type associated with one resource.

<aside class="success">

Every media type defines a default processing model. For example, HTML defines a rendering process for hypertext and the browser behavior around each element. It has no relation to the resource methods GET/PUT/POST/DELETE/… other than the fact that some media type elements will define a process model that goes like “anchor elements with an href attribute create a hypertext link that, when selected, invokes a retrieval request (GET) on the URI corresponding to the CDATA-encoded href attribute.”

</aside>

### Resource Methods

Other important thing associated with REST is resource methods to be used to perform the desired transition. A large number of people wrongly relate resource methods to HTTP GET/PUT/POST/DELETE methods.

Roy Fielding has never mentioned any recommendation around which method to be used in which condition. All he emphasizes is that it should be uniform interface. If you decide HTTP POST will be used for updating a resource – rather than most people recommend HTTP PUT – it’s alright and application interface will be RESTful.

Ideally, everything that is needed to change the resource state shall be part of API response for that resource – including methods and in what state they will leave the representation.

A REST API should be entered with no prior knowledge beyond the initial URI (bookmark) and set of standardized media types that are appropriate for the intended audience (i.e., expected to be understood by any client that might use the API). From that point on, all application state transitions must be driven by client selection of server-provided choices that are present in the received representations or implied by the user’s manipulation of those representations. The transitions may be determined (or limited by) the client’s knowledge of media types and resource communication mechanisms, both of which may be improved on-the-fly (e.g., code-on-demand).
[Failure here implies that out-of-band information is driving interaction instead of hypertext.]

Another thing which will help you while building RESTful APIs is that query based API results should be represented by a list of links with summary information, not by arrays of original resource representations because query is not a substitute for identification of resources.

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

Use GET requests to retrieve resource representation/information only – and not to modify it in any way. As GET requests do not change the state of the resource, these are said to be safe methods. Additionally, GET APIs should be idempotent, which means that making multiple identical requests must produce the same result every time until another API (POST or PUT) has changed the state of the resource on the server.

If the Request-URI refers to a data-producing process, it is the produced data which shall be returned as the entity in the response and not the source text of the process, unless that text happens to be the output of the process.

For any given HTTP GET API, if the resource is found on the server then it must return HTTP response code 200 (OK) – along with response body in JSON content.

In case resource is NOT found on server then it must return HTTP response code 404 (NOT FOUND). 

Similarly, if it is determined that GET request itself is not correctly formed then server will return HTTP response code 400 (BAD REQUEST).

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
include_services | false | If set to true, the result will also include cats.
available | true | If set to false, the result will include kittens that have already been adopted.

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

`GET http://carerelay.com/api//{product_id}`

Use GET requests to retrieve resource representation/information only – and not to modify it in any way. As GET requests do not change the state of the resource, these are said to be safe methods. Additionally, GET APIs should be idempotent, which means that making multiple identical requests must produce the same result every time until another API (POST or PUT) has changed the state of the resource on the server.

If the Request-URI refers to a data-producing process, it is the produced data which shall be returned as the entity in the response and not the source text of the process, unless that text happens to be the output of the process.

For any given HTTP GET API, if the resource is found on the server then it must return HTTP response code 200 (OK) – along with response body in JSON content.

In case resource is NOT found on server then it must return HTTP response code 404 (NOT FOUND). 

Similarly, if it is determined that GET request itself is not correctly formed then server will return HTTP response code 400 (BAD REQUEST).

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

Use GET requests to retrieve resource representation/information only – and not to modify it in any way. As GET requests do not change the state of the resource, these are said to be safe methods. Additionally, GET APIs should be idempotent, which means that making multiple identical requests must produce the same result every time until another API (POST or PUT) has changed the state of the resource on the server.

If the Request-URI refers to a data-producing process, it is the produced data which shall be returned as the entity in the response and not the source text of the process, unless that text happens to be the output of the process.

For any given HTTP GET API, if the resource is found on the server then it must return HTTP response code 200 (OK) – along with response body in JSON content.

In case resource is NOT found on server then it must return HTTP response code 404 (NOT FOUND). 

Similarly, if it is determined that GET request itself is not correctly formed then server will return HTTP response code 400 (BAD REQUEST).

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

Use GET requests to retrieve resource representation/information only – and not to modify it in any way. As GET requests do not change the state of the resource, these are said to be safe methods. Additionally, GET APIs should be idempotent, which means that making multiple identical requests must produce the same result every time until another API (POST or PUT) has changed the state of the resource on the server.

If the Request-URI refers to a data-producing process, it is the produced data which shall be returned as the entity in the response and not the source text of the process, unless that text happens to be the output of the process.

For any given HTTP GET API, if the resource is found on the server then it must return HTTP response code 200 (OK) – along with response body in JSON content.

In case resource is NOT found on server then it must return HTTP response code 404 (NOT FOUND). 

Similarly, if it is determined that GET request itself is not correctly formed then server will return HTTP response code 400 (BAD REQUEST).

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

This endpoint retrieves all Products/Services.

### HTTP Request

`POST http://carerelay.com/api/requests`

### POST Service Request Details
Parameter | Default | Description
--------- | ------- | -----------
include_services | false | If set to true, the result will also include cats.
available | true | If set to false, the result will include kittens that have already been adopted.

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

This endpoint retrieves a specific Product/Service.

### HTTP Request

`GET http://carerelay.com/api/requests/{request_id}`

Use GET requests to retrieve resource representation/information only – and not to modify it in any way. As GET requests do not change the state of the resource, these are said to be safe methods. Additionally, GET APIs should be idempotent, which means that making multiple identical requests must produce the same result every time until another API (POST or PUT) has changed the state of the resource on the server.

If the Request-URI refers to a data-producing process, it is the produced data which shall be returned as the entity in the response and not the source text of the process, unless that text happens to be the output of the process.

For any given HTTP GET API, if the resource is found on the server then it must return HTTP response code 200 (OK) – along with response body in JSON content.

In case resource is NOT found on server then it must return HTTP response code 404 (NOT FOUND). 

Similarly, if it is determined that GET request itself is not correctly formed then server will return HTTP response code 400 (BAD REQUEST).

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

This endpoint retrieves all Products/Services.

### HTTP Request

`PATCH http://carerelay.com/api/requests/{request_id}`

HTTP PATCH requests are to make partial update on a resource. If you see PUT requests also modify a resource entity so to make it clearer – PATCH method is the correct choice for partially updating an existing resource and PUT should only be used if you’re replacing a resource in its entirety.

### POST Service Request Details
Parameter | Default | Description
--------- | ------- | -----------
include_services | false | If set to true, the result will also include cats.
available | true | If set to false, the result will include kittens that have already been adopted.

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

This endpoint retrieves a specific Product/Service.

### HTTP Request

`DELETE http://carerelay.com/api/requests/{request_id}`

As the name applies, DELETE APIs are used to delete resources (identified by the Request-URI).

A successful response of DELETE requests SHOULD be HTTP response code 200 (OK) if the response includes an entity describing the status, 202 (Accepted) if the action has been queued, or 204 (No Content) if the action has been performed but the response does not include an entity.

DELETE operations are idempotent. If you DELETE a resource, it’s removed from the collection of resource. Repeatedly calling DELETE API on that resource will not change the outcome – however calling DELETE on a resource a second time will return a 404 (NOT FOUND) since it was already removed. Some may argue that it makes DELETE method non-idempotent.

If the request passes through a cache and the Request-URI identifies one or more currently cached entities, those entries SHOULD be treated as stale. Responses to this method are not cacheable.

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the Product/Service to retrieve