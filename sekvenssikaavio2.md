sequenceDiagram
    participant user as User
    participant browser as Browser
    participant server as Server
    
    user->>browser: Navigates to https://studies.cs.helsinki.fi/exampleapp/spa
    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/spa
