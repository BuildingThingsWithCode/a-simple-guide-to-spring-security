# Spring Boot Authentication Flow

This is the authentication flow for a user trying to log in to a Spring Boot application.

```mermaid
sequenceDiagram
    participant User
    participant Browser
    participant SpringSecurityFilter
    participant AuthenticationManager
    participant AuthenticationProvider
    participant UserDetailsService
    participant SecurityContext
    participant Application

    User->>Browser: Enters Username & Password
    Browser->>SpringSecurityFilter: Sends login request (POST /login)
    SpringSecurityFilter->>AuthenticationManager: Extracts credentials & sends authentication request
    AuthenticationManager->>AuthenticationProvider: Delegates authentication
    AuthenticationProvider->>UserDetailsService: Fetch user details from database
    UserDetailsService-->>AuthenticationProvider: Returns user details
    AuthenticationProvider-->>AuthenticationManager: Validates password & authenticates user
    AuthenticationManager-->>SpringSecurityFilter: Authentication successful
    SpringSecurityFilter->>SecurityContext: Stores user authentication
    SecurityContext-->>Application: User is authenticated
    Application->>Browser: Redirects to home page or returns token
