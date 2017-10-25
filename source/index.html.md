---
title: API Reference

language_tabs:
  - shell

toc_footers:
  - <a href='https://github.com/tripit/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true
---




# Introduction

Welcome to Playground API.

## Applications identifying tokens

To access API all request must include identifying token header field.

`X-Application: {{APPLICATION_TOKEN}}`

<aside class="notice">
You must replace <code>{{APPLICATION_TOKEN}}</code> with your personal APP token.
</aside>

## Authentication

To access user specific data request should include authorization header field.

`Authorization: {{AUTHORIZATION_TOKEN}}`

<aside class="notice">
You must replace <code>{{AUTHORIZATION_TOKEN}}</code> with your personal authorization token.
</aside>


# Communication Protocol

## Request

All requests to the API have `path` component to access resources and can be followed by an `id` to get resource by id.

`https://playground.1dxr.com/{{path}}/{{id}}`

Accepted request `method`s are:

* `GET` - read data
* `POST` - create and update data
* `DELETE` - delete data


## Response

> JSON response structured

```json
{
  "data": null,
  "success": [
    {
      "code": 1020,
      "message": "Address created.",
      "debug_message": "postal_code missing.",
      "debug_id": 213124
    }
  ]
}
```

All responses are with HTTP status 200 and contain `data` parameter. Optionally there can be `success`, `error` and `warning` message elements.


### Response object parameters

Parameter | Type | Description
--------- | ---- | -----------
`data` | *array* | Content of response. `data` holds array of objects.
`success`, `warning`, `error`<br>*optional* | *array* | Messages with information for the request. More than one type of message can be returned in a response. `success` and `error` can't come in the same response. `warning` can be combined with `success` or `error`.

## Read


```shell
curl\
 -X GET\
 -H "Content-Type: application/json"\
 -H "X-Application: {{APPLICATION_TOKEN}}"\
 -H "Authorization: {{AUTHORIZATION_TOKEN}}"\
"https://playground.1dxr.com/jobs"
```

> The above request success response is:

```json
{
  "data": [
    {
      "id": 2584075,
      "app_time": 1504620000,
      "addresses": [
        {
          "id": 1,
          "postcode": "UB7 7LQ",
          "address": "75 Drayton Gardens, WEST DRAYTON, Middlesex, UB7 7LQ"
        }
      ],
      "comments": [
        {
          "id": 1,
          "comment": "This is a comment",
          "created_at": 1431936812
        }
      ]
    }
  ]
}
```

Read data by using `method: GET` and specifying `path` to resource you want to access. Get object by id with suffix `/{{id}}`

`"path": "jobs"`

## Create/Update

```shell
curl\
 -X POST\
 -H "Content-Type: application/json"\
 -H "X-Application: {{APPLICATION_TOKEN}}"\
 -H "Authorization: {{AUTHORIZATION_TOKEN}}"\
 -d '{
       "comment": "This is a comment"
   }'\
 "https://playground.1dxr.com/jobs/12/comments"
```

> The above request success response is:

```json
{
    "data": null,
    "success": [
        {
            "code": 1020,
            "message": "Comment created.",
            "debug_message": null,
            "debug_id": 213124
        }
    ]
}
```


Create objects by using `method: POST` and specifying `path` to resource you want to create.

`"path": "jobs/{{id}}/comments"`

## Delete

```shell
curl\
 -X DELETE\
 -H "Content-Type: application/json"\
 -H "X-Application: {{APPLICATION_TOKEN}}"\
 -H "Authorization: {{AUTHORIZATION_TOKEN}}"\
 -d ''\
 "https://playground.1dxr.com/jobs/12/comments/255"
```

> The above request success response is:

```json
{
  "data": null,
  "success": [
    {
      "code": 1020,
      "message": "Comment deleted.",
      "debug_message": null,
      "debug_id": 213124
    }
  ]
}
```

Delete objects by using `method: DELETE` and specifying `path` and `/{{id}}` suffix for object to delete.

`"path": "jobs/{{id}}/comments/{{id}}"`

If object is deleted successfully `"success"` is returned.

# Endpoints


## Job


```shell
curl\
 -X GET\
 -H "Content-Type: application/json"\
 -H "X-Application: {{APPLICATION_TOKEN}}"\
 -H "Authorization: {{AUTHORIZATION_TOKEN}}"\
"https://playground.1dxr.com/jobs"
```

> The above request success response is:

```json
{
  "data": [
    {
      "id": 2584075,
      "app_time": 1504620000,
      "addresses": [
        {
          "id": 1,
          "postcode": "UB7 7LQ",
          "address": "75 Drayton Gardens, WEST DRAYTON, Middlesex, UB7 7LQ"
        }
      ],
      "comments": [
        {
          "id": 1,
          "comment": "This is a comment",
          "created_at": 1431936812
        }
      ]
    }
  ]
}
```

Job object containing details about an appointment.

`"path": "jobs"`

### Response parameters

Parameter | Type | Description
-------- | ----- | -------
`id` | *integer* | Unique identifier
`app_time` | *integer* | Appointment time in UTC timestamp
`addresses` | *array<address>* | List of addresses for the appointment
`addresses.id` | *integer* | Unique identifier
`addresses.postcode` | *string* | Postal code of the address
`addresses.address` | *string* | More details about the address - street name, street number, apartment number etc.
`comments`<br>*editable* | *array<comment>* | List of comments
`comments.id` | *integer* | Unique identifier
`comments.comment` | *string* | More details about the address - street name, street number, apartment number etc.
`comments.created_at` | *integer* | Comment creation time in UTC timestamp

This endpoint returns:

* [Common errors](#common-errors)

