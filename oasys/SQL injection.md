# Description of the vulnerability
Office automation (OA) is the most frequently used application system for the daily operation and management of the organization, which greatly improves the office efficiency of the company.The system has SQL injection in the external address book query
# System situation
## version
V1.0
## Project address
https://gitee.com/aaluoxiang/oa_system

## analyse
1.The global search found that ${outtype} is used as a connection parameter in src/main/resources/mappers/address-mapper.xml:18.  So, if we can control the parameters, it's going to cause SQL injection.
![image](https://github.com/user-attachments/assets/e5020c41-7195-4f32-9a69-aad1cd9e5157)

2.Find the allDirector() method declaration in src/main/java/cn/gson/oasys/mappers/AddressMapper.java:13.  You can control outtype.  Let's go ahead and find where the allDirector() method is called.
![image](https://github.com/user-attachments/assets/46bc3b05-ca2d-4030-9fc4-8c21d9146343)

3.Clearly, we directly into the controller layer and found outtype parameters in src/main/Java/cn/gson/oasys/controller/address/AddrController Java:484 incoming. The allDirector () method is then called on line 489 to execute the SQL query. Therefore, as long as we are able to pass the corresponding parameters over HTTP, the SQL injection vulnerability can be triggered.
![image](https://github.com/user-attachments/assets/9285b932-7023-4ae2-bd34-3f5836f4c42b)


## verify
![image](https://github.com/user-attachments/assets/2bbb46f8-c007-46a2-9ecd-60d841f9394d)
r.txt
![image](https://github.com/user-attachments/assets/19abe2ec-d18a-402f-8897-cabe3a849be2)
sqlmap test results

```
sqlmap -r r.txt
```
![image](https://github.com/user-attachments/assets/66d8c630-fe29-48b3-b9f6-3823c35c21d7)
![image](https://github.com/user-attachments/assets/073a41cf-6abe-4866-82b9-e368e9be5eeb)





