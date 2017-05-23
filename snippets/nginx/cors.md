
THe following code will add CORS headers and also handle preflight checks. Place in a location block that you want to be CORS place option before any code in the location block and the CORS header after the proxy code.

Note that WebSockets are not checked for CORS and are not subject to the same policies. Simply ensure that it is using `wss` protocol with a valid server key,


```nginx

        # Handle preflight check
        if ($request_method = 'OPTIONS') {
            # Tell client that this pre-flight info is valid for 10 minutes, which is chrome's cap. Firefox's is 24 hours.
            add_header 'Access-Control-Max-Age' 600;
            add_header 'Content-Type' 'text/plain charset=UTF-8';
            add_header 'Content-Length' 0;
            add_header 'Access-Control-Allow-Origin' '*' always;
            add_header 'Access-Control-Allow-Credentials' 'true' always;
            add_header 'Access-Control-Allow-Methods' 'GET, POST, PUT, DELETE, OPTIONS' always;
            add_header 'Access-Control-Allow-Headers' 'Accept,Authorization,Cache-Control,Content-Type,DNT,If-Modified-Since,Keep-Alive,Origin,User-Agent,X-Requested-With' always;
            add_header 'Access-Control-Expose-Headers' 'Authorization' always;
            return 204;
        }
        
        # proxy code
        
        add_header 'Access-Control-Allow-Origin' '*' always;
        add_header 'Access-Control-Allow-Credentials' 'true' always;
        add_header 'Access-Control-Allow-Methods' 'GET, POST, PUT, DELETE, OPTIONS' always;
        add_header 'Access-Control-Allow-Headers' 'Accept,Authorization,Cache-Control,Content-Type,DNT,If-Modified-Since,Keep-Alive,Origin,User-Agent,X-Requested-With' always;
        add_header 'Access-Control-Expose-Headers' 'Authorization' always;
        # If you are using a custom header for, say an auth token make sure to include it in the Allow-Headers and Expose-Headers lists.

```


What if I want CORS for specific domains only?

```nginx
        set $cors '';
        # Add allowed domains in regex as ors.
        if ($http_origin ~ '^https?://(localhost|www\.yourdomain\.com|www\.yourotherdomain\.com)') {
            set $cors 'true';
        }

        if($cors = 'true') {

        

            add_header 'Access-Control-Allow-Origin' '*' always;
            add_header 'Access-Control-Allow-Credentials' 'true' always;
            add_header 'Access-Control-Allow-Methods' 'GET, POST, PUT, DELETE, OPTIONS' always;
            add_header 'Access-Control-Allow-Headers' 'Accept,Authorization,Cache-Control,Content-Type,DNT,If-Modified-Since,Keep-Alive,Origin,User-Agent,X-Requested-With' always;
            add_header 'Access-Control-Expose-Headers' 'Authorization' always;
            # If you are using a custom header for, say an auth token make sure to include it in the Allow-Headers and Expose-Headers lists.
        }
        # Handle preflight check, this part unchanged.
        if ($request_method = 'OPTIONS') {
            # Tell client that this pre-flight info is valid for 10 minutes, which is chrome's cap. Firefox's is 24 hours.
            add_header 'Access-Control-Max-Age' 600;
            add_header 'Content-Type' 'text/plain charset=UTF-8';
            add_header 'Content-Length' 0;
            return 204;
        }

```
