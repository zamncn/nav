# 一个简单的导航 By Chenn

个人自用网址导航页，纯静态站点，直接跑在 **GitHub Pages** 上。

- 线上域名：<https://chenn.us.ci>（`www.chenn.us.ci` 会自动 301 到主域）
- 主页面：站点根目录的 `index.html`（**没有 `/cn/` 子目录了**，2026-09-22 从 `cn/` 迁到根目录）
- 配色：**只有深色一套**，默认深色，不跟随系统主题，也没有切换按钮（浅色模式已于 2026-09-22 删除）

## 目录结构

| 路径 | 说明 |
|------|------|
| `index.html` | 导航主页面（分类 + 链接卡片），站点根目录 |
| `about.html` | 关于本站（站点说明 / 隐私承诺 / 使用说明） |
| `404.html` | 自定义 404 |
| `cn/index.html` | **旧地址兼容页**，只做跳转回根目录，可直接删除 |
| `assets/css/nav.css` | 本站自定义样式（布局与结构） |
| `assets/css/dark-mode.css` | 本站**唯一**的配色（深色）。必须在 `nav.css` 之后加载 |
| `assets/images/logos/` | 站点图标资源 |
| `assets/` 其余 | WebStack / Xenon 模板原有资源 |

## 怎么加 / 改链接

在 `index.html` 里找对应分类的 `<div class="row">`，按这个格式复制一段：

```html
<div class="col-sm-3">
    <div class="xe-widget xe-conversations box2 label-info" onclick="window.open('https://example.com/', '_blank')"
         data-toggle="tooltip" data-placement="bottom" title="" data-original-title="https://example.com/">
        <div class="xe-comment-entry">
            <a class="xe-user-img">
                <svg class="brand-svg" viewBox="0 0 1024 1024" width="40" height="40" aria-hidden="true">
                    <use xlink:href="#ni-xxx" href="#ni-xxx"></use>
                </svg>
            </a>
            <div class="xe-comment">
                <a href="#" class="xe-user-name overflowClip_1"><strong>站点名</strong></a>
            </div>
        </div>
    </div>
</div>
```

- 图标放在页面末尾的「图标精灵」区块（`<symbol id="ni-xxx">`），用 `<use>` 引用；
  也可以直接用 `<img src="assets/images/logos/xxx.png" class="brand-img" width="40" height="40">`
  （注意：资源前缀是 `assets/`，**不再是 `../assets/`**）。
- 新增**分类**时，除了加 `<h4 class="text-gray">` 区块，还要在左侧栏 `#main-menu` 里加一个
  `<li><a href="#锚点" class="smooth">`。

> 页面末尾的图标精灵区块由脚本生成，改图标请连同 `<use>` 一起调整；不要只删 `<symbol>`。

## 本地预览

```bash
python -m http.server 8090
# 打开 http://127.0.0.1:8090/index.html
```

## 改配色时注意两个坑

1. **`dark-mode.css` 必须在 `nav.css` 之后加载。** 两个文件里都有 `.box2` 卡片底色这类
   同优先级规则，靠加载顺序覆盖；调换 `<link>` 顺序会让配色失效。
2. **底色只能挂在 `body` 上，绝不能写 `html, body { background-color: ... }`。**
   背景照片是 `body::before` + `z-index:-1` 实现的，前提是 `html` 没有自己的底色
   （这样 `body` 的底色会「传播到画布」而不自己绘制）。给 `html` 设了底色，
   背景图会被整片盖住。详见 `nav.css` 顶部与 `dark-mode.css` 第 2 节的说明。

## 说明

基于开源的 [WebStackPage](https://github.com/WebStackPage/WebStackPage.github.io)（Xenon 后台模板）改造，
原项目 MIT 许可，见 `LICENSE`。
