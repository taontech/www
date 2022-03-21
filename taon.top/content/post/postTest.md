---
title: "PostTest"
date: 2022-03-15T10:24:02+08:00
---
### test Auto webhook
红米 AX6S 解锁 SSH 安装 ShellClash 并刷入 openwrt
暴躁鸭2022年3月10日 15:12
202203092215670

准备工作

红米 AX6S 路由器
一台 Windows 或 Mac 的电脑
提前下载好需要的固件
下载安装好 Termius（老手可以不安装，直接用系统自带的 terminal）
如果你只需要 ShellClash 的功能，只用看前半部分就 OK ；需要刷 openwrt 可以跳过 ShellClash 的部分。不用担心变砖，刷坏了用官方修复工具即可刷回原厂。

解锁 SSH

1. 升级开发版固件
202203092209940
登录红米 AX6S 的后台（一般是：192.168.31.1），点击右上角选择-系统升级-选择手动升级，勾选下载好的「内测版」固件，点击开始升级。等待系统升级完成重启，重新连接上 Wi-Fi。
2. 在线计算 root 密码
202203092210359
浏览器打开 https://www.oxygen7.cn/miwifi/ 输入路由器后台右下角完整的 SN 号，点击 GO。计算出来的结果就是 root 密码，复制保存好。
3. telnet 连接开启 ssh
打开 Termius，可以选择不登录 Continue Without Account。
8C2AAD6B-524A-420B-BFD0-C41C91B5DD24
点击 New Host 添加
51541936-2C8F-4B4A-9730-4CCEC7BA4900
Address 填写：192.168.31.1
SSH：取消勾选
Telnet：勾选
然后点击向右的箭头，最后选择 Hosts 里的「192.168.31.1」开始 telnet 连接。
265346AF-FDA1-488A-8A34-B2FFF01D0C08
login 用户名：root
密码通过在线计算得来，复制粘贴回车即可。（输入不显示）
72D3F040-C74B-41C0-B688-DA903A00AD89
复制以下命令，回车即可开启 ssh。

nvram set ssh_en=1 & nvram set uart_en=1 & nvram set boot_wait=on & nvram set bootdelay=3 & nvram set flag_try_sys1_failed=0 & nvram set flag_try_sys2_failed=1
nvram set flag_boot_rootfs=0 & nvram set "boot_fw1=run boot_rd_img;bootm"
nvram set flag_boot_success=1 & nvram commit & /etc/init.d/dropbear enable & /etc/init.d/dropbear start
4. 尝试 ssh 连接路由器
31FE7942-F350-4A16-B7D0-291FD84D8932
选择 Hosts-点击 New Host 添加
Address 填写：192.168.31.1
SSH 的用户名里填写：root
Password 粘贴之前计算出来的 root 密码
点击右上角箭头，再点击 Hosts 里的 192.168.31.1 就应该能连接上 SSH 了。（注意选择 ssh 不是 telnet）
9373666F-3D32-474B-97F7-226220669E9F

7398B7D3-AE8D-4891-BB51-E637AA9C0B92
选择 ADD AND CONTINUE，就会进入 SSH 连接。

安装 ShellClash

在 SSH 里复制此命令开始安装 ShellClash

export url='http://shellclash.ga/' && sh -c "$(curl -kfsSl $url/install.sh)" && source /etc/profile &> /dev/null
56A56B4E-9D1F-4AC1-B3E2-0337A5038571

选择 2 测试版（AX6S 暂时只支持测试版）
然后 1 确认安装

配置 Clash
输入 Clash 回车进行配置
494D1DFF-03AE-4C83-8A2F-63BE9F322442
选择 1 主机或旁路由
选择 1 不代理 UDP
933A6F45-F250-4B82-A87D-6B9DF07903D7
选 1 安装 Dashboard 面板
选择 2 YACD 面板
选择 1 的路径
选择 1 确认开启
12EBAFF0-3B7A-44D7-A651-5276CACA8286
1 开始导入
1 在线生成
粘贴你的订阅链接（你的机场✈️后台有提供）
3252BB1C-4A3B-45FC-AB27-530AC3C3DC37
1 开始生成配置文件
1 立即启动 Clash 服务
最后选择 0 退出脚本即可
202203092216633
现在应该就能正常使用了，在浏览器里打开 http://192.168.31.1:9999/ui 就能访问控制后台。可以在手机小米路由器 App 上选择关闭更新，以防止自动更新，麻烦。我的建议：不折腾的就不用固化，喜欢折腾就直接刷下面的 openwrt。

安装 openwrt 系统

1. 刷入过渡 openwrt 固件
在 SSH 里复制粘贴下面的命令，便可刷入 openwrt 过渡固件。

cd /tmp
curl -L https://sebs.oss-cn-shanghai.aliyuncs.com/factory.bin -o factory.bin
mtd -r write /tmp/factory.bin firmware
202203092211047
刷入过渡固件后会自动重启，Wi-Fi 名会变为 openwrt-5G。
默认后台：192.168.6.1
用户名：root
密码：password

2. 刷写其它第三方固件：
202203092213319
在路由器后台选择-System-Backup / Flash Firmware
202203092211802
不要勾选 Keep settings，然后 Image 选择文件选择 openwrt 固件，然后点击 Flash image。
202203092210656
最后选择 Proceed 即可。
202203092210982
你可以用同样的方法刷不同版本的 openwrt 固件（不保留配置升级），这里就不过多的介绍，以后应该会有更多不同编译版本的 openwrt 固件让选择。
IMG_2422
另外 openwrt 里开启 160Mhz 也是有效的，不过 4*4 mimo 和 160Mhz 得二选一，两者不可兼得。

本文转自：https://qust.me/post/ax6s/

