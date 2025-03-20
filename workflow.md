# 项目工作流程说明书

## 项目概述

本项目是一个基于Jekyll的个人博客网站，使用GitHub Pages进行托管。网站采用了Chirpy主题，支持响应式设计、PWA功能、文章分类与标签等特性。

> 这是一个静态博客网站项目，不需要数据库支持，完全基于文件系统。Chirpy主题提供了现代化的设计和丰富的功能，适合个人博客使用。

## 技术栈

- **静态网站生成器**: Jekyll
- **主题**: Jekyll-theme-chirpy
- **托管平台**: GitHub Pages
- **版本控制**: Git
- **自动化部署**: GitHub Actions
- **本地开发环境**: Docker (可选)

> Jekyll是一个Ruby语言开发的静态网站生成器，可以将Markdown文件转换为HTML网页。GitHub Pages提供免费的静态网站托管服务，与GitHub仓库无缝集成。

## 工作流程

### 1. 初始设置

项目已经完成初始设置，主要配置文件为`_config.yml`，其中包含了网站的基本信息、社交媒体链接、评论系统等配置。

> `_config.yml`是Jekyll项目的核心配置文件，定义了网站的全局设置。修改此文件后需要重新启动Jekyll服务器才能生效。

### 2. 本地开发

#### 使用Docker (推荐)

1. **安装Docker**
   - 访问[Docker官网](https://www.docker.com/get-started)下载并安装Docker Desktop

   > Docker Desktop提供了图形界面，便于管理容器。对于Windows用户，需要启用WSL2或Hyper-V功能。

2. **启动本地预览服务器**
   ```bash
   docker run -it --rm \
     --volume="$PWD:/srv/jekyll" \
     --publish 4000:4000 \
     jekyll/jekyll:4.2.0 \
     jekyll serve
   ```

   > 这个命令会创建一个临时的Docker容器，将当前目录挂载到容器内，并在容器中启动Jekyll服务。
   > `--volume="$PWD:/srv/jekyll"` 将当前目录映射到容器内的/srv/jekyll目录
   > `--publish 4000:4000` 将容器内的4000端口映射到主机的4000端口
   > `jekyll serve` 在容器内启动Jekyll服务

3. **访问本地预览**
   - 打开浏览器访问 http://localhost:4000

   > Jekyll服务启动后，会监听文件变化并自动重新生成网站，便于实时预览修改效果。

#### 不使用Docker

1. **安装Ruby和Jekyll**
   - 安装[Ruby](https://www.ruby-lang.org/en/downloads/)
   - 安装Jekyll: `gem install jekyll bundler`

   > Ruby是Jekyll的运行环境，不同操作系统安装方式不同。Windows用户建议使用RubyInstaller，Mac用户可以使用homebrew安装。

2. **安装依赖**
   ```bash
   bundle install
   ```

   > `bundle install`会根据Gemfile文件安装所有需要的Ruby依赖包，包括Jekyll及其插件。

3. **启动本地预览服务器**
   ```bash
   bundle exec jekyll serve
   ```

   > `bundle exec`确保使用Gemfile中指定版本的Jekyll，避免版本冲突。

### 3. 内容创作

#### 创建新文章

1. **在`_posts`目录下创建新的Markdown文件**
   - 文件名格式: `YYYY-MM-DD-title.md`
   - 例如: `2023-01-01-hello-world.md`

   > 文件名格式非常重要，Jekyll会根据文件名解析文章的发布日期。日期格式必须是YYYY-MM-DD，否则文章可能不会被正确处理。

2. **添加文章前置信息**
   ```yaml
   ---
   title: 文章标题
   date: 2023-01-01 12:00:00 +0800
   categories: [分类1, 分类2]
   tags: [标签1, 标签2]
   image: /path/to/image.jpg  # 可选，文章预览图
   pin: false  # 可选，是否置顶
   ---
   ```

   > 前置信息（Front Matter）是YAML格式，位于文件顶部，两组三个连字符之间。
   > `title`: 文章标题，会显示在浏览器标签和文章页面顶部
   > `date`: 发布日期和时间，+0800表示东八区时间
   > `categories`: 文章分类，可以有多级分类，用于文章归档
   > `tags`: 文章标签，用于文章聚合和搜索
   > `image`: 文章预览图，会显示在首页和分享链接中
   > `pin`: 是否将文章置顶显示在首页

3. **编写文章内容**
   - 使用Markdown语法编写文章内容
   - 支持代码高亮、表格、图片等Markdown特性

   > Chirpy主题使用kramdown作为Markdown解析器，支持GitHub风格的Markdown语法，包括表格、代码块、任务列表等。

#### 添加图片

1. **将图片文件放在`/assets/img/`目录下**

   > 建议按照文章或类别创建子文件夹，如`/assets/img/2023/01/image.jpg`，便于管理大量图片。

2. **在文章中引用图片**
   ```markdown
   ![图片描述](/assets/img/example.jpg)
   ```

   > 图片描述会作为图片的alt属性，对SEO和无障碍访问很重要。
   > 路径以/开头表示从网站根目录开始的绝对路径。

### 4. 部署流程

#### 自动部署 (通过GitHub Actions)

1. **提交更改到GitHub仓库**
   ```bash
   git add .
   git commit -m "添加新文章"
   git push origin main
   ```

   > `git add .` 将所有修改添加到暂存区
   > `git commit -m "消息"` 提交修改并添加说明
   > `git push origin main` 将本地main分支推送到远程仓库

2. **GitHub Actions自动构建和部署**
   - 提交到`main`分支后，GitHub Actions会自动触发构建
   - 构建完成后，网站会自动部署到`gh-pages`分支
   - 部署完成后，可以通过`https://username.github.io`访问网站

   > GitHub Actions是GitHub提供的CI/CD服务，会根据仓库中的workflow配置文件自动执行构建和部署任务。
   > 构建过程会将Markdown文件转换为HTML，生成静态网站文件。
   > `gh-pages`分支专门用于存放构建后的静态文件，GitHub Pages服务会自动从这个分支提供网站访问。

#### 手动部署 (不推荐)

如果需要手动部署，可以执行以下步骤：

1. **构建网站**
   ```bash
   JEKYLL_ENV=production bundle exec jekyll build
   ```

   > `JEKYLL_ENV=production`设置环境变量，告诉Jekyll这是生产环境构建，会启用一些只在生产环境使用的功能。
   > 构建结果会保存在`_site`目录中。

2. **将`_site`目录的内容推送到`gh-pages`分支**

   > 手动部署需要额外的Git操作，容易出错，不推荐使用。自动部署更可靠且省时。

### 5. 网站维护

#### 更新主题

1. **添加上游仓库**
   ```bash
   git remote add upstream https://github.com/cotes2020/jekyll-theme-chirpy.git
   ```

   > 这会将原始主题仓库添加为远程仓库，命名为"upstream"。

2. **获取上游更新**
   ```bash
   git fetch upstream
   ```

   > 获取原始主题仓库的最新代码，但不会自动合并。

3. **合并更新**
   ```bash
   git merge upstream/master
   ```

   > 将原始主题的更新合并到本地仓库。可能需要解决合并冲突，特别是如果您修改了主题文件。

#### 自定义样式

1. **在`_sass`目录下创建或修改SCSS文件**

   > SCSS是CSS的扩展语言，提供了变量、嵌套、混合等功能，使样式表更易于维护。
   > 建议创建自己的SCSS文件，而不是直接修改主题文件，以便于主题更新。

2. **在`assets/css/style.scss`中引入自定义样式**

   > 这个文件是样式的入口点，Jekyll会将其编译为CSS文件。
   > 自定义样式应该放在最后，以覆盖主题默认样式。

## 常见问题解答

### Q: 我的电脑关机后，网站是否还能访问？
A: 可以。网站内容托管在GitHub的服务器上，与您的个人电脑无关。只要完成了部署，访问者就可以随时访问您的网站。

> GitHub Pages提供24/7的托管服务，一旦部署完成，即使您的电脑关机或断网，网站仍然可以正常访问。

### Q: Docker的作用是什么？
A: Docker主要用于创建一个标准化的本地开发环境，确保所有开发者使用相同的Jekyll版本和依赖。它简化了环境配置过程，避免了"在我电脑上能运行"的问题。使用Docker是可选的，您也可以直接在本地安装Jekyll环境。

> Docker通过容器化技术，将应用及其依赖打包在一起，确保在任何环境中都能一致运行。
> 对于Jekyll项目，使用Docker可以避免Ruby版本冲突和依赖安装问题，特别是在Windows系统上。

### Q: 如何添加评论功能？
A: 在`_config.yml`中配置评论系统。Chirpy主题支持Disqus、Utterances和Giscus三种评论系统。选择一种并填写相应的配置信息即可。

> Disqus是传统的第三方评论系统，功能丰富但加载较慢。
> Utterances和Giscus都基于GitHub Issues，轻量级且集成GitHub账号登录，适合技术博客。
> Giscus是基于GitHub Discussions的新一代评论系统，提供更丰富的互动功能。

### Q: 如何更改网站主题色调？
A: 在`_config.yml`中修改`theme_mode`选项。可选值为`light`、`dark`或留空（跟随系统偏好）。

> Chirpy主题支持亮色模式、暗色模式，以及跟随系统偏好自动切换。
> 用户也可以通过侧边栏底部的切换按钮手动切换主题模式。

## 资源链接

- [Chirpy主题文档](https://chirpy.cotes.page/)
- [Jekyll官方文档](https://jekyllrb.com/docs/)
- [Markdown语法指南](https://www.markdownguide.org/)
- [GitHub Pages文档](https://docs.github.com/en/pages) 

> Chirpy主题文档提供了主题的详细配置和使用说明。
> Jekyll官方文档包含了Jekyll的完整功能和插件说明。
> Markdown语法指南可以帮助您编写格式丰富的文章内容。
> GitHub Pages文档解释了如何配置自定义域名、HTTPS等高级功能。
