

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
