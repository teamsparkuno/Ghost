### Security Requirements specified in Ghost Documentation

Ghost advertises itself as a Platform as a service for hosting a blog. Some of the features advertised under PaaS (Platform as a Service) are ensuring data security, role privilege access. Also, Ghost advertises of providing SSL by default and isolated applications, firewalls and spam protection. Ghost is built on Restful JSON API, and the data access is handled by the API. Since Ghost uses RESTFUL principles, SSL plays a vital role in securing the data access over the resource oriented URL’s. The URL’s are easily guessable.

The documentation of Ghost talks in detail, of how the API provide secure access to data.
The security requirements we could extract from the API documentation provided were related to the use of the Restful JSON API for secure access of data over the blog. The restful JSON API makes use of the HTTP authorizations to provide private access.
To provide better secure platform for data, ghost divides the API into two, a Public API and a private API. Public API provides read only access and Private API is restricted to the admin to read write data. The client authentication to the API is done by OAuth client authentication. The access to the API is further restricted based on the domain of the website from where the API calls are made. This way the System prevents data being modified by rogue users.

By analyzing from the above features provided from Ghost, we can say that it handles API security requirements, that we could extract from our misuse case. The document also explains how the system allows access to the API from restricted domains, this addresses our security requirements related to session hijacking.

The documentation indirectly talks about Privilege escalation in the API documentation. How different roles access are handled by the API. However, it just lists the user role capabilities and their access. We feel that the documentation should have covered how the privilege escalation is handled by the system and explain it directly in terms of the roles assigned in the system.
Further when we consider security concerns related to Script injections, the documentation fails to mention of requirements related script injections. This makes us ask the question if at all script injection is handled by the Ghost system.

