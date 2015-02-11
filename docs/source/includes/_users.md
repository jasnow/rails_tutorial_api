# Users

## List Users
```http
GET /api/v1/users HTTP/1.1
User-Agent: MyClient/1.0.0
Accept: application/json
```
```http
HTTP/1.1 200 OK
Content-Length: 4567
{
  "users":[
    {
      "id":89,
      "email":"example-88@railstutorial.org",
      "name":"Kenna Ondricka",
      "activated":true,
      "created_at":"2015-01-13T20:35:47Z",
      "updated_at":"2015-02-02T22:09:50Z",
      "micropost_ids":[],
      "following_ids":[],
      "follower_ids":[]
    },
    {
      "id":90,
      "email":"example-89@railstutorial.org",
      "name":"Della Oberbrunner PhD",
      "activated":true,
      "created_at":"2015-01-13T20:35:47Z",
      "updated_at":"2015-02-02T22:09:50Z",
      "micropost_ids":[],
      "following_ids":[],
      "follower_ids":[]
    }
  ],
  "meta":{
    "current_page":45,
    "next_page":46,
    "prev_page":44,
    "total_pages":53,
    "total_count":105
  }
}
```

You can GET all users in /api/v1/users.
It doesn't require authentication.


## Create a User
```http
POST /api/v1/users HTTP/1.1
User-Agent: MyClient/1.0.0
Accept: application/json

{
  "user": {
    "id":89,
    "email":"example-88@railstutorial.org",
    "name":"Kenna Ondricka",
  }
}
```
```http
HTTP/1.1 200 OK
Content-Length: 4567
{
  "user": {
    "id":89,
    "email":"example-88@railstutorial.org",
    "name":"Kenna Ondricka",
    "activated":true,
    "created_at":"2015-01-13T20:35:47Z",
    "updated_at":"2015-02-02T22:09:50Z",
    "micropost_ids":[],
    "following_ids":[],
    "follower_ids":[]
  }
},
```

You can create a new user sending a POST to `/api/v1/users` with the necessary attributes.
A user object should at least include, an email, a password
It doesn't require authentication.


## Show a User
```http
PUT /api/v1/users/89 HTTP/1.1
User-Agent: MyClient/1.0.0
Accept: application/json
{
  "user": {
    "id":89,
    "email":"example-88@railstutorial.org",
    "name":"An updated name",
  }
}
```
```http
HTTP/1.1 200 OK
Content-Length: 4567
{
  "user": {
    "id":89,
    "email":"example-88@railstutorial.org",
    "name":"An updated name",
    "activated":true,
    "created_at":"2015-01-13T20:35:47Z",
    "updated_at":"2015-02-02T22:09:50Z",
    "micropost_ids":[],
    "following_ids":[],
    "follower_ids":[]
  }
},
```
You can retrieve a user's info by sending a GET request to `/api/v1/users/{id}`.


## Update a User
```http
GET /api/v1/users/89 HTTP/1.1
User-Agent: MyClient/1.0.0
Accept: application/json
```
```http
HTTP/1.1 200 OK
Content-Length: 4567
{
  "user": {
    "id":89,
    "email":"example-88@railstutorial.org",
    "name":"Kenna Ondricka",
    "activated":true,
    "created_at":"2015-01-13T20:35:47Z",
    "updated_at":"2015-02-02T22:09:50Z",
    "micropost_ids":[],
    "following_ids":[],
    "follower_ids":[]
  }
},
```
You can update a user's attributes by sending a PUT request to `/api/v1/users` with the necessary attributes.


## Destroy a User
