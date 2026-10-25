<p align="center">
  <img src="docs/preview-light.jpg" width="49%" alt="浅色主题下的 2048 游戏界面">
  <img src="docs/preview-dark.jpg" width="49%" alt="深色主题下的 2048 游戏界面">
</p>

<h1 align="center">2048 · Material Design</h1>

<p align="center">
  一款 Material Design 3 风格的 2048 游戏：单文件、零依赖、离线可玩。
</p>

* * *

## 特性

-   **Material Design 3** 视觉风格，森林绿主色与奶油底色
-   **两套配色**：国风配色（毛绿 · 湘蓝 · 流黄）与经典配色（绿金双阶）
-   **明暗主题**：跟随系统 / 浅色 / 深色，首帧无闪烁
-   **背景**：默认纯色底，可选择本地图片作为背景（图片不写入 HTML）；自定义背景可调节毛玻璃模糊度，选中图片后可一键取消回到纯色底
-   **双语界面**：中文 / English，选择会被记住
-   **平板模式**：设置、新游戏、撤销与全屏按钮统一为 69px 圆形并对齐屏幕右端同一竖线，新游戏变为绿色镜像图标；手机分辨率下无需开关，操作按钮自动停靠屏幕底部居中横排（56px 圆形）
-   **键盘操作**：方向键或 `W` `A` `S` `D`
-   **触摸与鼠标拖拽**：跟手移动、挤压形变与边缘回弹动画
-   **撤销**：最多回退最近 20 步，方块原路返回、合并块分裂还原
-   **进度自动保存**：关闭或刷新页面后继续上一局，棋盘、分数与撤销记录都会保留
-   **终局破碎**：游戏结束点「再来一局」时，整盘方块炸成碎片后开新局
-   **弹层下沉**：打开设置或终局对话框时，棋盘、分数卡与按钮整体缩小下移，类移动应用的模态层次感
-   **达成 2048 后可继续**挑战更高分，最高分保存在本地
-   **响应式布局**，适配手机安全区，支持全屏模式
-   尊重系统的「减少动态效果」设置，提供无障碍标签与键盘可达性

整个游戏只有 **一个 HTML 文件**，字体已内嵌，不需要网络、构建工具或依赖安装，断网也能直接玩。

## 平板模式预览

<p align="center">
  <img src="docs/preview-tablet-light.jpg" width="32%" alt="浅色主题下的平板模式：四个圆形按钮沿屏幕右侧纵向排列">
  <img src="docs/preview-tablet-dark.jpg" width="32%" alt="深色主题下的平板模式：四个圆形按钮沿屏幕右侧纵向排列">
</p>

开启设置中的「平板模式」后，设置、新游戏、撤销与全屏按钮统一为 69px 圆形，并停靠在屏幕右侧同一竖线。手机分辨率下无需开启平板模式，操作按钮自动停靠屏幕底部居中横排（56px 圆形，全屏按钮在浏览器支持全屏时一并并入），平板模式开关在手机上不显示。

<p align="center">
  <img src="docs/preview-tablet-settings-light.jpg" width="32%" alt="浅色主题下的平板模式设置面板：靠右侧打开，背景界面下沉变暗">
  <img src="docs/preview-tablet-settings-dark.jpg" width="32%" alt="深色主题下的平板模式设置面板：靠右侧打开，背景界面下沉变暗">
</p>

打开设置时，背后棋盘与按钮整体下沉变暗，面板在平板模式下靠右侧打开、与按钮列留出间距；手机上保持居中。

## 手机版预览

<p align="center">
  <img src="docs/preview-mobile-light.jpg" width="32%" alt="浅色主题下的手机版：操作按钮停靠屏幕底部居中">
  <img src="docs/preview-mobile-dark.jpg" width="32%" alt="深色主题下的手机版：操作按钮停靠屏幕底部居中">
</p>

## 操作说明

| 操作 | 方式 |
| --- | --- |
| 移动方块 | 方向键 / `W` `A` `S` `D`，或在棋盘上滑动 / 拖拽 |
| 新游戏 | 「新游戏」按钮 |
| 撤销 | 「撤销」按钮（最多 20 步） |
| 设置 | 齿轮按钮：配色、主题、背景、语言、平板模式 |
| 全屏 | 全屏按钮（浏览器支持时显示；手机端并入底部按钮条） |
| 关闭弹窗 | `Esc` |

## 文件结构

```text
.
├── index.html          # 游戏本体（单文件，内嵌字体）
├── README.md
├── LICENSE             # MIT 许可证
├── .gitignore
├── .nojekyll           # 让 GitHub Pages 跳过 Jekyll 处理
└── docs/
    ├── preview-light.jpg
    ├── preview-dark.jpg
    ├── preview-mobile-light.jpg
    ├── preview-mobile-dark.jpg
    ├── preview-tablet-light.jpg
    ├── preview-tablet-dark.jpg
    ├── preview-tablet-settings-light.jpg
    └── preview-tablet-settings-dark.jpg
```

## 实现说明

-   纯 HTML / CSS / JavaScript，无框架、无外部请求。
-   游戏核心 `GameCore` 为纯函数实现，负责滑动、合并、计分与状态判断。
-   内嵌两套字体的界面子集：数字与英文用 Times New Roman（常规+粗体），中文用新宋体（NSimSun），覆盖界面全部文案字符与 ASCII 全集，woff2 合计约 0.15MB，字形与完整字体完全一致；子集外的字符（如背景图文件名中的生僻字）由系统字体回退显示。`index.html` 约 0.33MB，首次加载后由浏览器缓存。
-   动画基于 `requestAnimationFrame` 与 Pointer Events，包含拖拽跟手、方块挤压和边缘弹簧回弹。
-   仅使用 `localStorage` 保存最高分、当前进度与界面偏好（`md2048-best`、`md2048-save`、`md2048-theme`、`md2048-palette`、`md2048-lang`、`md2048-bg`、`md2048-bg-url`、`md2048-bg-name`、`md2048-bg-blur`、`md2048-tablet`），不会上传任何数据。
-   自定义背景图片只在运行时按 URL 引用（object URL，刷新后先尝试与 HTML 同目录的原文件名），不会写入 HTML；地址失效时自动回退为纯色背景。毛玻璃模糊度通过 CSS 变量 `--scene-custom-filter` 即时生效，默认 0（原图清晰），最大 40px。

## 浏览器支持

适用于支持 Pointer Events、CSS 自定义属性与 `backdrop-filter` 的现代浏览器（Chrome、Edge、Firefox、Safari）。旧浏览器或关闭动画时，交互会退回为普通滑动，不影响正常游玩。

## English

A single-file 2048 game with a Material Design 3 look. No dependencies, no build step, fully offline. It features two color palettes, light/dark themes, Chinese/English UI, keyboard and pointer-drag controls, up to 20 undo steps, automatic progress saving across reloads, and a locally stored best score.

Deploy with GitHub Pages by setting the branch to `main` and the folder to `/ (root)`.

The code and original assets are released under the [MIT License](LICENSE).

## 许可证

本项目采用 [MIT 许可证](LICENSE)，可自由使用、修改和分发，但需保留版权与许可声明。

> 代码与原创素材采用 MIT 许可证；如内嵌字体来自第三方，其权利仍归原权利人所有。