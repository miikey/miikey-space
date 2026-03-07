# miikey-space 项目规则

## 图片规范

### 存放位置
- **所有配图必须下载到本地**，存放在 `public/images/blog/` 或 `public/images/` 目录
- 禁止直接使用外链图片（Unsplash/外部 CDN），防止链接失效
- 文件命名：`{文章slug}-{序号}.jpg`，例如 `defi-summer-01.jpg`

### 图片尺寸标准
- Hero image（文章头图）：1200×630px
- 行内插图：1000×480px
- About 页配图：根据版块情景选取

### 图片格式
- 统一使用 `.jpg`（用 curl 下载 Unsplash 时加 `?w=1200&h=630&fit=crop&auto=format`）
- 存入 `public/` 后在 markdown 中用 `/images/blog/xxx.jpg` 引用

### 图片布局规则（重要）
- **禁止**图片紧跟 `## 标题` 之后，必须先有至少 1-2 段文字
- **禁止**行内图片与 hero 图片使用同一张照片（视觉重复）
- 图片应放在段落之间，起到视觉缓冲和内容补充的作用
- 每篇文章图片数量：行内 2-3 张，分布在文章中部，不集中在开头

### 下载命令模板
```bash
curl -L "https://images.unsplash.com/photo-{ID}?w=1200&h=630&fit=crop&auto=format" -o public/images/blog/{filename}.jpg
```

## SEO 规范

- `site` 必须是 `https://miikey.com`（已在 astro.config.mjs 设置）
- 每篇博客必须有 `heroImage`、`heroAlt`、`description`
- 文章页 BaseHead 传 `type="article"` + `pubDate`

## 品牌规范

- 网站名：`0xmiikey` / `0xMiikey`
- Twitter：`@0xmiikey`
- GitHub：`miikey`
- **禁止在 About 以外的任何页面出现 "UQPAY" 字眼**
- **合规要求：禁止将 UQPAY 与加密货币/DeFi/crypto 直接关联描述**
  - ✅ 可以：描述 MIIKEY 个人有 DeFi/crypto 背景
  - ✅ 可以：描述 UQPAY 为"跨境支付基础设施"、"全球支付公司"
  - ❌ 禁止：描述 UQPAY 为"crypto-native"、"加密支付"、"DeFi 相关"

## 构建规范

- 每次 push 前 Husky 会自动运行 `npm run build`
- build 失败不允许 push
- preview-*.astro 等临时文件使用后必须删除

## 内容规范

- 所有博客文章需包含：行内插图 2-3 张 + blockquote 至少 1 个
- Blockquote 要有真实数据或有力洞察，不能是废话
- 图片要有说明文字（图片后跟 `*斜体说明*`）
