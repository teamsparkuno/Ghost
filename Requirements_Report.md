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

### Security Requirements specified in Ghost Documentation

Ghost advertises itself as a Platform as a service for hosting a blog. Some of the features advertised under PaaS (Platform as a Service) are ensuring data security, role privilege access. Also, Ghost advertises of providing SSL by default and isolated applications, firewalls and spam protection. Ghost is built on Restful JSON API, and the data access is handled by the API. Since Ghost uses RESTFUL principles, SSL plays a vital role in securing the data access over the resource oriented URL’s. The URL’s are easily guessable.

The documentation of Ghost talks in detail, of how the API provide secure access to data.
The security requirements we could extract from the API documentation provided were related to the use of the Restful JSON API for secure access of data over the blog. The restful JSON API makes use of the HTTP authorizations to provide private access.
To provide better secure platform for data, ghost divides the API into two, a Public API and a private API. Public API provides read only access and Private API is restricted to the admin to read write data. The client authentication to the API is done by OAuth client authentication. The access to the API is further restricted based on the domain of the website from where the API calls are made. This way the System prevents data being modified by rogue users.

By analyzing from the above features provided from Ghost, we can say that it handles API security requirements, that we could extract from our misuse case. The document also explains how the system allows access to the API from restricted domains, this addresses our security requirements related to session hijacking.

The documentation indirectly talks about Privilege escalation in the API documentation. How different roles access are handled by the API. However, it just lists the user role capabilities and their access. We feel that the documentation should have covered how the privilege escalation is handled by the system and explain it directly in terms of the roles assigned in the system.
Further when we consider security concerns related to Script injections, the documentation fails to mention of requirements related script injections. This makes us ask the question if at all script injection is handled by the Ghost system.


### Security related configuration

We can add a custom configuration file to override Ghost's default behavior. Ghost's configuration is managed by [nconf](https://github.com/indexzero/nconf) which is a custom configuration JSON file and must be in the root folder.

#### [Ghost Environment](https://docs.ghost.org/docs/config) 

Ghost uses Node.js which has the concept of environments. It has two built in environment modes development and production. 

development environment | production environment
---|---
config.development.json | config.production.json


Development environment is used when developing and debugging ghost where as production environment is used in live blog. By default, ghost is configured in development mode. In production, we need to set a configuration variable NODE_ENV to production. If this is not configured then it can lead to loss of sensitive data.

#### [Mail Config](https://docs.ghost.org/docs/mail-config)
A mail service should be configured in ghost so that ghost sends email such as forgotten password and user invitation mail. Wrong configuration of this service will lead to loss of sensitive data and privileges.

#### [Admin URL](https://docs.ghost.org/docs/cli-knowledge-base#section-ssl)
Ghost has configuration option for securing URL's using SSL. We need to specify that admin URL as HTTPS instead of HTTP because without SSL the username and password entered in any URL is a plain text. By this network sniffers will not able to interpret the exchanged data.

#### Privacy Config
Ghost provides a mechanism where we can turn off all the unused featured in the application. This features should be listed in [PRIVACY.md](https://github.com/TryGhost/Ghost/blob/master/PRIVACY.md) file. If this privacy configuration is not set, it can lead to security risks.

##### *Automatic Update check*
Ghost has an automatic update check service to upgrade third party services. If this is not properly configured then there is a security risk of using out dated services.
See [PRIVACY.md#automatic-update-checks](https://github.com/TryGhost/Ghost/blob/master/PRIVACY.md#automatic-update-checks) for more details.
#### Maintenance Mode
Ghost has a Maintenance Mode that will serve 503 HTTP response. We need to make sure that Maintenance Mode should be enabled while debugging the application. If this is not enabled, it can leak sensitive data when it is in maintenance.
#### Logging
We can configure what detailed should be logged. We need to take care of logs so that they should not reveal any sensitive data.
#### Spam and Cache settings
Ghost has spam and Cache settings, which when enabled prevents the spam requests. If this is not configured properly, there is a chance of Denial of Service attack. 
See [spam configuration in Ghost](https://github.com/TryGhost/Ghost/blob/master/core/server/config/defaults.json#L26).
See [caching configuration in Ghost](https://github.com/TryGhost/Ghost/blob/master/core/server/config/defaults.json#L57).

### Installation Issues
* Ghost documentation for installing ghost in local server is mainly focused on ghost theme development. It lacks more information about Ghost-Admin installation procedure.
* In Ghost-Admin installation procedure, documentation is missing the details of SQL Server installation that needs to be installed before installing the application.

