# 观潮台历 · Tide Macro Desk

单文件、零依赖的宏观事件速查台历：未来 14 天滚动窗口，把美国宏观数据、财报、IPO、拆股、分红排在一起看，原创暖色桌面风格，纯原生 HTML/CSS/JS。

## 功能

- **14 天滚动窗口**：自今日起算，日期导轨用圆点标注当日事件数，点击平滑滚动到对应分组；周末自动淡化。
- **分类筛选**：全部 / 宏观 / 财报 / IPO / 拆股 / 分红 胶囊按钮，数量实时统计，点击即筛。
- **KPI 概览**：窗口事件总数、三星高关注、待公布、距下次议息会议天数。
- **议息会议卡**：倒计时大字 + 决议时刻、发布会、点阵图、纪要等元信息，天数按当天自动计算。
- **事件分组列表**：时间、关注度星级、分类标签、事件名、最新值、市场预期、差值胶囊（绿偏强 / 红偏弱）；未公布显示「待公布」。
- **实时美东时钟**与事件名搜索框。
- **响应式**：桌面四列 KPI / 横向日期导轨，平板两列，手机单列堆叠，事件表横向滚动。

## 本地运行

浏览器直接打开 `index.html`，无需服务器与构建。

## 接入真实数据

`index.html` 内 `EVENTS` 为内置演示样本，替换该数组即可，字段约定：

| 字段 | 含义 | 示例 |
| --- | --- | --- |
| `offset` | 距今天天数（0 = 今天） | `1` |
| `t` | 发布时间（美东 ET） | `"08:30"` |
| `stars` | 关注度 1–3 | `3` |
| `cat` | `macro` / `earnings` / `ipo` / `splits` / `dividends` | `"macro"` |
| `name` | 事件名 | `"非农就业新增"` |
| `actual` | 最新值（未公布填 `"待公布"`） | `"12.0万"` |
| `est` | 市场预期 | `"16.2万"` |
| `delta` | 差值（带符号） | `"-4.2万"` |
| `trend` | `"up"` / `"down"` / `null`（决定箭头与红绿） | `"down"` |
| `published` | 是否已公布 | `true` |
| `hl` | 是否高亮行（可选） | `true` |

可选数据源：Financial Modeling Prep Economic Calendar、Benzinga Economics API、TradingView Economic Calendar Widget；FOMC 日期以美联储官方日历为准。浏览器直连第三方接口可能有 CORS 限制，正式使用建议经自有后端转发。

## 设计参考

事件组织方式参考了通用经济日历惯例：三星关注度、最新值 / 预期 / 差值、美东时间；配色与版式为本项目原创，未照搬任何现有产品界面。

## 部署（GitHub Pages）

- 仓库：`shuyaolu93/rilidoubao`（Public）
- 线上：https://shuyaolu93.github.io/rilidoubao/
- Pages：Settings → Pages → `Deploy from a branch`，`main` / `(root)`。

更新后重新发布：

```bash
git add -A && git commit -m "update"
git push origin main
```

Push 后 Pages 自动重建，约 1 分钟生效。示例数字不代表真实行情。
