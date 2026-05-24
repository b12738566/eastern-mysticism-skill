# Eastern Mysticism — 东方神秘学命理分析

基于子平八字、五行学说的 Claude Code 技能。交互式逐项收集用户信息，自动完成排盘、五行分析、大运流年推算，最后生成可视化 HTML 报告。

## 快速开始

在 Claude Code 对话中输入：

```
使用 Eastern mysticism帮我算一下
```

skill 启动后会像算命师傅一样逐项询问：出生日期 → 时间 → 性别 → 出生地 → 想算什么，然后完整输出命理报告。

---

## 功能

**命理分析**
- 八字排盘 — 四柱、藏干、十神、五行、纳音
- 五行分析 — 旺衰判断、喜用神/忌神
- 十神解读 — 10 种十神的配置与格局判定
- 大运推算 — 顺逆排法、起运年龄、十年一运
- 流年详批 — 刑冲合害关系 + 12 月热度图
- 运势起伏表 — 人生各阶段星级评分 + 可视化曲线

**专项分析**
- 姻缘 — 配偶宫、桃花位、适婚年龄
- 事业 — 官杀印星、适合行业、关键期
- 财运 — 正偏财格局、各阶段走势
- 健康 — 五行偏枯对应脏腑、养生建议

**增值服务**
- 起名改名、合婚配对、择日吉时

**HTML 报告**（分析完成后自动生成）
- 八字四柱卡片（日柱红色高亮）
- 五行 CSS 柱状图（五色渐变）
- 运势起伏图（五级渐变色，标注当前运和巅峰）
- 月度热力图（12 个月五色圆点）
- 十神网格、专项分析四宫格
- 顶部粘性导航、响应式、打印友好
- 中式暗金配色，Google Fonts

## 安装

```bash
git clone https://github.com/b12738566/eastern-mysticism-skill.git
cd your-project
mkdir -p .agents/skills
cp -r path/to/eastern-mysticism-skill/eastern-mysticism .agents/skills/
```

## 使用

| 启动方式 | 示例 |
|----------|------|
| 主命令 | `使用 Eastern mysticism帮我算一下` |
| 简化命令 | `使用 Eastern mysticism` |
| 自然触发 | "算命"、"看八字"、"算姻缘"、"看财运"、"起名字"、"选吉日" |

### 交互示例

```
用户：使用 Eastern mysticism帮我算一下
Claude：您好！请问您的出生日期是公历还是农历？哪一年哪一月哪一日？
用户：农历 2001年x月初一
Claude：好的。请问具体的出生时间是几点几分？
用户：凌晨1点
Claude：丑时。请问您的性别？
用户：男
Claude：请问出生地点？（用于真太阳时校正）
用户：x省x市
Claude：信息齐全。您想了解哪些方面？
用户：都要
Claude：[排盘 → 五行 → 十神 → 大运 → 起伏表 → 流年 → 专项 → 建议]
        报告已保存至 fortune-reports/命理报告_2026-05-24.html
```

## 目录

```
eastern-mysticism/
  SKILL.md                         # 技能定义 + 速查表
  README.md
  references/
    flows/
      consultation-flow.md         # 交互式咨询流程
    guides/
      bazi-paipan.md               # 八字排盘
      five-elements.md             # 五行生克
      shishen.md                   # 十神详解
      nayin.md                     # 纳音速查
      html-report-template.md      # HTML 报告模板
```

## 技术

纯 CSS/HTML 图表，零 JS 依赖。响应式布局 + 打印支持。

## 免责声明

仅供娱乐参考，不可作为人生决策唯一依据。命运掌握在自己手中。


