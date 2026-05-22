这里存放的是我的个人网站部署文件。

我的个人网站网址：https://guyue.me

邮箱：hi@guyue.me

## 本地预览

克隆项目后，先安装依赖：

```bash
npm ci
```

本项目使用了 `hexo-renderer-pandoc`，新环境需要先安装 `pandoc`：

```bash
# macOS
brew install pandoc

# Ubuntu / Debian
sudo apt-get install pandoc
```

然后清理、生成并启动本地预览服务：

```bash
npx hexo clean
npx hexo generate
npx hexo server
```

浏览器打开：

```text
http://localhost:4000
```

也可以使用项目内的 npm scripts：

```bash
npm run clean
npm run build
npm run server
```

## 尽量模拟 GitHub Actions

部署工作流使用 Node.js `24.15.0` 和 `npm ci`。如果想让本地预览尽量接近 Actions 构建结果，请在本地切换到相同 Node.js 版本后再执行上述命令。
