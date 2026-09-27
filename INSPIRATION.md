# ASCII / 终端美学资源索引

> 个人网站的参考库。按「看什么学什么」分四组，难度标注沿用原始调研。

## ① 标杆网站（气质与浓度）

| # | 站点 | 一句话 | 可借鉴 | 难度 |
|---|---|---|---|---|
| 1 | [ertdfgcvb.xyz](https://ertdfgcvb.xyz/) — Andreas Gysin | ASCII 动画教父，字符既是内容也是像素 | 实时 ASCII hero 的天花板 | 中 |
| 2 | [terminal.shop](https://www.terminal.shop/) | 用 SSH 卖咖啡，网页就是终端 | 整站终端化的完成度 + 幽默感标杆（`<title>` 恶趣味） | 中–难 |
| 3 | [charm.land](https://charm.land/) · [bubbletea](https://github.com/charmbracelet/bubbletea) ⭐43.8k | 让命令行变可爱 | 粉紫配色、圆角边框；顺手做 CLI 名片彩蛋 | 易–中 |
| 4 | [departuremono.com](https://departuremono.com/) · [仓库](https://github.com/rektdeckard/departure-mono) ⭐2.9k | 像素等宽字体，字体即主角 | ASCII 站的地基是选对 mono 字体，免费可商用 | 易 |
| 5 | [sacred.computer](https://www.sacred.computer/) (SRCL) · [仓库](https://github.com/internet-development/www-sacred) ⭐1.5k | React 终端美学组件库 | 等宽网格 / ASCII 边框 / 键盘导航，直接当 UI 层 | 易 |
| 6 | [ghostty.org](https://ghostty.org/) · [website 源码](https://github.com/ghostty-org/website) ⭐317 | 终端产品官网 | mono 正文的字号/行高分寸感，读源码 | 中 |
| 7 | [wiki.xxiivv.com](https://wiki.xxiivv.com/) — Devine Lu Linvega | plaintext 宇宙、自造工具链 | 个站「自成世界观」；效果可少，气质必须完整 | 概念向 |

## ② 字符动画引擎与技术

| # | 资源 | 一句话 | 可借鉴 | 难度 |
|---|---|---|---|---|
| 8 | [play.core](https://play.ertdfgcvb.xyz/) · [仓库](https://github.com/ertdfgcvb/play.core) ⭐532 | Gysin 开源的逐格字符渲染引擎 + 在线编辑器 | 写一个 `main(coord, context)` 就出效果，零依赖 | 中 |
| 9 | [three.js AsciiEffect](https://threejs.org/examples/webgl_effects_ascii.html) · [drei](https://github.com/pmndrs/drei) ⭐9.8k | 任意 3D 场景一键字符化 | 与 Blender 管线衔接；自写 shader 参考 "ASCII movAX13h" | 易(套)/难(写) |
| 10 | [Matrix rain](https://rezmason.github.io/matrix/) · [仓库](https://github.com/Rezmason/matrix) ⭐3.8k | 最考究的黑客帝国字符雨（WebGL） | 要用这个梗就用对的版本 | 中 |
| 11 | [asciicker.com](https://asciicker.com/) · [仓库](https://github.com/msokalski/asciicker) ⭐356 | 纯字符 3D 游戏引擎（C++→WASM） | 字符渲染的上限参照系 | 难 |
| 12 | [donut math 原文](https://www.a1k0n.net/2011/07/20/donut-math.html) | `donut.c` 作者亲自拆解 | 移植 ~200 行 JS 做 404/console 彩蛋 | 中 |
| 13 | [Codrops ASCII 专题](https://tympanus.net/codrops/tag/ascii/) | 教程 + demo 合集，附源码 | 想要具体效果先来搜 | 不一 |

## ③ 终端风作品集与 UI 框架（直接可抄）

| # | 资源 | 一句话 | 可借鉴 | 难度 |
|---|---|---|---|---|
| 14 | [LiveTerm](https://liveterm.vercel.app/) · [仓库](https://github.com/Cveinnt/LiveTerm) ⭐5.4k | 配置驱动的终端个站模板（Next.js） | 改一个 config 就是你的站 | 易 |
| 15 | [terminal.satnaing.dev](https://terminal.satnaing.dev/) · [仓库](https://github.com/satnaing/terminal-portfolio) ⭐792 | 终端交互细节最全 | Tab 补全 / ↑ 历史 / `themes` 命令的手感清单 | 易 |
| 16 | [term.fathi.me](https://term.fathi.me/) · [仓库](https://github.com/m4tt72/terminal) ⭐1.5k | 高颜值终端站（Svelte） | 三个模板横向对比取长 | 易 |
| 17 | [terminalcss.xyz](https://terminalcss.xyz/) · [仓库](https://github.com/Gioni06/terminal.css) ⭐1.4k | 3KB 纯 CSS 终端皮肤 | 一个 `<link>` 给博客换终端皮 | 易 |
| 18 | [xterm.js](https://xtermjs.org/) · [仓库](https://github.com/xtermjs/xterm.js) ⭐20.9k | VS Code 同款网页真终端 | 「真终端模式」彩蛋，比假终端高一档 | 中 |

## ④ 素材与工具

| # | 资源 | 用途 |
|---|---|---|
| 19 | [TAAG](https://patorjk.com/software/taag/) · [figlet.js](https://github.com/patorjk/figlet.js) ⭐3.0k | FIGlet 大字 banner（console 欢迎语 / README 头图） |
| 20 | [asciiflow.com](https://asciiflow.com/) · [仓库](https://github.com/lewish/asciiflow) ⭐5.8k | ASCII 架构框图 |
| 21 | [asciinema](https://asciinema.org/) · [player](https://github.com/asciinema/asciinema-player) ⭐2.9k | 终端录屏嵌入网页，展示 CLI 项目的正解 |
| 22 | [ascii-image-converter](https://github.com/TheZoraiz/ascii-image-converter) ⭐3.4k | 图片转彩色字符画（hero 素材 / 头像） |
| 23 | [asciiart.eu](https://www.asciiart.eu/) · [asciimation.co.nz](https://www.asciimation.co.nz/) | 老派字符画档案馆 · 1997 年至今的星战 ASCII 动画 |

## 本仓库对这些资源的消化

- `playground.html` — play.core 思路的自研逐格渲染 playground（①-1 / ② 8·12）
- `terminal.html` — 终端风个人站原型：命令导航 + 主题 + 彩蛋（② 10·12 / ③ 14-16 手感清单 / ①-2·3 气质）
