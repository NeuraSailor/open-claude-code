# Open Claude Code
开源版 Claude Code 命令行
从 `@anthropic-ai/claude-code` npm 包的 source map 还原 TypeScript 源码。

## 前置要求

- Node.js & npm
- [reverse-sourcemap](https://github.com/danielkec/node-reverse-sourcemap)

## 使用方法

```bash
cc_ver=2.1.88
npm install -g reverse-sourcemap
npm pack @anthropic-ai/claude-code@${cc_ver}
mkdir -p claude-code-${cc_ver} unpack
tar -xzf anthropic-ai-claude-code-${cc_ver}.tgz -C claude-code-${cc_ver} --strip-components=1
reverse-sourcemap -v -o unpack claude-code-${cc_ver}/cli.js.map
```

也可以

```bash
node ./bin/open-claude-code.js -v 2.1.88 -d ./src
node ./src/open-claude-code-2.1.88/cli.js --version
```


## 输出结构

解包后得到以下文件和目录：

### `./anthropic-ai-claude-code-{version}.tgz`

npm 原始包

### `./claude-code-{version}/`

npm 原始包原始内容：
- `cli.js` — 打包后的 CLI 入口（~13MB）
- `cli.js.map` — Source map 文件（~60MB）

### `./unpack/claude-code-{version}/`

还原的 TypeScript 源码：

```
./unpack/claude-code-{version}/
├── src/                # 主源码目录（~1900 个 .ts 文件）
│   ├── main.tsx        # 入口文件
│   ├── tools/          # 工具模块
│   ├── commands/       # 命令处理
│   ├── services/       # 服务层
│   ├── server/         # 服务端代码
│   ├── voice/          # 语音功能
│   ├── vim/            # Vim 模式
│   └── ...
├── node_modules/       # 依赖库源码
└── vendor/             # 第三方代码
```

## 注意事项

- 还原的源码仅供学习研究使用
