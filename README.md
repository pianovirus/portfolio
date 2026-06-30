# 포트폴리오

**김명희** · Fullstack AI Engineer
📮 [pianovirus@naver.com](mailto:pianovirus@naver.com)

---

## 📁 프로젝트

### [`chatbot-portfolio/`](./chatbot-portfolio/)
**사내 지식 기반 RAG AI 어시스턴트** — 5개 업종(약국·병의원·학원·한의원·공통) 매뉴얼 답변 챗봇

- 📄 [README (포트폴리오 본문)](./chatbot-portfolio/README.md)
- 🌐 [HTML 버전](./chatbot-portfolio/portfolio.html)
- 📑 [PDF 버전](./chatbot-portfolio/portfolio.pdf)

PostgreSQL · pgvector 하이브리드 검색 + Cross-encoder 리랭킹, 멀티모달 문서 처리(PDF·PPTX·Notion)를 결합한
사내 RAG 챗봇. 검색·생성 파이프라인부터 관리자 콘솔 · 사용자 분석 · 배포까지 **풀스택 단독 개발**.

### [`aipharm-portfolio/`](./aipharm-portfolio/)
**AI Pharm** — 약국 처방전 기반 AI 영양제 추천 시스템

- 📄 [README (포트폴리오 본문)](./aipharm-portfolio/README.md)
- 🌐 [HTML 버전](./aipharm-portfolio/portfolio.html)
- 📑 [PDF 버전](./aipharm-portfolio/portfolio.pdf)

식약처 · PubMed · FDA 공공 데이터를 통합하고, **LLM Multi-Provider Fallback Chain · 외부 의료 정보 도구 (MCP) · 다단계 환각 차단**으로
환자별 맞춤 영양제·생활가이드를 추천하는 풀스택 헬스케어 AI 플랫폼.

> 📌 상세 알고리즘은 면접 시 직접 시연합니다 (출원·등록 특허 보호 영역)

---

## 🌱 오픈소스 기여

### [kfda-mcp](https://github.com/pianovirus/kfda-mcp) — Korean MFDS MCP Server
**한국 헬스케어 AI 커뮤니티 첫 MCP 서버** (Author, MIT)

한국 식품의약품안전처(MFDS) 공공 OpenAPI를 Anthropic MCP 프로토콜로 감싼 서버.
LLM 에이전트(Claude Desktop 등)가 한국 의약품 마스터 · DUR 안전사용 · e약은요
정보를 자율적으로 조회 가능. 글로벌 MCP 생태계(BioMCP, Medical MCP)가 한국 식약처
데이터를 다루지 않는 점에 착안해 단독 개발.

Stack: Python · Anthropic MCP SDK · httpx

---

## 📦 통합 PDF (두 프로젝트 한 파일)

📥 [**portfolio_combined.pdf**](https://github.com/pianovirus/portfolio/raw/main/portfolio_combined.pdf) — RAG 챗봇 + AI Pharm 한 PDF
