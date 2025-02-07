# Spring Boot Authentication Flow

This is the authentication flow for a user trying to log in to a Spring Boot application.

```mermaid
sequenceDiagram
    participant User as U
    participant Browser as B
    participant SpringSecurityFilter as SSF
    participant AuthenticationManager as AM
    participant AuthenticationProvider as AP
    participant UserDetailsService as UDS
    participant SecurityContext as SC
    participant Application as App

    U->>B: Enters Username & Password
    B->>SSF: Sends login request (POST /login)
    SSF->>AM: Extracts credentials & sends authentication request
    AM->>AP: Delegates authentication
    AP->>UDS: Fetch user details from database
    UDS-->>AP: Returns user details
    AP-->>AM: Validates password & authenticates user
    AM-->>SSF: Authentication successful
    SSF->>SC: Stores user authentication
    SC-->>App: User is authenticated
    App->>B: Redirects to home page or returns token

    class U, B fill:#f9f,stroke:#333,stroke-width:2px;
    class SSF, AM fill:#ccf,stroke:#333,stroke-width:2px;
    class AP, UDS fill:#cff,stroke:#333,stroke-width:2px;
    class SC, App fill:#cfc,stroke:#333,stroke-width:2px;
