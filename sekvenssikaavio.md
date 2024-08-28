# KAAVIO 1 SIVUN AVAAMISESTA


sequenceDiagram
    participant browser as Browser
    participant server as Server
    
    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/notes
    activate server
    server-->>browser: HTML document
    deactivate server
    
    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/main.css (html-koodi hakee main.css)
    activate server
    server-->>browser: CSS file
    deactivate server
    
    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/main.js  (html-koodi hakee main.js)
    activate server
    server-->>browser: JavaScript file
    deactivate server
    
    Note right of browser: The browser starts executing the JavaScript code  (Selain suorittaa js-tiedoston, joka tekee HTTP GET ‑pyynnön osoitteeseen https://studies.cs.helsinki.fi/exampleapp/data.json, josta muistiinpanot palautetaan JSON-muotoisena raakadatana)
    
    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/data.json
    activate server
    server-->>browser: JSON data [{ "content": "HTML is easy", "date": "2023-1-1" }, ...]
    deactivate server
    
    Note right of browser: Datan saapuessa selain suorittaa tapahtumankäsittelijän, joka renderöi muistiinpanot ruudulle käyttäen DOM-apia

# KAAVIO 2 JOSSA KÄYTTÄJÄ  TEKEE MUISTIINPANON


sequenceDiagram
    participant browser
    participant server
    
    user->>browser: Kirjoittaa tekstikenttään ja painaa "tallenna"-nappia
    browser->>server: POST https://studies.cs.helsinki.fi/exampleapp/new_note
    activate server
    
    Note right of server: Serveri käsittelee pyynnön ja tallentaa uuden muistiinpanon tietokantaan
    
    server-->>browser: 302 Redirect (uudelleenohjaus)
    deactivate server
    
    Note right of browser: Selain lähettää uuden GET-pyynnön palvelimelle
    
    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/notes
    activate server
    server-->>browser: HTML document
    deactivate server
    
    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/main.css 
    activate server
    server-->>browser: the css file
    deactivate server
    
    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/main.js 
    activate server
    server-->>browser: the JavaScript file
    deactivate server
    
    Note right of browser: Selain alkaa suorittaa koodia, joka hakee päivitetyn json-tiedoston palvelimelta.
    
    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/data.json
    activate server
    server-->>browser: [{ "content": "HTML is easy", "date": "2023-1-1" }, { "content": "Uusi muistiinpano", "date": "2024-8-28" }, ... ]
    deactivate server

    Note right of browser: Selain tallentaa/lähettää päivitetyt datat.










