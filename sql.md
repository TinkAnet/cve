SQL injection exists in the ibos office OA. Procedure

official website:http://www.ibos.com.cn/

version:4.5.5

Function point: Background management = "File cabinet =" Delete file function

![WPS图片(1)](https://github.com/TinkAnet/cve/assets/118334129/9f4401cb-e267-4123-b46a-b6908355dfa9)

Route: r=file/dashboard/trash&op=del

The injection parameter: fids exists

Successfully burst the database name by reporting an error injection

![WPS图片(2)](https://github.com/TinkAnet/cve/assets/118334129/fd652a3a-72b9-46e7-9a89-f175bcbf4835)

![WPS图片(3)](https://github.com/TinkAnet/cve/assets/118334129/e736b455-d33e-48ee-837a-3cc943630779)
![WPS图片(4)](https://github.com/TinkAnet/cve/assets/118334129/e51c1e10-6ba1-4753-a0db-ca692c1252f2)
![WPS图片(5)](https://github.com/TinkAnet/cve/assets/118334129/d5f9c480-a4b1-4d6d-be80-61fb428c6825)
![WPS图片(6)](https://github.com/TinkAnet/cve/assets/118334129/4732514c-8412-4d54-b617-fa8d414e2048)
