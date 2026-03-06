# Mengmeng Ge - 学术主页

基于 [Academic Pages](https://github.com/academicpages/academicpages.github.io) 模板、Jekyll 构建的学术个人主页。内容已根据 [ORCID 0000-0001-6912-6152](https://orcid.org/0000-0001-6912-6152) 信息初始化。

---

## 一、部署到 GitHub Pages

### 方式 A：用户站点（推荐）

若希望网站地址为 `https://你的用户名.github.io`：

1. 在 GitHub 创建新仓库，**仓库名必须**为：`你的用户名.github.io`
2. 将本项目代码推送到该仓库
3. 在 `_config.yml` 中修改：
   ```yaml
   url: https://你的用户名.github.io
   baseurl: ""
   repository: "你的用户名/你的用户名.github.io"
   ```
4. 仓库 **Settings → Pages** 中选择 `main` 分支，保存后等待构建

### 方式 B：项目站点

若希望网站地址为 `https://你的用户名.github.io/HomePage`：

1. 在 GitHub 创建名为 `HomePage` 的仓库
2. 推送代码后，在 `_config.yml` 中修改：
   ```yaml
   url: https://你的用户名.github.io
   baseurl: "/HomePage"
   repository: "你的用户名/HomePage"
   ```
3. **Settings → Pages** 中 Source 选择 `Deploy from a branch`，Branch 选 `main`，路径选 `/ (root)`

---

## 二、本地预览

```bash
# 安装依赖
bundle install

# 启动本地服务器（访问 http://localhost:4000）
bundle exec jekyll serve -l -H localhost
```

修改 `_config.yml` 后需重启 Jekyll 才能生效。

---

## 三、内容管理指南

### 主页配置位置速查

| 配置项 | 文件路径 | 说明 |
|--------|----------|------|
| **首页正文** | `_pages/about.md` | 含 `permalink: /`，即网站首页。修改简介、About、Research Interests、News 等在此 |
| **站点级配置** | `_config.yml` | 站点标题、描述、URL；`author` 块控制侧边栏个人信息（姓名、bio、邮箱、ORCID、GitHub 等） |
| **顶部导航** | `_data/navigation.yml` | 顶部栏目及其顺序 |
| **新闻动态** | `_data/news.yml`（英文）、`_data/news-zh.yml`（中文） | 首页 News 板块，可切换语言 |

### 1. 个人信息（侧边栏）

编辑 **`_config.yml`** 中 `author` 部分：

| 字段 | 说明 |
|------|------|
| `name` | 显示姓名 |
| `bio` | 简短个人介绍 |
| `email` | 邮箱 |
| `location` | 所在地 |
| `employer` | 当前单位 |
| `orcid` | ORCID 链接 |
| `googlescholar` | Google Scholar 链接 |
| `github` | GitHub 用户名 |
| `avatar` | 头像图片名，放在 `images/` 目录 |

### 2. 添加 / 修改论文（Publications）

在 **`_publications/`** 目录下新建 Markdown 文件，文件名格式：`YYYY-MM-DD-简短标题.md`

```markdown
---
title: "论文标题"
collection: publications
category: manuscripts   # 或 conferences（会议论文）
permalink: /publication/文件名-不含扩展名
excerpt: '一句话摘要'
date: 2024-06-20
venue: '期刊/会议名称'
paperurl: 'https://doi.org/xxx'
citation: 'Ge, M. (2024). &quot;论文标题.&quot; <i>期刊名</i>.'
---

[Download paper here](论文链接)

（可在此补充详细描述）
```

- **category**：`manuscripts` = 期刊，`conferences` = 会议
- **date**：用于排序，越新越靠前

### 3. 添加 / 修改演讲（Talks）

在 **`_talks/`** 目录下新建 `YYYY-MM-DD-标题.md`：

```markdown
---
title: "演讲标题"
permalink: /talk/2024-03-01-talk-title
date: 2024-03-01
venue: "会议/机构名称"
location: "城市, 国家"
---
```

### 4. 添加 / 修改教学经历（Teaching）

在 **`_teaching/`** 目录下新建 Markdown 文件。

### 5. 修改首页 / 关于页

- **`_pages/about.md`**：首页内容（`permalink: /`）
- 修改标题、简介、研究兴趣等直接编辑该文件

### 6. 修改 CV 简历页

- **`_pages/cv.md`**：简历 Markdown 内容
- **`_data/cv.json`**：JSON 版简历数据（用于 `/cv-json/` 等页面）

### 7. 顶部导航栏的增删改

编辑 **`_data/navigation.yml`** 控制顶部栏目的显示。

**删除栏目**：删除对应项，或用 `#` 注释掉。

```yaml
main:
  - title: "Publications"
    url: /publications/
  # - title: "Talks"          # 注释后该栏目不显示
  #   url: /talks/
  - title: "Teaching"
    url: /teaching/
```

**增加栏目**：在 `main:` 下新增一项，格式如下：

```yaml
  - title: "栏目显示名称"
    url: /目标路径/
```

- `url` 以 `/` 开头，项目站点会自动加上 `baseurl`
- 对应页面需在 `_pages/` 或相应 collection 中存在，否则点击会 404

**调整顺序**：直接修改文件中各项的先后顺序即可。

### 8. News 板块（首页新闻动态）

- **`_data/news.yml`**：英文新闻（默认显示）
- **`_data/news-zh.yml`**：中文新闻（点击「中文」切换）
- 首页 News 旁有 **English | 中文** 切换，选择会保存到本地

每条新闻支持以下字段：

| 字段 | 必填 | 说明 |
|------|------|------|
| `date` | ✓ | 日期 YYYY-MM-DD |
| `text` | ✓ | 内容，支持 Markdown：`**加粗**`、`*斜体*`、`[链接](url)` |
| `url` | | 点击跳转链接 |
| `icon` | | Font Awesome 图标，如 `fa-bullhorn`、`fa-graduation-cap`、`fa-file-alt` |
| `icon_color` | | 图标颜色，如 `#0066cc`、`#c00` |
| `bold` | | `true` 时整条加粗 |
| `color` | | CSS 颜色，如 `#0066cc`、`red` |

```yaml
- date: 2025-03-01
  text: "**重要** 新闻内容"
  icon: "fa-star"
  bold: true
  color: "#c00"
  url: https://example.com
```

---

## 四、修改后如何生成与发布

### 本地生成与预览

```bash
# 本地构建（输出到 _site/ 目录）
bundle exec jekyll build

# 本地启动服务并实时预览（修改 Markdown 会自动刷新）
bundle exec jekyll serve -l -H localhost
# 浏览器访问 http://localhost:4000
```

- 修改 `.md`、`.html` 文件后，`jekyll serve` 会自动重建
- 修改 `_config.yml` 后需**重启** `jekyll serve` 才能生效

### 发布到线上（GitHub Pages）

1. **提交并推送**：
   ```bash
   git add .
   git commit -m "描述本次修改"
   git push origin main
   ```

2. **自动构建**：推送到 GitHub 后，GitHub Actions 会自动构建并部署
   - 在仓库 **Actions** 标签页可查看构建状态
   - 通常 1–3 分钟后网站更新

3. **在网页端修改**：也可在 GitHub 网页上编辑文件，保存后会自动触发构建

---

## 五、从 ORCID 同步论文

当前论文列表已根据 ORCID 记录手动导入。后续新增论文可：

1. **手动添加**：按第二节方法在 `_publications/` 新建对应 Markdown
2. **半自动**：使用 `markdown_generator/` 中的脚本：
   - 将 ORCID 导出的 BibTeX 放到 `files/` 或项目根目录
   - 运行 `markdown_generator/pubsFromBib.py` 或对应 Jupyter 笔记本生成 Markdown

---

## 六、文件结构说明

```
HomePage/
├── _config.yml          # 站点配置（标题、作者、链接等）
├── _data/
│   ├── navigation.yml   # 顶部导航
│   ├── news.yml         # 首页 News（英文）
│   ├── news-zh.yml      # 首页 News（中文）
│   └── cv.json          # CV JSON 数据
├── _pages/              # 固定页面（about、cv 等）
├── _publications/       # 论文
├── _talks/              # 演讲
├── _teaching/           # 教学
├── _posts/              # 博客文章
├── images/              # 图片（含 profile.png 头像）
├── files/               # 可下载文件（如 PDF）
└── markdown_generator/  # 批量生成 Markdown 的脚本
```

---

## 七、常见问题

**Q: 修改后网站没有更新？**  
GitHub Pages 构建需要几分钟，可在仓库 **Actions** 中查看构建状态。

**Q: 如何更换主题？**  
在 `_config.yml` 中修改 `site_theme`，可选：`default`, `air`, `sunrise`, `mint`, `dirt`, `contrast`。

**Q: 如何添加头像？**  
将头像图片命名为 `profile.png` 放到 `images/` 目录。

---

## 八、参考链接

- [Academic Pages 官方文档](https://academicpages.github.io/)
- [Jekyll 文档](https://jekyllrb.com/docs/)
- [GitHub Pages 文档](https://docs.github.com/pages)
- [ORCID 档案](https://orcid.org/0000-0001-6912-6152)
