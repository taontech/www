---
title: "Even Theme Show"
date: 2022-04-05T18:58:20+08:00
---

## Mermaid 主题演示
> 四种，分别如下所示

```
%%{init: {'theme': 'dark', "flowchart" : { "curve" : "basis" } } }%%
```
###**dark**
``` mermaid
%%{init: {'theme': 'dark', "flowchart" : { "curve" : "basis" } } }%%
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
```
###**neutral**
``` mermaid
%%{init: {'theme': 'neutral' } }%%
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
```
###**default**
``` mermaid
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
            D
            E
            F
            G
          end
```
###**forest**
``` mermaid
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
            D
            E
            F
            G
          end
```