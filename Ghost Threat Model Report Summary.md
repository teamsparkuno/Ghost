### Ghost Threat Model Report Summary Review. 

The Ghost threat model generated covers all the Misuse cases such as Privilege escalation, Session hijacking, API authentication, Sql Injection, Script injection. We have documented the mitigation strategies for each threat identified per interaction. 
The  common threats identified from our threat model are focused between the trust boundaries of the process and the external entities.The threats can be classified generally under STRIDE as follows.

**Spoofing** : User Impersonation,Request forgery.

**Tampering** : Sql Injection attack,Cross site scripting.

**Repudiation** : Denying the data was not received by the external entity or external API.

**Information disclosure** : Data Sniffing.

**Denial of service attack** : Data flow interruption across trust boundary, Resource consumption attacks.

**Elevation of privileges** : User Impersonation to gain admin privileges.

For detailed description of the threats identified and for the mitigations provided for each of them please refer to our [HTML report](https://github.com/teamsparkuno/Ghost/blob/master/Ghost%20threat%20report.pdf) generated using Microsoft threat modeling tool 2016. 

After going through the design of Ghost , we have found that it mitigates most of the threats identified from the threat model.

* Spoofing is mitigated by User authentication.
* Under tampering we found that Ghost is mitigating Sql Injection by using Object relational mappers (ORM) programming technique, but when it comes to Cross site scripting attacks , we could not find any evidence or security requirement in the documentation which handles it. This is a critical threat that has to be addressed by Ghost. 
* Repudiation threats are mitigated by ghost using logs in the system. 
* Information disclosure threats are mitigated by using https protocol which has SSL layer thus ensuring encryption. 
* Denial of service attack threats under ghost needs to be investigated for further evidence, as the documentation or the design doesn’t provide any mitigation strategy to handle that. 
* Elevation of privilege threats are mitigated as Ghost provides Role based authentication and access to data.


