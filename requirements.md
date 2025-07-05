# Requirement Specifications for Airbnb Clone Backend

## User Authentication

- **Endpoint:** `POST /api/register`
  - **Input:** `{ "username": string, "email": string, "password": string, "role": string }`
  - **Output:** `{ "message": "User registered successfully", "user_id": integer }` or `{ "error": "Error message" }`
  - **Validation:** Username unique, email valid and unique, password ≥ 8 chars, role in ['host', 'guest']
  - **Performance:** < 2 seconds

- **Endpoint:** `POST /api/login`
  - **Input:** `{ "email": string, "password": string }`
  - **Output:** `{ "message": "Login successful", "token": string }` or `{ "error": "Invalid credentials" }`
  - **Validation:** Email and password match existing user
  - **Performance:** < 1 second

## Property Management

- **Endpoint:** `POST /api/properties`
  - **Input:** `{ "title": string, "description": string, "location": string, "price": decimal }`
  - **Output:** `{ "message": "Property listed successfully", "property_id": integer }` or `{ "error": "Error message" }`
  - **Validation:** User is host, title and location not empty, price > 0
  - **Performance:** < 3 seconds

- **Endpoint:** `PUT /api/properties/{id}`
  - **Input:** `{ "title": string, "description": string, "location": string, "price": decimal }`
  - **Output:** `{ "message": "Property updated successfully" }` or `{ "error": "Error message" }`
  - **Validation:** User is property owner, fields valid
  - **Performance:** < 2 seconds

## Booking System

- **Endpoint:** `POST /api/bookings`
  - **Input:** `{ "property_id": integer, "check_in_date": date, "check_out_date": date }`
  - **Output:** `{ "message": "Booking successful", "booking_id": integer }` or `{ "error": "Error message" }`
  - **Validation:** User is guest, property available, dates valid (future, check_out > check_in)
  - **Performance:** < 5 seconds