---
title: "Shortcode"
date: 2022-03-23T15:06:26+08:00
---
# 为even主题添加mermaid支持

##1. **增加 shortcode 模板**
搬运自荒野无灯的博客
[灯神的原帖](https://ttys3.dev/post/add-mermaid-shortcode-to-hugo/)

如果用 mermaid 官方的集成方法，会带来一个问题： 官方集成方法会导致我们的每个文章页面都会加载 mermaid.js ，但是 我们写博客的时候，并不是每个页面都需要加载 mermaid 这个 js, 只在文章里面包含 mermaid 代码时我们才需要加载。因此这里我们用 js 动态加载 mermaid.

首先，这个 js 我们也懒得放在主题里了，直接用 CDN 的：

去 https://www.jsdelivr.com/package/npm/mermaid 我们点开 dist 目录，然后找到完整版的js文件（注意不要看错了，选了 core 那个）：

https://cdn.jsdelivr.net/npm/mermaid@8.14.0/dist/mermaid.min.js

新增加 shortcode, 目前我用的主题是 even 因此在 themes/even 下新建：

layouts/shortcodes/mermaid.html 文件，内容如下：
```html
<!-- https://github.com/matcornic/hugo-theme-learn/blob/master/layouts/shortcodes/mermaid.html -->
<pre class="mermaid" align="{{ if .Get "align" }}{{ .Get "align" }}{{ else }}center{{ end }}">{{ safeHTML .Inner }}</pre>
```

## 加载 mermaid js

网上大部分的模板都不够自动， 很多是需要在配置里选择是否加载 mermaid 的， 这里老灯写了个根据文章内容动态加载的 js .

修改模板的 footer.html 文件，增加 js:
``` javascript
  const loadScript = (url, onloadFunction) => {
    var newScript = document.createElement("script");
    newScript.onerror =  (oError) => {
      throw new URIError("The script " + oError.target.src + " didn't load correctly.");
    };
    if (onloadFunction) { newScript.onload = onloadFunction; }
    document.head.insertAdjacentElement('beforeend', newScript);
    newScript.src = url;
  }

  // mermaid loader by ttys3.dev
  const loadMermaidOnNeed = () => {
    if (document.querySelectorAll('.mermaid').length > 0) {
      loadScript('https://cdn.jsdelivr.net/npm/mermaid@8.10.1/dist/mermaid.min.js', () => {
        document.head.insertAdjacentHTML("beforeend", `<style>.mermaid svg { background-color: #dadcd8 !important; }</style>`);
        // default, dark, neutral, forest
        mermaid.initialize({ startOnLoad: false, securityLevel: "strict", theme: "neutral" });
        // https://github.com/mermaid-js/mermaid/blob/e6e94ad57ea06ef8627bf91ddfbd88f5082952bf/src/mermaid.js#L153
        // mermaid.contentLoaded();
        mermaid.init();
        console.log("mermaid init done");
      })
    }
  }

  window.addEventListener('load', function(event) {
    // load mermaid
    loadMermaidOnNeed();
  });

```

如果要调试问题，可以在配置里增加 logLevel: 1,

theme: "neutral" 是指定主题，可以从 default, dark, neutral, forest 四个里面选。 如果不太满意默认的，也可以自行 DIY, 参考 https://mermaid-js.github.io/mermaid/#/theming

startOnLoad 选项其实在我们这里并没有什么用。 如果调用 mermaid.contentLoaded() 渲染的话，需要设置 startOnLoad 为 true. 但是其实 contentLoaded 就是判断了一下 startOnLoad 然后调用了 mermaid.init()， 因此这里老灯直接调用 mermaid.init() 渲染了。

最后，偷懒的可以直接用老灯这个修改版的terminal主题 https://github.com/ttys3/hugo-theme-terminal/tree/ttys3

