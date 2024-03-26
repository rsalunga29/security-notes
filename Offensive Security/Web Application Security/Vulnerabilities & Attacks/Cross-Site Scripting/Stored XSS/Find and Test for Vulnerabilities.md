Testing for stored XSS manually can be challenging. All relevant entry points and exit points - at which that data might appear in the response, must be tested.

Entry points in the application's processing include:
- Parameters or other data within the URL query string and message body
- URL file path
- HTTP request headers
- Any out-of-band routes via which an attacker can delivery data into the application.

The exit points for stored XSS attacks are all possible HTTP responses that are returned to any kind of application user in any situation.

The first step in testing for this vulnerability is to locate links between the entry and exit points. The reasons why this can be challenging are that:
- Data submitted to any entry point can be omitted from any exit point.
- Data that is currently stored in the application can be overwritten due to other actions performed within the application.

A more realistic approach for this kind of testing is to work systematically through the data entry points, submitted a specific value into each one, and monitoring the application's responses to detect where the submitted value appears. Once links between entry points and exit points have been identified, each must be tested if a stored XSS vulnerability is present.