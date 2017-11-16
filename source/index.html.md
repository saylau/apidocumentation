---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell
  - ruby
  - python
  - javascript

toc_footers:
  - <a href='#'>Sign Up for a Developer Key</a>
  - <a href='https://github.com/lord/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true
---

# Introduction

Welcome to the SDU alumni API!
# User

## Sign Up

```shell
curl "http://SERVER_NAME/v1/users"

body
{ "user":
	{
		"email" : "ts1@gmail.com",
		"password" : "123456789",
		"password_confirmation" : "123456789",
		"specialty_id" : 1,

		"graduation_date" : "2017-01-01",
		"faculty_id": 1,
		"industry_ids" :[1,2,3]
		
	}
}
```



> The above command returns JSON structured like this:

```json
{
    "data": {
        "user": {
            "id": 23,
            "email": "ts1@gmail.com",
            "authentication_token": "2CCC9G3xDpsgkyP1iMd_"
        }
    }
}
```

This endpoint registers new user. Returns authentification Token for current session

### HTTP Request

`POST http://SERVER_NAME/v1/users`

### Request Body Parameters

Parameter | Required | Type | Description
--------- | ------- |------| ----------------
email | Yes | String | User's email
password | Yes | String | User's password
password_confiramtion| Yes | String | Password confirmation
faculty_id | Yes | int | Id of faculty, which user graduated
specialty_id |  Yes | int | Id of user's specialty, in specified faculty
graduation_date | Yes | int | User's graduation date
industry_ids | Optional | int array | User's current industry sphares
first_name | Optional | string | User's first name
last_name | Optional | string | User's surname


<aside class="success">
Remember — a happy user is an authenticated user!
</aside>

## Sign In





```shell
curl "http://SERVER_NAME/v1/sessions"

body
{
	"email": "macie_howell@smitham.com",
	"password":"123456789"
}

```

> The above command returns JSON structured like this:

```json
{
    "data": {
        "user": {
            "id": 4,
            "email": "macie_howell@smitham.com",
            "authentication_token": "y63gSE2ooYxJYGcjpqhT"
        }
    }
}
```

This endpoint creates session and authentification token for user's current session.


### HTTP Request

`POST http://SERVER_NAME/v1/sessions`

### Request Body Parameters

Parameter | Requaired | Type | Description
--------- | ------- |------| -----------
email | Yes | String | User's email
password | Yes | String | User's password
## Destroy session



```shell
curl "http://example.com/v1/sessions"
  -H "X-User-Email: kyra@schroeder.net" 
  -H "X-User-Token: aCzvjX7omkMZAGMk4VMb"
```



> The above command returns no data, just status 

```json

```

This endpoint destroys a specific session.Headers "X-User-Email:" and "X-User-Token" required.

### HTTP Request

`DELETE http://SERVER_NAME/v1/sessions`




### Headers
Header Name | Description
------------|---------
X-User-Email | Current user's email
X-User-Token | Current user's authentification token for current session 

## Profile Info

This endpoint gets information about specified user(current user can specify himself).

```shell
curl "http://example.com/v1/users/2"
  -H "X-User-Email: kyra@schroeder.net" 
  -H "X-User-Token: aCzvjX7omkMZAGMk4VMb"
```



> The above command returns no data, just status 

```json
{
    "is_friend": false,
    "friends": 1,
    "data": {
        "id": 2,
        "email": "kyra@schroeder.net",
        "first_name": "Janie",
        "last_name": "Harber",
        "graduation_date": "2002-01-09",
        "specialty_id": 17,
        "specialty": "Учет и аудит",
        "faculty": "Инженерии и естественных наук",
        "industry": null
    }
}
```

Headers "X-User-Email:" and "X-User-Token" required.

### HTTP Request

`GET http://SERVER_NAME/v1/users/(:id)`

### URL Parameters

Parameter | Requaired | Type | Description
--------- | ------- |------| -----------
(:id) | Yes | int | Id of user, whose profile info we want to get




### Headers
Header Name | Description
------------|---------
X-User-Email | Current user's email
X-User-Token | Current user's authentification token for current session 

## Update User info

This endpoint updates information about user.User must be authenticated to do this request.

```shell
curl "http://example.com/v1/users/"
  -H "X-User-Email: kyra@schroeder.net" 
  -H "X-User-Token: aCzvjX7omkMZAGMk4VMb"
```



> The above command returns no data, just status 

```json
{
    "is_friend": false,
    "friends": 1,
    "data": {
        "id": 2,
        "email": "kyra@schroeder.net",
        "first_name": "Janie",
        "last_name": "Harber",
        "graduation_date": "2002-01-09",
        "specialty_id": 17,
        "specialty": "Учет и аудит",
        "faculty": "Инженерии и естественных наук",
        "industry": null
    }
}
```

Headers "X-User-Email:" and "X-User-Token" required.

### HTTP Request

`PUT http://SERVER_NAME/v1/users/(:id)`

### Request Body Parameters

Parameter | Required | Type | Description
--------- | ------- |------| ----------------
email | Optional | String | User's email
password | Optional | String | User's password
password_confiramtion| Optional | String | Password confirmation
faculty_id | Optional | int | Id of faculty, which user graduated
specialty_id |  Optional | int | Id of user's specialty, in specified faculty
graduation_date | Optional | int | User's graduation date
industry_ids | Optional | int array | User's current industry sphares
first_name | Optional | string | User's first name
last_name | Optional | string | User's surname



### Headers
Header Name | Description
------------|---------
X-User-Email | Current user's email
X-User-Token | Current user's authentification token for current session 



## Search User

This endpoint gets list of users by filter params.

```shell
curl "http://localhost:3000/v1/find_friends?by_period[started_at]=20000101&by_period[ended_at]=202001013"
  -H "X-User-Email: kyra@schroeder.net" 
  -H "X-User-Token: aCzvjX7omkMZAGMk4VMb"
```



> The above command returns no data, just status 

```json
{
    "data": [
        {
            "id": 1,
            "email": "zshanabek@gmail.com",
            "first_name": "Anya",
            "last_name": "Kessler",
            "graduation_date": "2017-01-26",
            "specialty_id": 1,
            "faculty_id": 3,
            "industry": []
        },
        {
            "id": 2,
            "email": "haie_auer@oberbrunner.com",
            "first_name": "Garfield",
            "last_name": "Pfannerstill",
            "graduation_date": "2013-10-21",
            "specialty_id": 21,
            "faculty_id": 1,
            "industry": []
        },
        {
            "id": 3,
            "email": "aracely.predovic@mayershanahan.co",
            "first_name": "Princess",
            "last_name": "Hane",
            "graduation_date": "2002-04-26",
            "specialty_id": 16,
            "faculty_id": 4,
            "industry": []
        }
    ]
}
```

Headers "X-User-Email:" and "X-User-Token" required.

### HTTP Request

`GET http://SERVER_NAME/v1/find_friends`

### URL Parameters

Parameter | Required | Type | Description
--------- | ------- |------| ---------------------
by_period[started_at] | Optional | int | Start of time period, in which filter will search for user's graduation date
by_period[ended_at] | Optional(YES if "by_period[started_at]" specified) | int | End of time period
by_faculty | Optional | int | Id of faculty
by_specialty | Optional | int | Id of specialty in faculty
by_industry | Optional | int | Id of industry



### Headers
Header Name | Description
------------|---------
X-User-Email | Current user's email
X-User-Token | Current user's authentification token for current session 


# User Connections (Friendship)





##User's friends

This endpoint shows list of friends of specified user.
Headers "X-User-Email:" and "X-User-Token" required


```shell
curl "http://localhost:3000/v1/requested_friends"
  -H "X-User-Token: 2rkx82qQJYqZPyDdyGpz"
  -H "X-User-Email: kyra@schroeder.net"
```

> The above command returns JSON structured like this:

```json
{
    "data": [
        {
            "id": 4,
            "email": "macie_howell@smitham.com",
            "first_name": "Claude",
            "last_name": "Fritsch",
            "graduation_date": "2016-03-13",
            "specialty_id": 19,
            "faculty_id": 3,
            "industry": []
        },
        {
            "id": 1,
            "email": "zshanabek@gmail.com",
            "first_name": "Anya",
            "last_name": "Kessler",
            "graduation_date": "2017-01-26",
            "specialty_id": 1,
            "faculty_id": 3,
            "industry": []
        }
    ]
}
```



### HTTP Request

`GET http://localhost:3000/v1/users/(:user_id)/friends`

### Headers
Header Name | Description
------------|---------
X-User-Email | Current user's email
X-User-Token | Current user's authentification token for current session 

### URL Parameters

Parameter | Required | Type | Description
--------- | ------- |------| -----------
(:user_id) | Yes | int | Id of user, whose friends list you want to see


##Friendship request

This endpoint makes friendship request from current user to specified user.
Headers "X-User-Email:" and "X-User-Token" required

```shell
curl "http://SERVER_NAME/v1/users/2/friendships"
  -H "X-User-Token: 7i9cM2-z7TrwhGLiP66B"
  -H "X-User-Email: temmir@gmail.com"
```

> The above command returns JSON structured like this:

```json
{
    "is_friend": false,
    "friends": 1,
    "data": {
        "id": 2,
        "email": "kyra@schroeder.net",
        "first_name": "Janie",
        "last_name": "Harber",
        "graduation_date": "2002-01-09",
        "specialty_id": 17,
        "specialty": "Учет и аудит",
        "faculty": "Инженерии и естественных наук",
        "industry": null
    }
}
```



### HTTP Request

`POST http://SERVER_NAME/v1/users/:user_id/friendships`

### URL Parameters

Parameter | Required | Type | Description
--------- | ------- |------| -----------
(:user_id) | Yes | int | Id of user which you want to add as friend


### Headers
Header Name | Description
------------|---------
X-User-Email | Current user's email
X-User-Token | Current user's authentification token for current session 

##Friendship accept

This endpoint accepts friendship request of specified user.
Headers "X-User-Email:" and "X-User-Token" required


```shell
curl "http://localhost:3000/v1/users/22/accept"
  -H "X-User-Token: 2rkx82qQJYqZPyDdyGpz"
  -H "X-User-Email: zshanabek@gmail.com"
```

> The above command returns JSON structured like this:

```json
{
    "is_friend": true,
    "friends": 1,
    "data": {
        "id": 22,
        "email": "temmir@gmail.com",
        "first_name": null,
        "last_name": null,
        "graduation_date": "2017-01-01",
        "specialty_id": 1,
        "specialty": "Информационные системы",
        "faculty": "Инженерии и естественных наук",
        "industry": null
    }
}
```



### HTTP Request

`PUT http://localhost:3000/v1/users/(:user_id)/accept`

### URL Parameters

Parameter | Required | Type | Description
--------- | ------- |------| -----------
(:user_id) | Yes | int | Id of user which you want to add as friend

### Headers
Header Name | Description
------------|---------
X-User-Email | Current user's email
X-User-Token | Current user's authentification token for current session 

##Friendship decline

This endpoint declines friendship request of specified user.
Headers "X-User-Email:" and "X-User-Token" required


```shell
curl "http://localhost:3000/v1/users/22/decline"
  -H "X-User-Token: 2rkx82qQJYqZPyDdyGpz"
  -H "X-User-Email: kyra@schroeder.net"
```

> The above command returns JSON structured like this:

```json
{
    "is_friend": false,
    "friends": 1,
    "data": {
        "id": 22,
        "email": "temmir@gmail.com",
        "first_name": null,
        "last_name": null,
        "graduation_date": "2017-01-01",
        "specialty_id": 1,
        "specialty": "Информационные системы",
        "faculty": "Инженерии и естественных наук",
        "industry": null
    }
}
```



### HTTP Request

`PUT http://localhost:3000/v1/users/(:user_id)/decline`

### URL Parameters

Parameter | Required | Type | Description
--------- | ------- |------| -----------
(:user_id) | Yes | int | Id of user which you want to add as friend

### Headers
Header Name | Description
------------|---------
X-User-Email | Current user's email
X-User-Token | Current user's authentification token for current session 

##Get Requested Friendships

This endpoint shows list of friendship requests for current user.
Headers "X-User-Email:" and "X-User-Token" required


```shell
curl "http://localhost:3000/v1/requested_friends"
  -H "X-User-Token: 2rkx82qQJYqZPyDdyGpz"
  -H "X-User-Email: kyra@schroeder.net"
```

> The above command returns JSON structured like this:

```json
{
    "data": [
        {
            "id": 4,
            "email": "macie_howell@smitham.com",
            "first_name": "Claude",
            "last_name": "Fritsch",
            "graduation_date": "2016-03-13",
            "specialty_id": 19,
            "faculty_id": 3,
            "industry": []
        },
        {
            "id": 1,
            "email": "zshanabek@gmail.com",
            "first_name": "Anya",
            "last_name": "Kessler",
            "graduation_date": "2017-01-26",
            "specialty_id": 1,
            "faculty_id": 3,
            "industry": []
        }
    ]
}
```



### HTTP Request

`GET http://localhost:3000/v1/requested_friends`

### Headers
Header Name | Description
------------|---------
X-User-Email | Current user's email
X-User-Token | Current user's authentification token for current session 

##Get Pending Friendships

This endpoint shows list of currents user's friendship requests,that are not accepted or declined yet.
Headers "X-User-Email:" and "X-User-Token" required


```shell
curl "http://localhost:3000/v1/pending_friends"
  -H "X-User-Token: 2rkx82qQJYqZPyDdyGpz"
  -H "X-User-Email: zshanabek@gmail.com"
```

> The above command returns JSON structured like this:

```json
{
    "data": [
        {
            "id": 2,
            "email": "haie_auer@oberbrunner.com",
            "first_name": "Garfield",
            "last_name": "Pfannerstill",
            "graduation_date": "2013-10-21",
            "specialty_id": 21,
            "faculty_id": 1,
            "industry": []
        },
        {
            "id": 3,
            "email": "aracely.predovic@mayershanahan.co",
            "first_name": "Princess",
            "last_name": "Hane",
            "graduation_date": "2002-04-26",
            "specialty_id": 16,
            "faculty_id": 4,
            "industry": []
        }
    ]
}
```



### HTTP Request

`GET http://localhost:3000/v1/pending_friends`


### Headers
Header Name | Description
------------|---------
X-User-Email | Current user's email
X-User-Token | Current user's authentification token for current session 



##Remove friend

This endpoint removes specified user from current user's friends.
Headers "X-User-Email:" and "X-User-Token" required


```shell
curl "http://localhost:3000/v1/users/(:user_id)/remove"
  -H "X-User-Token: 2rkx82qQJYqZPyDdyGpz"
  -H "X-User-Email: zshanabek@gmail.com"
```

> The above command returns JSON structured like this:

```json
{
    "is_friend": false,
    "friends": 0,
    "data": {
        "id": 1,
        "email": "zshanabek@gmail.com",
        "first_name": "Anya",
        "last_name": "Kessler",
        "graduation_date": "2017-01-26",
        "specialty_id": 1,
        "faculty_id": 3,
        "industry": null
    }
}
```



### HTTP Request

`PUT http://localhost:3000/v1/users/(:user_id)/remove`

### URL Parameters

Parameter | Required | Type | Description
--------- | ------- |------| -----------
(:user_id) | Yes | int | Id of user which you want to remove from friends list

### Headers
Header Name | Description
------------|---------
X-User-Email | Current user's email
X-User-Token | Current user's authentification token for current session 


# Static Data

Requests to get static data as: faculties, specialties and industries


## Get Faculty list

```shell
  curl "http://localhost:3000/v1/faculties"
```


> The above command returns JSON structured like this:

```json
{
    "data": [
        {
            "id": 1,
            "name": "Инженерии и естественных наук"
        },
        {
            "id": 2,
            "name": "Юриспруденции и социально-гуманитарных наук"
        },
        {
            "id": 3,
            "name": "Педогогических и гуманитарных наук"
        },
        {
            "id": 4,
            "name": "Бизнес-школа СДУ"
        }
    ]
}
```

This endpoint get list of faculties


### HTTP Request

`GET http://localhost:3000/v1/faculties`




## Get Specialty list


```shell
  curl "http://localhost:3000/v1/specialties"
```


> The above command returns JSON structured like this:

```json
{
    "data": [
        {
            "id": 1,
            "name": "Информационные системы",
            "faculty_id": 1
        },
        {
            "id": 2,
            "name": "Вычислительная техника и программное обеспечение",
            "faculty_id": 1
        },
        {
            "id": 3,
            "name": "Математика (научная)",
            "faculty_id": 1
        }
    ]
}
```

This endpoint get list of specialties with faculty ids


### HTTP Request

`GET http://localhost:3000/v1/specialties`


## Get Industry list


```shell
  curl "http://localhost:3000/v1/industries"
```

> The above command returns JSON structured like this:

```json
{
    "data": [
        {
            "id": 1,
            "name": "Маркетинг"
        },
        {
            "id": 2,
            "name": "Информационные технологии"
        },
        {
            "id": 3,
            "name": "Бухгалтерский учёт"
        }
    ]
}
```

This endpoint get list of industries


### HTTP Request

`GET http://localhost:3000/v1/industries`



