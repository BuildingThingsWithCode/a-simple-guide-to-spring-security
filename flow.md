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

    %% Style the participants
    style U fill:#f9f,stroke:#333,stroke-width:2px;
    style B fill:#f0f0f0,stroke:#333,stroke-width:2px;
    style SSF fill:#ccf,stroke:#333,stroke-width:2px;
    style AM fill:#e0e0e0,stroke:#333,stroke-width:2px;
    style AP fill:#cff,stroke:#333,stroke-width:2px;
    style UDS fill:#cfc,stroke:#333,stroke-width:2px;
    style SC fill:#cff,stroke:#333,stroke-width:2px;
    style App fill:#cfc,stroke:#333,stroke-width:2px;

