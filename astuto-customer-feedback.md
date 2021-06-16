https://github.com/riggraz/astuto.git

**Note 1**: check whether a file named `.env` is present in the root directory of Astuto. If not, create it. You can copy the template of [.env-example](https://github.com/riggraz/astuto/blob/master/.env-example).

**Note 2**: each time you change an environment variable inside `.env` you need to stop docker containers and run `script/docker-run.sh` to start them again.

**Note 3**: you should never use double quotation marks, even for strings with multiple words (e.g. `APP_NAME=Your App Name` is good, `APP_NAME="Your App Name"` is bad).

You **have to** define the following environment variables inside the `.env` file.

| Name | Possible values | Description |
| --- | --- | --- |
| ENVIRONMENT | development, production | The environment in which Astuto has to run. If you don't know what it is, use production. **You must run `script/docker-update.sh` after changing this**. |
| SECRET\_KEY\_BASE | string of 64 chars | Copy the 64 random hex characters from [this website](https://www.grc.com/passwords.htm). |
| POSTGRES\_USER | string | Username to access the database. It will also be the name of the database. |
| POSTGRES\_PASSWORD | string | Password to access the database. |
| APP\_NAME | string | The name of your product. It will appear in the header and title of the website. |
| SHOW\_LOGO | yes, no | If yes then a logo will be shown in the header. To setup a custom logo you have to replace the default one at `app/javascript/images/logo.png` (you may also want to set a custom favicon by replacing the default one at `app/javascript/images/favicon.png`). |
| POSTS\_PER\_PAGE | number | Number of posts to show per page. Suggested value is 15. If not defined, default to 0. |
| EMAIL\_CONFIRMATION | yes, no | whether your user will have to confirm their email addresses or not. Since emails don't work yet in Astuto, set it to no. |

# This is an example configuration for the .env file
# You need to create the .env file yourself
# For more information check out this page:
# https://github.com/riggraz/astuto/wiki/Required-environment-variables

ENVIRONMENT=production
SECRET_KEY_BASE=secretkeybasehere

POSTGRES_USER=yourusernamehere
POSTGRES_PASSWORD=yourpasswordhere

APP_NAME=You App Name Here
SHOW_LOGO=yes
POSTS_PER_PAGE=15

EMAIL_CONFIRMATION=no