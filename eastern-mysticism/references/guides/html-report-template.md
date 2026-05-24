# HTML 可视化报告模板

此模板用于生成命理分析的 HTML 可视化报告。纯 CSS/HTML 实现，无需外部依赖。

## 使用说明

Claude 根据排盘结果，将实际数据填入模板中的 `{{占位符}}`，生成完整 HTML 文件。

## 完整模板

```html
<!DOCTYPE html>
<html lang="zh-CN">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>命理分析报告 - {{姓名代号}}</title>
<style>
  :root {
    --bg: #1a1a2e;
    --card: #16213e;
    --accent: #e2b04a;
    --gold: #c9a84c;
    --text: #e0d5c1;
    --text-secondary: #a09080;
    --fire: #e74c3c;
    --wood: #2ecc71;
    --water: #3498db;
    --metal: #f39c12;
    --earth: #d4a853;
    --border: #2a2a4a;
    --good: #27ae60;
    --warn: #f39c12;
    --bad: #e74c3c;
  }

  * { margin: 0; padding: 0; box-sizing: border-box; }

  body {
    font-family: "PingFang SC", "Microsoft YaHei", "Noto Serif SC", serif;
    background: var(--bg);
    color: var(--text);
    line-height: 1.7;
    padding: 20px;
    max-width: 960px;
    margin: 0 auto;
  }

  /* ===== 封面 ===== */
  .cover {
    text-align: center;
    padding: 60px 20px;
    border: 2px solid var(--gold);
    border-radius: 12px;
    margin-bottom: 40px;
    background: linear-gradient(180deg, #1a1a2e 0%, #1e2a3a 100%);
  }
  .cover h1 {
    font-size: 2.4em;
    color: var(--gold);
    letter-spacing: 4px;
    margin-bottom: 10px;
  }
  .cover .subtitle {
    font-size: 1.1em;
    color: var(--text-secondary);
    letter-spacing: 2px;
  }
  .cover .divider {
    width: 60px; height: 2px; background: var(--gold);
    margin: 20px auto;
  }
  .cover .info-grid {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 8px 40px;
    max-width: 500px;
    margin: 30px auto 0;
    text-align: left;
    font-size: 0.95em;
  }
  .cover .info-grid .label { color: var(--text-secondary); }
  .cover .info-grid .value { color: var(--text); }

  /* ===== 章节标题 ===== */
  .section-title {
    font-size: 1.5em;
    color: var(--gold);
    border-left: 4px solid var(--gold);
    padding-left: 14px;
    margin: 40px 0 20px;
    letter-spacing: 2px;
  }

  /* ===== 八字排盘卡片 ===== */
  .bazi-cards {
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    gap: 12px;
    margin: 20px 0;
  }
  @media (max-width: 640px) {
    .bazi-cards { grid-template-columns: repeat(2, 1fr); }
  }
  .bazi-card {
    background: var(--card);
    border-radius: 10px;
    padding: 16px 12px;
    text-align: center;
    border: 1px solid var(--border);
    position: relative;
  }
  .bazi-card .pillar-name {
    position: absolute; top: -10px; left: 50%; transform: translateX(-50%);
    background: var(--gold); color: #1a1a2e;
    font-size: 0.75em; padding: 2px 10px; border-radius: 10px;
    letter-spacing: 1px;
  }
  .bazi-card .tg {
    font-size: 1.8em; font-weight: bold; margin: 8px 0 4px;
  }
  .bazi-card .dz {
    font-size: 1.4em; color: var(--gold); margin-bottom: 6px;
  }
  .bazi-card .detail {
    font-size: 0.75em; color: var(--text-secondary);
    line-height: 1.5;
  }

  /* ===== 五行柱状图 ===== */
  .wuxing-chart {
    display: flex; align-items: flex-end; gap: 16px;
    height: 200px; padding: 20px 0; margin: 20px 0;
    border-bottom: 2px solid var(--border);
  }
  .wuxing-bar-wrap {
    flex: 1; display: flex; flex-direction: column; align-items: center;
    height: 100%; justify-content: flex-end;
  }
  .wuxing-bar {
    width: 48px; border-radius: 6px 6px 0 0;
    transition: height 0.6s ease; position: relative;
    min-height: 8px;
  }
  .wuxing-bar .count {
    position: absolute; top: -22px; left: 50%; transform: translateX(-50%);
    font-weight: bold; font-size: 0.9em;
  }
  .wuxing-label {
    margin-top: 8px; font-size: 0.85em; font-weight: bold;
  }
  .wuxing-status {
    font-size: 0.7em; color: var(--text-secondary); margin-top: 2px;
  }

  /* ===== 喜忌神指示器 ===== */
  .xiji-row {
    display: flex; gap: 16px; margin: 16px 0;
  }
  .xiji-tag {
    padding: 6px 16px; border-radius: 20px; font-size: 0.9em;
    font-weight: bold; letter-spacing: 1px;
  }
  .xiji-tag.good { background: #27ae6044; color: #2ecc71; border: 1px solid #27ae60; }
  .xiji-tag.bad  { background: #e74c3c22; color: #e74c3c; border: 1px solid #e74c3c; }

  /* ===== 大运起伏图 ===== */
  .fortunes-chart { margin: 20px 0; }
  .fortunes-row {
    display: flex; align-items: center; gap: 12px;
    padding: 8px 0; border-bottom: 1px solid var(--border);
  }
  .fortunes-row .age {
    width: 60px; font-size: 0.8em; color: var(--text-secondary);
    text-align: right; flex-shrink: 0;
  }
  .fortunes-row .dayun {
    width: 44px; font-size: 0.9em; font-weight: bold;
    text-align: center; flex-shrink: 0;
  }
  .fortunes-row .bar-wrap {
    flex: 1; height: 22px; background: #ffffff08;
    border-radius: 4px; overflow: hidden; position: relative;
  }
  .fortunes-row .bar-fill {
    height: 100%; border-radius: 4px;
    transition: width 0.6s ease;
  }
  .fortunes-row .bar-fill.top    { background: linear-gradient(90deg, #27ae60, #2ecc71); }
  .fortunes-row .bar-fill.good   { background: linear-gradient(90deg, #2ecc71aa, #27ae60); }
  .fortunes-row .bar-fill.mid    { background: linear-gradient(90deg, #f39c12, #e67e22); }
  .fortunes-row .bar-fill.low    { background: linear-gradient(90deg, #e74c3caa, #c0392b); }
  .fortunes-row .bar-fill.bad    { background: linear-gradient(90deg, #c0392b, #e74c3c); }
  .fortunes-row .stars {
    width: 80px; font-size: 0.75em; flex-shrink: 0;
    letter-spacing: 1px;
  }
  .fortunes-row .tag {
    font-size: 0.7em; padding: 1px 8px; border-radius: 8px;
    flex-shrink: 0;
  }
  .fortunes-row .tag.current {
    background: #3498db33; color: #3498db; border: 1px solid #3498db;
  }
  .fortunes-row .tag.peak {
    background: #f39c1233; color: #f39c12; border: 1px solid #f39c12;
  }

  /* ===== 月度热力图 ===== */
  .monthly-grid {
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    gap: 8px;
    margin: 16px 0;
  }
  @media (max-width: 640px) {
    .monthly-grid { grid-template-columns: repeat(3, 1fr); }
  }
  .month-cell {
    background: var(--card); border-radius: 8px;
    padding: 10px; text-align: center; border: 1px solid var(--border);
  }
  .month-cell .mon-name { font-size: 0.8em; color: var(--text-secondary); }
  .month-cell .mon-ganzhi { font-size: 1em; font-weight: bold; margin: 4px 0; }
  .month-cell .mon-bar {
    height: 6px; border-radius: 3px; margin: 6px 0 4px;
  }
  .month-cell .mon-tip {
    font-size: 0.68em; color: var(--text-secondary);
    overflow: hidden; text-overflow: ellipsis; white-space: nowrap;
  }
  .heat-5 { background: linear-gradient(90deg, #27ae60, #2ecc71); }
  .heat-4 { background: linear-gradient(90deg, #2ecc7188, #27ae6088); }
  .heat-3 { background: linear-gradient(90deg, #f39c12, #e67e22); }
  .heat-2 { background: linear-gradient(90deg, #e74c3c88, #c0392b88); }
  .heat-1 { background: linear-gradient(90deg, #c0392b, #e74c3c); }

  /* ===== 专项分析卡片 ===== */
  .special-grid {
    display: grid;
    grid-template-columns: repeat(2, 1fr);
    gap: 14px; margin: 16px 0;
  }
  @media (max-width: 640px) {
    .special-grid { grid-template-columns: 1fr; }
  }
  .special-card {
    background: var(--card); border: 1px solid var(--border);
    border-radius: 10px; padding: 18px;
  }
  .special-card h3 {
    font-size: 1em; color: var(--gold);
    margin-bottom: 10px; padding-bottom: 8px;
    border-bottom: 1px solid var(--border);
  }
  .special-card p, .special-card li {
    font-size: 0.85em; color: var(--text-secondary);
    margin: 4px 0; line-height: 1.6;
  }
  .special-card ul { padding-left: 16px; }

  /* ===== 建议区 ===== */
  .suggest-box {
    background: linear-gradient(135deg, #2c2c1e 0%, #1a1a2e 100%);
    border: 1px solid var(--gold); border-radius: 10px;
    padding: 20px 24px; margin: 16px 0;
  }
  .suggest-box h3 { color: var(--gold); margin-bottom: 12px; }
  .suggest-box li { font-size: 0.9em; margin: 6px 0; color: var(--text); }

  /* ===== 页脚 ===== */
  .footer {
    text-align: center; padding: 30px 0 20px;
    color: var(--text-secondary); font-size: 0.8em;
    border-top: 1px solid var(--border); margin-top: 40px;
  }

  @media print {
    body { background: white; color: #333; }
    .footer { display: none; }
  }
</style>
</head>
<body>

<!-- ===== 封面 ===== -->
<div class="cover">
  <h1>命理分析报告</h1>
  <div class="subtitle">八字排盘 · 五行分析 · 运势推算</div>
  <div class="divider"></div>
  <div class="info-grid">
    <div><span class="label">姓名代号</span></div><div><span class="value">{{姓名代号}}</span></div>
    <div><span class="label">公历生日</span></div><div><span class="value">{{公历生日}}</span></div>
    <div><span class="label">农历生日</span></div><div><span class="value">{{农历生日}}</span></div>
    <div><span class="label">出生时间</span></div><div><span class="value">{{出生时间}}（{{时辰}}时）</span></div>
    <div><span class="label">出生地点</span></div><div><span class="value">{{出生地点}}</span></div>
    <div><span class="label">性别</span></div><div><span class="value">{{性别}}</span></div>
  </div>
</div>

<!-- ===== 一、八字排盘 ===== -->
<h2 class="section-title">一、八字排盘</h2>
<div class="bazi-cards">
  <div class="bazi-card">
    <div class="pillar-name">年柱</div>
    <div class="tg">{{年干}}</div>
    <div class="dz">{{年支}}</div>
    <div class="detail">藏干：{{年藏干}}<br>十神：{{年十神}}<br>纳音：{{年纳音}}</div>
  </div>
  <div class="bazi-card">
    <div class="pillar-name">月柱</div>
    <div class="tg">{{月干}}</div>
    <div class="dz">{{月支}}</div>
    <div class="detail">藏干：{{月藏干}}<br>十神：{{月十神}}<br>纳音：{{月纳音}}</div>
  </div>
  <div class="bazi-card" style="border-color: var(--gold);">
    <div class="pillar-name" style="background:#e74c3c;">日柱·我</div>
    <div class="tg" style="color:#e74c3c;">{{日干}}</div>
    <div class="dz" style="color:#e74c3c;">{{日支}}</div>
    <div class="detail">藏干：{{日藏干}}<br>日主：{{日主五行}}<br>纳音：{{日纳音}}</div>
  </div>
  <div class="bazi-card">
    <div class="pillar-name">时柱</div>
    <div class="tg">{{时干}}</div>
    <div class="dz">{{时支}}</div>
    <div class="detail">藏干：{{时藏干}}<br>十神：{{时十神}}<br>纳音：{{时纳音}}</div>
  </div>
</div>

<!-- ===== 二、五行分析 ===== -->
<h2 class="section-title">二、五行分析</h2>

<div class="wuxing-chart">
  <div class="wuxing-bar-wrap">
    <div class="wuxing-bar" style="height:{{金高度}}%; background:var(--metal);">
      <div class="count">{{金数量}}</div>
    </div>
    <div class="wuxing-label" style="color:var(--metal);">金</div>
    <div class="wuxing-status">{{金状态}}</div>
  </div>
  <div class="wuxing-bar-wrap">
    <div class="wuxing-bar" style="height:{{木高度}}%; background:var(--wood);">
      <div class="count">{{木数量}}</div>
    </div>
    <div class="wuxing-label" style="color:var(--wood);">木</div>
    <div class="wuxing-status">{{木状态}}</div>
  </div>
  <div class="wuxing-bar-wrap">
    <div class="wuxing-bar" style="height:{{水高度}}%; background:var(--water);">
      <div class="count">{{水数量}}</div>
    </div>
    <div class="wuxing-label" style="color:var(--water);">水</div>
    <div class="wuxing-status">{{水状态}}</div>
  </div>
  <div class="wuxing-bar-wrap">
    <div class="wuxing-bar" style="height:{{火高度}}%; background:var(--fire);">
      <div class="count">{{火数量}}</div>
    </div>
    <div class="wuxing-label" style="color:var(--fire);">火</div>
    <div class="wuxing-status">{{火状态}}</div>
  </div>
  <div class="wuxing-bar-wrap">
    <div class="wuxing-bar" style="height:{{土高度}}%; background:var(--earth);">
      <div class="count">{{土数量}}</div>
    </div>
    <div class="wuxing-label" style="color:var(--earth);">土</div>
    <div class="wuxing-status">{{土状态}}</div>
  </div>
</div>

<p style="color:var(--text-secondary);font-size:0.9em;">
  <strong>日主：</strong>{{日主五行}}（{{日主阴阳}}性）｜
  <strong>得令：</strong>{{得令}}｜
  <strong>得地：</strong>{{得地}}｜
  <strong>得势：</strong>{{得势}}｜
  <strong>综合：</strong><span style="color:{{身旺弱颜色}};">{{身旺弱}}</span>
</p>

<h3>喜用神 & 忌神</h3>
<div class="xiji-row">
  <span class="xiji-tag good">🟢 喜用神：{{喜用神}}</span>
  <span class="xiji-tag bad">🔴 忌神：{{忌神}}</span>
</div>
<p style="font-size:0.8em;color:var(--text-secondary);">{{喜忌说明}}</p>

<!-- ===== 三、十神格局 ===== -->
<h2 class="section-title">三、十神格局</h2>

{{十神表格行}}

<p style="color:var(--text-secondary);font-size:0.9em;">
  <strong>格局判定：</strong>{{格局名称}} —— {{格局说明}}
</p>

<!-- ===== 四、大运走势 ===== -->
<h2 class="section-title">四、大运走势</h2>
<p style="color:var(--text-secondary);">
  起运年龄：<strong>{{起运年龄}}岁</strong>（{{顺逆排}}）｜ 当前年龄：<strong>{{当前年龄}}岁</strong>
</p>

<!-- ===== 五、人生运势起伏表 ===== -->
<h2 class="section-title">五、人生运势起伏表</h2>

<div class="fortunes-chart">
  {{运势起伏行}}
</div>

<p style="color:var(--text-secondary);font-size:0.85em;margin-top:16px;">
  {{人生运势概述}}
</p>

<!-- ===== 六、当前流年详批 ===== -->
<h2 class="section-title">六、当前流年详批（2026年）</h2>

<p style="margin-bottom:8px;">
  <strong>所处大运：</strong>{{当前大运干支}}（{{当前大运年龄段}}）|
  <strong>流年：</strong><span style="color:var(--gold);">丙午</span>
</p>

<h3>流年与命局关系</h3>
<ul style="color:var(--text-secondary);font-size:0.85em;">
  {{流年关系列表}}
</ul>
<p style="font-weight:bold;color:var(--gold);">{{流年总评}}</p>

<h3>月度运势热力图</h3>
<div class="monthly-grid">
  {{月度热力格子}}
</div>

<!-- ===== 七、专项分析 ===== -->
<h2 class="section-title">七、专项分析</h2>
<div class="special-grid">
  {{专项分析卡片}}
</div>

<!-- ===== 八、综合建议 ===== -->
<h2 class="section-title">八、综合建议</h2>
<div class="suggest-box">
  <h3>🌟 转运方法</h3>
  <ul>
    {{转运建议列表}}
  </ul>
</div>

<div class="suggest-box" style="margin-top:12px;">
  <h3>⚠️ 关键提醒</h3>
  <ul>
    {{关键提醒列表}}
  </ul>
</div>

<div class="footer">
  <p>以上命理分析仅供娱乐参考，不可作为人生决策唯一依据。</p>
  <p>命由天定，运由己造。祝您一切顺利！</p>
  <p style="margin-top:8px;">生成时间：{{生成时间}}</p>
</div>

</body>
</html>
```

## 数据换算规则

### 五行柱状图高度计算

以最大五行数量为 100% 基准：
- 高度 = (该五行数量 ÷ 最大数量) × 100
- 最低不低于 8%

### 月度热度等级

| 条件 | 热度等级 | CSS类 |
|------|----------|-------|
| 月干支全为喜用神 | 5 | heat-5 |
| 月干支大部分喜用 | 4 | heat-4 |
| 月干支喜忌各半 | 3 | heat-3 |
| 月干支多为忌神 | 2 | heat-2 |
| 月干支全为忌神 | 1 | heat-1 |

### 运势柱状图宽度

| 评分 | 宽度 | CSS类 |
|------|------|-------|
| ★★★★★ | 100% | top |
| ★★★★☆ | 75% | good |
| ★★★☆☆ | 50% | mid |
| ★★☆☆☆ | 30% | low |
| ★☆☆☆☆ | 15% | bad |

## 文件命名规则

```
fortune-reports/命理报告_YYYY-MM-DD_HHmmss.html
```

例如：`fortune-reports/命理报告_2026-05-24_143052.html`
