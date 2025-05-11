# Airbnb Use Case Diagram

This directory (`use-case-diagram/`) contains the use case diagram for the Airbnb system, as part of the `alx-airbnb-project-documentation` repository. The diagram visualizes the interactions between actors (Guest, Host, Admin) and the system's key functionalities, such as user registration, property booking, and payments.

## Files

- **`use_case_diagram.png`**: PNG export of the use case diagram.
- **`README.md`**: This file, documenting the directory and diagram.

## Diagram Overview

The use case diagram captures the following:

### Actors
- **Guest**: Searches and books properties, makes payments, writes reviews, and sends/receives messages.
- **Host**: Registers properties, manages bookings, and communicates with guests.
- **Admin**: Manages users and views system reports.

### Key Functionalities
- **User Registration**: Create a new account (Guest, Host, Admin).
- **User Login**: Authenticate to access the system.
- **Search Properties**: Find properties by location, price, etc.
- **Book Property**: Create a booking for a property.
- **Make Payment**: Pay for a booking.
- **Write Review**: Leave a rating and comment for a property.
- **Send/Receive Messages**: Communicate between guests and hosts.
- **Register Property**: Add a new property to the system.
- **Manage Bookings**: Confirm or cancel bookings.
- **Manage Users**: Update user roles or ban users.
- **View System Reports**: Monitor bookings, payments, or user activity.

### Relationships
- **Include**: Use cases like "Book Property" and "Make Payment" require "User Login".
- **Extend**: "Write Review" is an optional extension of "Book Property" after a stay.

## Mermaid Diagram

The diagram is created using Mermaid syntax and rendered below. It is also exported as `use_case_diagram.png` for static viewing.

```mermaid
graph TD
    subgraph System
        UR[User Registration]:::usecase
        UL[User Login]:::usecase
        SP[Search Properties]:::usecase
        BP[Book Property]:::usecase
        MP[Make Payment]:::usecase
        WR[Write Review]:::usecase
        SRM[Send/Receive Messages]:::usecase
        RP[Register Property]:::usecase
        MB[Manage Bookings]:::usecase
        MU[Manage Users]:::usecase
        VSR[View System Reports]:::usecase
    end

    Guest[Guest]:::actor
    Host[Host]:::actor
    Admin[Admin]:::actor

    Guest --> UR
    Guest --> UL
    Guest --> SP
    Guest --> BP
    Guest --> MP
    Guest --> WR
    Guest --> SRM

    Host --> UR
    Host --> UL
    Host --> RP
    Host --> MB
    Host --> SRM

    Admin --> UR
    Admin --> UL
    Admin --> MU
    Admin --> VSR

    BP -->|includes| UL
    MP -->|includes| UL
    WR -->|extends| BP
    MB -->|includes| UL
    MU -->|includes| UL
    VSR -->|includes| UL
    SRM -->|includes| UL

    classDef usecase fill:#f9f,stroke:#333,shape:oval
    classDef actor fill:#bbf,stroke:#333,shape:rect