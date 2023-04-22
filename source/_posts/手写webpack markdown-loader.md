title: 手写webpack markdown-loader
author: 黄罐头
tags: ['webpack']
categories: web

date: 2023-04-20 22:05:38
---

## loader

作为webpack的核心，负责资源文件从输入到输出的转换

## 实现

```markdown
///readme.md
## MarkDown-Loader
```

```javascript
///index.js
import md from './readme.md';

document.write(md);
```

```javascript
///markdown-loader.js
///loader的返回必须是js代码
const { marked } = require('marked');

module.exports = (source) => {
  const html = marked(source);
  return `module.exports = ${JSON.stringify(html)}`;
};
```

```javascript
///webpack.config.js
const path = require('path');

module.exports = {
  mode: 'none',
  entry: './src/index.js',
  output: {
    filename: '[name].js',
    path: path.join(__dirname, 'dist'),
  },
  module: {
    rules: [
      {
        test: /\.md$/,
        use: './markdown-loader',
      },
    ],
  },
};
```



