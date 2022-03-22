---
title: "Markdonw"
date: 2022-03-22T12:27:53+08:00
---
# Markdown 高级用法

### sequenceDiagram
```mermaid
sequenceDiagram
Alice->>John: Hello John, how are you?
loop Healthcheck
    John->>John: Fight against hypochondria
end
Note right of John: Rational thoughts!
John-->>Alice: Great!
John->>Bob: How about you?
Bob-->>John: Jolly good!
```
### gantt 甘特图
```mermaid
gantt
section Section
Completed :done,    des1, 2014-01-06,2014-01-08
Active        :active,  des2, 2014-01-07, 3d
Parallel 1   :         des3, after des1, 1d
Parallel 2   :         des4, after des1, 1d
Parallel 3   :         des5, after des3, 1d
Parallel 4   :         des6, after des4, 1d
section 22
Completed :         done,    des1, 2014-01-06,2014-01-08
Active        :     done,  des2, 2014-01-07, 3d
Parallel 2   :         des, after Completed, 1d
Parallel 4   :         ssss, after des4, 1d
```
### classDiagram 类图
```mermaid
classDiagram
Class01 <|-- AveryLongClass : Cool
<<interface>> Class01
Class09 --> C2 : Where am i?
Class09 --* C3
Class09 --|> Class07
Class07 : equals()
Class07 : Object[] elementData
Class01 : size()
Class01 : int chimp
Class01 : int gorilla
class Class10 {
  <<service>>
  int id
  size()
}
```

### stateDiagram 状态图

code：
>\```mermaid
stateDiagram
[\*] --> Still
Still --> [\*]
Still --> Moving
Moving --> Still
Moving --> Crash
Crash --> [\*]
\```

render：
```mermaid
stateDiagram
[*] --> Still
Still --> [*]
Still --> Moving
Moving --> Still
Moving --> Crash
Crash --> [*]
```

- [x] Write math example
  - [x] Write diagram example
- [ ] Do something else

