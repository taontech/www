---
title: "Method for HDRGainMap From HEIC"
date: 2022-04-07T11:49:37+08:00
---
# 从HEIC中获取HDR gainmap的方法
>简单方法
```
let ciImage = CIImage(contentsOf: input, options: [.init(rawValue: "kCIImageAuxiliaryHDRGainMap"): true])
```
>更复杂的方法
```swift
import UIKit
import MobileCoreServices.UTCoreTypes

if #available(iOS 14.1, *) {
    let input = Bundle.main.url(forResource: "IMG_0037", withExtension: "HEIC")!
    let output = FileManager().temporaryDirectory.appendingPathComponent("IMG_0037.GAIN_MAP.BMP")
    let source = CGImageSourceCreateWithURL(input as CFURL, nil)!

    // urn:com:apple:photo:2020:aux:hdrgainmap
    let dataInfo = CGImageSourceCopyAuxiliaryDataInfoAtIndex(source, 0, kCGImageAuxiliaryDataTypeHDRGainMap)! as Dictionary
    let data = dataInfo[kCGImageAuxiliaryDataInfoData] as! Data
    let description = dataInfo[kCGImageAuxiliaryDataInfoDataDescription]! as! [String: Int]
    let size = CGSize(width: description["Width"]!, height: description["Height"]!)
    
    let ciImage = CIImage(bitmapData: data, bytesPerRow: description["BytesPerRow"]!, size: size, format: .L8, colorSpace: nil)
    let cgImage = CIContext().createCGImage(ciImage, from: CGRect(origin: CGPoint(x: 0, y: 0), size: size))!
    
    let destRef = CGImageDestinationCreateWithURL(output as CFURL, kUTTypeBMP, 1, nil)!
    CGImageDestinationAddImage(destRef, cgImage, [:] as CFDictionary)
    CGImageDestinationFinalize(destRef)

    print(output)
}
```

来源
[https://gist.github.com/kiding/fa4876ab4ddc797e3f18c71b3c2eeb3a](https://gist.github.com/kiding/fa4876ab4ddc797e3f18c71b3c2eeb3a)
