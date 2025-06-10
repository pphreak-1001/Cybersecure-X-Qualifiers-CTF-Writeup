### Vulnerability: Remote code execution due to unrestricted file upload with htaccess overwrite 

In order to solve this,

Upload a .htaccess file with this config:

```
AddType application/x-httpd-php .phar
AddHandler application/x-httpd-php .phar
```

The application disallowed uploading php file along with its variants as php5, php7, phtml etc but allowed .phar file. 
Using the above htaccess i overwrite th rule to execute the .phar file as php which allowed me to get a shell.

Flag:

![image](https://github.com/user-attachments/assets/f4e124c7-1f55-4b3a-b12b-80131b27a1b3)
