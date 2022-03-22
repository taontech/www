---
title: "Music"
date: 2022-03-22T22:08:21+08:00
---

# 测试播放音乐的功能

{{% music "28196554" %}}

{{% music id="28196554" %}}
{{% music id="28196554" auto="1" %}}

{{% music "28196554" %}}
{{% music "28196554" "1" %}}

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