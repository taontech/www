---
title: "Heic Creation"
date: 2022-04-06T15:14:53+08:00
---
# heic 文件带辅助数据的生成

> In iOS 11 we support two kinds of images with depth. The first is HEIF HEVC, the new format, also called HEIC files, and there, there is first-class support for depth...The second format we support is JPEG. Boy, JPEG wasn't meant to do tricks like this, but we made it do this trick anyway. The map is 8-bit lossy JPEG if it's filtered, or if it has not a numbers in it, we use 16-bit lossless JPEG encoding to preserve all of the not a numbers, and we store it as a second image at the bottom of the JPEG, so it's like a multipicture object, if you're familiar with that.

**下面函数是从AR Session中创建包含深度信息的heic图片实例**
```swift
if let currentFrame = session.currentFrame, let depthData = currentFrame.capturedDepthData { // The session variable is an ARSession object  
        let outputURL: URL? = filePath(forKey: "test")
        guard let cgImageDestination = CGImageDestinationCreateWithURL(outputURL! as CFURL, kUTTypeJPEG, 1, nil) else {
            return
        }

        depthData.depthDataMap.normalize() // Normalizing depth data between 0.0 and 1.0
        let sixteenBitDepthData = depthData.converting(toDepthDataType: kCVPixelFormatType_DepthFloat16)

        let ciImage = CIImage(cvPixelBuffer: currentFrame.capturedImage)
        let context = CIContext(options: nil)
        let dict: NSDictionary = [
            kCGImageDestinationLossyCompressionQuality: 1.0,
            kCGImagePropertyIsFloat: kCFBooleanTrue,
        ]
        if let cgImage: CGImage = context.createCGImage(ciImage, from: ciImage.extent) {
            CGImageDestinationAddImage(cgImageDestination, cgImage, nil)
        }

        var auxDataType: NSString?
        let auxData = sixteenBitDepthData.dictionaryRepresentation(forAuxiliaryDataType: &auxDataType)
        CGImageDestinationAddAuxiliaryDataInfo(cgImageDestination, auxDataType!, auxData! as CFDictionary)

        CGImageDestinationFinalize(cgImageDestination)

        if let second = getDepthBufferFromFile(key: "test") {
            self.compareBuffers(first: sixteenBitDepthData.depthDataMap, second: second)
        }
    }
```