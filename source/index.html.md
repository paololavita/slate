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

<aside class="notice">
You must replace <code>carecaptain</code> with your personal API key.
</aside>

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

`GET http://carerelay.com/api/carerelay`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
include_services | false | If set to true, the result will also include cats.
available | true | If set to false, the result will include kittens that have already been adopted.

<aside class="success">
Remember — a happy customer is an authenticated member!
</aside>

## Get a Product/Service

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

`GET http://example.com/kittens/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the Product/Service to retrieve

# Query Price/Time

## Get Estimate/Price

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
  "id": 2,
  "deleted" : ":("
}
```

This endpoint retrieves a specific Quote/Price

### HTTP Request

`DELETE http://example.com/kittens/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the kitten to delete

## Get Time/Date Estimates

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
  "id": 2,
  "deleted" : ":("
}
```

This endpoint retrieves a specific Time/Date Estimate.

### HTTP Request

`DELETE http://example.com/carerelay/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of carerelay to delete

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

`GET http://carerelay.com/api/carerelay`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
include_services | false | If set to true, the result will also include cats.
available | true | If set to false, the result will include kittens that have already been adopted.

<aside class="success">
Remember — a happy customer is an authenticated kitten!
</aside>

## Get a Service Request Details

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

This endpoint creates a Service Request.

### HTTP Request

`POST http://carerelay.com/request/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the Product/Service to retrieve

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

`GET http://carerelay.com/api/carerelay`

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

`GET http://example.com/kittens/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the Product/Service to retrieve

