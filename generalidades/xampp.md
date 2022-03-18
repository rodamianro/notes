# Xampp
## Download
Visit the xampp's page and [download](https://www.apachefriends.org/es/download.html) the version that you need

## Creates local host in Windows
Search the hosts file in C:\Windows\System32\drivers\etc and add the virtualhost
```sh
127.0.0.1 your-domain.com
```

## Configure Apache to accept the virtualhosts
Search the vhost file in C:\xampp\apache\conf\extra, the file name is httpd-vhosts.conf.
Edit the file and put the virtual host
```sh
<VirtualHost *:80>
    DocumentRoot "C:/xampp/htdocs/fndback/web"
    ServerName local.fnd.com.co
</VirtualHost>
```