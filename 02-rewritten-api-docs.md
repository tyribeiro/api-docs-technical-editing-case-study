# Rewritten API Documentation

This document provides the improved, structured, and technically accurate API reference based on the original notes in `01-original-api-docs.md`.  
The content follows standard API documentation conventions and global English principles.

---

# 1. Authentication

All endpoints require an API key provided in the following header:

Authorization: Bearer {api_key}

Requests without a valid authentication header will return HTTP 401 Unauthorized.

---

# 2. API Endpoints

## 2.1 Update User  
**POST /user/update**

Updates an existing user record.

### Required Fields
- `userId` (string): Unique user identifier  
- `email` (string): Valid email address  

### Optional Fields
- `name` (string): Full name of the user  
- `phone` (string): Telephone number in E.164 format  

### Request Body Example
{
"userId": "12345",
"email": "test@example.com
",
"name": "Jane Doe"
}


### Successful Response
"success": true,
"updatedUserId": "12345"
}


### Error Responses
- **400 Bad Request**: Missing required fields or invalid data format  
- **404 Not Found**: User does not exist  
- **500 Internal Server Error**: Unexpected server error  

---

## 2.2 Get User Information  
**GET /user**

Retrieves user information.

### Query Parameters
- `userId` (string, required): The user identifier  

### Example Request  
`GET /user?userId=12345`

### Successful Response
{
"userId": "12345",
"email": "test@example.com
",
"name": "Jane Doe"
}


### Error Responses
- **400 Bad Request**: Missing `userId` parameter  
- **404 Not Found**: User does not exist  

---

## 2.3 Process Return  
**POST /return/process**

Processes a customer return event.

### Required Fields
- `itemId` (string): Unique item identifier  
- `status` (string): Return status. Accepted values:  
  - "initiated"  
  - "received"  
  - "approved"  
  - "rejected"  

### Request Body Example
{
"itemId": "A1001",
"status": "initiated"
}


### Successful Response
{
"success": true,
"processedItemId": "A1001"
}

### Error Responses
- **400 Bad Request**: Missing required fields  
- **422 Unprocessable Entity**: Unsupported return status value  
- **500 Internal Server Error**: Unexpected server error  

---

## Notes on Response Consistency

- All endpoints return JSON.  
- Successful responses include `"success": true`.  
- Error responses include:
  - `success: false`  
  - `errorCode`  
  - `message`  

This ensures consistent handling across clients.
