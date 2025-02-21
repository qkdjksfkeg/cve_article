# Description of the vulnerability
Mini-Tmall is a mini Tmall mall based on Spring Boot, which can be quickly deployed and run, and is suitable as a template for completion.
## System situation
## version
2025/02/11 latest
## Project address
https://gitee.com/project_team/Tmall_demo

## analyse
1.The global search found that ${orderUtil. orderBy} is used as a connection parameter in mybatis/mapper/ProductMapper.xml:88.  So, if we can control the parameters, it's going to cause SQL injection.
![image](https://github.com/user-attachments/assets/2605c63d-2d6d-4247-80df-b93339a65ce8)

2.Find the select() method declaration in com/xq/tmall/dao/ProductMapper.java:16.  You can control orderUtil. orderBy by passing an argument to orderUtil.  Let's go ahead and find where the select() method is called.
![image](https://github.com/user-attachments/assets/cbdac2e6-74d2-44a4-89fb-b5050ea0de26)

3.You can see the call to ProductMapper.select() found in com/xq/tmall/service/impl/ProductServiceImpl.java:38. Let's go up and see where getList() is called.
![image](https://github.com/user-attachments/assets/3454b37a-90d8-48c2-bf44-11b675bbe8b4)

4.It is obvious that we went directly to the controller layer and found that getList() was called in com/xq/tmall/controller/fore/ForeProductListController.java:168.  So, as long as we can pass the corresponding parameters over HTTP, we can trigger the SQL injection vulnerability.
![image](https://github.com/user-attachments/assets/16470dc7-ef6d-4b79-b30f-9691867247ca)

5.The orderby parameter is obtained from line 128 through the http request.  In the next 145 lines give the OrderUtil class.  You can go further and look at the class's constructor.
![image](https://github.com/user-attachments/assets/e3e99996-7874-4780-bf77-900170176242)
![image](https://github.com/user-attachments/assets/393d9132-0669-49c5-9a74-43e912a58ab2)
## verify
sqlmap test results
![image](https://github.com/user-attachments/assets/d1c33aa8-8ad3-42b2-9591-81cbdad45f71)


