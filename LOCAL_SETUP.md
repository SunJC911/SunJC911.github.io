# 本地运行指南

本文档介绍如何在本地运行此 Jekyll 博客。提供两种方式：Docker（推荐）和原生 Ruby。

---

## 方式一：Docker（推荐）

Docker 方式无需安装 Ruby 环境，更简单且避免版本冲突问题。

### 1. 安装 Docker Desktop

1. 访问 https://www.docker.com/products/docker-desktop/
2. 下载 Windows 版本并安装
3. 安装过程中会提示启用 WSL2，按提示操作
4. 安装完成后启动 Docker Desktop，等待左下角显示绿色 "Running"

### 2. 启动本地服务器

打开终端（PowerShell 或 CMD），进入项目目录：

```bash
cd D:\projects\SunJC911.github.io
```

运行以下命令：

```bash
docker run -it --rm --volume="${PWD}:/srv/jekyll" --publish 4000:4000 jekyll/jekyll:4.2.0 jekyll serve --force_polling
```

> **说明**：
> - `--volume` 将当前目录映射到容器内
> - `--publish 4000:4000` 映射端口
> - `--force_polling` 在 Windows 上启用文件变化监听

### 3. 访问网站

打开浏览器访问：http://localhost:4000

### 4. 停止服务器

在终端按 `Ctrl + C`

---

## 方式二：原生 Ruby

### 1. 安装 Ruby

1. 访问 https://rubyinstaller.org/downloads/
2. 下载 **Ruby+Devkit 3.2.x (x64)** 版本（带 Devkit）
3. 运行安装程序，安装时勾选：
   - [x] Add Ruby executables to your PATH
   - [x] Associate .rb and .rbw files with this Ruby installation
4. 安装完成后会弹出命令行窗口，输入 `1` 并回车安装 MSYS2

### 2. 验证安装

打开新的终端窗口，运行：

```bash
ruby -v
```

应显示类似 `ruby 3.2.x` 的版本号。

### 3. 安装项目依赖

进入项目目录：

```bash
cd D:\projects\SunJC911.github.io
```

安装 Bundler 和项目依赖：

```bash
gem install bundler
bundle install
```

> **注意**：首次运行 `bundle install` 可能需要几分钟，会下载 Jekyll 及相关依赖。

### 4. 启动本地服务器

```bash
bundle exec jekyll serve --livereload
```

或简写：

```bash
bundle exec jekyll s -l
```

### 5. 访问网站

打开浏览器访问：http://127.0.0.1:4000

### 6. 停止服务器

在终端按 `Ctrl + C`

---

## 常见问题

### Q: 修改文章后页面没有更新？

刷新浏览器，或检查终端是否有报错。`--livereload` 参数会自动刷新页面。

### Q: 修改 `_config.yml` 后没有生效？

修改配置文件后需要重启服务器（Ctrl+C 后重新运行启动命令）。

### Q: 端口 4000 被占用？

使用其他端口：

```bash
# Docker 方式
docker run -it --rm --volume="${PWD}:/srv/jekyll" --publish 4001:4000 jekyll/jekyll:4.2.0 jekyll serve

# 原生 Ruby 方式
bundle exec jekyll serve --port 4001
```

然后访问 http://localhost:4001

### Q: Windows 上 bundle install 报错？

确保安装的是带 Devkit 的 Ruby 版本，并且 MSYS2 已正确安装。可以重新运行：

```bash
ridk install
```

选择选项 `3` 完整安装。
