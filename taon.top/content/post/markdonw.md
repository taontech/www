---
title: "Markdonw"
date: 2022-03-22T12:27:53+08:00
---
# Markdown 高级用法

> **⚠ WARNING: Aliens are coming.**  
> A description of the colour, smell and dangerous behaviour of the aliens.

```flowchart
st=>start: Start|past:>http://www.google.com[blank]
e=>end: End:>http://www.google.com
op1=>operation: My Operation|past
op2=>operation: Stuff|current
sub1=>subroutine: My Subroutine|invalid
cond=>condition: Yes
or No?|approved:>http://www.google.com
c2=>condition: Good idea|rejected
io=>inputoutput: catch something...|request

st->op1(right)->cond
cond(yes, right)->c2
cond(no)->sub1(left)->op1
c2(yes)->io->e
c2(no)->op2->e
```

{{< mermaid >}}
%%{init: {'theme': 'neutral'}}%%
        graph TD
          A[Christmas] -->|Get money| B(Go shopping)
          B --> C{Let me think}
          B --> G[/Another/]
          C ==>|One| D[Laptop]
          C -->|Two| E[iPhone]
          C -->|Three| F[fa:fa-car Car]
          subgraph section
            C
            D
            E
            F
            G
          end
{{< /mermaid >}}

{{< mermaid >}}
graph LR
    A[Square Rect] -- Link text --> B((Circle))
    A --> C(Round Rect)
    B --> D{Rhombus}
    C --> D
{{< /mermaid >}}

{{< mermaid >}}
pie
    title Key elements in Product X
    "Calcium" : 42.96
    "Potassium" : 50.05
    "Magnesium" : 10.01
    "Iron" :  5
{{< /mermaid >}}

{{< mermaid >}}
erDiagram
    CAR ||--o{ NAMED-DRIVER : allows
    CAR {
        string registrationNumber
        string make
        string model
    }
    PERSON ||--o{ NAMED-DRIVER : is
    PERSON {
        string firstName
        string lastName
        int age
    }
{{< /mermaid >}}
## 可以成功的

{{< mermaid >}}
stateDiagram
[*] --> Still
Still --> [*]
Still --> Moving
Moving --> Still
Moving --> Crash
Crash --> [*]
{{< /mermaid >}}

{{< mermaid >}}
sequenceDiagram
    participant Alice
    participant Bob
    Alice->>John: Hello John, how are you?
    loop Healthcheck
        John->>John: Fight against hypochondria
    end
    Note right of John: Rational thoughts<br/>prevail...
    John-->>Alice: Great!
    John->>Bob: How about you?
    Bob-->>John: Jolly good!
{{< /mermaid >}}

{{< mermaid >}}
gantt
dateFormat  YYYY-MM-DD
title 使用Mermaid增加甘特图
excludes weekdays 2014-01-10

section A 部分
已完成的任务            :done,    des1, 2014-01-06,2014-01-08
正在做的任务               :active,  des2, 2014-01-09, 3d
未完成任务1               :         des3, after des2, 5d
未完成任务2               :         des4, after des3, 5d
{{< /mermaid >}}

{{< mermaid >}}
classDiagram
Class01 <|-- AveryLongClass : Cool
Class03 *-- Class04
Class05 o-- Class06
Class07 .. Class08
Class09 --> C2 : Where am i?
Class09 --* C3
Class09 --|> Class07
Class07 : equals()
Class07 : Object[] elementData
Class01 : size()
Class01 : int chimp
Class01 : int gorilla
Class08 <--> C2: Cool label
{{< /mermaid >}}

```mermaid
%%{init: {'theme': 'base'}}%%
        graph TD
          A[Christmas] -->|Get money| B(Go shopping)
          B --> C{Let me think}
          B --> G[/Another/]
          C ==>|One| D[Laptop]
          C -->|Two| E[iPhone]
          C -->|Three| F[fa:fa-car Car]
          C -->|Fr| H[hahah]
          subgraph section
            C
            D
            E
            F
            G
          end
```