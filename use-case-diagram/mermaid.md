
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