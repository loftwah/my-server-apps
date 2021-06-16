$ docker run -p 80:80 \
    -e APP_NAME=XBackBone \
    -e URL=http:\/\/127.0.0.1 \
    --name xbb \
    pe46dro/xbackbone-docker

    Environment Variables
When you start this image, you can adjust the configuration by passing one or more environment variables on the docker run command line.

APP_NAME
This will specify the app name, if none is provided the default is XBackBone -e APP_NAME=XBackBone

URL
This will specify the app url, slashes need to be escaped like follow -e URL=http:\/\/127.0.0.1

GENERATE_RELEASE=TRUE dev-only
If set, this environment variable will generate a release zip and will place it on srv/xbb/storage

Build Args Variables
When you build the image yourself, you can adjust the version using the --build-arg variable=value parameter on the docker build command line.

XBACKBONE_VERSION
You can specify the tag from XBackBone release and download the desired one

Where to Store Data
Available mount point
/app/storage
/app/resources/database
/app/logs
/app/config (to keep config files - Docker container only)
Permissions
The folder on host system need to have both UID and GID 1000

PHP Customization
You can specify eg. php.memory_limit=256M as dynamic env variable which will set memory_limit = 256M as php setting. Refer to webdevops documentation for more details

Environment variable	Description	Default
php.{setting-key}	Sets the {setting-key} as php setting	
PHP_DATE_TIMEZONE	date.timezone	UTC
PHP_DISPLAY_ERRORS	display_errors	0
PHP_MEMORY_LIMIT	memory_limit	512M
PHP_MAX_EXECUTION_TIME	max_execution_time	300
PHP_POST_MAX_SIZE	post_max_size	50M
PHP_UPLOAD_MAX_FILESIZE	upload_max_filesize	50M
PHP_OPCACHE_MEMORY_CONSUMPTION	opcache.memory_consumption	256
PHP_OPCACHE_MAX_ACCELERATED_FILES	opcache.max_accelerated_files	7963
PHP_OPCACHE_VALIDATE_TIMESTAMPS	opcache.validate_timestamps	default
PHP_OPCACHE_REVALIDATE_FREQ	opcache.revalidate_freq	default
PHP_OPCACHE_INTERNED_STRINGS_BUFFER	opcache.interned_strings_buffer	16
FPM_PROCESS_MAX	process.max	distribution default
FPM_PM_MAX_CHILDREN	pm.max_children	distribution default
FPM_PM_START_SERVERS	pm.start_servers	distribution default
FPM_PM_MIN_SPARE_SERVERS	pm.min_spare_servers	distribution default
FPM_PM_MAX_SPARE_SERVERS	pm.max_spare_servers	distribution default
FPM_PROCESS_IDLE_TIMEOUT	pm.process_idle_timeout	distribution default
FPM_MAX_REQUESTS	pm.max_requests	distribution default
FPM_REQUEST_TERMINATE_TIMEOUT	request_terminate_timeout	distribution default
FPM_RLIMIT_FILES	rlimit_files	distribution default
FPM_RLIMIT_CORE	rlimit_core	distribution default
Example
mkdir -p /srv/xbb/storage
mkdir -p /srv/xbb/database
mkdir -p /srv/xbb/logs
mkdir -p /srv/xbb/config

chown -R 1000:1000 /srv/xbb
MySQL Database
Clone repo
Customize ENV flags in xbb.env
Build and run
git clone https://github.com/Pe46dro/XBackBone-docker.git .
docker-compose up -d
LDAP Authentication
The following environment variables are available to configure LDAP authentication:

LDAP_ENABLED
LDAP_HOST
LDAP_PORT
LDAP_BASE_DOMAIN
LDAP_USER_DOMAIN
LDAP_RDN_ATTRIBUTE
See the docs for explanation.