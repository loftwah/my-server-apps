docker pull f0rc3/barcodebuddy-docker:YOURTAG

docker run -it -e GOKAPI_USERNAME=admin -e GOKAPI_PASSWORD=123456 f0rc3/gokapi:latest

Name

Action

GOKAPI_AWS_BUCKET

Sets the bucket name

GOKAPI_AWS_REGION

Sets the region name

GOKAPI_AWS_KEY

Sets the API key

GOKAPI_AWS_KEY_SECRET

Sets the API key secret

GOKAPI_AWS_ENDPOINT

Sets the endpoint

### Available environment variables[¶](#available-environment-variables "Permalink to this headline")

#### General[¶](#general "Permalink to this headline")

|
Name

 |

Action

 |

Persistent\*

 |

Default

 |

Required for unattended setup

 |
| --- | --- | --- | --- | --- |
|

GOKAPI\_CONFIG\_DIR

 |

Sets the directory for the config file

 |

No

 |

config

 |

No

 |
|

GOKAPI\_CONFIG\_FILE

 |

Sets the name of the config file

 |

No

 |

config.json

 |

No

 |
|

GOKAPI\_DATA\_DIR

 |

Sets the directory for the data

 |

Yes

 |

data

 |

No

 |
|

GOKAPI\_USERNAME

 |

Sets the admin username

 |

Yes

 |

unset

 |

Yes

 |
|

GOKAPI\_PASSWORD

 |

Sets the admin password

 |

Yes

 |

unset

 |

Yes

 |
|

GOKAPI\_PORT

 |

Sets the server port

 |

Yes

 |

53842

 |

Yes

 |
|

GOKAPI\_EXTERNAL\_URL

 |

Sets the external URL where Gokapi can be reached

 |

Yes

 |

unset

 |

Yes

 |
|

GOKAPI\_REDIRECT\_URL

 |

Sets the external URL where Gokapi will redirect to the index page is accesses

 |

Yes

 |

unset

 |

Yes

 |
|

GOKAPI\_LOCALHOST

 |

Bind server to localhost. Expects true/false/yes/no, always false for Docker images

 |

Yes

 |

false for Docker, otherwise unset

 |

Yes

 |
|

GOKAPI\_SALT\_FILES

 |

Sets the salt for the file password hashes

 |

Yes

 |

random salt

 |

Yes

 |
|

GOKAPI\_USE\_SSL

 |

Serve all content through HTTPS and generate certificates. Expects true/false/yes/no

 |

Yes

 |

unset

 |

Yes

 |
|

GOKAPI\_SALT\_ADMIN

 |

Sets the salt for the admin password hash

 |

Yes

 |

random salt

 |

No

 |
|

GOKAPI\_SALT\_FILES

 |

Sets the salt for the file password hashes

 |

Yes

 |

random salt

 |

No

 |
|

GOKAPI\_LENGTH\_ID

 |

Sets the length of the download IDs. Value needs to be 5 or more

 |

Yes

 |

15

 |

No

 |

\*Variables that are persistent must be submitted during the first start when Gokapi creates a new config file. They can be omitted afterwards. Non-persistent variables need to be set on every start.

