# MaxFoot Shopify Theme 项目

## 主题位置
- 源文件: `C:\Users\Coulson\Desktop\maxfoot-theme\`
- 远程仓库: https://github.com/LONDOBELL3151/MMX.git (main 分支)
- 用户授权: Shopify 后台连这个 repo 自动同步

## Shopify OS 2.0 主题规范(踩过的坑,死都不能忘)

### 文件结构
- `sections/*.liquid` — 普通 section
- `sections/header-group.json` + `sections/footer-group.json` — **section group JSON**,不是 liquid
- `templates/*.json` — 模板定义,**绝不引用 header-group/footer-group/header/footer**
- `layout/theme.liquid` 里用 `{% sections 'header-group' %}` 和 `{% sections 'footer-group' %}` 自动渲染 header/footer
- `config/settings_schema.json` + `config/settings_data.json` — 全局主题设置

### `{% schema %}` 块硬性规范
1. `{% schema %}` 后必须换行,不能直接 `{% schema %}{`
2. `{% endschema %}` 前必须换行,不能 `}{% endschema %}`
3. 文件结尾必须有一个 trailing newline
4. **schema 里不能同时有 `default` 和 `presets`** — `presets` 就是默认
5. **顶层 `default` key 只在 section group JSON(`.json` 文件)里合法,普通 `.liquid` section 不能用** — 默认 blocks 写在 `presets` 里:
   ```json
   "presets": [
     { "name": "Header", "blocks": [
       { "type": "menu_link", "settings": { ... } }
     ]}
   ]
   ```
6. `url` 类型 setting 的 default 必须是完整 `https://...` URL 或**留空**(相对路径 `/pages/xxx` 不行)
7. JSON 里不能有字面换行符在 string 内(`"default": "line1\nline2"` 必须 `"line1, line2"` 或转义为 `\\n`)
8. JSON 不能有 trailing comma

### Liquid 规范
- `{% if X >= Y %}` — **不能加括号** (`{% if (X >= Y) %}` 会报 "Expected dotdot")
- 默认值字符串里有 em-dash (`—` U+2014) / smart quotes (`'` `'` `"` `"`) / ellipsis (`…`) 会让 Liquid parser 崩 — **避免在 `default:` filter 字符串里用**
- `{% liquid %}` 块在某些 Shopify 版本被误判"嵌套 schema" — 改用 `{% assign %}` 串行
- section 文件**不能**用 `{% sections 'X' %}`(嵌套) — 只能 layout 用
- 任何 inline HTML `{{ x | default: '<p>...</p>' }}` 字符串里不能有特殊字符,改用 `{% if x != blank %}{% else %}<p>...</p>{% endif %}` 块

### Template JSON 规范
- **`type: "header-group"` 和 `type: "footer-group"` 不能出现在 template 里** — Shopify 自动通过 layout 渲染
- 每个 section type 必须对应 `sections/<type>.liquid` 文件
- block type 必须在 schema `blocks` 里定义才能在 template 里用
- template 引用不存在的 section type 会 cascade 报错所有相关 section

### 验证流程
- 改完跑 `C:\Users\Coulson\diagnose-theme-v2.py`(本地 JSON 合法性 + template 引用)
- 但本地脚本**不够** — Shopify 服务端还有 URL/em-dash/`{% schema %}` 格式等额外检查
- 部署后必须让用户**在 Shopify 后台 pull + customize** 实测确认

## 工作流硬性要求(2026-06-23)
- **任何对 maxfoot-theme/ 的代码改动,改完必须 `git add` + `git commit` + `git push origin main`**
- 用户(Mavis 自己)有过失忆前科,session 修过之后不知道改了什么 — commit 是唯一的真实记录
- push 后告诉用户:commit hash + 改动文件 + 让用户在 Shopify 后台 hard refresh 编辑器验证
- **不要**只改不 commit / 只 commit 不 push — 半截活是事故源头
- 例外:`AGENTS.md` 自身的更新、临时调试文件(`.bak`、`.log` 等)不需要 commit

### 救命参考
- Shopify Dawn 主题源码 = 黄金标准: https://github.com/Shopify/dawn
  - `sections/collapsible-content.liquid` — FAQ/accordion 参考
  - `sections/header-group.json` / `footer-group.json` — section group 格式
  - `templates/product.json` — template **不引用 header/footer**
  - `layout/theme.liquid` — `{% sections 'header-group' %}` 触发点

## 主题当前状态(2026-06-17)
- 70 个文件,push 到 LONDOBELL3151/MMX main 分支
- Shopify 编辑器可正常加载
- 用户确认:能进 Customize