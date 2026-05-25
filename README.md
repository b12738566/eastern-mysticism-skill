# Eastern Mysticism — Chinese Fortune-Telling Skill

A Claude Code skill based on traditional Chinese BaZi (Eight Characters / Four Pillars of Destiny) and Five Elements (Wu Xing) metaphysics. Interactively collects birth details, performs a full destiny analysis, and generates a visual HTML report.

## Quick Start

In Claude Code, type:

```
使用 Eastern mysticism帮我算一下
```

The skill will ask you step-by-step: birth date → time → gender → birthplace → what to analyze, then output a full fortune-telling report with an HTML file.

## Features

**Core Analysis**
- BaZi chart — Four Pillars (year/month/day/hour), Hidden Stems, Ten Gods, Five Elements, NaYin
- Five Elements — strength/weakness judgment, favorable/unfavorable elements
- Ten Gods — full interpretation of all 10 gods and pattern identification
- DaYun (10-year luck cycles) — forward/reverse direction, starting age, decade-by-decade
- Annual forecast — relationships between the current year and natal chart + 12-month heatmap
- Life fortune curve — star ratings with visual bar chart for every life stage

**Specialty Readings**
- Love & Marriage — spouse palace, peach blossom, ideal marriage age
- Career & Education — official/kill + seal configurations, suitable industries
- Wealth — direct/indirect wealth patterns, investment advice
- Health — organ correspondences, seasonal cautions, wellness tips

**Extra Services**
- Chinese name generation, couple compatibility, auspicious date selection

**HTML Report** (auto-generated after every reading)
- BaZi pillar cards (day pillar highlighted in red)
- Five Elements CSS bar chart (gradient colors)
- Life fortune curve (5-level gradient bars, current cycle + peak marked)
- Monthly heatmap (12 months, colored indicators)
- Ten Gods grid, specialty reading cards
- Sticky navigation, responsive, print-friendly
- Traditional Chinese dark-gold aesthetic, Google Fonts

## Installation

```bash
git clone https://github.com/b12738566/eastern-mysticism-skill.git

```

## Usage

| Method | Example |
|--------|---------|
| Main command | `使用 Eastern mysticism帮我算一下` |
| Short command | `使用 Eastern mysticism` |
| Natural trigger | "算命" (fortune), "看八字" (check BaZi), "算姻缘" (love), "看财运" (wealth), "起名字" (name), "选吉日" (date) |

> **Note:** All triggers are in Chinese. The skill operates entirely in Chinese (Simplified).

### Example Interaction

```
User: 使用 Eastern mysticism帮我算一下
Claude: Hello! Let me analyze your BaZi destiny chart.
        Is your birth date solar (公历) or lunar (农历)? Year, month, day?

User: 农历 2001年X月初一 (Lunar, 1st day of Xth month, 2001)
Claude: Got it. What time were you born?

User: 1:00 AM
Claude: That's the Chou hour (丑时). Gender? (male/female)

User: 男 (Male)
Claude: Where were you born? (for true solar time correction)

User: X省X市 
Claude: All set. What aspects would you like me to focus on?
        Destiny overview / Love / Career / Wealth / Health?

User: 都要 (All of them)
Claude: [Chart → Five Elements → Ten Gods → Cycles → Fortune Curve
         → Annual Forecast → Monthly Heatmap → Specialty → Advice]
        Report saved to fortune-reports/命理报告_2026-05-24.html
```

## Structure

```
eastern-mysticism/
  SKILL.md                         # Skill definition with quick reference tables
  README.md                        # Chinese documentation
  README_EN.md                     # English documentation (this file)
  references/
    flows/
      consultation-flow.md         # Interactive consultation workflow
    guides/
      bazi-paipan.md               # BaZi chart calculation
      five-elements.md             # Five Elements theory
      shishen.md                   # Ten Gods interpretation
      nayin.md                     # NaYin quick reference
      html-report-template.md      # HTML report template
```

## Tech Stack

Pure CSS/HTML charts, zero JavaScript dependencies. Responsive layout + print support via `@media` queries.

## Disclaimer

For entertainment purposes only. Do not use as the sole basis for life decisions.


