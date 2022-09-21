# Apache multihost widh PHP

 - mount to /var/www/html

##### Directory structure:
```
/var/www/html
|___ _log
|  |__ apache
|  | |_ error.log
|  | |_ access.log
|  |__ php
|    |_ error.log (not working right now)
|    |_ slow.log (not working right now)
|
|___ domain.tld
|  |_ www
|  |_ anothersubdomain
|___ anotherdomain.tld
   |_ www
   |_ nextsubdomain
```
