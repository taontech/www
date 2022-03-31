---
title: "Metal_Build"
date: 2022-03-31T11:04:00+08:00
---
## Metal编译时报错的解决办法
编译metal的shader时，运行下面kernel创建时会报运行时错误：
```swift
return try! CIColorKernel(functionName: "brightness", fromMetalLibraryData: data)
```

```shell
Fatal error: 'try!' expression unexpectedly raised an error: Error Domain=CIKernel Code=1 "(null)" UserInfo={CINonLocalizedDescriptionKey=Function does not exist in library data. }
```
其实是你的metal函数并没有编译进default.metallib
xcode的报错信息很少，后来发现是需要修改两个编译选项：

- **Other Metal Compiler Flags**                
  - -fcikernel
- **Other Metal Linker Flags**                     
  - -cikernel

随着xcode的版本变化，现在的metal文件编译不再那么复杂，可以自动的编译到default.metallib.但是隐藏有些设置项。