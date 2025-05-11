# Airbnb Clone Backend Use Case Diagram

This directory (`use-case-diagram/`) contains a use case diagram visualizing the interactions between users and the Airbnb Clone backend, as part of the `alx-airbnb-project-documentation` repository. The diagram captures key functionalities such as user registration, property booking, and payments, based on the features outlined in `features-and-functionalities/`.

## Files

- **`README.md`**: This file, documenting the use case diagram and directory contents.
- **`airbnb_use_case_diagram.png`**: Use case diagram illustrating actor-system interactions.

## Use Case Diagram Overview

The use case diagram, created using Draw.io, represents the interactions between actors (Guest, Host, Admin, System) and the Airbnb Clone backend. It covers the following functionalities:

### Actors
- **Guest**: A registered user who books properties, writes reviews, and sends messages.
- **Host**: A registered user who manages properties, responds to messages, and views bookings/payments.
- **Admin**: A privileged user who manages users, moderates content, and views audit logs.
- **System**: The backend, handling automated processes (e.g., availability checks, notifications).

### Key Use Cases
1. **User Authentication**:
   - Register (Guest, Host)
   - Login (Guest, Host, Admin)
   - Logout (Guest, Host, Admin)
   - Manage Profile (Guest, Host, Admin)
   - Manage Users (Admin)
2. **Property Management**:
   - Create Property (Host)
   - Update Property (Host)
   - Delete Property (Host)
   - List Properties (Guest, Host, Admin)
   - Search/Filter Properties (Guest, Host)
   - Manage Locations (Admin)
3. **Booking System**:
   - Create Booking (Guest, includes Check Availability)
   - Confirm/Cancel Booking (Guest, Host, Admin)
   - View Bookings (Guest, Host, Admin)
   - View Booking History (Guest, Host)
4. **Payments**:
   - Process Payment (Guest)
   - View Payment History (Guest, Host, Admin)
5. **Reviews**:
   - Write Review (Guest)
   - View Reviews (Guest, Host, Admin)
   - Moderate Reviews (Admin)
6. **Messaging**:
   - Send Message (Guest, Host)
   - View Messages (Guest, Host, Admin)
   - Monitor Messages (Admin)
7. **Additional**:
   - Receive Notifications (Guest, Host)
   - View Audit Logs (Admin)

### Diagram Details
- **Tool**: Created using Draw.io with UML shapes.
- **Structure**: Actors are connected to use cases within a system boundary (“Airbnb Clone Backend”).
- **Relationships**:
  - Associations: Direct lines from actors to use cases (e.g., Guest → Create Booking).
  - Include: Create Booking includes Check Availability (mandatory).
- **Styling**: Colored actors (blue for Guest, green for Host, red for Admin, gray for System) with clear, legible text.

To view the diagram, open `airbnb_use_case_diagram.png` in this directory.

## Repository Structure

- **Repository**: `alx-airbnb-project-documentation`
- **Directory**: `use-case-diagram/`
- **Files**:
  - `README.md`
  - `airbnb_use_case_diagram.png`

## Usage

- **Review Interactions**: Use the diagram to understand how users interact with the backend.
- **Development**: Reference the diagram when designing API endpoints or user workflows.
- **Documentation**: Combine with `features-and-functionalities/` for comprehensive project documentation.

## Contact

For questions or issues, please open an issue in the `alx-airbnb-project-documentation` repository or contact the repository owner.