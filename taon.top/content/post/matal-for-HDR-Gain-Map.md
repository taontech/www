---
title: "Matal for HDR Gain Map"
date: 2022-04-08T11:03:31+08:00
---

``` C++
#include <metal_stdlib>
using namespace metal;

#include <CoreImage/CoreImage.h>

extern "C" { namespace coreimage {
    float maxRGB(float r,float g,float b){
        return max(r,max(g,b));
    }
    float minRGB(float r,float g,float b){
        return min(r,min(g,b));
    }
    float lofRGB(float r,float g,float b){
        return r*0.213+g*0.715+b*0.072;
    }
    float4 brightness( sample_t v ){
        float4 r = v;
//        float bb = (maxRGB(v.r, v.g, v.b)+minRGB(v.r, v.g, v.b))/2;
        float bb = lofRGB(v.r, v.g, v.b);
        // bb = pow(bb,1/2.2);
//        float numer = v
        bb = bb;
        float vbb = bb/max((1-bb),0.001)*2;
        bb = vbb - bb;
//        bb = vbb - bb*2.0;
        bb = bb/(1+bb);
        r.r = bb;
        r.g = bb;
        r.b = bb;
        return r;
    }
    }
}
```

```swift
func brightnessFromHeic(heicPath:String, jpgPath:String) ->NSImage?{
    let heicImage = NSImage(contentsOfFile: heicPath)
    let url = URL(fileURLWithPath: heicPath)
    let ci = CIImage(contentsOf: url)
//    let jpgImageData =
//    let ciimage = CIImage(cgImage: heicImage.cgImage(forProposedRect: <#T##NSRect?#>, context: <#T##NSGraphicsContext?#>, hints: <#T##[NSImageRep.HintKey : Any]?#>))
    let brightness: CIColorKernel = {
        let url = Bundle.main.url(forResource: "default", withExtension: ".metallib")!
        let data = try! Data.init(contentsOf: url)
        let nn = CIColorKernel.kernelNames(fromMetalLibraryData: data)
//        CIColorKernel.kernelNames(fromMetalLibraryData: )
        print(nn)
        return try! CIColorKernel(functionName: "brightness", fromMetalLibraryData: data)
    }()
    let width = heicImage!.size.width
    let height = heicImage!.size.height
    let extent = CGRect(x: 0, y: 0, width: width, height: height)
    guard let final = brightness.apply(extent: extent,
     roiCallback: {(index,rect) in
           return rect
     },
    arguments: [ci]) else {
        return nil
    }
    let rep = NSCIImageRep(ciImage: final)
    let nsImage = NSImage(size: rep.size)
    nsImage.addRepresentation(rep)
    
    let jpgImageData = nsImage.imageJPEGRepresentation()
    
    FileManager.default.createFile(atPath: jpgPath, contents: jpgImageData, attributes: nil)
    let jpgImage = NSImage(contentsOfFile: jpgPath)
    return jpgImage
}

```

### HDR GAIN MAP

```swift
func gainMapFromHeic(heicPath:String, jpgPath:String) ->NSImage?{
    let input = URL(fileURLWithPath: heicPath)
    guard let ciImage = CIImage(contentsOf: input, options: [.init(rawValue: "kCIImageAuxiliaryHDRGainMap"): true]) else {
        return nil
    }
    
    let rep = NSCIImageRep(ciImage: ciImage)
    let nsImage = NSImage(size: rep.size)
    nsImage.addRepresentation(rep)
    
    let jpgImageData = nsImage.imageJPEGRepresentation()
    
    FileManager.default.createFile(atPath: jpgPath, contents: jpgImageData, attributes: nil)
    let jpgImage = NSImage(contentsOfFile: jpgPath)
    return jpgImage
//    return nil
}
```