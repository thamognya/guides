# cgit-guide-on-apache
This is a guide for cgit on apache. I will be using debian for this tutorial.

this tutorial assumes you already have virtual hosts and git server setup

- install cgit
- install perl and cgi

and then continue

`a2enmod cgid`

make git.conf 

```
<VirtualHost *:80>
    ServerName www.git.thamognya.com
    Redirect permanent / https://git.thamognya.com/
</VirtualHost>

<VirtualHost *:80>
    ServerName git.thamognya.com
    ServerAlias www.git.thamognya.com
    DocumentRoot /usr/lib/cgit
    <Directory /usr/lib/cgit>
        Options +ExecCGI +FollowSymLinks +SymLinksIfOwnerMatch
        AllowOverride All
        order allow,deny
        Allow from all
        AddHandler cgi-script cgi
        DirectoryIndex cgit.cgi
    </Directory>
RewriteEngine on
RewriteCond %{SERVER_NAME} =git.thamognya.com [OR]
RewriteCond %{SERVER_NAME} =www.git.thamognya.com
RewriteRule ^ https://%{SERVER_NAME}%{REQUEST_URI} [END,NE,R=permanent]
</VirtualHost>

```

 git-le-ssl.conf
 
 ```
 <IfModule mod_ssl.c>
<VirtualHost *:443>
    ServerName git.thamognya.com
    ServerAlias www.git.thamognya.com
    DocumentRoot /usr/lib/cgit
    <Directory /usr/lib/cgit>
        Options +ExecCGI +FollowSymLinks +SymLinksIfOwnerMatch
        AllowOverride All
        order allow,deny
        Allow from all
        AddHandler cgi-script cgi
        DirectoryIndex cgit.cgi
    </Directory>
</IfModule>
 ```

