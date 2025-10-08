# MRD Creation Workflow Controller with Data Visualization

## Overview
이 문서는 완성도 높은 MRD(Market Requirements Document)를 생성하고 데이터를 시각화하기 위한 통합 워크플로우 컨트롤러입니다. 
Step 1부터 Step 7까지 순차적으로 진행하며, 각 단계에서 수집한 데이터를 저장하고 시각화합니다. 최종 결과를 저장할 때는, 이모지는 빼주세요.

## Project Structure
```
.cursor/rules/MRD/
├── AGENTS.md (this file)
├── rules/
│   ├── 00-general-mrd.md
│   ├── 01-market-analysis.md
│   ├── 02-customer-segmentation.md
│   ├── 03-problem-definition.md
│   ├── 04-competitor-analysis.md
│   ├── 05-solution-ideation.md
│   ├── 06-metrics-business-case.md
│   ├── 07-synthesis.md
│   └── 08-visualization.md
└── mrd-output/
    ├── data/                    # JSON 형식의 원시 데이터
    │   ├── market-data.json
    │   ├── personas.json
    │   ├── problems.json
    │   ├── competitors.json
    │   ├── solutions.json
    │   ├── metrics.json
    │   └── master-data.json    # 통합 데이터
    ├── visualizations/          # 시각화 파일
    │   ├── dashboard.html       # 인터랙티브 대시보드
    │   ├── charts/
    │   └── notion-charts.md     # Notion용 차트
    ├── drafts/                  # 작업 중 문서
    ├── versions/                # 버전 관리
    └── final/
        ├── MRD-Document.md      # 최종 MRD 문서
        ├── MRD-Dashboard.md     # 시각화 대시보드
        └── MRD-Integrated.md    # 통합 문서 (선택적)
```

## Prerequisites
- Perplexity MCP 활성화 (설정되지 않은 경우 Tavily MCP 사용)
- Playwright MCP 활성화
- `.cursor/rules/MRD/rules/` 폴더에 모든 규칙 파일 존재
- `mrd-output/` 폴더 구조 생성

---

# MRD Creation Process with Data Capture

## Initial Setup

### Required Information Collection
```markdown
## 프로젝트 기본 정보
1. **제품명**: [귀하의 제품/서비스 이름]
2. **타겟 시장**: [예: Cloud Security, SaaS Analytics, E-commerce Tools]
3. **지리적 범위**: [Global / North America / Asia / Korea]
4. **분석 기간**: [예: 2024-2029]
5. **예상 출시일**: [예: 2024 Q4]
6. **데이터 시각화 선호도**: [Notion / HTML / Both]
```

### Data Collection Template
```json
{
  "project": {
    "name": "",
    "created_date": "",
    "last_updated": "",
    "version": "1.0"
  },
  "data": {}
}
```

---

## Step 1: Market Analysis with Data Capture
**규칙 파일**: `.cursor/rules/MRD/rules/01-market-analysis.md`

### 1.1 Information Gathering
```markdown
필요 정보:
- [ ] 타겟 시장/산업 정의
- [ ] 분석할 지리적 범위
- [ ] 시장 분석 기간 (현재-미래)

확인사항:
Q1: 타겟 시장은 [입력값]이 맞나요?
Q2: 특별히 집중하고 싶은 하위 시장이 있나요?
Q3: 경쟁사로 고려하는 회사들이 있나요?
```

### 1.2 Execution
```bash
@perplexity Following .cursor/rules/MRD/rules/01-market-analysis.md, analyze:
- Market: [USER_INPUT_MARKET]
- Geography: [USER_INPUT_GEO]
- Timeline: [USER_INPUT_TIMELINE]

Research and collect data for:
1. Market size (current and projected)
2. Growth rates (CAGR)
3. Market segments
4. Key trends
5. TAM/SAM/SOM calculations

Note: Perplexity MCP가 설정되지 않은 경우 Tavily MCP를 사용하세요.
```

### 1.3 Data Storage
```json
// Save to: mrd-output/data/market-data.json
{
  "market_analysis": {
    "market_name": "",
    "current_size": {
      "value": 0,
      "unit": "USD",
      "year": 2024
    },
    "projected_size": {
      "value": 0,
      "unit": "USD",
      "year": 2029
    },
    "cagr": 0,
    "tam": {
      "value": 0,
      "methodology": "top-down"
    },
    "sam": {
      "value": 0,
      "percentage_of_tam": 0
    },
    "som": {
      "value": 0,
      "percentage_of_sam": 0
    },
    "segments": [],
    "trends": [],
    "growth_drivers": []
  }
}
```

### 1.4 Visualization Components
```markdown
## Market Analysis Visualizations

### 1. TAM/SAM/SOM Waterfall Chart
\```mermaid
graph LR
    TAM[TAM: $100B] --> SAM[SAM: $30B]
    SAM --> SOM[SOM: $3B]
\```

### 2. Market Growth Projection (HTML)
<canvas id="marketGrowthChart"></canvas>

### 3. Market Segments (Notion Table)
| Segment | Size (2024) | CAGR | 2029 Projection |
|---------|------------|------|-----------------|
| [Data]  | [Data]     | [%]  | [Data]         |
```

### 1.5 Output
- Raw Data: `mrd-output/data/market-data.json`
- Document: `mrd-output/drafts/01-market-analysis.md`
- Visualizations: `mrd-output/visualizations/01-market-charts.html`

---

## Step 2: Customer Segmentation & Personas with Data Capture
**규칙 파일**: `.cursor/rules/MRD/rules/02-customer-segmentation.md`

### 2.1 Information Gathering
```markdown
Step 1 결과 기반 추가 정보:
- [ ] 주요 타겟 고객층
- [ ] 산업별 우선순위
- [ ] 고객이 겪는 주요 문제

질문:
Q1: 현재 고객이 있다면, 가장 성공적인 고객의 특징은?
Q2: 이상적인 고객의 회사 규모는?
Q3: 주요 의사결정자는 누구인가요?
```

### 2.2 Execution
```bash
@perplexity Following .cursor/rules/MRD/rules/02-customer-segmentation.md:

Create detailed personas and collect structured data for:
1. Demographics/Firmographics
2. Goals and challenges
3. Buying process
4. Budget ranges

Note: Perplexity MCP가 설정되지 않은 경우 Tavily MCP를 사용하세요.
```

### 2.3 Data Storage
```json
// Save to: mrd-output/data/personas.json
{
  "personas": [
    {
      "name": "",
      "title": "",
      "company_size": "",
      "industry": [],
      "goals": [],
      "challenges": [],
      "budget_range": {
        "min": 0,
        "max": 0
      },
      "decision_criteria": [],
      "influence_score": 0
    }
  ],
  "segments": [
    {
      "name": "",
      "size": 0,
      "growth_rate": 0,
      "priority": 0
    }
  ]
}
```

### 2.4 Visualization Components
```markdown
## Customer Visualizations

### 1. Persona Comparison Matrix (Notion)
| Attribute | Persona 1 | Persona 2 | Persona 3 |
|-----------|-----------|-----------|-----------|
| Company Size | | | |
| Budget | | | |
| Main Challenge | | | |

### 2. Segment Priority Map (Mermaid)
\```mermaid
quadrantChart
    title Customer Segment Priority
    x-axis Low Growth → High Growth
    y-axis Small Size → Large Size
    quadrant-1 Develop
    quadrant-2 Prioritize
    quadrant-3 Deprioritize
    quadrant-4 Maintain
    Segment1: [0.7, 0.8]
    Segment2: [0.3, 0.6]
\```

### 3. Interactive Persona Cards (HTML)
<div class="persona-cards"></div>
```

---

## Step 3: Problem Definition with Data Capture
**규칙 파일**: `.cursor/rules/MRD/rules/03-problem-definition.md`

### 3.1 Information Gathering
```markdown
페르소나 기반 문제 탐색:
- [ ] 각 페르소나의 핵심 문제
- [ ] 현재 해결 방법과 불만족 이유
- [ ] 문제로 인한 비용/시간 손실
```

### 3.2 Data Storage
```json
// Save to: mrd-output/data/problems.json
{
  "problems": [
    {
      "id": "P001",
      "description": "",
      "severity": 0,
      "frequency": "",
      "affected_personas": [],
      "affected_percentage": 0,
      "current_solutions": [],
      "satisfaction_score": 0,
      "impact": {
        "time_waste": "",
        "cost": 0,
        "productivity_loss": 0
      },
      "priority_score": 0
    }
  ]
}
```

### 3.3 Visualization Components
```markdown
## Problem Analysis Visualizations

### 1. Problem Priority Matrix (HTML)
<canvas id="problemMatrix"></canvas>

### 2. Impact vs Effort Chart (Mermaid)
\```mermaid
graph TB
    subgraph High Impact
        P1[Problem 1<br/>80% affected]
        P2[Problem 2<br/>60% affected]
    end
    subgraph Low Impact
        P3[Problem 3<br/>30% affected]
    end
\```

### 3. Problem Severity Heatmap (Notion)
| Problem | Severity | Frequency | Impact | Priority |
|---------|----------|-----------|--------|----------|
| [Data] | 🔴 High | Daily | $XXX | 1 |
```

---

## Step 4: Competitive Analysis with Data Capture
**규칙 파일**: `.cursor/rules/MRD/rules/04-competitor-analysis.md`

### 4.1 Data Storage
```json
// Save to: mrd-output/data/competitors.json
{
  "competitors": [
    {
      "name": "",
      "website": "",
      "market_share": 0,
      "strengths": [],
      "weaknesses": [],
      "features": {},
      "pricing": {
        "model": "",
        "tiers": []
      },
      "target_segments": [],
      "positioning": "",
      "customer_satisfaction": {
        "nps": 0,
        "g2_score": 0
      }
    }
  ],
  "positioning_map": {
    "x_axis": "",
    "y_axis": "",
    "positions": []
  }
}
```

### 4.2 Visualization Components
```markdown
## Competitive Visualizations

### 1. Feature Comparison Matrix (Notion)
| Feature | Us | Comp A | Comp B | Comp C |
|---------|-----|--------|--------|--------|
| Feature 1 | ✅ | ✅ | ❌ | ✅ |

### 2. Positioning Map (HTML)
<canvas id="positioningMap"></canvas>

### 3. Competitive SWOT (Mermaid)
\```mermaid
mindmap
  root((Competitive Analysis))
    Strengths
      Strong brand
      Tech advantage
    Weaknesses
      High price
      Limited features
    Opportunities
      Market gaps
      New segments
    Threats
      New entrants
      Substitutes
\```
```

---

## Step 5: Solution Ideation with Data Capture
**규칙 파일**: `.cursor/rules/MRD/rules/05-solution-ideation.md`

### 5.1 Data Storage
```json
// Save to: mrd-output/data/solutions.json
{
  "solutions": [
    {
      "id": "S001",
      "name": "",
      "description": "",
      "solves_problems": [],
      "features": [],
      "rice_score": {
        "reach": 0,
        "impact": 0,
        "confidence": 0,
        "effort": 0,
        "total": 0
      },
      "priority": 0,
      "phase": "",
      "dependencies": []
    }
  ],
  "roadmap": {
    "phases": []
  }
}
```

### 5.2 Visualization Components
```markdown
## Solution Visualizations

### 1. Feature Roadmap (Mermaid)
\```mermaid
gantt
    title Product Roadmap
    dateFormat YYYY-MM-DD
    section MVP
    Core Feature 1 :2024-01-01, 30d
    Core Feature 2 :30d
    section Phase 2
    Feature 3 :60d
    Feature 4 :30d
\```

### 2. RICE Scoring Chart (HTML)
<canvas id="riceChart"></canvas>

### 3. Solution-Problem Mapping (Notion)
| Solution | Addressed Problems | Impact | Priority |
|----------|-------------------|--------|----------|
```

---

## Step 6: Metrics & Business Case with Data Capture
**규칙 파일**: `.cursor/rules/MRD/rules/06-metrics-business-case.md`

### 6.1 Data Storage
```json
// Save to: mrd-output/data/metrics.json
{
  "financial_projections": {
    "revenue": {
      "year1": 0,
      "year2": 0,
      "year3": 0,
      "year4": 0,
      "year5": 0
    },
    "costs": {},
    "metrics": {
      "cac": 0,
      "ltv": 0,
      "payback_period": 0,
      "break_even": ""
    }
  },
  "kpis": [
    {
      "name": "",
      "current": 0,
      "target": 0,
      "timeline": ""
    }
  ],
  "pricing": {
    "model": "",
    "tiers": []
  }
}
```

### 6.2 Visualization Components
```markdown
## Business Metrics Visualizations

### 1. Revenue Projections (HTML)
<canvas id="revenueChart"></canvas>

### 2. Unit Economics (Notion)
| Metric | Value | Industry Benchmark | Status |
|--------|-------|-------------------|--------|
| CAC | $X | $Y | ✅/⚠️/❌ |
| LTV | $X | $Y | ✅/⚠️/❌ |
| LTV/CAC | X:1 | 3:1 | ✅/⚠️/❌ |

### 3. Financial Timeline (Mermaid)
\```mermaid
timeline
    title Financial Milestones
    2024 Q1 : MVP Launch
             : $0 Revenue
    2024 Q3 : First Customers
             : $100K ARR
    2025 Q1 : Break Even
             : $1M ARR
\```
```

---

## Step 7: Synthesis & Dashboard Creation
**규칙 파일**: `.cursor/rules/MRD/rules/07-synthesis.md`
**규칙 파일**: `.cursor/rules/MRD/rules/08-visualization.md`

### 7.1 Data Integration
```bash
# Merge all data files into master-data.json
Combine data from:
- market-data.json
- personas.json
- problems.json
- competitors.json
- solutions.json
- metrics.json

Output: mrd-output/data/master-data.json
```

### 7.2 Dashboard Generation

#### A. Notion Dashboard (MRD-Dashboard.md)
```markdown
# MRD Executive Dashboard

## Key Metrics at a Glance
| Metric | Value | Status |
|--------|-------|--------|
| TAM | $XB | 🟢 |
| Target Launch | Q4 2024 | 🟡 |
| Priority Segments | 3 | 🟢 |

## Market Overview
[Market charts and visualizations]

## Customer Insights
[Persona comparisons and segment analysis]

## Competitive Landscape
[Positioning maps and feature comparisons]

## Solution Roadmap
[Timeline and priority matrix]

## Financial Projections
[Revenue charts and metrics]
```

#### B. Interactive HTML Dashboard
```html
<!-- Save to: mrd-output/visualizations/dashboard.html -->
<!DOCTYPE html>
<html>
<head>
    <title>MRD Interactive Dashboard</title>
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <style>
        .dashboard-grid {
            display: grid;
            grid-template-columns: repeat(2, 1fr);
            gap: 20px;
        }
        .chart-container {
            padding: 20px;
            border: 1px solid #ddd;
            border-radius: 8px;
        }
    </style>
</head>
<body>
    <h1>MRD Interactive Dashboard</h1>
    
    <div class="dashboard-grid">
        <div class="chart-container">
            <h3>Market Growth</h3>
            <canvas id="marketChart"></canvas>
        </div>
        
        <div class="chart-container">
            <h3>Customer Segments</h3>
            <canvas id="segmentChart"></canvas>
        </div>
        
        <div class="chart-container">
            <h3>Problem Priority</h3>
            <canvas id="problemChart"></canvas>
        </div>
        
        <div class="chart-container">
            <h3>Revenue Projection</h3>
            <canvas id="revenueChart"></canvas>
        </div>
    </div>
    
    <script>
        // Load data from master-data.json
        fetch('../data/master-data.json')
            .then(response => response.json())
            .then(data => {
                renderCharts(data);
            });
    </script>
</body>
</html>
```

### 7.3 Final Outputs

#### Standard Outputs
1. **MRD Document**: `mrd-output/final/MRD-Document.md`
   - Complete text-based MRD
   - All sections from Steps 1-6
   
2. **MRD Dashboard**: `mrd-output/final/MRD-Dashboard.md`
   - Notion-compatible visualization dashboard
   - Key metrics and charts
   
3. **Interactive Dashboard**: `mrd-output/visualizations/dashboard.html`
   - HTML/JavaScript interactive charts
   - Real-time data visualization

#### Optional: Integrated Document
```markdown
User Request: "MRD 문서 안에 시각화를 임베드해주세요"

Response: Creating integrated document...
Output: mrd-output/final/MRD-Integrated.md
- Text content + embedded visualizations
- Notion-compatible format
- Complete standalone document
```

---

# Visualization Rules File

## Create: `.cursor/rules/MRD/rules/08-visualization.md`
```markdown
# Visualization Rules

## Objective
수집된 데이터를 효과적으로 시각화하여 인사이트를 제공

## Visualization Types by Data

### Market Data
- TAM/SAM/SOM: Waterfall chart or nested circles
- Growth projections: Line chart with projections
- Market segments: Pie chart or stacked bar
- Trends: Timeline or trend arrows

### Customer Data
- Personas: Comparison cards or radar charts
- Segments: Bubble chart (size vs growth)
- Journey: Flow diagram

### Problem Data
- Priority matrix: 2x2 quadrant (severity vs frequency)
- Impact analysis: Heatmap
- Problem-persona mapping: Sankey diagram

### Competitive Data
- Feature comparison: Matrix table
- Positioning: Scatter plot
- SWOT: Mind map or quadrants

### Solution Data
- Roadmap: Gantt chart
- RICE scores: Bar chart
- Dependencies: Network diagram

### Financial Data
- Revenue projection: Area chart
- Unit economics: Gauge charts
- Break-even: Line intersection chart

## Format Guidelines

### Notion Format
- Use markdown tables for comparisons
- Mermaid for flow diagrams
- Emoji indicators for status (🟢🟡🔴)
- Toggle lists for detailed sections

### HTML/JavaScript
- Use Chart.js for standard charts
- Responsive design
- Interactive tooltips
- Export functionality

### Data Storage
- All visualizations must reference data/*.json
- Maintain data versioning
- Support incremental updates
```

---

# Execution Commands Summary

## Quick Start with Visualization
```bash
# Start the complete MRD process with data capture
cursor .cursor/rules/MRD/AGENTS.md

# Generate visualizations after data collection
cursor .cursor/rules/MRD/rules/08-visualization.md

# View interactive dashboard
open mrd-output/visualizations/dashboard.html

# Export for Notion
cat mrd-output/final/MRD-Dashboard.md
```

## Data Management
```bash
# Check collected data
ls -la mrd-output/data/

# Merge data files
cat mrd-output/data/*.json > mrd-output/data/master-data.json

# Version control
cp -r mrd-output/data/ mrd-output/versions/$(date +%Y%m%d-%H%M%S)/
```

---

# Progress Tracking with Metrics

## Completion Status
```markdown
- [ ] Step 1: Market Analysis | Data: [ ] | Visual: [ ]
- [ ] Step 2: Customer Segmentation | Data: [ ] | Visual: [ ]
- [ ] Step 3: Problem Definition | Data: [ ] | Visual: [ ]
- [ ] Step 4: Competitive Analysis | Data: [ ] | Visual: [ ]
- [ ] Step 5: Solution Ideation | Data: [ ] | Visual: [ ]
- [ ] Step 6: Business Case | Data: [ ] | Visual: [ ]
- [ ] Step 7: Synthesis | Dashboard: [ ] | Integration: [ ]

Data Collection: [0/6] Complete
Visualizations: [0/6] Complete
Overall Progress: [0/7] Steps Complete
```

## Data Quality Metrics
```markdown
각 데이터 섹션 완성도 (0-100%):
- Market Data: [ ]%
- Customer Data: [ ]%
- Problem Data: [ ]%
- Competitive Data: [ ]%
- Solution Data: [ ]%
- Financial Data: [ ]%
```

---

# Final Checklist

## Before Starting
- [ ] Perplexity MCP 연결 확인
- [ ] Playwright MCP 연결 확인
- [ ] 데이터 저장 폴더 생성
- [ ] 시각화 도구 준비

## After Completion
- [ ] 모든 데이터 파일 생성 확인
- [ ] 시각화 대시보드 검증
- [ ] Notion 호환성 확인
- [ ] 인터랙티브 차트 작동 확인
- [ ] 데이터 백업 완료

---

# Tips for Success

1. **데이터 일관성**: 모든 단계에서 동일한 형식 유지
2. **점진적 저장**: 각 단계마다 데이터 저장
3. **시각화 선택**: 데이터 특성에 맞는 차트 선택
4. **인터랙티브 요소**: 사용자 경험 고려
5. **버전 관리**: 정기적인 백업과 버전 기록

---

# Support

문제가 발생하거나 도움이 필요한 경우:
1. 현재 단계와 수집된 데이터 확인
2. 시각화 오류 시 데이터 형식 검증
3. 필요한 차트 유형 명시
4. 원하는 출력 형식 지정

---