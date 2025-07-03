# Requirements Specification
## 1. User Authentication
    Enables users to register, log in, and access secure areas of the application. Handles authentication tokens (e.g., JWT).
### API Endpoints
    POST /api/auth/register

    Input(JSON):
``` 
{
  "firstName": "Jane",
  "lastName": "Doe",
  "email": "jane@example.com",
  "password": "Secret123!",
  "phoneNumber": "0712345678",
  "role": "guest"
}
```
    Validation:
    - Email must be valid and unique
    - Password must be at least 8 characters

    Output (Success - 201 Created)
<br />

    GET /api/auth/me

``` Header: Authorization: Bearer <jwt_token> ```

    Output(200):
``` 
{
"userId": "uuid",
"email": "jane@example.com",
"role": "guest"
}
```

## 2. Property Management
### API Endpoints
    POST /api/properties/add

    Input(JSON):
```
{
  "name": "Seaside Villa",
  "description": "A villa with ocean view.",
  "location": "Mombasa, Kenya",
  "pricePerNight": 120.00
}
```
    Validation:
    - Authenticated host required
    - Name required (3–100 chars)
    - Price must be > 0
<br/>

    Output(201) - Success, Created
```
{
  "message": "Property created",
  "propertyId": "uuid"
}
```

    GET /api/properties

    Input:
    As Query Params : (location, priceMin, priceMax)

    Output(200):

```
[
  {
    "propertyId": "uuid",
    "name": "Seaside Villa",
    "location": "Mombasa, Kenya",
    "pricePerNight": 120.00
  }
]
```

## 3. Booking System
### API Endpoints
    POST /api/bookings

    Input(JSON):
```
{
  "propertyId": "uuid",
  "startDate": "2025-08-10",
  "endDate": "2025-08-12"
}
```
    Validation:
    - Guest must be authenticated
    - Dates must not overlap existing bookings
    - Property must exist
<br/>

    Output(201) - Success, Created:
```
{
"bookingId": "uuid",
"totalPrice": 240.00,
"status": "pending"
}
```