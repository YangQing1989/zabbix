# zabbix

## H3C [MIB](https://www.h3c.com/cn/d_200905/635750_30003_0.htm)


# 进程自动发现LLD脚本
```
#!/usr/bin/env python
#yq
#2020-04-22

import json
import os
 
result=[]
cmd=os.popen("""ps -ef | grep '\./' | grep -v grep | grep -Ev '/bin/bash|/bin/sh|python|zabbix|autossh|query-rem|query|sze-log|ctp-log|sse-log' | awk '{print $1,$8}' | sort -nr | uniq -c""")
 
for item in cmd.readlines():
    item=item.strip()
    result+=[{"{#PROCNAME}": item.split()[2], "{#PROCOWNER}": item.split()[1], "{#PROCNUMBER}": item.split()[0]}]
 
print json.dumps(result)
```
