# Airbnb Clone Backend User Stories

This file documents the user stories derived from the use case diagram in the `use-case-diagram/` directory of the `alx-airbnb-project-documentation` repository. Each user story captures a core interaction between actors (Guest, Host, Admin) and the Airbnb Clone backend, based on the features outlined in `features-and-functionalities/`.

## User Stories

The following user stories represent key functionalities of the Airbnb Clone backend, formatted as: “As a [role], I want to [action] so that [benefit].”

1. **User Registration**
   - **Story**: As a new user, I want to register an account with my email and password so that I can access the platform as a guest or host.
   - **Description**: Allows new users to sign up, specifying their role (guest or host), enabling access to booking or property management features.

2. **Create Booking**
   - **Story**: As a guest, I want to book a property for specific dates so that I can secure my accommodation.
   - **Description**: Enables guests to select a property and dates, triggering an availability check and creating a pending booking.

3. **Process Payment**
   - **Story**: As a guest, I want to pay for my confirmed booking using a credit card or PayPal so that I can complete the reservation process.
   - **Description**: Allows guests to make full or partial payments for confirmed bookings, supporting multiple payment methods.

4. **Create Property**
   - **Story**: As a host, I want to list a new property with details like location and price so that guests can book it.
   - **Description**: Enables hosts to add properties to the platform, specifying details like name, description, and price per night.

5. **Write Review**
   - **Story**: As a guest, I want to write a review with a rating for a property I stayed at so that I can share my experience with others.
   - **Description**: Allows guests to submit reviews (rating 1–5 and comments) for properties they’ve booked, enhancing trust and transparency.

6. **Confirm/Cancel Booking**
   - **Story**: As a host, I want to confirm or cancel a booking request for my property so that I can manage my availability.
   - **Description**: Enables hosts to approve or decline booking requests, updating the booking status accordingly.

7. **Manage Users**
   - **Story**: As an admin, I want to manage user accounts (e.g., deactivate or change roles) so that I can maintain platform security and compliance.
   - **Description**: Allows admins to oversee user accounts, ensuring proper role assignments and handling violations.

8. **Search/Filter Properties**
   - **Story**: As a guest, I want to search for properties by location and filter by price or dates so that I can find suitable accommodations.
   - **Description**: Enables guests to browse properties with filters for location, price range, or availability, improving the search experience.

## Context

These user stories are derived from the use case diagram (`use-case-diagram/airbnb_use_case_diagram.png`), which visualizes interactions between actors (Guest, Host, Admin, System) and the backend. They align with the features documented in `features-and-functionalities/` and support the development of a robust backend system.

## Usage

- **Development**: Use these stories to guide API endpoint design and feature implementation (e.g., REST endpoints for booking, payment processing).
- **Testing**: Create test cases based on these stories to ensure all user interactions are functional.
- **Documentation**: Combine with other project artifacts (e.g., use case diagram, flowchart) for comprehensive documentation.