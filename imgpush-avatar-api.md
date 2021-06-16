https://github.com/hauxir/imgpush.git

Usage
Uploading an image:

> curl -F 'file=@/some/file.jpg' http://some.host
{"filename":"somename.png"}
Fetching a file in a specific size(e.g. 320x240):

http://some.host/somename.png?w=320&h=240
returns the image cropped to the desired size

Running
imgpush requires docker

docker run -v <PATH TO STORE IMAGES>:/images -p 5000:5000 hauxir/imgpush:latest

Liveness
imgpush provides the /liveness endpoint that always returns 200 OK that you can use for docker Healthcheck and kubernetes liveness probe.

For Docker, as curl is install in the image :

healthcheck:
    start_period: 0s
    test: ['CMD-SHELL', 'curl localhost:5000/liveness -s -f -o /dev/null || exit 1']
    interval: 30s

    Configuration
Setting	Default value	Description
OUTPUT_TYPE	Same as Input file	An image type supported by imagemagick, e.g. png or jpg
MAX_SIZE_MB	"16"	Integer, Max size per uploaded file in megabytes
MAX_UPLOADS_PER_DAY	"1000"	Integer, max per IP address
MAX_UPLOADS_PER_HOUR	"100"	Integer, max per IP address
MAX_UPLOADS_PER_MINUTE	"20"	Integer, max per IP address
ALLOWED_ORIGINS	"['*']"	array of domains, e.g ['https://a.com']
VALID_SIZES	Any size	array of integers allowed in the h= and w= parameters, e.g "[100,200,300]". You should set this to protect against being bombarded with requests!
NAME_STRATEGY	"randomstr"	randomstr for random 5 chars, uuidv4 for UUIDv4
Setting configuration variables is all set through env variables that get passed to the docker container.

Example:
docker run -e ALLOWED_ORIGINS="['https://a.com', 'https://b.com']" -s -v <PATH TO STORE IMAGES>:/images -p 5000:5000 hauxir/imgpush:latest
or to quickly deploy it locally, run

docker-compose up -d