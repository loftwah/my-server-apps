https://www.kimai.org/documentation/docker.html

 [![Kimai logo](https://www.kimai.org/assets/icon/apple-touch-icon.png) Kimai time-tracker](https://www.kimai.org/)

[DE](https://www.kimai.org/de/ "Kimai Homepage") EN [FR](https://www.kimai.org/fr/ "Kimai accueil")

[Cloud](https://www.kimai.cloud "Kimai-Cloud - Use Kimai directly without setup. Free Kimai hosting!")

[](#)

*   [Home](https://www.kimai.org/)
*   [About Kimai](https://www.kimai.org/about/)
*   [Demo](https://www.kimai.org/demo/)
*   [Download](https://www.kimai.org/download/)
*   [Marketplace](https://www.kimai.org/store/)
*   [News](https://www.kimai.org/blog/)
*   [Documentation](https://www.kimai.org/documentation/)
*   [Kimai v1](https://www.kimai.org/v1/)
*   [Deutsch](https://www.kimai.org/de/ "Kimai Homepage")
*   [Français](https://www.kimai.org/fr/ "Kimai accueil")

# Docker

Running Kimai inside docker

**First steps**

[Installation](https://www.kimai.org/documentation/installation.html) [Initial setup](https://www.kimai.org/documentation/inital-setup.html) [Updates](https://www.kimai.org/documentation/updates.html) [Docker](https://www.kimai.org/documentation/docker.html) [Backups](https://www.kimai.org/documentation/backups.html)

**User manual**

[Timesheet](https://www.kimai.org/documentation/timesheet.html) [Invoices](https://www.kimai.org/documentation/invoices.html) [Export](https://www.kimai.org/documentation/export.html) [Reporting](https://www.kimai.org/documentation/reporting.html) [Customer](https://www.kimai.org/documentation/customer.html) [Projects](https://www.kimai.org/documentation/project.html) [Activities](https://www.kimai.org/documentation/activity.html) [Tags](https://www.kimai.org/documentation/tags.html) [Users](https://www.kimai.org/documentation/users.html) [User preferences](https://www.kimai.org/documentation/user-preferences.html) [Teams](https://www.kimai.org/documentation/teams.html)

**Configuration**

[Configurations](https://www.kimai.org/documentation/configurations.html) [Reloading cache](https://www.kimai.org/documentation/cache.html) [Calendar](https://www.kimai.org/documentation/calendar.html) [Dashboard](https://www.kimai.org/documentation/dashboard.html) [Emails](https://www.kimai.org/documentation/emails.html) [Permissions](https://www.kimai.org/documentation/permissions.html) [LDAP](https://www.kimai.org/documentation/ldap.html) [SAML](https://www.kimai.org/documentation/saml.html) [Switch to AM/PM](https://www.kimai.org/documentation/i18n-am-pm.html) [Logging](https://www.kimai.org/documentation/logging.html)

**Developer**

[Developers](https://www.kimai.org/documentation/developers.html) [Plugins](https://www.kimai.org/documentation/plugins.html) [Rest API](https://www.kimai.org/documentation/rest-api.html) [Custom fields](https://www.kimai.org/documentation/meta-fields.html) [Translations / i18n](https://www.kimai.org/documentation/translations.html) [Theme](https://www.kimai.org/documentation/theme.html)

[Edit this page](https://github.com/kimai/www.kimai.org/blob/master/_documentation/docker.md)

[Back to documentation](https://www.kimai.org/documentation/)

## Docker

[Kimai version](#)

[development](https://www.kimai.org/documentation/development/docker.html) [1.14.3 (latest version)](https://www.kimai.org/documentation/docker.html)

*   [Production docker](#production-docker)
    *   [Build the docker](#build-the-docker)
    *   [Run the docker](#run-the-docker)
    *   [Running commands in the docker](#running-commands-in-the-docker)
    *   [Using a custom local.yaml](#using-a-custom-localyaml)

## Production docker

[@tobybatch](https://github.com/tobybatch) is managing the Kimai Docker images, both for development and a docker-compose setup suitable for running in a production environment.

*   [https://github.com/tobybatch/kimai2](https://github.com/tobybatch/kimai2) - his repository with all the docker sources
*   [https://hub.docker.com/r/kimai/kimai2](https://hub.docker.com/r/kimai/kimai2) - dockerhub repo, auto-building prod and dev containers

Any issues with the container rather than the application itself should be raised [here](https://github.com/tobybatch/kimai2/issues).

### Build the docker

```
docker build -t my-local-kimai .

```

### Run the docker

```
docker run -ti -p 8001:8001 --name kimai2 --rm my-local-kimai

```

You can then access the site on http://127.0.0.1:8001. If that doesn’t work check the IP of your docker:

```
docker inspect -f '{{range .NetworkSettings.Networks}}{{.IPAddress}}{{end}}' kimai2

```

#### Mac using docker-machine

When using docker-machine on your Mac, you need to use the IP of your machine. Considering you started the machine named `default`, you find the IP with:

```
docker-machine ip default

```

### Running commands in the docker

You can run any command in the container in this fashion once it is started. Add `-ti` to attach a terminal.

```
docker exec -ti kimai2 bash

```

#### Create a user and dummy data

This creates a user admin/password with all privileges.

```
docker exec kimai2 /opt/kimai/bin/console kimai:create-user admin admin@example.com ROLE_SUPER_ADMIN password

```

To install the test data (fixtures):

```
docker exec kimai2 /opt/kimai/bin/console kimai:reset-dev

```

### Using a custom local.yaml

You can mount a [custom configuration](https://www.kimai.org/documentation/configurations.html) into the container while starting it:

```
docker run --rm -ti -p 8001:8001 --name kimai2 -v $(pwd)/config/packages/local.yaml:/opt/kimai/config/packages/local.yaml kimai/kimai2:dev

```

The [official docker documentation](https://docs.docker.com/) has more options on running the container.

*   [Twitter](https://twitter.com/kimai_org "Product updates at Twitter")
*   [Site notice](https://www.kimai.org/site-notice/)
*   [Privacy Policy](https://www.kimai.org/privacy-policy/)

*   Made by [Kevin Papst](https://www.kevinpapst.de) @ [GitHub](https://github.com/kevinpapst/kimai2)
*   [Donate](https://www.kimai.org/donate/ "Support Kimai with a donation")