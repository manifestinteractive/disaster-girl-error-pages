Disaster Girl Error Pages
---

I made these for my nginx servers.  Here is how I use them:

```bash
mkdir -p /usr/share/nginx/html/error-pages
cd /usr/share/nginx/html/error-pages
git clone https://github.com/manifestinteractive/disaster-girl-error-pages.git .
```

Then we can make a file named `snippets/error-pages.conf`

```
error_page 403 /error_403.html;
error_page 404 /error_404.html;
error_page 500 /error_500.html;
error_page 503 /error_503.html;
error_page 504 /error_504.html;

location = /custom_403.html {
        root /usr/share/nginx/html/error-pages;
        internal;
}
location = /custom_404.html {
        root /usr/share/nginx/html/error-pages;
        internal;
}
location = /custom_500.html {
        root /usr/share/nginx/html/error-pages;
        internal;
}
location = /custom_503.html {
        root /usr/share/nginx/html/error-pages;
        internal;
}
location = /custom_504.html {
        root /usr/share/nginx/html/error-pages;
        internal;
}
```

Then you can include the file in your websites config file:

```
server {
  
  ...
  
  include snippets/error-pages.conf;

  ...
}
```