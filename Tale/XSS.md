# Description of the vulnerability
Tale is a Java developed blog system based on MVC framework lightweight platform, the system admin route authentication has security issues, resulting in direct access without login.
# vendor
https://github.com/otale/tale
# version
v2.0.5
# analyse
In System Settings - Site Settings Routing /options/save, user-supplied site titles are not filtered or cleaned when stored in the database. Allows an attacker to inject something like ```"> <img src=1 onerror=alert(/xss/)>"``` to close the HTML tag and execute JavaScript. XSS is triggered when you visit the front page
![image](https://github.com/user-attachments/assets/e6b3eff0-65da-45a1-b240-8c9f950cd713)
![image](https://github.com/user-attachments/assets/962fa942-e8e8-4cc8-864e-adb0680607f8)
# verify
![image](https://github.com/user-attachments/assets/16ea36c8-fb4e-4d09-8768-9d1b7266902e)
![image](https://github.com/user-attachments/assets/ca04cdd0-1d51-4fcf-ab34-d0a7fee7216c)







