# 一个简单的导航 By Chenn

个人自用网址导航页，纯静态站点，直接跑在 **GitHub Pages** 上。

- 线上域名：<https://chenn.us.ci>
- 主页面：`cn/index.html`（根 `index.html` 会跳转到它）
- 深浅色主题：默认**深色**，右上角可切换，选择记在浏览器本地

## 目录结构

| 路径 | 说明 |
|------|------|
| `index.html` | 入口，跳转到 `cn/` |
| `cn/index.html` | 导航主页面（分类 + 链接卡片） |
| `cn/about.html` | 关于本站（站点说明 / 隐私承诺 / 使用说明） |
| `404.html` | 自定义 404 |
| `assets/css/nav.css` | 本站自定义样式 |
| `assets/css/dark-mode.css` | 深色主题 |
| `assets/images/logos/` | 站点图标资源 |
| `assets/` 其余 | WebStack / Xenon 模板原有资源 |

## 怎么加 / 改链接

在 `cn/index.html` 里找对应分类的 `<div class="row">`，按这个格式复制一段：

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
  也可以直接用 `<img src="../assets/images/logos/xxx.png" class="brand-img" width="40" height="40">`。
- 新增**分类**时，除了加 `<h4 class="text-gray">` 区块，还要在左侧栏 `#main-menu` 里加一个
  `<li><a href="#锚点" class="smooth">`。

> 页面末尾的图标精灵区块由脚本生成，改图标请连同 `<use>` 一起调整；不要只删 `<symbol>`。

## 本地预览

```bash
python -m http.server 8090
# 打开 http://127.0.0.1:8090/cn/index.html
```

## 说明

基于开源的 [WebStackPage](https://github.com/WebStackPage/WebStackPage.github.io)（Xenon 后台模板）改造，
原项目 MIT 许可，见 `LICENSE`。
