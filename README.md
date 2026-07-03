# V60 GitHub Pages + 共享JSON基础库 + 智谱BigModel AI识别版

本版本在 V59 基础上修复：AI 返回了“JSON字符串 + 额外解释文字”时，前端无法解析的问题。

## 更新方式

上传覆盖 GitHub 仓库根目录：

- index.html
- README.md
- data/

等待 GitHub Pages 更新后，用 Ctrl+F5 强制刷新。

## 说明

- 基础数据库：data/*.json，共享读取
- 项目文件：只在用户浏览器中处理，不上传 GitHub
- AI Key：保存在用户浏览器 localStorage
- 本次修复：允许解析被模型包成字符串的 JSON，并自动截取第一个完整 JSON 对象，忽略后续解释文字。
