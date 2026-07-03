# 锻造事业部BOM和节拍核算 V56

版本定位：**GitHub Pages + 共享 JSON 基础数据库 + 本地 OpenRouter AI Key**。

## 核心逻辑

- 所有人打开同一个 GitHub Pages 链接。
- 页面启动后自动读取 `data/process_db.json` 和 `data/cast_rules.json` 作为共享基础数据库。
- 每个人上传自己的 PDF / PNG / JPG / XLSX，页面直接调用其本机浏览器保存的 OpenRouter Key 做 AI 识别。
- AI 只识别字段，BOM、棒料、工艺路线、Capacity Study 由页面固定算法计算。
- 项目文件、识别结果、AI Key 不上传到 GitHub，也不会共享给同事。

## 部署到 GitHub Pages

把本文件夹内容上传到 GitHub 仓库根目录，最终结构应为：

```text
XUSFORGING/
├── index.html
├── README.md
└── data/
    ├── process_db.json
    ├── cast_rules.json
    ├── equipment_map.json
    └── prompt_rules.json
```

然后在 GitHub：

```text
Settings → Pages → Deploy from branch → main / root → Save
```

访问地址通常为：

```text
https://你的用户名.github.io/XUSFORGING/
```

## 更新共享基础数据库

管理员修改基础数据库时，直接编辑仓库中的：

```text
data/process_db.json
data/cast_rules.json
```

提交后，所有人刷新页面并点击“同步共享基础库”即可读取最新版。

## AI Key

每个用户在页面顶部“本地AI设置”中填写自己的 OpenRouter Key。Key 只保存在该用户当前浏览器 localStorage。

默认模型：

```text
openrouter/free
```

免费模型可能限流；遇到 HTTP 429 时，稍后重试或改用其他支持 vision 的 OpenRouter 模型。

## 支持输入

- 锻造毛坯成本分析：PDF / PNG / JPG / XLSX
- 机加工 Production capacity study：PDF / PNG / JPG / XLSX / PPTX

XLSX 会先在浏览器解析为表格文本，再交给 AI 按固定 JSON 结构识别。

## 固定算法

- 外购棒/挤压棒：不受铸棒直径限制，不计算扒皮和料头料尾，直接带入短棒信息。
- 内铸棒：按短棒直径 + 扒皮余量匹配长棒直径；低于最小长棒按最小长棒计算并提示扒皮量过大；高于最大长棒报错。
- 机加工：单件循环 = Scycle / Cavity。
- 机加工识别后自动追加自动打码，节拍跟随最后一道机加工。
- 锻造、热处理、酸洗、抛丸节拍只取原表结果值，不用中间参数替代。
