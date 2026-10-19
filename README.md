# JACKAL 事件日历（Event Calendar）小工具

一个单文件、零依赖的美股宏观事件日历前端：未来 14 天滚动窗口的宏观数据 / 财报 / IPO / 拆股 / 分红一览，界面复刻自参考稿（米色纸张质感、暗红强调、衬线大数字、三星重要性、实际 / 预期 / 差值列）。

## 功能

- **14 天滚动窗口**：自今日起 14 天，日期条上以红点标注当日事件数量，点击某天平滑滚动到对应分组。
- **五类统计卡**：Macro 日程 / Earnings 财报 / IPO / Splits 拆股 / Dividends 分红，数量由数据实时统计；点击卡片按类别筛选列表，再次点击取消。
- **FOMC 卡片**：下次议息会议日期、利率决议、新闻发布会、点阵图 / SEP、倒计时（按当天日期自动计算）。
- **按日分组的事件列表**：时间、三星重要性、事件名、期别、实际值、预期值、差值（▲ 绿 / ▼ 红）；未公布事件显示「未公布」。
- **响应式**：桌面 5 列统计卡 / 14 格日期条，平板 3 列，手机 2 列，事件表横向滚动。
- 纯原生 HTML + CSS + JS，无构建、无框架、无外部 JS 依赖（字体走自托管镜像）。

## 本地运行

直接用浏览器打开 `index.html` 即可，无需服务器。

## 接入真实数据

当前 `index.html` 内的 `EVENTS` 为内置示例数据（界面演示用）。接入真实数据时替换该数组，字段约定：

| 字段 | 含义 | 示例 |
| --- | --- | --- |
| `offset` | 距今天天数（0 = 今天） | `1` |
| `t` | 发布时间（美东 ET） | `"08:30"` |
| `stars` | 重要性 1–3 | `3` |
| `cat` | `macro` / `earnings` / `ipo` / `splits` / `dividends` | `"macro"` |
| `name` | 事件名 | `"非农就业人口"` |
| `period` | 数据期别 | `"Sep"` |
| `actual` | 实际值（未公布填 `"未公布"`） | `"120"` |
| `est` | 预期值 | `"162"` |
| `delta` | 差值（带符号） | `"-42"` |
| `trend` | `"up"` / `"down"` / `null`（决定箭头与红绿） | `"down"` |
| `published` | 是否已公布 | `true` |
| `hl` | 是否高亮行（可选） | `true` |

可选数据源（公开 / 商用）：Financial Modeling Prep Economic Calendar、Benzinga Economics API、TradingView Economic Calendar Widget、Investing.com 日历解析；FOMC 会议日期以美联储官方日历为准。注意浏览器直连第三方接口可能有 CORS 限制，正式使用建议经自有后端转发。

## GitHub 参考与借鉴

动手前在 GitHub 检索了同类实现，借鉴点如下：

- [andrevlima/economic-calendar-api](https://github.com/andrevlima/economic-calendar-api)：事件 JSON 模型（时间 / 币种 / 事件 / 重要性 / 实际 / 预期 / 前值）。
- [freenetwork/investing.com.economic-calendar](https://github.com/freenetwork/investing.com.economic-calendar)：日历解析字段组织方式。
- Forex Factory 日历惯例：三星重要性评级、Actual / Forecast / Prior 三列、Δ = 预期 − 前值、美东时间 ET、每日更新一次。
- 政府源直连思路（[DEV 文章](https://dev.to/timmkal01/i-built-an-economic-calendar-from-government-sources-instead-of-scraping-forexfactory-5ahk)）：就业数据取自 BLS、FOMC 日期取自美联储官方，不依赖爬虫。

本仓库为界面复刻与学习用途，示例数字不代表真实行情。

## 部署到 GitHub Pages（仓库名 rilidouboa，Public）

1. GitHub 网页新建空仓库：https://github.com/new ，名称填 `rilidouboa`，选 **Public**，**不要**勾选 Add a README / license；
2. 解压仓库包并推送（密码框粘贴 PAT，不是 GitHub 登录密码）：

```bash
tar xzf macro-event-calendar-repo.tar.gz
cd macro-event-calendar
git remote add origin https://github.com/<你的用户名>/rilidouboa.git
git push -u origin main
```

3. 仓库 **Settings → Pages** → Source 选 `Deploy from a branch`，Branch 选 `main` / `(root)`，Save；
4. 约 1 分钟后访问：`https://<你的用户名>.github.io/rilidouboa/`。

无需本地 git 历史时的全新初始化：

```bash
mkdir rilidouboa && cd rilidouboa && git init -b main
# 把 index.html / README.md / .gitignore 拷进来
git add -A && git commit -m "init: JACKAL 事件日历"
git remote add origin https://github.com/<你的用户名>/rilidouboa.git
git push -u origin main
```
