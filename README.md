# MolluAI

**캐릭터 기반 AI 채팅/롤플레이 앱.**

> 개발 중 — 코드는 리네임 마디(0.2)에 이 리포로 이사합니다. 지금은 이름 자리표예요.

## 무엇이 다른가

기존 계열(SillyTavern, RisuAI)은 "frontend"를 자칭하지만, 구조적으로는
프론트/백이 강결합된 모놀리스다. MolluAI는 그 결합을 이음매(UI ↔ core RPC)로
절단한 **앱**이다 — 같은 코어가 두 방식으로 배포된다:

| 배포 | 구조 |
|---|---|
| ① Serverless | 브라우저가 전부 — core + PGlite(WASM PostgreSQL), 서버 없음 |
| ② Server | 서버가 core·PostgreSQL 18(+pgvector)·WAL-G 백업을 소유, 브라우저는 thin client |

- 저장은 처음부터 SQL (PostgreSQL-first) — 메시지는 content-addressed 3-테이블(git 모델)
- 변경 전파는 커서 기반 catch-up이 본체, SSE는 포그라운드 가속 — 모바일 제약에서 도출
- 프롬프트 조작은 [mollu](https://github.com/shittim-plana/mollu) 부품 시스템 위에 (예정)

## License

코드 이사 시 확정.
