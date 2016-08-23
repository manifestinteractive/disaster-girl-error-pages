Disaster Girl Error Pages
===

Everyone Loves Disaster Girl... so why not use that chaotic smile to let your users know your site is broken ?

![Disaster Girl Error Pages](https://s3.amazonaws.com/disaster-girl/distaster-girl-error-page.gif "Disaster Girl Error Pages")


Demos:
---

* [Error 403](https://s3.amazonaws.com/disaster-girl/error_403.html)
* [Error 404](https://s3.amazonaws.com/disaster-girl/error_404.html)
* [Error 500](https://s3.amazonaws.com/disaster-girl/error_500.html)
* [Error 503](https://s3.amazonaws.com/disaster-girl/error_503.html)
* [Error 504](https://s3.amazonaws.com/disaster-girl/error_504.html)

Installation ( Nginx ):
---

I made these for my nginx servers.  Here is how I use them:

```bash
mkdir -p /usr/share/nginx/html/error-pages
cd /usr/share/nginx/html/error-pages
git clone https://github.com/manifestinteractive/disaster-girl-error-pages.git .
```

Then we can make the config file:
 
```
sudo nano /etc/nginx/snippets/error-pages.conf
```

and paste in the following 

```
error_page 403 /error_403.html;
error_page 404 /error_404.html;
error_page 500 /error_500.html;
error_page 503 /error_503.html;
error_page 504 /error_504.html;

location = /error_403.html {
    root /usr/share/nginx/html/error-pages;
    internal;
}
location = /error_404.html {
    root /usr/share/nginx/html/error-pages;
    internal;
}
location = /error_500.html {
    root /usr/share/nginx/html/error-pages;
    internal;
}
location = /error_503.html {
    root /usr/share/nginx/html/error-pages;
    internal;
}
location = /error_504.html {
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

Since these are HTML files being delivered to the browser, I went ahead and set them with the correct permissions.

```bash
sudo chmod -R u+rwX,go+rX,go-w /usr/share/nginx/html/error-pages
sudo chown -R $USER:$USER /usr/share/nginx/html/error-pages
```