# Description of the vulnerability
Tale is a Java developed blog system based on MVC framework lightweight platform, the system admin route authentication has security issues, resulting in direct access without login.
# vendor
https://github.com/otale/tale
# version
v2.0.5
# verify
Direct access to http://127.0.0.1:9000/admin/api/logs will jump to the login screen

![image](https://github.com/user-attachments/assets/52e00c56-fdd9-4ce2-bd5c-de1a8c0af0d2)
![image](https://github.com/user-attachments/assets/167ab1a5-8e9e-4efe-b4d2-f9e19e5e967b)

Access to http://127.0.0.1:9000/%61dmin/api/logs can bypass the login direct access, leak the administrator account password, there is a problem of permission verification.

![image](https://github.com/user-attachments/assets/2ad79427-8b37-4579-bae9-83482716956c)
![image](https://github.com/user-attachments/assets/4a1a31e7-9aaa-4d48-ae0d-89e6bea954a0)



