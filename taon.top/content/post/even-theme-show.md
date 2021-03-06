---
title: "Even Theme Show"
date: 2022-04-05T18:58:20+08:00
---

## Mermaid 主题演示

> 四种，分别如下所示

```javascript
%%{init: {'theme': 'dark', "flowchart" : { "curve" : "basis" } } }%%
```

### base
自定义的主题推荐使用：
```
%%{init: {'theme': 'base', 'themeVariables': { 'primaryColor': '#ffcccc', 'edgeLabelBackground':'#ffffee', 'tertiaryColor': '#fff0f0'} } }%%
```
可以修改的内容如下：

```mermaid
%%{init: {'theme': 'base', 'themeVariables': { 'primaryColor': '#22aadd', 'edgeLabelBackground':'#223366', 'tertiaryColor': '#222233','lineColor':'#888888','textColor':'#888888','primaryTextColor':'#ffffff'} } }%%
        graph TD
          A[Christmas] -->|Get money| B(Go shopping)
          B --> C{Let me think}
          B --> G[/Another/]
          C ==>|One| D[Laptop]
          C -->|Two| E[iPhone]
          C -->|Three| F[fa:fa-car Car]
          C --> G
          subgraph section
            C
            D
            E
            F
            G
          end
```
```mermaid
%%{init: {'theme': 'dark', "flowchart" : { "curve" : "basis" } } }%%
        graph TD
          A[Christmas] -->|Get money| B(Go shopping)
          B --> C{Let me think}
          B --> G[/Another/]
          C ==>|One| D[Laptop]
          C -->|Two| E[iPhone]
          C -->|Three| F[fa:fa-car Car]
          C --> G
          subgraph section
            C
            D
            E
            F
            G
          end
```

###**neutral**

```mermaid
%%{init: {'theme': 'neutral' } }%%
        graph TD
          A[Christmas] -->|Get money| B(Go shopping)
          B --> C{Let me think}
          B --> G[(Another)]
          C ==>|One| D[Laptop]
          C -->|Two| E[iPhone]
          C -->|Three| F[fa:fa-car Car]
          subgraph section
            D
            E
            F
            G
          end
```

### default

```mermaid
%%{init: {'theme': 'default' } }%%
        graph TD
          A[Christmas] -->|Get money| B(Go shopping)
          B --> C{Let me think}
          B --> G[/Another/]
          C ==>|One| D[Laptop]
          C -->|Two| E[iPhone]
          C -->|Three| F[fa:fa-car Car]
          subgraph section
            C
            B
          end
```

###**forest**

```mermaid
%%{init: {'theme': 'forest' } }%%
        graph TD
          A[Christmas] -->|Get money| B(Go shopping)
          B --> C{Let me think}
          B --> G[/Another/]
          C ==>|One| D[Laptop]
          C -->|Two| E[iPhone]
          C -->|Three| F[fa:fa-car Car]
          subgraph section
            C
            G
          end
```