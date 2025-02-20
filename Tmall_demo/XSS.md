# Description of the vulnerability
Mini-Tmall is a mini Tmall mall based on Spring Boot, which can be quickly deployed and run, and is suitable as a template for completion.
# System situation
## version
2025/02/11 latest
## Project address
https://gitee.com/project_team/Tmall_demo
## verify
The audit of this project found that the filter layer had no code for protecting XSS.

Further verification from the perspective of black box testing.

There is an XSS vulnerability in Admin Background - My Account - Administrator nickname. Access the function, Type the XSS Vulnerability verification POC in the administrator nickname,click Save, trigger the XSS box, as shown below:

<img width="666" alt="WXWorkLocal_174003408742" src="https://github.com/user-attachments/assets/979a2a9f-d4df-4d08-b1d3-b83f63c053f2" />
<img width="932" alt="WXWorkLocal_17400355138468" src="https://github.com/user-attachments/assets/f67a32ff-779f-4726-85b8-2bd64154d0d9" />


