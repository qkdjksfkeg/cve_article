# Description of the vulnerability
Tale is a Java developed blog system based on MVC framework lightweight platform, the system admin route authentication has security issues, resulting in direct access without login.
# vendor
https://github.com/otale/tale
# version
v2.0.5
# analyse
In System Settings - Site Settings Routing /options/save, user-supplied site titles are not filtered or cleaned when stored in the database. Allows an attacker to inject something like ```"> <img src=1 onerror=alert(/xss/)>"``` to close the HTML tag and execute JavaScript. XSS is triggered when you visit the front page
![Uploading image.png…]()



# verify
![Uploading image.png…]()






