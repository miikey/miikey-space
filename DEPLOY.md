# 给部署 Agent 的说明

## 目标与范围

将本包内已定稿的英文个人站部署到 GitHub Pages，再绑定用户指定的域名。

- 发布目录：`site/`。
- 纯静态页面，无安装步骤、构建步骤、环境变量或后端。
- 保持现有文字、布局、字号与 `miikey_` 字标；蓝色下划线为 `#3659dd`。
- 本包不包含旧版页面、Git 历史、凭证或原托管平台配置。
- 不需要重新设计、添加页面、语言切换或研究文章。

## 1. 确认部署位置

向用户取得 GitHub 目标仓库（或仓库所有者和新仓库名）、最终域名、DNS 服务商。包内没有硬编码这些值。

如果仓库已经存在，先检查其内容和 Pages 配置，合并本站文件，不要覆盖无关项目。新仓库可命名为 `miikey-site`；也可以使用 `<owner>.github.io` 作为用户主页仓库。

GitHub Free 的 Pages 需要公开仓库；私有仓库托管需要支持该功能的付费方案。仓库可见性按用户选择配置。

## 2. 推送文件并启用 GitHub Pages

把 **miikey-site 文件夹里面的内容** 放在目标 Git 仓库根目录，包含隐藏的 `.github/` 目录；不要再嵌套一层 `miikey-site/`。

推送到 `main`。如果目标仓库默认分支不同，修改 `.github/workflows/pages.yml` 的 `on.push.branches`。

进入仓库：

**Settings → Pages → Build and deployment → Source → GitHub Actions**

已附工作流会上传 `site/` 并部署。首次推送若发生在 Pages 启用之前，启用后从 **Actions → Deploy website to GitHub Pages → Run workflow** 手动运行一次。

等待 workflow 成功，读取部署返回的 GitHub Pages URL，并验证页面、CSS、字体和外链。不要仅凭推送成功认定发布成功。

本包的资源均使用相对路径，支持 `https://<owner>.github.io/<repo>/`；无需先绑定域名才能预览。

## 3. 绑定自定义域名

先在 GitHub 账号的 **Settings → Pages** 验证域名，按 GitHub 给出的内容添加 TXT 记录。

随后在仓库 **Settings → Pages → Custom domain** 填写最终域名并保存，**再配置 DNS**。

本包采用 GitHub Actions 发布。域名通过 Pages 设置配置；GitHub 会忽略这种发布方式中的 `CNAME` 文件，因此不能只添加该文件。

### 根域名，例如 miikey.com

DNS 服务商的主机记录一般填 `@`，添加以下四条 A 记录：

| 类型 | 主机 | 值 |
| --- | --- | --- |
| A | @ | 185.199.108.153 |
| A | @ | 185.199.109.153 |
| A | @ | 185.199.110.153 |
| A | @ | 185.199.111.153 |
| CNAME | www | `<owner>.github.io` |

将 `<owner>` 换成实际 GitHub 仓库所有者。CNAME 的目标不包含 `https://`、路径或仓库名。

如果只使用子域名，例如 `me.example.com`，在 Pages 的 Custom domain 填该完整子域名，并将 `me` 的 CNAME 指向 `<owner>.github.io`，无需修改根域名记录。

如果现有域名已有网站，先完成临时 GitHub Pages 地址的验证，再切换域名解析。仅调整此次网站对应的 A/AAAA/CNAME；保留 MX、邮件认证 TXT 和其他无关记录。检查旧 AAAA 记录是否仍指向旧站，避免 IPv4 与 IPv6 访问不同站点。

## 4. HTTPS 与验收

- DNS 检查通过、证书签发后，在 Pages 勾选 **Enforce HTTPS**。
- DNS 和证书生效可能需要等待；证书尚未就绪时继续检查状态。
- 验证最终域名的 HTTPS 首页、两个字体文件和 CSS 均正常返回。
- 检查 390px 手机宽度下无横向溢出。
- 报告最终 URL、GitHub 仓库链接和成功的 Actions 运行链接。

## 官方资料

- GitHub Pages 建站：https://docs.github.com/en/pages/getting-started-with-github-pages/creating-a-github-pages-site
- GitHub Actions 部署：https://docs.github.com/en/pages/getting-started-with-github-pages/using-custom-workflows-with-github-pages
- 自定义域名与 DNS：https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/managing-a-custom-domain-for-your-github-pages-site
- 官方静态站模板：https://github.com/actions/starter-workflows/blob/main/pages/static.yml

文档依据 GitHub 官方说明核对于 2026-09-21。
