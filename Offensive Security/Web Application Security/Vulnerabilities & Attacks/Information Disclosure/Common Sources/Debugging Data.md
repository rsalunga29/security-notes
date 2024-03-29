Debug messages may sometimes be logged in a separate file, or even in a dedicated page within the application, specially if the debug is turned on in the config. It can serve as a useful reference for understanding the application's runtime state. It can also provide several clues as to how they can supply crafted input to manipulate the application state and control the information received.

Debug messages can sometimes contain vital information for developing an attack, including:
- Values for key session variables that can be manipulated via user input
- Hostnames and credentials for back-end components
- File and directory names on the server
- Keys used to encrypt data transmitted via the client