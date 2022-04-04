---
title: "Even Chroma Conflict Mermaid"
date: 2022-04-04T21:49:09+08:00
---

## 终于Mermai完美运行
如果even主题，你打开了 Syntax highlighting by Chroma ,这时候如果添加mermaid, 实际上是mermaid并不能正确的渲染。这是因为 highlighting会修改 lauguage-mermaid,导致后面mermaid不能正确渲染图像。

``` mermaid
graph LR
   A(早晨的阳光) -- 天气冷 --> B(好好学习)
   B --> D{这个第三个}
   C(第三个) --> D
   B --> C
   D --> A
```
```mermaid
graph LR
    A[Config] -- 配置了Highlighting --> B((不支持表情符号))
    A --> C(括号是圆角矩形)
    B --> D{大括号是菱形}
    C --> D
```