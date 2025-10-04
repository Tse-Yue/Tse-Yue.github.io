---
title: 在 Fuwari 中使用 Giscus 评论系统
published: 2025-10-04
description: Fuwari + Giscus 评论系统
tags:
  - Fuwari
  - Giscus
  - Blog
category: 折腾电脑记
draft: false
---

### 前言

### 一、准备工作

- 已经部署好的 Fuwari，还没部署可以先去看我的[这篇文章](https://nimeblogs.netlify.app/posts/building_blogs/)
- 一个较好的心态，但我是一次成功的，所以不是很必要吧

### 二、为 Giscus 进入 Fuwari 做好准备

1. 在 Github 中，新建一个仓库，命名随意，如 `fuwari-comments`，**但一定要 `public`**!

2. 打开 `setting`，在 `General` 一栏的 `Feature` 中，勾选 `Discussions`。

3. 安装 [Giscus Apps](https://github.com/apps/giscus)。

4. 打开 [Giscus](https://giscus.app/zh-CN)。

	- `语言` 默认。
	- `仓库` 填你新建的仓库，注意是否所有的条件均满足。
	- `页面 ↔️ discussion 映射关系` 默认即可。
	- `Discussion 分类` 选择 `Announcements`。
	- `特性` 可多勾选上 `将评论框放在评论上方`。

5. 记下 仓库ID `data-repo-id` 和 分类ID `data-category-id`，等会要用。

### 三、喜迎 Giscus 入~~藏~~本地

1. 打开 Fuwari 的本地根目录。

2. 打开 `src/components/misc`，新建 `Giscus.astro` 文件，内容如下：

```diff lang="astro"
---
interface Props {
  repo: string;
  repoId: string;
  category: string;
  categoryId: string;
  mapping?: string;
  reactionsEnabled?: boolean;
  emitMetadata?: boolean;
  inputPosition?: 'top' | 'bottom';
  lang?: string;
}

const {
  repo,
  repoId,
  category,
  categoryId,
  mapping = 'pathname',
  reactionsEnabled = true,
  emitMetadata = false,
+  inputPosition = '根据你的设置定 ‘top’ or ‘bottom’',
  lang = 'zh-CN'
} = Astro.props;
---

<div id="giscus-container"></div>

<script define:vars={{ repo, repoId, category, categoryId, mapping, reactionsEnabled, emitMetadata, inputPosition, lang }}>
  function loadGiscus() {
    const container = document.getElementById('giscus-container');
    if (!container) return;

    const isDark = document.documentElement.classList.contains('dark');
    const theme = isDark ? 'dark' : 'light';

    const script = document.createElement('script');
    script.src = 'https://giscus.app/client.js';
    script.setAttribute('data-repo', repo);
    script.setAttribute('data-repo-id', repoId);
    script.setAttribute('data-category', category);
    script.setAttribute('data-category-id', categoryId);
    script.setAttribute('data-mapping', mapping);
    script.setAttribute('data-strict', '0');
    script.setAttribute('data-reactions-enabled', reactionsEnabled ? '1' : '0');
    script.setAttribute('data-emit-metadata', emitMetadata ? '1' : '0');
    script.setAttribute('data-input-position', inputPosition);
    script.setAttribute('data-theme', theme);
    script.setAttribute('data-lang', lang);
    script.setAttribute('data-loading', 'lazy');
    script.crossOrigin = 'anonymous';
    script.async = true;

    container.appendChild(script);
  }

  // 监听主题变化
  function updateGiscusTheme() {
    const giscusFrame = document.querySelector('iframe[src*="giscus"]');
    if (giscusFrame) {
      const isDark = document.documentElement.classList.contains('dark');
      const theme = isDark ? 'dark' : 'light';

      giscusFrame.contentWindow.postMessage({
        giscus: {
          setConfig: {
            theme: theme
          }
        }
      }, 'https://giscus.app');
    }
  }

  // 监听DOM变化来检测主题切换
  const observer = new MutationObserver((mutations) => {
    mutations.forEach((mutation) => {
      if (mutation.type === 'attributes' && mutation.attributeName === 'class') {
        updateGiscusTheme();
      }
    });
  });

  // 页面加载时初始化
  if (document.readyState === 'loading') {
    document.addEventListener('DOMContentLoaded', loadGiscus);
  } else {
    loadGiscus();
  }

  // 开始观察主题变化
  observer.observe(document.documentElement, {
    attributes: true,
    attributeFilter: ['class']
  });
</script>
```

4. 保存。

5. 打开 `src/pages/posts/[...slug].astro`，加入如下内容：

```diff lang="astro"
<!-- 开头 -->
import path from "node:path";
import License from "@components/misc/License.astro";
import Markdown from "@components/misc/Markdown.astro";
+import Giscus from "../../components/misc/Giscus.astro";
import I18nKey from "@i18n/i18nKey";
import { i18n } from "@i18n/translation";
import MainGridLayout from "@layouts/MainGridLayout.astro";
```

```diff lang="astro"
<!-- 中间 -->
            <Markdown class="mb-6 markdown-content onload-animation">
                <Content />
            </Markdown>

            {licenseConfig.enable && <License title={entry.data.title} slug={entry.slug} pubDate={entry.data.published} class="mb-6 rounded-xl license-container onload-animation"></License>}

+            <Giscus
+               repo="你的用户名/仓库名"
+               repoId="仓库ID"
+               category="Announcements"
+               categoryId="分类 ID"
+               lang="语言，默认‘zh-CN’"
+            />
            <br>
```

（上面给了附近的代码，可以自行定位）

6. 重新推送（可以先预览一下）

```bash
git add .
git commit -m "更新"
git push
```

$\color{#3A3}{\large{finish}}$