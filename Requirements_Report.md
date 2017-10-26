
# Requirement Report for Ghost


### [Final Assurance claims](https://www.lucidchart.com/invitations/accept/0a976aa4-6349-48fc-8ed8-dc3c684c11d4)
* 	Ghost Login module successfully averts session hijacking.
* 	Ghost Login Module has no exploitable SQL_injection weaknesses.
* 	The Ghost User Story Module has mitigated all privilege escalations.
* 	Ghost code injection module has no exploitable XSS Weaknesses.
* 	Ghost system has no API Authentication weaknesses.

### Security Requirements

[Project misuse cases available here](https://www.lucidchart.com/invitations/accept/12f66949-a4b7-4950-84f2-78229cdff59d)

#### Privilege Escalation
* The system should enforce access control list for to handle privilege roles in the application.
* Implement data sanitization to avoid injection of malicious scripts in the data fields in the system.


#### User Authentication
* The system should use a pseudorandom number generator to create session ID of higher entropy.
* The system should use https to encrypt all traffic end to end during session management.
* The system should use captcha for user authentication to prevent unwanted access to ghost admin.
* The system should enforce a security question, when the user performs critical tasks related to the database.
* The system should use cookie based authentication for users. 


#### API
* The system should make sure that the API calls are authenticated with secret key.
* The system should ensure that the requests made to the API are restricted to select list of IP addresses.
* The system should ensure limited restriction to API from third party application which use GHOST.


#### Script Injection
* The system should have protection against user and password enumeration attack.
* The system should implement generic error messages to avoid exposing system sensitive data.
* The system should prevent session hijacking through XSS attacks on the cookies.
* Implement data sanitization to prevent script injection in input fields of the system.
