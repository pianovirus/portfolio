<div align="center">

# 🧪 AIPharm 포트폴리오

### 약국 처방전 기반 AI 영양제 추천 시스템

**AI Pharm** — 식품의약품안전처 · PubMed · FDA 공공 의료 데이터를 통합해
**환자별 맞춤 영양제·생활가이드를 자동 추천**하는 풀스택 헬스케어 AI 플랫폼

![Domain](https://img.shields.io/badge/Domain-Healthcare%20AI-6366f1?style=for-the-badge)
![Stack](https://img.shields.io/badge/Stack-FastAPI-009688?style=for-the-badge&logo=fastapi)
![DB](https://img.shields.io/badge/DB-MySQL-4479A1?style=for-the-badge&logo=mysql&logoColor=white)
![LLM](https://img.shields.io/badge/LLM-Multi--Provider%20Fallback-ec4899?style=for-the-badge)
![MCP](https://img.shields.io/badge/MCP-Medical%20Tool--use-8b5cf6?style=for-the-badge)
![Status](https://img.shields.io/badge/Status-Production-10b981?style=for-the-badge)

</div>

---

## 🧪 Live Demo

<div align="center">

### 처방전 입력 → AI 추천 결과까지 실제 운영 중인 시스템

> **▶ 면접 시 직접 시연 가능**

</div>

---

## 📊 Impact in Numbers

<div align="center">

| 데이터 자산 | 규모 | 출처 |
|:---|---:|:---|
| 🍃 **건강기능식품 마스터** | **45,244** | 식약처 OpenAPI 매일 자동 수집 |
| 💊 **의약품 허가정보** | **43,179** | 식약처 실시간 OpenAPI |
| 🛡 **DUR 안전성 룰** | **812,128** | 병용금기·임부금기·노인주의 등 |
| 🧬 **영양소 마스터 (정규화 후)** | **614** | 741 → 127개 중복 자동 정리 |

</div>

---

## 📌 Overview

약사가 처방전을 받았을 때, **환자의 질병코드(KCD)·처방약·연령**을 종합 분석해
**"이 환자에게 이 영양제가 왜 필요한지"** AI 가 근거와 함께 즉시 추천하고,
그 결과를 멀티 디바이스로 환자에게 보여주는 풀스택 시스템.

단순 LLM Wrapper 가 아니라, **PubMed 논문 · 식약처 DUR · 미국 FDA** 라는 공공 의료 데이터를 직접 수집·정규화하고,
LLM 의 잘못된 답변을 다단계로 교차 검증해 **근거 없는 추천을 자동으로 차단**하는 신뢰성 중심 설계가 핵심.

> 📌 상세 알고리즘·아키텍처 다이어그램은 면접 시 직접 시연합니다 (출원·등록 특허 보호 영역)

---

## 🏗 시스템 아키텍처 한눈에

<table>
<tr>
<td width="33%" valign="top">

### 🟢 LAYER 1
**데이터 수집·정규화**

- 식약처 의약품 허가 OpenAPI
- 식품안전나라 건기식 OpenAPI
- 식약처 DUR 안전성 룰
- PubMed 의학논문 검색
- 미국 FDA Drug Label
- 자동 fuzzy 매칭 (영양소 ↔ 제품)

</td>
<td width="33%" valign="top">

### 🔵 LAYER 2
**AI 추천 & 검증**

- 통합 advisor: KCD·ATC 라우팅
- **LLM Multi-Provider Fallback Chain**
- **외부 의료 정보 도구 (MCP tool-use)**
- LLM 환각 차단 다단계 교차 검증
- 병용금기 자동 차단 (DUR 룰)
- 결과 캐시 · 토큰 비용 최소화

</td>
<td width="33%" valign="top">

### 🟣 LAYER 3
**API & 멀티 디바이스 UI**

- FastAPI REST endpoints
- 비동기 Async Batch 처리
- 어드민 SPA (Alpine.js + Tailwind)
- 멀티 디바이스 동기화
- 외부 시스템 양방향 통신
- 처방전 호출 이력 추적

</td>
</tr>
</table>

---

## ⚙ 기술적 의사결정 하이라이트

### 🔬 LLM 환각 차단 시스템
LLM 이 만들어낸 가짜 논문 근거가 환자에게 노출되지 않도록,
**공공 의학 데이터베이스와 LLM 응답을 다단계로 교차 검증**하는 환각 차단 파이프라인 구축.
미통과 항목은 자동 검토 큐로 분리해 약사가 후처리.

### ⚡ 대량 매핑 Async Batch
POS 가 대량의 미매핑 상품을 한 번에 보내도 클라이언트 timeout 없이 즉시 ack 후
백그라운드 threadpool 에서 fuzzy 매칭을 비동기 처리.
row-level 실패 추적 + 완료 시 DB 결과 반영.

### 🛡 병용금기 자동 차단
식약처 DUR **81만건 룰**을 환자 처방약과 자동 비교, 위험 조합 영양소·생활가이드는 추천에서 자동 제외.
약사가 받는 결과는 이미 1차 안전성 필터링 완료 상태.

### 🔁 LLM Multi-Provider Fallback + 외부 의료 정보 도구
LLM Provider 장애 시 자동 전환되는 Fallback Chain 구축.
외부 의료 정보 도구 (MCP tool-use) 로 약물 상호작용·논문 evidence 직접 조회.
결과 캐시로 분리형 endpoint 가 같은 처방을 여러 번 호출해도 LLM 1회만 사용.

### 📱 멀티 디바이스 통합
같은 추천 결과를 여러 디바이스에 각각 맞는 레이아웃으로 렌더링.
디바이스 동작에 따라 실시간 화면 push 전환.

---

## 🗂 통합한 공공 의료 데이터 출처

| 출처 | 활용 |
|:---|:---|
| 🇰🇷 **식품의약품안전처** | 의약품 제품 허가정보 OpenAPI · DUR · e약은요 |
| 🇰🇷 **식품안전나라** | 건강기능식품 인허가 OpenAPI |
| 🇺🇸 **PubMed** | 미국 국립의학도서관 의학 논문 DB · 근거 논문 메타데이터 조회 |
| 🇺🇸 **미국 FDA** | Drug Label · 효능 / 경고 / 상호작용 |
| 🇰🇷 **보건복지부** | KCD-7 질병분류코드 |
| 🇰🇷 **심평원** | ATC 매핑 · 보험 EDI 코드 |

---

## 👤 담당 역할 (전 영역 단독)

| 영역 | 내용 |
|:---|:---|
| 🏗 시스템 아키텍처 | 데이터 수집 → 정규화 → 검증 → 추천 → 멀티 디바이스 전체 흐름 |
| 🔌 외부 API 통합 | 공공 데이터 OpenAPI / 인증·페이지네이션·재시도·rate limit |
| 🧠 LLM · 검증 시스템 | Multi-provider fallback, 다단계 환각 차단, 외부 의료 정보 도구 |
| 💾 DB 설계 + ETL | MySQL 60+ 운영 테이블 / fuzzy 매칭 / 자동 중복 정리 |
| 🎨 어드민 SPA + 멀티 UI | Alpine.js + Tailwind, 30+ 페이지 |
| 🚀 DevOps · 배포 | SSH 자동 배포 / 백업·롤백 / 무중단 재기동 |

---

## 🌱 Open Source Contribution

### [kfda-mcp](https://github.com/pianovirus/kfda-mcp) — Korean MFDS MCP Server
한국 헬스케어 AI 커뮤니티 첫 MCP 서버 (Author, MIT, 단독 개발).

글로벌 MCP 생태계(BioMCP, Medical MCP 등)가 한국 식약처 데이터를 다루지 않는 점에
착안해, 한국 식품의약품안전처(MFDS) 공공 OpenAPI를 Anthropic MCP 프로토콜로 감싼
오픈소스 서버를 단독 개발. LLM 에이전트(Claude Desktop 등)가 한국 의약품 마스터, DUR
안전사용, e약은요 정보를 자율적으로 호출 가능.

Stack: Python · Anthropic MCP SDK · httpx

---

## 🛠 기술 스택

`Python` · `FastAPI` · `MySQL` · `PooledDB` · `Jinja2`
`Alpine.js` · `Tailwind CSS`
`LLM Multi-Provider Fallback Chain` · `외부 의료 정보 MCP tool-use`
`공공 OpenAPI 통합` (PubMed · FDA · KFDA · 식품안전나라 · 보건복지부 · 심평원)

---

## 📑 자세히 보기

- 🌐 [HTML 버전 다운로드](https://github.com/pianovirus/portfolio/raw/main/aipharm-portfolio/portfolio.html)
- 📄 [PDF 버전 다운로드](https://github.com/pianovirus/portfolio/raw/main/aipharm-portfolio/portfolio.pdf)

---

<div align="center">

## 📮 Contact

**김명희** · Fullstack AI Engineer

📧 [pianovirus@naver.com](mailto:pianovirus@naver.com)

> 본 포트폴리오는 실제 운영 중인 AI Pharm 시스템의
> 기술적 의사결정과 성과를 정리한 자료입니다.

</div>
