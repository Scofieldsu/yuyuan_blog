
---
title: 获取mac地址
date: 2015-08-28 16:18:20
categories: python 
tags: [mac,socket]
---
##获取mac地址的比较

**方法1**
```python
def get_mac(self):
        sd=os.popen("ipconfig/all").read()
        lans= sd.split("\r\n\r\n")
        lns=[]
        for i in lans:
            ln=[str(s).strip() for s in i.split("\r\n")]
            lns.append(ln)
        dip=socket.gethostbyname(socket.gethostname())#获取主机IP地址
        import re
        mac="";
        for i in lns:#获取MAC地址
            for j in i:
                if j.strip().find(dip)!=-1:
                    for m in i:
                        L = re.findall('([0-9,A-F]{2}-[0-9,A-F]{2}-[0-9,A-F]{2}-[0-9,A-F]{2}-[0-9,A-F]{2}-[0-9,A-F]{2})', m)
                        if L:
                            mac=L[0]
        return mac
```
**方法2**
```python 
import uuid
def get_mac_address(): 
    mac=uuid.UUID(int = uuid.getnode()).hex[-12:] 
    return "-".join([mac[e:e+2] for e in range(0,11,2)])
```
- *当电脑有多个网卡时，例如开启虚拟机，方法2获取的为最后一个网卡的物理地址,故方法1更合理*
>    MAC（Media Access Control或者Medium Access Control）地址，意译为媒体访问控制，或称为物理地址、硬件地址，用来定义网络设备的位置。在OSI模型中，第三层网络层负责 IP地址，第二层数据链路层则负责 MAC地址。因此一个主机会有一个MAC地址，而每个网络位置会有一个专属于它的IP地址。
> 
>MAC地址是网卡决定的，是固定的。
