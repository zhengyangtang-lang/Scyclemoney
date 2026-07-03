# 锻造事业部BOM和节拍核算 V59｜GitHub共享基础库 + 智谱 BigModel AI识别版

## 结构

```
index.html
data/process_db.json
data/cast_rules.json
data/equipment_map.json
data/prompt_rules.json
```

## 使用

1. 上传到 GitHub Pages 根目录。
2. 打开页面后点击「同步共享基础库」。
3. 在顶部「本地AI设置」中填写智谱 BigModel API Key。
4. 默认模型：`glm-4.6v-flash`。
5. 保存AI设置后，上传锻造或机加工 PDF / PNG / JPG / XLSX。

## 说明

- 基础数据库从 GitHub `data/*.json` 读取。
- 项目文件和分析结果只在当前浏览器处理，不上传 GitHub。
- API Key 保存在当前浏览器 localStorage。
- AI只负责识别字段；BOM、棒料、工艺路线和 Capacity Study 由固定 JS 算法生成。
