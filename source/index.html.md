---
title: API Reference

<!--language_tabs: # must be one of https://git.io/vQNgJ-->
<!--  - curl-->

toc_footers:
  - <a href='https://eff-dev.herokuapp.com/'>Development Base URL</a>

search: true
---

# Introduction

## General

This document should serve as the de-facto guide for the Eff API. It aims to cover all aspects of the RESTful API upon which the main website is built. If you see any issues please do not hesitate to open up an issue in the repository from which this was cloned.  

## JSON Formatting

The JSON request and response body code blocks borrow from Swift's type declaration syntax. While the keys are always strings, the values are declared by the type expected. Values that have the potential of being nil are represented with a question mark. For example, if a key is always expected to return a string it is declared as `String` –– similarly if that key has the potential of being nil inside of a response then it will be marked as `String?`. The same applies for requests.

## Signed Requests

There are certain requests that are required to be signed with an authentication token. The appropriate manner to do this is through a header with the `Authorization` key. The value of this header should contain the word `Bearer` with a single space and then finally the authentication token of the user attempting to make the request. The following is an example of such a header. `"Authorization: Bearer BFF2F560-1AC3-4131-BA94-8E1BA8921799"`

# Authentication

## Register

> Request Body:

```swift
{
    "session":  {
        "name" : String
    },
    "user":  {
        "bio": String?
        "email": String
        "location": String?
        "name": String
        "password": String
        "username": String
        "website": String?
    }
}
```


> Response Body:

```swift
{
    "session": {
        "token": String
        "name": String
    }
    "user": {
        "bio": String?
        "email": String
        "id": UUID
        "location": String?
        "name": String
        "username": String
        "website": String?
    }
}
```
`POST users/register`

This endpoint registers a new user.

## Login 

> Request Body:

```swift
{
    "email": String
    "password": String
}
```

> Response Body:

```swift
{
    "session": {
        "token": String
        "name": String
    }
    "user": {
        "bio": String?
        "email": String
        "id": UUID
        "location": String?
        "name": String
        "username": String
        "website": String?
    }
}
```

`POST users/register`

Obtain an authorization token for an existing user to use for future signed requests.

# Debug

## Ping

> Response Body:

```
pong
```

`GET debug/ping`

Ping the server.


# Users

## Me

> Response Body:

```swift
"user": {
    "bio": String?
    "email": String
    "id": UUID
    "location": String?
    "name": String
    "username": String
    "website": String?
}
```

`GET users/me`

Fetch data about the logged in user.

<aside class="notice">
This is a signed request.
</aside>

## Fetch

> Response Body:

```swift
"user": {
    "bio": String?
    "email": String
    "id": UUID
    "location": String?
    "name": String
    "username": String
    "website": String?
}
```

`GET users/:id`

Fetch a user by their ID.

## Update

> Request Body:

```swift
{
    "bio": String?
    "email": String?
    "location": String?
    "name": String?
    "username": String?
    "website": String?
}
```

> Response Body:

```swift
{
    "bio": String?
    "email": String?
    "location": String?
    "name": String?
    "username": String?
    "website": String?
}
```

`PUT users/me/update`

Update details of the logged in user.

<aside class="notice">
Signed request.
</aside>
