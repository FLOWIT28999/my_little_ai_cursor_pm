# TRD Generation Agent Orchestrator

## Overview
이 에이전트는 PRD 분석 결과를 기반으로 포괄적인 기술 요구사항 문서(TRD)를 자동으로 생성합니다. 특히 사용자로부터 명확한 기술 스택을 확정받아 구체적이고 실행 가능한 기술 명세를 작성합니다.

## Prerequisites
- PRD 생성 완료 및 technical requirements 초안 존재
  - `prd-output/analysis/technical-requirements.md`
  - `prd-output/analysis/user-stories.md`
  - `prd-output/final/PRD-Document.md`
- Perplexity MCP 구성 (기술 조사용)
- 모든 규칙 파일이 `.cursor/rules/TRD/rules/` 디렉토리에 존재
- **출력 언어**: 한국어

## Project Structure
```
.cursor/
├── rules/
│   ├── PRD/                           # PRD 워크플로우
│   │   └── prd-output/
│   │       ├── analysis/
│   │       │   ├── technical-requirements.md  # TRD 초안
│   │       │   └── user-stories.md
│   │       └── final/
│   │           └── PRD-Document.md
│   │
│   └── TRD/                           # TRD 워크플로우
│       ├── AGENTS.md (this file)
│       ├── rules/
│       │   ├── 01-tech-stack-selection.md
│       │   ├── 02-system-architecture.md
│       │   ├── 03-functional-requirements.md
│       │   ├── 04-nfr-specification.md
│       │   ├── 05-api-data-specification.md
│       │   ├── 06-testing-requirements.md
│       │   ├── 07-deployment-operations.md
│       │   └── 08-generate-trd.md
│       └── trd-output/
│           ├── analysis/              # 중간 분석 결과
│           │   ├── tech-stack.md
│           │   ├── architecture.md
│           │   ├── functional-req.md
│           │   ├── nfr.md
│           │   ├── api-spec.md
│           │   ├── test-plan.md
│           │   └── deployment.md
│           ├── versions/              # 버전 관리
│           └── final/
│               └── TRD-Document.md    # 최종 TRD (한국어)
```

## Execution Workflow

### Phase 0: PRD Analysis & Tech Stack Confirmation
**중요**: 사용자로부터 기술 스택을 명확히 확정받는 단계

1. **PRD 기술 요구사항 검토** 
   - 입력: `@prd-output/analysis/technical-requirements.md`
   - PRD에서 제안된 기술 요구사항 분석
   - 불명확하거나 결정되지 않은 기술 스택 식별

2. **기술 스택 확정** (`.cursor/rules/TRD/rules/01-tech-stack-selection.md`)
   - **사용자 인터랙션 필수**
   - 질문 예시:
     ```
     PRD 분석 결과, 다음 기술 스택 확정이 필요합니다:
     
     1. 프론트엔드 프레임워크를 선택해주세요:
        [ ] React
        [ ] Vue.js
        [ ] Angular
        [ ] Next.js
        [ ] 기타: ___
     
     2. 백엔드 언어/프레임워크를 선택해주세요:
        [ ] Node.js (Express/Fastify)
        [ ] Python (FastAPI/Django)
        [ ] Java (Spring Boot)
        [ ] Go (Gin/Echo)
        [ ] 기타: ___
     
     3. 데이터베이스를 선택해주세요:
        [ ] PostgreSQL
        [ ] MySQL
        [ ] MongoDB
        [ ] 기타: ___
     
     4. 클라우드 플랫폼을 선택해주세요:
        [ ] AWS
        [ ] Google Cloud
        [ ] Azure
        [ ] On-premise
        [ ] 기타: ___
     ```
   - 출력: `.cursor/rules/TRD/trd-output/analysis/tech-stack.md`

### Phase 1: Architecture Design (아키텍처 설계)

3. **시스템 아키텍처 설계** (`.cursor/rules/TRD/rules/02-system-architecture.md`)
   - 입력: 확정된 기술 스택 + PRD 분석
   - 아키텍처 패턴 결정 (Microservices, Monolithic, Serverless 등)
   - 컴포넌트 정의 및 통신 패턴 설계
   - Mermaid 다이어그램 생성
   - 출력: `.cursor/rules/TRD/trd-output/analysis/architecture.md`

### Phase 2: Requirements Specification (요구사항 명세)

4. **기능 요구사항 명세** (`.cursor/rules/TRD/rules/03-functional-requirements.md`)
   - 입력: PRD user stories + 아키텍처 설계
   - User Story를 기술 요구사항으로 변환
   - API 엔드포인트 매핑
   - 상세 처리 로직 정의
   - 출력: `.cursor/rules/TRD/trd-output/analysis/functional-req.md`

5. **비기능 요구사항 명세** (`.cursor/rules/TRD/rules/04-nfr-specification.md`)
   - 입력: PRD NFR + 기술 스택
   - 성능, 보안, 확장성 요구사항 상세화
   - 측정 가능한 목표값 설정
   - 검증 방법 정의
   - 출력: `.cursor/rules/TRD/trd-output/analysis/nfr.md`

### Phase 3: Technical Specification (기술 명세)

6. **API 및 데이터 명세** (`.cursor/rules/TRD/rules/05-api-data-specification.md`)
   - 입력: 기능 요구사항 + 데이터베이스 선택
   - OpenAPI 3.0 명세 생성
   - ERD 설계 (Mermaid)
   - SQL DDL 스크립트 생성
   - 출력: `.cursor/rules/TRD/trd-output/analysis/api-spec.md`

7. **테스트 요구사항** (`.cursor/rules/TRD/rules/06-testing-requirements.md`)
   - 입력: 모든 요구사항 명세
   - 테스트 전략 수립
   - 인수 기준 정의 (Given-When-Then)
   - 테스트 자동화 계획
   - 출력: `.cursor/rules/TRD/trd-output/analysis/test-plan.md`

### Phase 4: Operations Planning (운영 계획)

8. **배포 및 운영 요구사항** (`.cursor/rules/TRD/rules/07-deployment-operations.md`)
   - 입력: 아키텍처 + NFR + 클라우드 플랫폼
   - 배포 전략 (Blue-Green, Rolling 등)
   - 인프라 요구사항 정의
   - 모니터링 및 백업 전략
   - 출력: `.cursor/rules/TRD/trd-output/analysis/deployment.md`

### Phase 5: Document Generation (문서 생성)

9. **TRD 통합 생성** (`.cursor/rules/TRD/rules/08-generate-trd.md`)
   - 입력: 모든 분석 결과물
   - 완전한 TRD 문서 생성 (한국어)
   - AI 코딩 에이전트를 위한 지침 포함
   - 출력: `.cursor/rules/TRD/trd-output/final/TRD-Document.md`

## Agent Commands

### 전체 TRD 생성 (권장)
```bash
# 1. PRD 분석 및 기술 스택 확정
@prd-output/analysis/technical-requirements.md 참조
사용자에게 기술 스택 확정 요청

# 2. 모든 규칙 순차 실행 (01-08)
각 단계별 분석 수행

# 3. 최종 TRD 생성
모든 분석 결과를 통합하여 TRD 작성
```

### 빠른 TRD 생성 (기술 스택이 이미 확정된 경우)
```bash
# 기술 스택이 명확한 경우
규칙 01 건너뛰고 02-08 실행
```

### 특정 섹션만 업데이트
```bash
# API 명세만 재생성
규칙 05 실행 후 TRD의 해당 섹션 업데이트
```

## Context Management

### 파일 참조
- PRD 참조: `@prd-output/analysis/*.md`, `@prd-output/final/PRD-Document.md`
- TRD 중간 결과: `@.cursor/rules/TRD/trd-output/analysis/*.md`
- 최종 TRD: `@.cursor/rules/TRD/trd-output/final/TRD-Document.md`

### 일관성 유지
- 기술 스택은 Phase 0에서 확정 후 변경 불가
- 모든 섹션에서 동일한 용어 사용
- 한국어 작성, 기술 용어는 영문 병기

## Quality Assurance

### 검증 포인트
각 단계 후 확인사항:
1. **기술 스택 확정**: 모든 레이어의 기술이 선택되었는가?
2. **아키텍처**: 선택된 기술 스택과 일치하는가?
3. **기능 요구사항**: 모든 user story가 매핑되었는가?
4. **NFR**: 측정 가능한 목표가 설정되었는가?
5. **API/데이터**: OpenAPI와 DDL이 유효한가?
6. **테스트**: 모든 요구사항에 인수 기준이 있는가?
7. **배포**: 인프라 요구사항이 현실적인가?

### 오류 처리
문제 발생 시:
1. PRD 파일 존재 확인
2. 기술 스택 확정 여부 확인
3. 이전 단계 출력 검토
4. 필요시 사용자에게 추가 정보 요청

## Output Standards

### TRD 특징
- **언어**: 한국어
- **형식**: Markdown
- **구조**: 모듈식, 계층적
- **다이어그램**: Mermaid.js 코드
- **API**: OpenAPI 3.0 YAML
- **데이터**: SQL DDL
- **대상 독자**: 개발팀 + AI 코딩 에이전트

### AI Coding Agent 호환성
TRD는 GitHub Copilot 등 AI 코딩 에이전트가 직접 참조할 수 있도록:
- 명확한 섹션 구분
- 코드 블록 언어 태그 명시
- 일관된 명명 규칙
- 상세한 API 명세

## 실행 예시

```markdown
사용자: PRD 기반으로 TRD를 생성해주세요.

AI 응답:
PRD 분석을 시작하겠습니다.

[PRD technical requirements 검토]
다음 기술 스택 결정이 필요합니다:

**프론트엔드 선택이 필요합니다:**
1. React (컴포넌트 기반, 큰 생태계)
2. Vue.js (쉬운 학습 곡선)
3. Next.js (SSR 지원, SEO 최적화)
4. 기타

**백엔드 선택이 필요합니다:**
1. Node.js + Express (JavaScript 풀스택)
2. Python + FastAPI (빠른 개발, ML 친화적)
3. Java + Spring Boot (엔터프라이즈)
4. 기타

선택해 주시면 TRD 생성을 진행하겠습니다.
```

## Troubleshooting

### 일반적인 문제 해결

| 문제 | 원인 | 해결 방법 |
|------|------|----------|
| PRD 파일을 찾을 수 없음 | PRD 생성이 완료되지 않음 | PRD 워크플로우 먼저 실행 |
| 기술 스택 불일치 | 중간에 기술 변경 | Phase 0부터 다시 시작 |
| API 명세 오류 | 잘못된 YAML 형식 | OpenAPI 검증 도구 사용 |
| Mermaid 렌더링 실패 | 구문 오류 | Mermaid live editor에서 검증 |

### 자주 묻는 질문

**Q: PRD 없이 TRD를 만들 수 있나요?**
A: 가능하지만 권장하지 않습니다. 최소한 사용자 스토리와 요구사항은 필요합니다.

**Q: 기술 스택을 나중에 변경할 수 있나요?**
A: Phase 0에서 확정 후에는 전체 TRD를 다시 생성해야 합니다.

**Q: AI 코딩 에이전트가 TRD를 어떻게 활용하나요?**
A: TRD의 API 명세, 데이터 모델, 인수 기준을 직접 참조하여 코드를 생성합니다.

## Best Practices

1. **기술 스택 확정 시 고려사항**
   - 팀의 기술 역량
   - 프로젝트 요구사항
   - 장기적 유지보수
   - 라이선스 비용

2. **TRD 작성 시 주의사항**
   - 모호한 표현 피하기
   - 측정 가능한 목표 설정
   - 실현 가능한 계획 수립

3. **AI 코딩 에이전트 최적화**
   - 명확한 명명 규칙
   - 상세한 주석
   - 구조화된 문서

## Version History

| 버전 | 날짜 | 변경사항 |
|------|------|----------|
| 1.0 | 2024-01 | 초기 버전 |

## Support

문제 발생 시 확인사항:
1. 모든 rules 파일이 올바른 경로에 있는지 확인
2. PRD 출력 파일들이 생성되었는지 확인
3. 기술 스택이 명확히 선택되었는지 확인
4. 각 단계별 출력이 정상적으로 생성되는지 확인

---

**참고**: 이 TRD 생성 시스템은 PRD → TRD의 완전한 자동화를 목표로 하며, 특히 AI 코딩 에이전트가 직접 활용할 수 있는 기계 가독성 높은 문서를 생성합니다.