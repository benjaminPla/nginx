```
http {
        include mime.types;

        server {
                listen 80;
                server_name <dns> www.<dns>

                location / {
                        return 301 https://www.<dns>;
                }
        }

        server {
                listen 443 ssl;
                server_name <dns> www.<dns>;
                root /var/www/html/cv;
                ssl_certificate /etc/letsencrypt/live/<dns>/cert.pem;
                ssl_certificate_key /etc/letsencrypt/live/<dns>/privkey.pem;

                location / {
                        try_files $uri $uri/ /index.html;
                }

                location = /favicon.ico {
                        access_log off;
                        log_not_found off;
                }
        }
}

events {}
```
