---
title: "NetworkSet"
date: 2022-03-19T09:37:02+08:00
---
# Openwrt 如何下发不同的DNS和网关
主路由指定旁路有的ip为dns和网关，就可以所有的设备不用设置自动走旁路由
修改/etc/config/network 文件
config 'interface' 'lan'            
        option 'type' 'bridge'      
        option 'ifname' 'eth0.0'    
        option 'proto' 'static'     
        option 'netmask' '255.255.255.0'
        option 'dns' '208.67.222.222'   
        option 'gateway' '192.168.3.1'  
        option 'ipaddr' '192.168.3.250'
————————————————
