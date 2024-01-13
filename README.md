[Tailwind CSS](https://tailwind.nodejs.cn/docs/installation) 学习

## 入门

### 安装 Tailwind CSS

```bash
> npm install -D tailwindcss
> npx tailwindcss init
```

### 配置模板路径

tailwind.config.js

```js
/** @type {import('tailwindcss').Config} */
module.exports = {
  content: ["./src/**/*.{html,js}"],
  theme: {
    extend: {},
  },
  plugins: [],
}

```

### 将 Tailwind 指令添加到你的 CSS

新增 src/input.css 作为 Tailwind CSS 的入口

```css
@tailwind base;
@tailwind components;
@tailwind utilities;
```

### 启动 Tailwind CLI 构建进程

--watch 监听文件变化，输出新的 build.css

```bash
> npx tailwindcss -i ./src/input.css -o ./dist/build.css --watch
```

将命令行构建替换成 scripts 脚本执行，在package.json 中新增

```json
{
  "scripts": {
    "start": "npx tailwindcss -i ./src/input.css -o ./dist/build.css --watch"
  }
}
```

### 开始在你的 HTML 中使用 Tailwind

新建 src/index.html，注意：本地测试需要注意路径，应为相对路径 ../dist/build.css

```html
<!doctype html>
<html>
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <link href="./dist/build.css" rel="stylesheet">
</head>
<body>
  <h1 class="text-3xl font-bold underline">
    Hello world!
  </h1>
</body>
</html>
```

### VS Code 插件 
> Visual Studio Code 的官方 Tailwind CSS IntelliSense 扩展通过为用户提供自动补齐、语法高亮和 linting 等高级功能来增强 Tailwind 开发体验。


![Tailwind CSS IntelliSense](/images/intellisense.c22de782.png)


`自动补齐`. 类名智能建议，CSS 函数和指令.
`Linting`. 高亮 CSS 和标记中的错误和潜在错误。
`悬停预览`. 将鼠标悬停在 Tailwind 类名称上可查看完整的 CSS。
`语法高亮`. 提供语法定义，以便正确高亮 Tailwind 功能。


## 使用 Prettier 自动分类
> 它会自动按照我们的 推荐的类顺序 对你的类进行排序。

### 安装依赖

```bash
> npm install -D prettier prettier-plugin-tailwindcss
```

### 新增配置文件
prettier.config.js

```js
// prettier.config.js
module.exports = {
  plugins: ['prettier-plugin-tailwindcss'],
}
```

### 执行 prettier CLI 来触发prettier代码格式化
./src/*.html src 文件下的所有 .html 的文件进行格式化

[更多prettier命令](https://www.prettier.cn/docs/cli.html)

```bash
> npx prettier ./src/*.html --write
```

我们也可将此 cli 加到 package.json 的脚本执行命令中

```json
{
  "scripts": {
    "prettier": "npx prettier ./src/*.html --write"
  }
}
```

## 生产环境优化 压缩 CSS
可以通过添加 --minify 标志来缩小 CSS：

```bash
> npx tailwindcss -i ./src/input.css -o ./dist/build.css --minify
```

通用我们也可以将上面的 cli 添加到 package.json 中 scripts
