# 0.4 New Note sequence diagram  
  
## Original Diagram  
```mermaid
sequenceDiagram  
participant browser  
participant server  
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
  
Note right of browser: The browser starts executing the JavaScript code that fetches the JSON from the server  
  
browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/data.json  
activate server  
server-->>browser: [{ "content": "HTML is easy", "date": "2023-1-1" }, ... ]  
deactivate server  
  
Note right of browser: The browser executes the callback function that renders the notes  
```  
  
## Based on `new_note` flow:  
```mermaid
sequenceDiagram  
participant browser  
participant server  
  
browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/new_note  
activate server  
server-->>browser: OK 302 /notes  
deactivate server  
  
Note right of browser: redirect triggered to /notes  
  
browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/notes  
activate server  
server-->>browser: HTML + CSS + JS  
deactivate server  
```

# 0.5: Single Page App diagram  
  
A version of the diagram in the case of the [notes](https://studies.cs.helsinki.fi/exampleapp/spa.) app in SPA form.  
  
```mermaid
sequenceDiagram  
participant browser  
participant server  
  
browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/spa  
activate server  
server-->>browser: OK 200 / HTML Document  
deactivate server  
  
browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/main.css  
activate server  
server-->>browser: OK 200 / CSS Document  
deactivate server  
  
browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/spa.js  
activate server  
server-->>browser: OK 200 / spa.js  
deactivate server  
  
browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/data.json  
activate server  
server-->>browser: OK 200 / data.json  
deactivate server  
  
Note right of browser: redrawNotes()  
  
```

# 0.6 Single Page App diagram when New Note is invoked  
  
```mermaid  
sequenceDiagram  
participant browser  
participant server  
  
Note over browser: {content: string, date: new Date()}  
Note over browser: redrawNotes()  
  
browser->>server: POST https://studies.cs.helsinki.fi/exampleapp/new_note_spa  
activate server  
  
server-->>browser: OK 200 / {message: "note created"}  
deactivate server  
```