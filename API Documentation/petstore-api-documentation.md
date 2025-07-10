# Swagger Petstore API Documentation

## Introduction

The Swagger Petstore API is a RESTful API that allows developers to interact with a virtual pet store. It provides endpoints to manage pets, store orders, and user accounts. 

## Base URL:
https://petstore.swagger.io/v2

## Authentication:
This API supports API Key-based authentication. It does not require an API key for most of its endpoints.

```
Authorization: YOUR_API_KEY
```
---

## Table of Contents

1. [Pets](#pets)
   - [Add a Pet](#add-a-pet)
   - [Update a Pet](#update-a-pet)
   - [Find Pets by Status](#find-pets-by-status)
   - [Find Pets by Tags](#find-pets-by-tags)
   - [Get Pet by ID](#get-pet-by-id)
   - [Delete Pet](#delete-pet)
2. [Store](#store)
   - [Place an Order](#place-an-order)
   - [Get Order by ID](#get-order-by-id)
   - [Delete Order](#delete-order)
   - [Get Inventory](#get-inventory)
3. [Users](#users)
   - [Create User](#create-user)
   - [Login User](#login-user)
   - [Logout User](#logout-user)
   - [Get User by Username](#get-user-by-username)
   - [Update User](#update-user)
   - [Delete User](#delete-user)
4. [Error Responses](#error-responses)
5. [Rate Limiting](#rate-limiting)

---

## Pets

### Add a Pet

- **URL:** `/pet`
- **Method:** POST
- **Description:** Add a new pet to the store.

**Request:**
```json
{
  "id": 0,
  "category": {
    "id": 1,
    "name": "Dogs"
  },
  "name": "Rex",
  "photoUrls": [
    "https://example.com/rex.jpg"
  ],
  "tags": [
    {
      "id": 1,
      "name": "friendly"
    }
  ],
  "status": "available"
}
```

**Response:**
```json
{
  "id": 0,
  "category": {
    "id": 1,
    "name": "Dogs"
  },
  "name": "Rex",
  "photoUrls": [
    "https://example.com/rex.jpg"
  ],
  "tags": [
    {
      "id": 1,
      "name": "friendly"
    }
  ],
  "status": "available"
}
```

---

### Update a Pet

- **URL:** `/pet`
- **Method:** PUT
- **Description:** Update an existing pet.

**Request:**
```json
{
  "id": 0,
  "name": "Rex",
  "status": "sold"
}
```

**Response:**
```json
{
  "id": 0,
  "name": "Rex",
  "status": "sold"
}
```

---

### Find Pets by Status

- **URL:** `/pet/findByStatus`
- **Method:** GET
- **Description:** Find pets by status `available`, `pending`, `sold`.
- **Query Parameters:**
  - `status` (string) — pet status

**Response:**
```json
[
  {
    "id": 1,
    "name": "Rex",
    "status": "available"
  }
]
```

---

### Find Pets by Tags

- **URL:** `/pet/findByTags`
- **Method:** GET
- **Description:** Find pets by tags.
- **Query Parameters:**
  - `tags` (string) — tag name

**Response:**
```json
[
  {
    "id": 2,
    "name": "Bella",
    "tags": [
      {
        "id": 1,
        "name": "cute"
      }
    ]
  }
]
```

---

### Get Pet by ID

- **URL:** `/pet/{petId}`
- **Method:** GET
- **Description:** Find pet by ID.
- **URL Parameters:**
  - `petId`: ID of the pet to fetch

**Response:**
```json
{
  "id": 1,
  "name": "Rex",
  "status": "available"
}
```

---

### Delete Pet

- **URL:** `/pet/{petId}`
- **Method:** DELETE
- **Description:** Delete a pet by ID.
- **URL Parameters:**
  - `petId`: ID of the pet to delete

**Response:**
```json
{
  "message": "Pet deleted"
}
```

---

## Store

### Place an Order

- **URL:** `/store/order`
- **Method:** POST
- **Description:** Place an order for a pet.

**Request:**
```json
{
  "id": 1,
  "petId": 2,
  "quantity": 1,
  "shipDate": "2025-07-10T10:00:00.000Z",
  "status": "placed",
  "complete": false
}
```

**Response:**
```json
{
  "id": 1,
  "status": "placed"
}
```

---

### Get Order by ID

- **URL:** `/store/order/{orderId}`
- **Method:** GET
- **Description:** Find purchase order by ID.
- **URL Parameters:**
  - `orderId`: ID of the order to fetch

**Response:**
```json
{
  "id": 1,
  "petId": 2,
  "quantity": 1,
  "status": "placed"
}
```

---

### Delete Order

- **URL:** `/store/order/{orderId}`
- **Method:** DELETE
- **Description:** Delete purchase order by ID.
- **URL Parameters:**
  - `orderId`: ID of the order to delete

**Response:**
```json
{
  "message": "Order deleted"
}
```

---

### Get Inventory

- **URL:** `/store/inventory`
- **Method:** GET
- **Description:** Returns pet inventories by status.

**Response:**
```json
{
  "available": 12,
  "pending": 2,
  "sold": 1
}
```

---

## Users

### Create User

- **URL:** `/user`
- **Method:** POST
- **Description:** Create a new user.

**Request:**
```json
{
  "id": 1,
  "username": "johndoe",
  "firstName": "John",
  "lastName": "Doe",
  "email": "john@example.com",
  "password": "password123",
  "phone": "1234567890",
  "userStatus": 1
}
```

**Response:**
```json
{
  "code": 200,
  "message": "User created"
}
```

---

### Login User

- **URL:** `/user/login`
- **Method:** GET
- **Description:** Log user into the system.
- **Query Parameters:**
  - `username`: user's username
  - `password`: user's password

**Response:**
```json
{
  "code": 200,
  "message": "Logged in successfully",
  "token": "abcdef12345"
}
```

---

### Logout User

- **URL:** `/user/logout`
- **Method:** GET
- **Description:** Log out the current user.

**Response:**
```json
{
  "code": 200,
  "message": "Logged out"
}
```

---

### Get User by Username

- **URL:** `/user/{username}`
- **Method:** GET
- **Description:** Get user by username.
- **URL Parameters:**
  - `username`: name of the user to fetch

**Response:**
```json
{
  "id": 1,
  "username": "johndoe",
  "email": "john@example.com"
}
```

---

### Update User

- **URL:** `/user/{username}`
- **Method:** PUT
- **Description:** Update user information.
- **URL Parameters:**
  - `username`: name of the user to update

**Request:**
```json
{
  "firstName": "Johnny",
  "email": "johnny@example.com"
}
```

**Response:**
```json
{
  "code": 200,
  "message": "User updated"
}
```

---

### Delete User

- **URL:** `/user/{username}`
- **Method:** DELETE
- **Description:** Delete user by username.
- **URL Parameters:**
  - `username`: name of the user to delete

**Response:**
```json
{
  "code": 200,
  "message": "User deleted"
}
```

---

## Error Responses

**Structure:**
```json
{
  "code": 400,
  "type": "error",
  "message": "Invalid input"
}
```

| Code | Type      | Description                                          |
|------|-----------|----------------------------------|
| 400  | Bad Request | Invalid syntax or request data   |
| 401  | Unauthorized | Missing or invalid credentials  |
| 404  | Not Found  | Resource does not exist          |
| 405  | Method Not Allowed | HTTP method not supported |
| 500  | Server Error | Internal server error           |

---

## Rate Limiting

- **Limit:** 1000 requests per minute

**Response When Exceeded:**
```json
{
  "code": 429,
  "message": "Too many requests. Try again later."
}
```
