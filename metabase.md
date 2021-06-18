# Metabase

```bash
docker run -d -p 3000:3000 \
-v ~/metabase-data:/metabase-data \
-e "MB_DB_FILE=/metabase-data/metabase.db" \
--name metabase metabase/metabase
```

https://www.metabase.com/docs/latest/operations-guide/running-metabase-on-docker.html

This page has all the instructions on configuration