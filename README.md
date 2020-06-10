# GoBarber Backend

## Api Version: 1.0

### Overview

The GoBarber backend brings together all of GoBarber modules. GoBarber-Web and GoBarber-mobile uses it to fill in data for user experience.

## Sessions

### [POST] /sessions

##### Overview

Starts a new user session.

###### URL

    /sessions

###### Request Body

- `email` - user e-mail **(required)**.
- `password` - user password **(required)**.

###### Response

A JSON object containing JWT token and user info.

```javascript
{
  "user": {
    "id": "29d77c71-1029-4255-bd8e-5ba47b64468f",
    "name": "John Doe",
    "email": "example@example.com",
    "avatar": "08cf793dc517edacd0d6.jpg",
    "created_at": "1970-01-01T00:00:0.000Z",
    "updated_at": "1970-01-01T00:00:0.000Z",
    "avatar_url": "http://localhost:3333/files/08cf793dc517edacd0d6.jpg"
  },
  "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpYXQiOjE1OTE4MTk5MjUsImV4cCI6MTU5MTkwNjMyNSwic3ViIjoiMjlkNzdjNzEtMTAyOS00MjU1LWJkOGUtNWJhNDdiNjQ0NjhmIn0.fwTu0_86frULE0qXf89XZX-IS1hRyojU9v4dVBvbSBg"
}
```

## Providers

### [GET] /providers **(Auth)**

##### Overview

Retrieves all registered providers.

###### URL

    /providers

###### Response

A JSON list containing all providers' info.

```javascript
[{
    "id": "29d77c71-1029-4255-bd8e-5ba47b64468f",
    "name": "John Doe",
    "email": "example@example.com",
    "avatar": "08cf793dc517edacd0d6.jpg",
    "created_at": "1970-01-01T00:00:0.000Z",
    "updated_at": "1970-01-01T00:00:0.000Z",
    "avatar_url": "http://localhost:3333/files/08cf793dc517edacd0d6.jpg"
  }, {...}, ...]
```

### [GET] /providers/:id/day-availability **(Auth)**

##### Overview

Retrieves a provider's schedule for a specific day.

###### URL

    /providers/:id/day-availability

###### Parameters

- `id` - provider id **(required)**
- `day` - schedule day **(required)**.
- `month` - schedule month **(required)**.
- `year` - schedule year **(required)**.

###### Response

A JSON list containing providers' schedule for a specific day.

```javascript
[{
    "hour": 8,
    "available": false
  },
  {
    "hour": 9,
    "available": true
  },
  {...}, ...]
```

### [GET] /providers/:id/month-availability **(Auth)**

##### Overview

Retrieves a provider's schedule for a specific day.

###### URL

    /providers/:id/month-availability

###### Parameters

- `id` - provider id **(required)**
- `month` - schedule month **(required)**.
- `year` - schedule year **(required)**.

###### Response

A JSON list containing providers' schedule for a specific month.

```javascript
[{
    "day": 1,
    "available": true
  },
  {
    "day": 2,
    "available": false
  },
  {...}, ...]
```

## Users

### [POST] /users

##### Overview

Creates a new user.

###### URL

    /users

###### Request Body

- `name` - user name **(required)**.
- `email` - user email **(required)**.
- `password` - user new password **(required)**.

###### Response

A JSON object containing all created user's info.

```javascript
{
  "id": "29d77c71-1029-4255-bd8e-5ba47b64468f",
  "name": "John Doe",
  "email": "example@example.com",
  "created_at": "1970-01-01T00:00:0.000Z",
  "updated_at": "1970-01-01T00:00:0.000Z",
  "avatar_url": null
}
```

### [GET] /profile **(Auth)**

##### Overview

Retrieves signed-in user's info.

###### URL

    /profile

###### Response

A JSON object containing all user's info.

```javascript
{
  "id": "29d77c71-1029-4255-bd8e-5ba47b64468f",
  "name": "John Doe",
  "email": "example@example.com",
  "avatar": "08cf793dc517edacd0d6.jpg",
  "created_at": "1970-01-01T00:00:0.000Z",
  "updated_at": "1970-01-01T00:00:0.000Z",
  "avatar_url": "http://localhost:3333/files/08cf793dc517edacd0d6.jpg"
}
```

### [PUT] /profile **(Auth)**

##### Overview

Updates signed-in user's info.

###### URL

    /profile

###### Request Body

- `name` - user name **(required)**.
- `email` - user email **(required)**.
- `old_password` - user old password.
- `password` - user new password **(required if old_password is given)**.

###### Response

A JSON object containing all user's updated info.

```javascript
{
  "id": "29d77c71-1029-4255-bd8e-5ba47b64468f",
  "name": "John Doe",
  "email": "example@example.com",
  "avatar": "08cf793dc517edacd0d6.jpg",
  "created_at": "1970-01-01T00:00:0.000Z",
  "updated_at": "1970-01-01T00:00:0.000Z",
  "avatar_url": "http://localhost:3333/files/08cf793dc517edacd0d6.jpg"
}
```

### [POST] /password/forgot

##### Overview

Sends an e-mail with token for password recovery.

###### URL

    /password/forgot

###### Response

Empty response (HTTP Code 204)

### [POST] /password/reset

##### Overview

Updates user's password.

###### URL

    /password/reset

###### Request Body

- `password` - user new password **(required)**.
- `token` - recovery token **(required)**.

###### Response

Empty response (HTTP Code 204)

### [PATCH] /users/avatar **(Auth)**

##### Overview

Updates signed-in user's avatar.

###### URL

    /users/avatar

###### Multipart Form

- `avatar` - Image file **(required)**.

###### Response

A JSON object containing all user's updated info.

```javascript
{
  "id": "29d77c71-1029-4255-bd8e-5ba47b64468f",
  "name": "John Doe",
  "email": "example@example.com",
  "avatar": "08cf793dc517edacd0d6.jpg",
  "created_at": "1970-01-01T00:00:0.000Z",
  "updated_at": "1970-01-01T00:00:0.000Z",
  "avatar_url": "http://localhost:3333/files/08cf793dc517edacd0d6.jpg"
}
```

## Appointments

### [GET] /appointments/me **(Auth)**

##### Overview

Retrieves all signed-in user's appointments in a specific day.

###### URL

    /appointments/me

###### Parameters

- `day` - appointments day **(required)**.
- `month` - appointments month **(required)**.
- `year` - appointments year **(required)**.

###### Response

A JSON list containing all appointment's info.

```javascript
[{
    "id": "0a6114ba-9b6d-4146-8536-a45b98ad631f",
    "provider_id": "3fba513a-0b54-4305-81ac-abb5943e5e0b",
    "user_id": "29d77c71-1029-4255-bd8e-5ba47b64468f",
    "date": "1970-01-01T08:00:00.000Z",
    "created_at": "1970-01-01T00:00:00.000Z",
    "updated_at": "1970-01-01T00:00:00.000Z",
    "user": {
      "id": "29d77c71-1029-4255-bd8e-5ba47b64468f",
      "name": "John Doe",
      "email": "example@example.com",
      "avatar": "08cf793dc517edacd0d6.jpg",
      "created_at": "1970-01-01T00:00:00.000Z",
      "updated_at": "1970-01-01T00:00:00.000Z",
      "avatar_url": "http://localhost:3333/files/08cf793dc517edacd0d6.jpg"
    }
  }, {...}, ...]
```

### [POST] /appointments **(Auth)**

##### Overview

Creates a new appointment.

###### URL

    /appointments

###### Request Body

- `provider_id` - provider's id **(required)**.
- `date` - appointment date **(required)**.

###### Response

A JSON object containing appointment's info.

```javascript
{
  "provider_id": "29d77c71-1029-4255-bd8e-5ba47b64468f",
  "user_id": "3fba513a-0b54-4305-81ac-abb5943e5e0b",
  "date": "1970-01-01T08:00:00.000Z",
  "id": "f6933f9d-d966-4313-8199-09443c26516d",
  "created_at": "1970-01-01T00:00:00.000Z",
  "updated_at": "1970-01-01T00:00:00.000Z"
}
```

### Reference

Routes with **(Auth)** requires the Bearer Token to be filled with a valid JWT Token.
