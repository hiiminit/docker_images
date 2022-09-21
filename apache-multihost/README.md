# Apache multihost widh PHP

 - mount to /var/www/html

directory structure

/var/www/html
|
|___ _log
|  |__ apache
|  | |_ error.log
|  | |_ access.log
|  |__ php
|    |_ error.log
|    |_ slow.log
|
|___ domain.tld
|  |_ www
|  |_ anothersubdomain
|___ anotherdomain.tld
   |_ www
   |_ nextsubdomain
