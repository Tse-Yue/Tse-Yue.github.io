---
title: 通过 Fuwari 搭建个人博客
published: 2025-10-03
description: Fuwari + Astro + Netlify 部署
tags:
  - Fuwari
  - Astro
  - Blog
category: 折腾电脑记
draft: true
---

### 关于 Fuwari

（todo）

### 你需要准备些什么？

- Windows 系统。
- 一个牛逼的脑子。遇到问题先思考，想不通就搜索，搜索不到就去和AI调情，最后实在不行。。。~~别来问我~~。
- [`Git`](https://git-scm.com/downloads)：用于对Github进行操作。
- [`Node.js`](https://nodejs.org/zh-cn)：Fuwari 基于 Astro，而 Astro 基于 Node.js，版本我用的是 `20.3.0`。
- 一个 Github 账号：用于创建一个仓库存放 Fuwari 的相关文件。
- 一个 [Netlify](https://www.netlify.com/) 账号：用于创建一个Pages并且绑定域名支持访问，最好用 Github 登录。
- Markdown 编辑器，有啥用啥吧。

当然，如果你比较牛逼，你可以尝试使用其他的托管。

（或许还有其他的吧？应该）

### 正文

#### 本地部署

> PS：这里对应官方文档第二种方法，第一种比较简单但。。。似乎有点问题

1. Fork 下面这个仓库，名字随意

::github{repo="saicaca/fuwari"}

![图炸了私信作者](https://s21.ax1x.com/2025/10/03/pVTRaoF.png)

![图炸了私信作者](https://s21.ax1x.com/2025/10/03/pVTRNZT.png)

2. 然后将仓库克隆到本地：

``` bat
git clone <你的仓库URL>.git
```

:::important[这里细说一下 `<你的仓库URL>.git`]

1. 点这个 `code` 按钮

![图炸了私信作者](https://s21.ax1x.com/2025/10/03/pVTRUdU.png)

2. 在 `https` 这栏里的这个链接就是我们要的链接

![图炸了私信作者](https://s21.ax1x.com/2025/10/03/pVTRwi4.png)

:::

3. 全局安装pnpm： `npm install -g pnpm`

4. 然后在**克隆下来的根目录**安装依赖：`pnpm install` 和 `pnpm add sharp`

至此，你成功在本地部署了 Fuwari，即使配置还是别人的。

#### 信息修改

1. 在根目录下的 `src` 文件夹中，找到 `config.ts`

2. 根据你本人的情况进行更改

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

3. 清理多余文件。 打开 `/src/content/posts`，把文章剪切到别处，别删，玩意哪天要用上呢。 

#### 本地预览

1. 在根目录下打开终端，输入 `pnpm dev`，这里要稍微等一下

![pVTRsQ1.png](https://s21.ax1x.com/2025/10/03/pVTRsQ1.png)

2. 戳 `http://localhost:4321/`，即可看到本地预览的情况（好像是实时预览的）

3. 这里补个点，你可以点击上方画板，拖拽拉杆，挑一个你喜欢的颜色，记下编号，写在 `config.ts` 里

4. `ctrl + c` 结束预览

#### 推到 github

1. 首先，你需要让Git知道你是谁：`git config --global user.name "你的Github用户名"` 和 `git config --global user.email "你的Github邮箱@example.com"`。

2. 更改远程仓库为ssh*（如果是通过ssh克隆的不用改）：`git remote set-url origin git@github.com:xxx/xxx`

:::important[细说 `git@github.com:xxx/xxx`]

重新打开你的 Github 仓库

1. 点这个 `code` 按钮

![图炸了私信作者](https://s21.ax1x.com/2025/10/03/pVTRUdU.png)

2. 在 `ssh` 这栏里的这个链接就是我们要的链接

![图炸了私信作者](https://s21.ax1x.com/2025/10/03/pVTRBW9.png)

:spoiler[~~没人发现我是copy的吧（超小声~~]

:::

3. 提交所有文件：`git add .`

4. 发布一个本地提交：`git commit -m "<爱填啥填啥>"`

5. 将本地更改提交到远程仓库：`git push`

$\large{done}$

#### Netlify

1. 打开 [Netlify](https://app.netlify.com)。

2. 点击 `Project`。

3. 点击 `Add new Project`。

![图炸了私信作者](https://cdn.luogu.com.cn/upload/image_hosting/vvopcc1k.png)

4. 选择你存 Fuwari 的仓库

![图炸了私信作者](https://s21.ax1x.com/2025/10/03/pVTfDDx.png)

![图炸了私信作者](https://s21.ax1x.com/2025/10/03/pVTfBK1.png)

5. 看着填吧

![图炸了私信作者](https://cdn.luogu.com.cn/upload/image_hosting/hz4amf3s.png)

6. 等他自动部署

7. 访问

$\color{#3B3}{\large{finish}}$
