# Airbnb Clone Backend Features and Functionalities

This directory (`features-and-functionalities/`) documents the key features and functionalities of the Airbnb Clone project backend, as part of the `alx-airbnb-project-documentation` repository. It includes a detailed list of features and a flowchart visualizing the backend processes.

## Files

- **`README.md`**: This file, documenting the features and directory contents.
- **`airbnb_backend_flowchart.png`**: Flowchart illustrating the backend functionalities (user authentication, property management, booking system, etc.).

## Features and Functionalities

The Airbnb Clone backend supports the following core functionalities, designed to mimic a simplified version of Airbnb’s platform:

### 1. User Authentication
- **Registration**: Users sign up with first name, last name, email, password, phone number, and role (guest, host, admin). Email is unique; password is hashed.
- **Login**: Users log in with email and password, receiving a session token (e.g., JWT).
- **Logout**: Users log out, invalidating their session.
- **Profile Management**: Users view/update their profile (name, phone, password). Admins manage user roles or deactivate accounts.
- **Role-Based Access**:
  - Guests: Book properties, write reviews.
  - Hosts: Manage properties, respond to messages.
  - Admins: Manage users, properties, bookings.

### 2. Property Management
- **Create Property**: Hosts create properties with name, description, location (city, state, country), and price per night.
- **Update Property**: Hosts update property details or availability.
- **Delete Property**: Hosts soft-delete properties to preserve booking history.
- **List Properties**: Users view/filter properties by location, price, or availability, including ratings.
- **Location Management**: Admins add/update locations for properties.

### 3. Booking System
- **Create Booking**: Guests book properties for specific dates, with total price calculated (price per night × nights). Status is “pending.”
- **View Bookings**: Guests view their bookings; hosts view property bookings; admins view all.
- **Update Booking**: Guests cancel bookings; hosts/admins confirm bookings.
- **Availability Check**: System ensures no overlapping confirmed bookings.
- **Booking History**: Users view past bookings (dates, price, status).

### 4. Payments
- **Process Payment**: Guests pay for confirmed bookings via credit card, PayPal, or Stripe (full or partial payments).
- **View Payment History**: Guests/hosts view payments; admins view all.
- **Payment Status**: Tracks payment amount, date, and method.

### 5. Reviews
- **Write Review**: Guests write reviews (rating 1–5, comment) for booked properties.
- **View Reviews**: Users view property reviews and average ratings.
- **Moderate Reviews**: Admins delete inappropriate reviews.

### 6. Messaging
- **Send Message**: Users send messages (e.g., booking inquiries).
- **View Messages**: Users view sent/received messages, sorted by timestamp.
- **Admin Oversight**: Admins monitor messages for moderation.

### 7. Additional Functionalities
- **Search and Filter**: Search properties by location, price, dates, or amenities.
- **Notifications**: Send booking confirmations or message alerts (email/in-app).
- **Audit Logging**: Log critical actions (e.g., registration, booking) for admin review.

## Flowchart

The flowchart (`airbnb_backend_flowchart.png`) visualizes the backend processes:
- **User Journey**: Register, log in, access dashboard.
- **Interactions**: Manage properties, create bookings, process payments, write reviews, send messages.
- **Admin Actions**: Manage users, moderate content, view logs.
- Created using Mermaid, with clear colors and labels for readability.

To view the flowchart, open `airbnb_backend_flowchart.png` in this directory.

## Repository Structure

- **Repository**: `alx-airbnb-project-documentation`
- **Directory**: `features-and-functionalities/`
- **Files**:
  - `README.md`
  - `airbnb_backend_flowchart.png`

## Usage

- **Review Features**: Read this `README.md` for a detailed list of backend functionalities.
- **View Flowchart**: Open `airbnb_backend_flowchart.png` to understand the workflow.
- **Development**: Use this documentation to guide backend implementation (e.g., API endpoints, database queries).


```mermaid
graph TD
    A[User] -->|Register| B[User Authentication]
    A -->|Login| B
    B -->|Success| C[Dashboard]
    C --> D[Property Management]
    C --> E[Booking System]
    C --> F[Messaging]
    C --> G[Reviews]
    C --> H[Payments]

    D --> D1[Create Property]
    D --> D2[Update Property]
    D --> D3[Delete Property]
    D --> D4[List Properties]
    D --> D5[Search by Location/Price]

    E --> E1[Search Properties]
    E1 --> E2[Check Availability]
    E2 --> E3[Create Booking]
    E3 --> E4[Confirm/Cancel Booking]
    E3 --> H1[Process Payment]

    H --> H1
    H --> H2[View Payment History]

    G --> G1[Write Review]
    G --> G2[View Reviews]

    F --> F1[Send Message]
    F --> F2[View Messages]

    B -->|Admin| I[Admin Panel]
    I --> I1[Manage Users]
    I --> I2[Moderate Reviews]
    I --> I3[Monitor Messages]
    I --> I4[View Audit Logs]

    style A fill:#f9f,stroke:#333
    style B fill:#bbf,stroke:#333
    style C fill:#bfb,stroke:#333
    style D fill:#ffb,stroke:#333
    style E fill:#bff,stroke:#333
    style F fill:#fbf,stroke:#333
    style G fill:#bff,stroke:#333
    style H fill:#ffb,stroke:#333
    style I fill:#f99,stroke:#333

## Contact

For questions or issues, please open an issue in the `alx-airbnb-project-documentation` repository or contact the repository owner.