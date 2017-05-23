# Browser Caching for Nginx

Add the following code to the server block of `/etc/nginx/sites-enabled/{site-name}`:

```bash
location ~*  \.(jpg|jpeg|png|gif|ico|css|js)$ {
        expires 365d;
    }

    location ~*  \.(pdf)$ {
        expires 30d;
    }
```