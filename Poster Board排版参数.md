# Poster Board 排版参数（对应“我们的项目.png”）

## 结论与定位

这一页是 Ripple Demo 的 **Discover / Poster Board** 视图。它由 HTML 壳、JavaScript 渲染逻辑、三层 CSS（组件库基础样式、项目扩展样式、iOS 预览覆盖样式）以及四张活动海报资源共同组成。

页面运行入口为 `index.html`；页面 DOM、活动数据与交互在 `app.js`；实际 Poster Board 的最终网格规则以 `ios-shell.css` 为准（它在 `index.html` 中最后加载，因此会覆盖前面的同名规则）。

## 页面尺寸与主要几何参数

| 区域 | 参数 | 值 |
| --- | --- | --- |
| 参考设备 | `referenceFrame` | `390 × 844 px` |
| 设备外壳 | `.device` | `390 × 844 px`，圆角 `48px` |
| 状态栏 | `.phone-statusbar` | 高 `47px`，左右 `24px` |
| Home indicator 区 | `.phone-home-area` | 高 `34px` |
| App 内容可用宽度 | `390 - 2 × 16` | `358px` |
| 页面横向边距 | `pageGutter` / 相关 padding | `16px` |
| 顶部视图切换 | `.segmented` | 高 `44px`，外边距 `16px 16px 0` |
| 分类筛选区 | `.filter-row` | 上下 `10px`、左右 `16px`，5 列网格，列间距 `4px` |
| Poster Board | `.poster-board` | 两等列 `repeat(2, minmax(0, 1fr))`，列间距 `12px`，无内边距 |
| 单列卡片垂直间距 | `.poster-column` | `12px` |
| 单张卡片 | `.poster-card` | 边框 `1px`，圆角 `18px`，内边距 `8px`，阴影 `0 3px 10px rgba(50,38,15,.05)` |
| 海报图 | `.poster-card > img` | 宽 `100%`、`1:1`、圆角 `12px`、`object-fit: cover` |
| 标题 | `.poster-card h3` | `13px / 17px`；基本样式中 margin `9px 0 4px` |
| 元数据 | `.poster-card p` | `9px / 14px`；基本样式中 `margin: 0` |
| 主办人行 | `.poster-card footer` | `8px / 12px`；基本样式中上外边距 `7px`、gap `5px` |
| 主办人头像 | `.poster-card footer img` | `20 × 20px`，圆形，`1px #d9ccb5` 描边 |
| 底部导航 | 最终 `.bottom-nav` | 高 `50px`；触控最小 `44 × 44px` |
| 加载更多按钮 | `.load-more` | 高 `44px`，虚线 `1px` 边框，圆角 `14px`，上下外边距 `12px 0` |

在 390px 的设计画板上，两列均分公式为：`(390 - 16 × 2 - 12) / 2 = 173px`。卡片外层宽约 173px，减去左右内边距后海报图宽约 157px。

## 最终生效的 Poster Board CSS

`ios-shell.css` 中以下规则是最终排版依据，并取消了较早版本交错卡片的 `margin-top`：

```css
.ripple-app .poster-board {
  display: grid;
  grid-template-columns: repeat(2, minmax(0, 1fr));
  align-items: start;
  column-gap: 12px;
  padding: 0;
}
.ripple-app .poster-column {
  min-width: 0;
  display: flex;
  flex-direction: column;
  align-items: stretch;
  gap: 12px;
}
.ripple-app .poster-card,
.ripple-app .poster-card:nth-child(2n) {
  width: 100%;
  min-width: 0;
  margin-top: 0;
}
.ripple-app .poster-card > img {
  width: 100%;
  height: auto;
  aspect-ratio: 1 / 1;
}
.ripple-app .poster-card h3 { font-size: 13px; line-height: 17px; overflow-wrap: anywhere; }
.ripple-app .poster-card p { font-size: 9px; line-height: 14px; overflow-wrap: anywhere; }
.ripple-app .poster-card footer { font-size: 8px; line-height: 12px; }
```

补充规则：`.view-panel` 允许纵向滚动；所有 `.segmented`、筛选按钮和卡片按钮的触控最小高度为 `44px`。窄屏（最大 `360px`）仅缩小状态栏的左右 padding 与 Dynamic Island 宽度，Poster Board 仍是双列。

## JavaScript：页面结构与数据

`renderDiscover()` 组合本页结构：顶部 tab、筛选条、可滚动内容区和底部导航。`renderPosterBoard()` 会把活动按索引奇偶拆分至左右列：0、2、4… 在左列；1、3、5… 在右列。因此并不是 CSS masonry 自动分栏，而是 JavaScript 明确分列。

```js
const source = [activities.coffee, activities.hike, activities.music, activities.pickle];
const renderedCards = [...list, ...extra].map(card);
const leftColumn = renderedCards.filter((_, index) => index % 2 === 0).join('');
const rightColumn = renderedCards.filter((_, index) => index % 2 === 1).join('');
return `<div class="poster-board"><div class="poster-column">${leftColumn}</div><div class="poster-column">${rightColumn}</div></div>`;
```

每张卡片由 `card(activity)` 生成，包含：方形活动图、取消/已加入/已满状态、标题、日期时间、地点价格、匿名主办人头像与 `joined/capacity`。

### 当前活动参数

| ID | 标题 | 海报文件 | 时间 | 地点 / 价格 | 人数 | 状态 |
| --- | --- | --- | --- | --- | --- | --- |
| `coffee` | Coffee & Good Conversations | `coffee-social.png` | Sat, Apr 26 · 10:00 AM | Melbourne CBD · $5 – $10 | 8/12 | 正常 |
| `hike` | Sunset Hike & Chill | `sunset-hike.png` | Sat, Apr 26 · 6:00 PM | Fitzroy · Free | 6/15 | 正常 |
| `music` | Indie Music Listening Night | `indie-music.png` | Fri, Apr 25 · 7:30 PM | Chinatown · $10 – $15 | 10/20 | `cancelled: true` |
| `pickle` | Pickleball for All Levels | `pickleball.png` | Sun, Apr 27 · 9:00 AM | Melbourne CBD · Free | 12/12 | 已满（Full） |

### 交互状态参数

- 初始状态：`discoverView: 'poster'`、`filter: 'For You'`、`feedState: 'initial'`、`feedExtra: false`。
- 初始进入 Poster Board 后，`feedState` 会先变为 `loading`，650ms 后变为 `loaded`。
- `Food` 仅显示 coffee；`Outdoors` 显示 hike 和 pickle；`For You` 与 `Trending` 显示四张活动；`Explore` 会模拟加载后错误状态。
- `Load more activities` 设置 `feedExtra: true`，追加 coffee 与 music，并显示 “You’re all caught up.”。
- 点击活动卡：`data-action="detail"`，打开对应详情页。

## 视觉 Tokens

| Token | 值 | 用途 |
| --- | --- | --- |
| `--red` | `#F04A2F` | 选中 tab / 筛选项、主视觉色 |
| `--red-dark` | `#CF341E` | 深红按压色、文字强调 |
| `--red-soft` | `#FEE9E3` | 柔和红色背景 |
| `--cream` | `#FFFCF3` | 页面背景 |
| `--surface` | `#FFFEFA` | 卡片表面 |
| `--paper` | `#F7F0DF` | 次级暖白底 |
| `--ink` | `#11191E` | 主文字 |
| `--muted` | `#6F706F` | 次级文字 |
| `--line` | `#DED9CB` | 分隔线 / 描边 |
| 字体 | Manrope | 通过 Google Fonts 引入 |
| 基础圆角 | `--radius: 18px` | 卡片圆角 |

## 本文件夹内的完整源文件

本说明旁边保留了该页面涉及的完整原始文件，未做删节：

- `index.html`：页面入口、样式加载顺序与 iPhone 外壳。
- `app.js`：Poster Board 的完整渲染、活动数据和点击交互。
- `styles.css`：项目层的基础页面、卡片、筛选与加载更多样式。
- `ios-shell.css`：iPhone 390×844 外壳以及最终的双列 Poster Board 覆盖规则。
- `Ripple_Component_Library/styles.css`：组件库 Token 与通用组件基线。
- `Ripple_Component_Library/tokens.json`：结构化设计 Token。
- `assets/`：本页面的四张海报 PNG 原图。

## 样式覆盖顺序（重要）

`index.html` 的加载顺序为：

1. `Ripple_Component_Library/styles.css`
2. `styles.css`
3. `ios-shell.css`

所以同等优先级下，最后的 `ios-shell.css` 覆盖前两者。例如基础层原本使用 `.poster-card:nth-child(2n){margin-top:16px}` 做错位瀑布流；项目层把它改为 `0`，最终 iOS 层又以 `.poster-card:nth-child(2n) { margin-top: 0; }` 明确固定为两列顶端对齐。
