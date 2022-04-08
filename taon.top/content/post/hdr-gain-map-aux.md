---
title: "Hdr Gain Map Aux"
date: 2022-04-08T19:01:10+08:00
---


``` swift
+ ( nullable NSData* )HDRGainMapImageData:(nonnull NSData *)imageData{
    NSData *hdrData = nil;
    
    CGImageSourceRef imageSource = CGImageSourceCreateWithData((CFDataRef)imageData, NULL);
    if (imageSource) {
        NSDictionary *auxDataDictionary = (__bridge NSDictionary *)CGImageSourceCopyAuxiliaryDataInfoAtIndex(imageSource, 0, kCGImageAuxiliaryDataTypeHDRGainMap);
        if (auxDataDictionary) {
            //
        }
        
        CFRelease(imageSource);
    }

    return hdrData;
}
```
内存数据为：

``` terminal
Printing description of auxDataDictionary:
{
    kCGImageAuxiliaryDataInfoData = {length = 749472, bytes = 0x26262626 26262626 26262626 26262626 ... 0c000000 00000000 };
    kCGImageAuxiliaryDataInfoDataDescription =     {
        BytesPerRow = 592;
        Height = 1266;
        Orientation = 1;
        PixelFormat = 1278226488;
        Width = 585;
    };
    kCGImageAuxiliaryDataInfoMetadata = "<CGImageMetadata 0x10900d060> (\n    Radiance:AdjustmentData = eyJ2ZXJzaW9uIjoiMSIsImFtb3VudCI6MC43NSwiYmxhbmNlIjowLjQwMDAwMDAwNTk2MDQ2NDQ4fQ==\n    HDRGainMap:HDRGainMapVersion = 65536\n    iio:hasXMP = True\n)\n";
}
```