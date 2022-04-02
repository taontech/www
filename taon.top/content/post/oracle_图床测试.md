---
title: "Oracle_图床测试"
date: 2022-04-02T15:34:32+08:00
---
## 本文中所有图片链接都来自Oracle对象存储
![oracle](https://objectstorage.ap-seoul-1.oraclecloud.com/p/DkmBWG3C7bJ9sThoNqhXu_k0aGals8XsrkQpNdIrTngzmiP5rxOcEH4HRrM-g_Mc/n/cnlim0eg821n/b/bucket-20220329-1150/o/imgTest5f38b1e0fd7921f2bdd4af0db6bf810f.JPG)

### 只是这链接的生成太过繁琐。

[桶链接](https://objectstorage.ap-seoul-1.oraclecloud.com/p/Eop1uwUlGE1vEUnWq8t7x9gANSVcUrEVLryl3Ko1v84fZfK-fP0R_FbFQpm3WfU1/n/cnlim0eg821n/b/bucket-20220329-1150/o/)

桶中所有资源都只需要在桶链接的基础上加上文件名称即可访问。

> 桶链接为 https://objectstorage.ap-seoul-1.oraclecloud.com/p/Eop1uwUlGE1vEUnWq8t7x9gANSVcUrEVLryl3Ko1v84fZfK-fP0R_FbFQpm3WfU1/n/cnlim0eg821n/b/bucket-20220329-1150/o/

![https://objectstorage.ap-seoul-1.oraclecloud.com/p/Eop1uwUlGE1vEUnWq8t7x9gANSVcUrEVLryl3Ko1v84fZfK-fP0R_FbFQpm3WfU1/n/cnlim0eg821n/b/bucket-20220329-1150/o/IMG_1420.JPG](https://objectstorage.ap-seoul-1.oraclecloud.com/p/Eop1uwUlGE1vEUnWq8t7x9gANSVcUrEVLryl3Ko1v84fZfK-fP0R_FbFQpm3WfU1/n/cnlim0eg821n/b/bucket-20220329-1150/o/IMG_1420.JPG)

上图中对应的亮度增益为

![亮度增益](https://objectstorage.ap-seoul-1.oraclecloud.com/p/Eop1uwUlGE1vEUnWq8t7x9gANSVcUrEVLryl3Ko1v84fZfK-fP0R_FbFQpm3WfU1/n/cnlim0eg821n/b/bucket-20220329-1150/o/mp1420.jpg)

可以看出，苹果对与亮度的处理还是非常细节。
上面亮度图使用iphone13pro拍摄的普通照片，格式采用兼容，则上面彩色途中的JPG中就会保存一张额外的亮度增益图，使用工具 exiftool 的命令

```shell
exiftool -b -"MPImage2" IMG_1058.JPG > mp1058.jpg
```
即可导出这张图，后续搞搞从heic中导出辅助图片的方法。