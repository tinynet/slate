---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell
  - ruby
  - python
  - javascript

toc_footers:
  - <a href='#'>Sign Up for a Developer Key</a>
  - <a href='https://github.com/slatedocs/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true
---

# Introduction

Welcome to the Hoxell API! 

Hoxell API allows to access and modify hotel resources.

Hoxell API follows very closely the concepts outlined in STRIPE API <a href="https://stripe.com/docs/api/">https://stripe.com/docs/api/</a> and the REST model. 

* URL Endpoints based on resources
* Request bodies: form encoded
* Response: JSON encoded
* HTTP: response code, authentication and verbs

API is accessible only through https

## Authentication

Hoxell API use API keys to authenticate requests via HTTP Basic Auth.

Each hotel has its own API key. The API key identify the account. Authorization is managed with JWT
<a href="https://stormpath.com/blog/token-auth-spa">https://stormpath.com/blog/token-auth-spa</a>


## Errors

Failure of API requests is indicated by standard HTTP response code:

* 2xx: OK
* 4xx: request error from client side
* 5xx: server errors

An additional description is contained in the response:

```{error:"Error message"}```


## Object Expansion

Related objects in the response object can be expanded with the ``expand```request parameter.
See: <a href="https://stripe.com/docs/api/expanding_objects">https://stripe.com/docs/api/expanding_objects</a>

## Idempotent Requests

POST requests accept an ```Idempotency-Key``` parameter.
The idempotency key is generate client side and it is an unique value.

Requests can be safely retried with the same idempotency key.

## Pagination

Top level resources support "list" methods.

All list methods return a list objects with a common structure and accept three parameters: ```limit```,  ```starting_after``` and ```ending_before```. Default dates for both are "forever" in the past and in the future.
Dates are applied on relevant object date field.

### Parameters

* limit: optional. Limit on the number of objects. Default is no limit
* starting_after: optional. Starting date, inclusive. Format = YYYY-MM-DD
* ending_before: optional. Ending date, inclusive. Format = YYYY-MM-DD

### List Response Format

* object: string, value: "list"
* data: array. An array containing response objects.
* has_more: boolean. True if there are more elements. False if is the end of the list.
* url: the URL for accessing this list

## Versioning

Forward compatible changes (E.g. New resources, optional parameters)  don't produce a new API version. 
API version used depends on API key.

# CORE OBJECTS

These objects are typically used by all modules.

## Domain objects

Core objects beloging to the domain.

### Guest

### Reservation

### Room

### Staff

## Application objects

Application objects are general system objects

### Department

### Menu

### Privilege

### Property

### Role





```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.get
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get()
```

```shell
curl "http://example.com/api/kittens"
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
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

This endpoint retrieves all kittens.

### HTTP Request

`GET http://example.com/api/kittens`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
include_cats | false | If set to true, the result will also include cats.
available | true | If set to false, the result will include kittens that have already been adopted.

<aside class="success">
Remember — a happy kitten is an authenticated kitten!
</aside>

## Get a Specific Kitten

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.get(2)
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get(2)
```

```shell
curl "http://example.com/api/kittens/2"
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
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

This endpoint retrieves a specific kitten.

<aside class="warning">Inside HTML code blocks like this one, you can't use Markdown, so use <code>&lt;code&gt;</code> blocks to denote code.</aside>

### HTTP Request

`GET http://example.com/kittens/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the kitten to retrieve

## Delete a Specific Kitten

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.delete(2)
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.delete(2)
```

```shell
curl "http://example.com/api/kittens/2"
  -X DELETE
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
let max = api.kittens.delete(2);
```

> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "deleted" : ":("
}
```

This endpoint deletes a specific kitten.

### HTTP Request

`DELETE http://example.com/kittens/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the kitten to delete

