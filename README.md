# zabbix

## H3C [MIB](https://www.h3c.com/cn/d_200905/635750_30003_0.htm)


# 进程自动发现LLD脚本

## 新增自定义监控项
```
UserParameter=Process.discovery,/etc/zabbix/script/Process_Discovery.py
```
脚本内容如下：
```
#!/usr/bin/env python

import json
import os
 
result=[]
cmd=os.popen("""ps -ef | grep '\./' | grep -v grep | grep -Ev '/bin/bash|/bin/sh|python' | awk '{print $1,$8}' | sort -nr | uniq -c""")
 
for item in cmd.readlines():
    item=item.strip()
    result+=[{"{#PROCNAME}": item.split()[2], "{#PROCOWNER}": item.split()[1], "{#PROCNUMBER}": item.split()[0]}]
 
print json.dumps(result)
```
## 配置发现规则（发现完成以后，可以disable此规则）
![image](https://user-images.githubusercontent.com/26144773/119589747-0d784880-be06-11eb-8a87-63b2f790ecd9.png)
![image](https://user-images.githubusercontent.com/26144773/119589779-1d902800-be06-11eb-9372-662713dc48fe.png)
![image](https://user-images.githubusercontent.com/26144773/119589802-2b45ad80-be06-11eb-95a6-f553b1dac9e5.png)
