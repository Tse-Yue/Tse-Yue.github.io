---
title: 通过 Fuwari 搭建个人博客
published: 2025-10-03
description: Fuwari + Astro + Netlify 部署
tags:
  - Fuwari
  - Astro
  - Blog
category: 折腾电脑记
draft: false
image: ./cover.png
---

### 关于 Fuwari

Fuwari 由 [saicaca](https://github.com/saicaca) 大佬（曾出品 Vivia）基于 Astro 彻底重写，不仅继承了 Vivia 的轻量基因，还在颜值与体验上全面进化（以下前2个的后半句纯属瞎编）：

- 界面更现代，移动端适配更细腻  
- 内置搜索，文章秒级索引  
- 渲染器贴近洛谷新渲染风格，代码块、数学公式开箱即用，更加适合 `更好的阅读体验`  
- 主题色、横幅、头像全可在 UI 里实时调色，保存即生效（本地） 

Vivia 的部署步骤确实少一两步，但 Fuwari 把后期操作全部可视化，长远看更省心。

一句话：想一步到位、写得爽又看得爽，直接跳 Fuwari 坑就对了！
### 🧰 一、准备工作（每一步都写清楚）

#### 1. 安装 Git（如果你没装）

- 打开官网：[https://git-scm.com/downloads](https://git-scm.com/downloads)
- 下载 Windows 版本，一路 Next 安装即可
- 安装完成后，打开命令行（Win + R → 输入 `cmd` → 回车），输入：

```bash
git --version
```

看到版本号就说明安装成功。

---
#### 2. 安装 Node.js（推荐 20.3.0）

- 打开官网：[https://nodejs.org/zh-cn](https://nodejs.org/zh-cn)
- 下载 20.3.0 版本（或 LTS 长期支持版）
- 安装时勾选 “Add to PATH”，其他默认即可
- 安装完后，在命令行输入：

```bash
node -v
npm -v
```

能看到版本号就说明安装成功。

---
#### 3. 注册 GitHub 账号（如果你还没有）

- 打开 [https://github.com](https://github.com)
- 点击右上角 Sign up，用邮箱注册
- 注册好后，登录

---
#### 4. 注册 Netlify 账号（用于部署）

- 打开 [https://netlify.com](https://netlify.com)
- 点击 Sign up，选择 GitHub 登录（推荐）

---


> PS：这里对应官方文档第二种方法，第一种比较简单但。。。似乎有点问题

### 🧪 二、Fork 模板仓库（复制别人代码到你账户）

1. 打开 Fuwari 模板仓库：

::github{repo="saicaca/fuwari"}

2. 点击右上角的 Fork 按钮：

![图炸了私信作者](https://s21.ax1x.com/2025/10/03/pVTRaoF.png)

3.  跳转到你的 GitHub 页面，仓库名默认是 `fuwari`，你可以改，比如叫 `my-blog`

![图炸了私信作者](https://s21.ax1x.com/2025/10/03/pVTRNZT.png)

---
### 📥 三、克隆仓库到本地（把代码下载到你电脑）

1. 打开你刚刚 Fork 的仓库页面（在你的 GitHub 账户下）

2. 点击绿色按钮 Code，复制 HTTPS 地址：

![图炸了私信作者](https://s21.ax1x.com/2025/10/03/pVTRUdU.png)

![图炸了私信作者](https://s21.ax1x.com/2025/10/03/pVTRwi4.png)
3. 打开命令行，输入：

```bash
git clone https://github.com/你的用户名/你的仓库名.git
```

例如：

```bash
git clone https://github.com/xiaoming/my-blog.git
```

---
### 📦 四、安装依赖（让项目能跑起来）

1. 进入项目文件夹：

```bash
cd my-blog
```

2. 安装 pnpm（比 npm 更快）：

```bash
npm install -g pnpm
```

3. 安装项目依赖：

```bash
pnpm install
```

4. 安装 sharp（图片处理依赖）：

```bash
pnpm add sharp
```

---
### ⚙ 五、修改博客信息（改成你自己的）

1. 用 VS Code 打开项目文件夹（推荐）

:::note[VS Code]

- 安装 VS Code：[https://code.visualstudio.com](https://code.visualstudio.com)
- 打开项目文件夹：`文件 → 打开文件夹 → 选择 my-blog`

:::

2. 打开配置文件：`src/config.ts`

:::tip[看不懂英文的看这里] 

- `title`： 标题
- `subtitle`：副标题，可选
- `lang`：语言
- `themeColor`：主题色（这边建议等会预览后在调整，毕竟现在连哪个色对那个编号还不知道呢）
- `banner`：背景
  - 这里的 `src`，是相对于文件夹 `src` 的路径

。。。其他设置不在这里仔细的展开，可以让 AI or 微软翻译 翻译注释

（实在搞不懂可以预览的时候注意一下）

:::

---
### 🧹 六、清理默认文章（把别人的文章搬走）

1. 打开文件夹：

```
src/content/posts
```

2. 把所有 `.md` 文件剪切到别的地方（比如桌面新建一个 `backup` 文件夹）

---
### 🖥 七、本地预览（看看长啥样）
#### 本地预览

1. 在命令行输入：

```bash
pnpm dev
```

![pVTRsQ1.png](https://s21.ax1x.com/2025/10/03/pVTRsQ1.png)

2. 戳 `http://localhost:4321/`

> 你会看到你的博客首页，实时更新，你改配置、写文章都会自动刷新。

---
### 🎨 八、选主题色（可选）

1. 在网页右上角点击调色板图标

2. 选一个你喜欢的颜色，记下编号

3. 打开 `src/config.ts`，把 `themeColor` 改成这个值

---
### ☁️ 九、推送到 GitHub（把本地代码同步到云端）

1. 配置 Git 用户信息（只设置一次）：

```bash
git config --global user.name "你的GitHub用户名"
git config --global user.email "你的GitHub邮箱"
```

2. 添加远程仓库（SSH 方式，推送更快）

- 打开你 GitHub 仓库页面，点击 Code → SSH，复制地址：

```bash
git@github.com:你的用户名/你的仓库名.git
```

- 设置远程地址：

```bash
git remote set-url origin git@github.com:你的用户名/你的仓库名.git
```

:::important[细说 `git@github.com:xxx/xxx`]

重新打开你的 Github 仓库

1. 点这个 `code` 按钮

![图炸了私信作者](https://s21.ax1x.com/2025/10/03/pVTRUdU.png)

2. 在 `ssh` 这栏里的这个链接就是我们要的链接

![图炸了私信作者](https://s21.ax1x.com/2025/10/03/pVTRBW9.png)

:spoiler[~~其实也可以直接按上面的填写，纯属凑字数行为~~]

:::

3. 提交代码：

```bash
git add .
git commit -m "初始化博客"
git push
```

$\large{done}$

### 🌍 十、部署到 Netlify（让全世界都能访问）

1. 打开 [https://app.netlify.com](https://app.netlify.com)

2. 点击 `Project`。

![图炸了私信作者](https://cdn.luogu.com.cn/upload/image_hosting/vvopcc1k.png)

2. 点击 `Add new project` → `Import an existing project`

![图炸了私信作者](https://cdn.luogu.com.cn/upload/image_hosting/vvopcc1k.png)

3. 选择 GitHub，授权 Netlify 访问你的仓库

4. 找到你刚刚推送的仓库（如 `my-blog`），点击它

![图炸了私信作者](https://s21.ax1x.com/2025/10/03/pVTfDDx.png)

![图炸了私信作者](https://s21.ax1x.com/2025/10/03/pVTfBK1.png)

5. 看着填吧，:spoiler[有些教程说这里不用填，但是]建议填，否则人家给你分配一个难记的地址就全完了。。。

![图炸了私信作者](https://cdn.luogu.com.cn/upload/image_hosting/hz4amf3s.png)

6. 等待部署完成（大概 1 分钟）

7. 部署成功后，Netlify 会给你个默认域名（当然，上面有填写这里的 `xxx`，就是你填的东西啦）：

```
https://xxx.netlify.app
```

---
### 📝 十二、写文章（重点！）

1. 在 `src/content/posts/` 新建一个 `.md` 文件，比如：

```
my-first-post.md
```

2. 文件开头必须写 Frontmatter（格式示例如下）：

```markdown
---
title: 我的第一篇文章
published: 2025-10-03
description: 这是我用 Fuwari 写的第一篇博客
tags: [生活, 记录]
category: 日常
draft: false
---

正文写在这里，支持 Markdown 语法。
```

:::tip[这里再补充一下如何新建一个有封面的文章]

1. 在 `src/content/posts/` 新建一个文件夹，比如：
```
my-second-post
```

2. 在文件夹中放入封面页，并新建一个 `index.md` 文件。

3. 在上面的格式后加入：

``` markdown
image: ./封面页文件名.格式
```

如：

```
image: ./cover.jpg
```

:::

3. 保存后，推送到 GitHub，Netlify 会自动重新部署

---
### ✅ 总结：你现在拥有了什么？

- 一个属于自己的博客网站
- 支持类似于洛谷的 Markdown 写作，甚至更好
- 自动部署在 Netlify 上
- 可自定义主题、标题、背景图

---
### 如果你遇到任何报错，建议：
1. 看终端提示

2. 复制错误信息搜索

3. 问 AI（比如 D老师、kimi、豆老妹）

4. 实在搞不定，~~别问我~~ 😄

$\color{#3B3}{\large{finish}}$
