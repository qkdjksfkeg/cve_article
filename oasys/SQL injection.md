# Description of the vulnerability
Office automation (OA) is the most frequently used application system for the daily operation and management of the organization, which greatly improves the office efficiency of the company.
# System situation
## version
V1.0
## Project address
https://gitee.com/aaluoxiang/oa_system

## analyse
1.The global search found that ${outtype} is used as a connection parameter in src/main/resources/mappers/address-mapper.xml:18.  So, if we can control the parameters, it's going to cause SQL injection.

2.Find the allDirector() method declaration in src/main/java/cn/gson/oasys/mappers/AddressMapper.java:13.  You can control outtype.  Let's go ahead and find where the allDirector() method is called.

3.Clearly, we directly into the controller layer and found outtype parameters in src/main/Java/cn/gson/oasys/controller/address/AddrController Java:484 incoming. The allDirector () method is then called on line 489 to execute the SQL query. Therefore, as long as we are able to pass the corresponding parameters over HTTP, the SQL injection vulnerability can be triggered.


## verify

r.txt

sqlmap test results
sqlmap.py -r r.txt


