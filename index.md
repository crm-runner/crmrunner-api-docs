---
title: CRM Runner API Documentation
---

# CRM Runner API Documentation

## Overview
CRM Runner provides a RESTful API that allows external integrations to manage CRM data such as Leads, Contacts, Tasks, and more.  
This Zapier integration currently supports **creating leads** inside CRM Runner.

**Base URL:**  
```
https://crm.crmrunner.com:4500
```

---

## Authentication

To connect CRM Runner with Zapier, you’ll need to log in with your **CRM Runner username** and password.

- **Username** → This is the same username you use to log into [CRM Runner](https://crmrunner.com/).
- **Password** → Your account password.

⚠️ Note: It is **not your email address** unless your CRM Runner account username is your email.  
If you are unsure, check how you normally log into the CRM Runner web application.

CRM Runner uses **JWT-based authentication**.

**Login Endpoint**
```
POST /login
```

**Request**
```json
{
  "username": "user@example.com",
  "password": "mypassword"
}
```

**Response**
```json
{
  "token": "<JWT_TOKEN>",
  "expires_in": 3600
}
```

Use the token in all subsequent requests:
```
Authorization: Bearer <JWT_TOKEN>
```

---

## Endpoints

### 1. Test Authentication
```
GET /users
```
Returns user profile if authentication is valid.

**Response Example**
```json
{
  "id": "12345",
  "email": "user@example.com",
  "first_name": "John",
  "last_name": "Doe"
}
```

---

### 2. Create Lead
```
POST /zapier/leads
```

**Headers**
```
Authorization: Bearer <JWT_TOKEN>
Content-Type: application/json
```

**Request Example**
```json
{
  "first_name": "John",
  "last_name": "Doe",
  "email_id": "john@example.com",
  "phone": {
    "phone_countrycode": "US",
    "phone_dialCode": "1",
    "phone": "5551234"
  },
  "mobile": {
    "mobile_countrycode": "IN",
    "mobile_dialCode": "91",
    "mobile": "9876543210"
  },
  "billing_address": {
    "country": "IE",
    "city": "Dublin",
    "zip": "D01",
    "address": "123 Main St"
  },
  "company_name": "Acme Corp",
  "refered_by": "Google Sheet",
  "tag": "zap"
}
```

**Response Example**
```json
{
  "_id": "64a91c2b4f99f12d34567890",
  "first_name": "John",
  "last_name": "Doe",
  "email_id": "john@example.com",
  "company_name": "Acme Corp",
  "created_at": "2025-08-26T14:23:00Z"
}
```

---

## Error Codes
- **401 Unauthorized** → Invalid credentials or expired token  
- **400 Bad Request** → Missing required fields  
- **500 Server Error** → Internal server issue  

---

## Example cURL
```bash
curl -X POST https://crm.crmrunner.com:4500/zapier/leads -H "Authorization: Bearer <JWT>" -H "Content-Type: application/json" -d '{
  "first_name":"John",
  "last_name":"Doe",
  "email_id":"john@example.com",
  "company_name":"Acme"
}'
```

---

## Support
- **Technical Contact:** abhiranjan.mukherjee@gmail.com  
- **Marketing Contact:** info@crmrunner.com  
- **Response Time:** Within 24 hours
