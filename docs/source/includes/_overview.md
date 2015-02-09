# Overview

## General Notes
You are encouraged to always provide a valid `user-agent` string.

## Current Version

The current version of API is V1. The version is defined on the resource, thus reflecting
the resource version and not in the Accept header.

```http
GET /api/v1/resource HTTP/1.1
User-Agent: MyClient/1.0.0
Accept: application/json
Host: rails-tutorial-api.heroku.com
```

## DateTimes representations


All date/time representations are on ISO 8601 format:
```
YYYY-MM-DDTHH:MM:SSZ
```
The returned timezone is UTC.

## Client Errors
```
HTTP/1.1 400 Bad Request
Content-Length: 35

{"message":"Problems parsing JSON"}
```

```
HTTP/1.1 422 Unprocessable Entity
 Content-Length: 149

 {
   "errors": [
     {
       "field": "title",
       "message": "title cannot be blank"
     },
     {
       "field": "description",
       "message": "description must be less than 1000 characters"
     },
   ]
 }
```


```
HTTP/1.1 401 Unprocessable Entity
 Content-Length: 149

 {
   "message": "Authentication Failed",
 }
```


```
HTTP/1.1 403 Unprocessable Entity
 Content-Length: 149

 {
   "message": "Not authorized action for that resource",
 }
```


```
HTTP/1.1 500 Unprocessable Entity
 Content-Length: 149

 {
   "message": "Something went terribly wrong here. Open a github issue :)",
 }
```

The client errors are pretty basic, yet helpful.

Error Code | Meaning
---------- | -------
400 | Bad Request -- You have a critical error on your request, like bad JSON representation
401 | Unauthorized -- You try to access a protected resource without providing authentication credentials or with wrong credentials
403 | Forbidden -- You try to access or act on a protected resource but your credentials that you provide do not authorize your action for that resource.
404 | Not Found -- The specified kitten could not be found
405 | Method Not Allowed -- You tried to access a kitten with an invalid method
406 | Not Acceptable -- You requested a format that isn't json
422 | lalala -- Your request is understood but you miss a required param, or part of your json is in wrong format (like sending an date object in an integer param)
429 | Too Many Requests -- Slown down! Follow the rate limits!
500 | Internal Server Error -- Something went terribly wrong, open a gihub issue :) 


## Authentication and Authentication

```http
GET /api/v1/resource HTTP/1.1
User-Agent: MyClient/1.0.0
Accept: application/vnd.travis-ci.2+json
Host: rails-tutorial-api.heroku.com
Authorization: Token token={token_here} user_email={user_email_here}
```

You can authenticate in the API by providing a token and an email in the `Authorization` header.


However to get that information, you have to send `POST` request to `api/v1/sessions` which is described here.


## Pagination
```http
GET /api/v1/resource?page=2&per_page=100 HTTP/1.1
User-Agent: MyClient/1.0.0
Accept: application/vnd.travis-ci.2+json
Host: rails-tutorial-api.heroku.com
```

Requests that return multiple items will be paginated to 30 items by default.
You can specify further pages with the `?page` parameter.
For some resources, you can also set a custom page size up to 100 with the `?per_page` parameter.


## Rate Limiting
```http
HTTP/1.1 200 OK
Date: Mon, 01 Jul 2013 17:27:06 GMT
Status: 200 OK
X-RateLimit-Limit: 60
X-RateLimit-Remaining: 56
X-RateLimit-Reset: 1372700873
```

For unauthenticated requests there is no limit currently.
However, there is a soft limit for authenticated requests, meaning that even if you pass the limit you will probably still be able to send more requests.

You can check the returned HTTP headers of any API request to see your current rate limit status.

It should be noted that the rate limit is variable, depending on the server load. Please stay on the limits.

If you have abused the limits, you will receive a 429 error as described in the [Client Errors](#client-errors)

<aside class="notice">
Although there are no hard limits, you should follow the limits defined on the API response
</aside>



## Cross Origin Resource Sharing
The API supports Cross Origin Resource Sharing (CORS) for AJAX requests from any origin.

