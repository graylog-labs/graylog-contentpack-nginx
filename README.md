# ⚠️ Deprecation notice ⚠️

This content pack has been deprecated and is not actively maintained.

Please use the community-maintained content pack by [@ronlut](https://github.com/ronlut) at https://github.com/ronlut/graylog-content-pack-nginx-docker instead.

----

# Graylog content pack for nginx

This content pack will create two inputs for the nginx `error_log` and `access_log`. Extractors are applied to effectively read the most important data into message fields. You will be able to do searches for all requests of a given remote IP, all requests that were answered with a HTTP 400 or just all requests that were slow.

The pack comes with a default dashboard to build upon and several streams that pre-group your HTTP requests into interesting categories. The additional log information described below (see *Configuring nginx*) will also add timing information to the requests handled by nginx.

![Screenshots](https://s3.amazonaws.com/graylog2public/images/contentpack-nginx-2.png)

![Screenshots](https://s3.amazonaws.com/graylog2public/images/contentpack-nginx-1.png)

### Configuring nginx

You need to run at least nginx version 1.7.1, which introduced syslog support.

**Add this to your nginx configuration file and restart the service:**

    log_format  graylog2_format  '$remote_addr - $remote_user [$time_local] "$request" $status $body_bytes_sent "$http_referer" "$http_user_agent" "$http_x_forwarded_for" <msec=$msec|connection=$connection|connection_requests=$connection_requests|millis=$request_time>';

    # replace the hostnames with the IP or hostname of your Graylog2 server
    access_log syslog:server=graylog2.example.org:12301 graylog2_format;
    error_log syslog:server=graylog2.example.org:12302;
