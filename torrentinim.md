https://github.com/sergiotapia/torrentinim.git

Usage Guide
Torrentinim was designed to be painless to run. You download an executable, and run it. Done. It will start slurping up data from supported sources automatically.

The NUKE_MY_DATABASE environment variable initializes the database. All subsequent runs should not include NUKE_MY_DATABASE or you will nuke your entire database.

$ NUKE_MY_DATABASE=true ./torrentinim
INFO Jester is making jokes at http://0.0.0.0:5000
Starting 1 threads
Subsequent runs, don't use the NUKE_MY_DATABASE flag!

$ ./torrentinim
INFO Jester is making jokes at http://0.0.0.0:50123
Starting 1 threads
Environment variables:

TORRENTINIM_PORT - what port the app will run on.
ALLOW_ORIGINS - CORS allowed origins.
Example:

TORRENTINIM_PORT=60000 ALLOW_ORIGINS="https://example.com" ./torrentinim
Use the search JSON endpoint to perform searches against all the scraped torrents you have saved locally.

http://localhost:50123/search?query=the other guys&page=1