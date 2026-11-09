# HSTK 灵感文案

**基于大语言模型的电商营销文案生成系统设计与实现**

《生成式AI与大模型技术》课程设计，组名 HSTK，组员孙涛、刘一行。

## 功能

- 商品名称、品类、价格、真实卖点与目标人群输入。
- 小红书、淘宝、抖音和微信朋友圈平台适配。
- 种草文案、商品标题、详情介绍和带货口播；四种风格，三种篇幅。
- 一次生成 1—3 个版本；连接 DeepSeek 后可按自定义要求继续改写。
- 文案直接编辑、复制、TXT 导出与收藏。
- 本地历史记录、关键词搜索、继续编辑和删除。
- 明确标注的本地模板演示模式，无需密钥即可体验流程。
- 响应式布局，适配手机和桌面。

## 使用

打开网站，点击「连接 DeepSeek」：选择真实 AI 模式，填写自己的 API Token 和账户可用模型。默认模型 `deepseek-flash`，请求地址固定为 DeepSeek 官方 `https://api.deepseek.com/chat/completions`。

API Token 仅保留在当前页面 JavaScript 内存中，不写入仓库、localStorage、sessionStorage、URL 或导出文件。刷新后需重新输入。商品信息、生成结果和收藏保存在当前浏览器的 localStorage 中；清除浏览器数据会丢失记录。历史上限为 60 组。

网站直接从浏览器调用 DeepSeek。如果网络或服务 CORS 策略阻止浏览器调用，会显示明确错误，可先使用演示模式。GitHub Pages 是静态托管，不能替用户保管共享服务端密钥；公开站点不内置付费 API Token。

## 本地运行

无需安装依赖，使用 Node.js 22+ 和 Python 3：

```sh
npm test
python3 -m http.server 4173
```

浏览器打开 `http://localhost:4173`。使用相对资源路径，兼容 GitHub Pages 子目录。

## 部署

仓库 Settings → Pages → Source 选择 GitHub Actions。推送 main 后，工作流先运行测试，再仅打包 index.html、.nojekyll 和 assets 目录，发布到 GitHub Pages。无需任何 API 密钥仓库变量或 Secrets。

## 技术路线

HTML / CSS / 原生 JavaScript 模块 → 结构化商品输入 → 平台化提示词 → DeepSeek Chat Completions JSON 输出 → 输出校验 → 文案编辑与本地持久化。

`assets/core.js`：提示词构造、API 请求、结构化结果校验、本地模板和导出。`assets/app.js`：界面状态、历史、收藏、编辑与请求取消。接口有两分钟超时和余额不足、无效密钥、限流等错误提示。

## 课程实验建议

选取生活日用、数码家电、食品饮料各若干商品，固定相同事实，比较简单提示词与本系统结构化提示词生成的内容；人工评估事实准确性、卖点覆盖、平台适配和表达自然度。保存原始输入输出及评分标准，不预设实验结论。

官方接口参考：[DeepSeek API](https://api-docs.deepseek.com/)、[JSON Output](https://api-docs.deepseek.com/guides/json_mode/)、[GitHub Pages](https://docs.github.com/en/pages/getting-started-with-github-pages/creating-a-github-pages-site)。
