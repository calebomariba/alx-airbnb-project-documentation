# Airbnb Clone Backend Requirement Specifications

This document outlines the technical and functional requirement specifications for the key backend features of the Airbnb Clone project, as part of the `alx-airbnb-project-documentation` repository. The specifications are based on the features documented in `features-and-functionalities/`, use case diagram (`use-case-diagram/`), user stories (`user-stories/`), and data flow diagram (`data-flow-diagram/`). The focus is on three core features: User Authentication, Property Management, and Booking System.

## 1. User Authentication

### 1.1 Functional Requirements
- **Registration**: Allow new users to create accounts with personal details and a role (guest or host).
- **Login**: Authenticate users with email and password, issuing a session token.
- **Logout**: Invalidate user sessions.
- **Profile Management**: Allow users to view and update their profile information.
- **Role-Based Access**: Restrict actions based on user roles (guest, host, admin).

### 1.2 Technical Requirements

#### 1.2.1 API Endpoints
- **POST /api/v1/auth/register**
  - **Description**: Register a new user.
  - **Input** (JSON):
    ```json
    {
      "first_name": "string",
      "last_name": "string",
      "email": "string",
      "password": "string",
      "phone_number": "string (optional)",
      "role": "string (guest or host)"
    }
    ```
  - **Output** (JSON):
    - Success (201):
      ```json
      {
        "user_id": "uuid",
        "email": "string",
        "role": "string",
        "message": "User registered successfully"
      }
      ```
    - Error (400, 409):
      ```json
      {
        "error": "Invalid input or Email already exists"
      }
      ```
- **POST /api/v1/auth/login**
  - **Description**: Authenticate a user and issue a JWT token.
  - **Input** (JSON):
    ```json
    {
      "email": "string",
      "password": "string"
    }
    ```
  - **Output** (JSON):
    - Success (200):
      ```json
      {
        "user_id": "uuid",
        "email": "string",
        "role": "string",
        "token": "jwt_token"
      }
      ```
    - Error (401):
      ```json
      {
        "error": "Invalid credentials"
      }
      ```
- **POST /api/v1/auth/logout**
  - **Description**: Invalidate the user’s session (requires JWT).
  - **Input**: None (Authorization header with JWT).
  - **Output** (JSON):
    - Success (200):
      ```json
      {
        "message": "Logged out successfully"
      }
      ```
    - Error (401):
      ```json
      {
        "error": "Invalid or expired token"
      }
      ```
- **GET /api/v1/users/profile**
  - **Description**: Retrieve the authenticated user’s profile (requires JWT).
  - **Input**: None (Authorization header with JWT).
  - **Output** (JSON):
    - Success (200):
      ```json
      {
        "user_id": "uuid",
        "first_name": "string",
        "last_name": "string",
        "email": "string",
        "phone_number": "string or null",
        "role": "string"
      }
      ```
    - Error (401):
      ```json
      {
        "error": "Unauthorized"
      }
      ```
- **PUT /api/v1/users/profile**
  - **Description**: Update the authenticated user’s profile (requires JWT).
  - **Input** (JSON):
    ```json
    {
      "first_name": "string (optional)",
      "last_name": "string (optional)",
      "phone_number": "string (optional)",
      "password": "string (optional)"
    }
    ```
  - **Output** (JSON):
    - Success (200):
      ```json
      {
        "message": "Profile updated successfully"
      }
      ```
    - Error (400, 401):
      ```json
      {
        "error": "Invalid input or Unauthorized"
      }
      ```

#### 1.2.2 Validation Rules
- **first_name, last_name**: String, 2–50 characters, letters and spaces only.
- **email**: Valid email format, unique in Users table.
- **password**: String, 8–50 characters, must include uppercase, lowercase, number, and special character.
- **phone_number**: String, valid format (e.g., +12345678901), optional.
- **role**: Enum (guest, host), default to guest.
- **JWT**: Valid token required for protected endpoints, expires in 24 hours.

#### 1.2.3 Performance Criteria
- Response time: < 500ms for login/register under normal load (100 concurrent users).
- Scalability: Handle 1,000 registrations/hour.
- Security: Passwords hashed with bcrypt; JWT signed with HMAC-SHA256.
- Availability: 99.9% uptime for authentication services.

## 2. Property Management

### 2.1 Functional Requirements
- **Create Property**: Allow hosts to list new properties with details (name, location, price).
- **Update Property**: Allow hosts to modify property details or availability.
- **Delete Property**: Allow hosts to remove properties (soft delete).
- **List Properties**: Allow users to view all properties or filter by criteria (location, price).
- **Search Properties**: Allow users to search properties by keywords or filters.

### 2.2 Technical Requirements

#### 2.2.1 API Endpoints
- **POST /api/v1/properties**
  - **Description**: Create a new property (requires JWT, host role).
  - **Input** (JSON):
    ```json
    {
      "name": "string",
      "description": "string",
      "location_id": "uuid",
      "pricepernight": "number"
    }
    ```
  - **Output** (JSON):
    - Success (201):
      ```json
      {
        "property_id": "uuid",
        "name": "string",
        "location_id": "uuid",
        "pricepernight": "number",
        "message": "Property created successfully"
      }
      ```
    - Error (400, 401, 403):
      ```json
      {
        "error": "Invalid input, Unauthorized, or Not a host"
      }
      ```
- **PUT /api/v1/properties/:property_id**
  - **Description**: Update an existing property (requires JWT, host role, ownership).
  - **Input** (JSON):
    ```json
    {
      "name": "string (optional)",
      "description": "string (optional)",
      "pricepernight": "number (optional)"
    }
    ```
  - **Output** (JSON):
    - Success (200):
      ```json
      {
        "message": "Property updated successfully"
      }
      ```
    - Error (400, 401, 403, 404):
      ```json
      {
        "error": "Invalid input, Unauthorized, Not owner, or Property not found"
      }
      ```
- **DELETE /api/v1/properties/:property_id**
  - **Description**: Soft-delete a property (requires JWT, host role, ownership).
  - **Input**: None (property_id in URL).
  - **Output** (JSON):
    - Success (200):
      ```json
      {
        "message": "Property deleted successfully"
      }
      ```
    - Error (401, 403, 404):
      ```json
      {
        "error": "Unauthorized, Not owner, or Property not found"
      }
      ```
- **GET /api/v1/properties**
  - **Description**: List properties with optional filters.
  - **Input** (Query Parameters):
    - `location_id`: UUID (optional)
    - `min_price`: Number (optional)
    - `max_price`: Number (optional)
    - `search`: String (optional, keyword search)
  - **Output** (JSON):
    - Success (200):
      ```json
      [
        {
          "property_id": "uuid",
          "name": "string",
          "description": "string",
          "location_id": "uuid",
          "pricepernight": "number",
          "host_id": "uuid"
        }
      ]
      ```
    - Error (400):
      ```json
      {
        "error": "Invalid query parameters"
      }
      ```

#### 2.2.2 Validation Rules
- **name**: String, 5–100 characters.
- **description**: String, 10–500 characters.
- **location_id**: Valid UUID, must exist in Locations table.
- **pricepernight**: Number, 0.01–10000.00, 2 decimal places.
- **host_id**: Valid UUID, must match authenticated user and have host role.
- **Query Parameters**:
  - `min_price, max_price`: Non-negative numbers, max_price ≥ min_price.
  - `search`: String, 1–50 characters.

#### 2.2.3 Performance Criteria
- Response time: < 1s for listing 100 properties under normal load.
- Scalability: Handle 10,000 property searches/hour.
- Consistency: Ensure property data is consistent across create/update/delete operations.
- Availability: 99.9% uptime for property management services.

## 3. Booking System

### 3.1 Functional Requirements
- **Create Booking**: Allow guests to book a property for specific dates.
- **Check Availability**: Ensure no overlapping bookings for the same property.
- **Confirm/Cancel Booking**: Allow guests, hosts, or admins to update booking status.
- **View Bookings**: Allow users to view their bookings or all bookings (admin).

### 3.2 Technical Requirements

#### 3.2.1 API Endpoints
- **POST /api/v1/bookings**
  - **Description**: Create a new booking (requires JWT, guest role).
  - **Input** (JSON):
    ```json
    {
      "property_id": "uuid",
      "start_date": "YYYY-MM-DD",
      "end_date": "YYYY-MM-DD"
    }
    ```
  - **Output** (JSON):
    - Success (201):
      ```json
      {
        "booking_id": "uuid",
        "property_id": "uuid",
        "user_id": "uuid",
        "start_date": "YYYY-MM-DD",
        "end_date": "YYYY-MM-DD",
        "total_price": "number",
        "status": "pending",
        "message": "Booking created successfully"
      }
      ```
    - Error (400, 401, 403, 409):
      ```json
      {
        "error": "Invalid input, Unauthorized, Not a guest, or Property unavailable"
      }
      ```
- **PUT /api/v1/bookings/:booking_id**
  - **Description**: Update booking status (requires JWT, guest/host/admin role, appropriate permissions).
  - **Input** (JSON):
    ```json
    {
      "status": "string (confirmed or canceled)"
    }
    ```
  - **Output** (JSON):
    - Success (200):
      ```json
      {
        "message": "Booking updated successfully"
      }
      ```
    - Error (400, 401, 403, 404):
      ```json
      {
        "error": "Invalid status, Unauthorized, Not authorized, or Booking not found"
      }
      ```
- **GET /api/v1/bookings**
  - **Description**: List bookings for the authenticated user or all bookings (admin).
  - **Input** (Query Parameters):
    - `user_id`: UUID (optional, admin only)
    - `property_id`: UUID (optional)
    - `status`: String (pending, confirmed, canceled, optional)
  - **Output** (JSON):
    - Success (200):
      ```json
      [
        {
          "booking_id": "uuid",
          "property_id": "uuid",
          "user_id": "uuid",
          "start_date": "YYYY-MM-DD",
          "end_date": "YYYY-MM-DD",
          "total_price": "number",
          "status": "string"
        }
      ]
      ```
    - Error (400, 401):
      ```json
      {
        "error": "Invalid query parameters or Unauthorized"
      }
      ```

#### 3.2.2 Validation Rules
- **property_id**: Valid UUID, must exist in Properties table.
- **start_date, end_date**: Valid dates, end_date ≥ start_date, start_date ≥ current date.
- **status**: Enum (pending, confirmed, canceled).
- **total_price**: Calculated as `pricepernight * (end_date - start_date)`, 2 decimal places.
- **user_id**: Valid UUID, must match authenticated user (guest) for creating bookings.
- **Availability Check**: No overlapping confirmed bookings for the same property_id.
- **Permissions**:
  - Guests can cancel their bookings.
  - Hosts can confirm/cancel bookings for their properties.
  - Admins can confirm/cancel any booking.

#### 3.2.3 Performance Criteria
- Response time: < 1s for creating a booking with availability check under normal load.
- Scalability: Handle 5,000 bookings/hour.
- Concurrency: Ensure atomic checks to prevent double bookings (use database transactions).
- Availability: 99.9% uptime for booking services.

## Related Documentation
- **Features and Functionalities**: `features-and-functionalities/README.md`
- **Use Case Diagram**: `use-case-diagram/airbnb_use_case_diagram.png`
- **User Stories**: `user-stories/user-stories.md`
- **Data Flow Diagram**: `data-flow-diagram/data-flow.png`
- **Database Schema**: `alx-airbnb-database/database-script-0x01/schema.sql`

## Contact
For questions or issues, please open an issue in the `alx-airbnb-project-documentation` repository or contact the repository owner.