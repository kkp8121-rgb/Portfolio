# 배현성 (Bae Hyeon Seong) — Software Engineer Portfolio

> **Unity 클라이언트 3년차 → Web/App/Backend 풀스택**으로 전환한 풀스택 엔지니어. 4년간 6개 프로덕트에 걸쳐 클라이언트·서버·모바일 앱을 모두 다뤄왔으며, 현재는 종합 콘텐츠 플랫폼의 **메인 프론트엔드 개발자 + 모바일 앱 단독 운영자**로 재직 중.

---

## At a Glance

| 항목 | 내용 |
|------|------|
| **이름** | 배현성 (Bae Hyeon Seong) |
| **경력** | 약 4년 (2022.05 ~ 진행 중) |
| **주력 분야** | Web Frontend(Next.js) · Mobile App(Expo) · Game Client(Unity) · Backend(.NET) |
| **현재 직무** | 풀스택 엔지니어 — 종합 콘텐츠 플랫폼 |

### 한눈에 보는 강점

- **풀스택 수직 슬라이스 처리** — 같은 기능을 프론트·앱·백엔드 한 명이 끝까지 가져가서 라운드트립 비용 제거
- **운영 콘솔까지 직접 처리** — AdSense / AdMob / Play Console / App Store Connect / Search Console / GCP / OneSignal 등 **개발 외 운영 영역을 한 명이 책임** ([상세](./operations-and-services.md))
- **레거시 → 모던 마이그레이션 경험** — Addressables↔AssetBundle / SSR↔CSR / 결제 모델 재설계 등 운영 중인 시스템의 안전 전환 다수
- **운영 안정성 시야** — P0 보안 이슈(JWT 콘솔 노출) 발견·차단, 모바일 앱 크래시 복구, NSFW·차단 정책 강화 등 살아있는 사용자가 있는 서비스의 안정화 경험
- **네이티브 영역까지** — Android 네이티브 모듈을 직접 작성할 수 있는 수준 (Java/Kotlin)
- **자기 도구화** — 본인 작업 효율을 위해 Claude Code Agent 시스템·자동 로컬라이징 파이프라인·자체 가이드 문서를 구축해서 운영

---

## 프로젝트 이력 (시간순)

| # | 기간 | 프로젝트 | 회사·구조 | 역할 | 상세 |
|---|------|---------|----------|------|------|
| 1 | 2022.05 ~ 2022.10 | **LG U+ 메타버스 아바타 빌더** | LG U+ 협업 / B2B | Unity 클라이언트 (메인) | [상세](./uplus-avatar-client.md) |
| 2 | 2023.08 | **SlimeHunter** | 8-Bit Games 협업 | Unity 클라이언트 (스팟 기여) | [상세](./SlimeHunter.md) |
| 3 | 2024.06 ~ 2024.08 | **BowwowDefence** (2D 디펜스) | 자체 IP | Unity 클라이언트 (게임플레이 코어) | [상세](./BowwowDefence.md) |
| 4 | 2024.09 ~ 진행 중 | **Talkain / StoryBeginz** Web | 자체 서비스 | Frontend 메인 | [상세](./avatarplay-frontend.md) |
| 5 | 2025.08 ~ 진행 중 | **Talkain / StoryBeginz** Mobile App | 자체 서비스 | App 단독 운영 | [상세](./avatarplay-app.md) |
| 6 | 2024.11 ~ 진행 중 | **Talkain / StoryBeginz** Backend | 자체 서비스 | 풀스택 협업 (백엔드 파트) | [상세](./avatarplay-chat-api.md) |
| ★ | 2024 ~ 진행 중 | **외부 서비스 · 운영 콘솔 작업** | 자체 서비스 | 광고 / 스토어 / SEO / 결제 / 인증 직접 운영 | [상세](./operations-and-services.md) |

> 프로젝트 4~6은 동일 프로덕트의 세 레이어(웹·앱·서버)이며, 한 명의 개발자가 세 영역을 모두 직접 다루고 있음.
> ★ 항목은 코드 작업과 별개로 진행한 **운영·콘솔 작업** 모음 — 광고 매출 / 스토어 출시 / 검색 노출 / 결제 인프라까지 한 명이 끌고 가는 능력을 보여주는 별도 섹션.

---

## 기술 스택

### Frontend / Mobile
- **Next.js 15** (App Router, RSC, SSR/CSR) · **React 18** · **TypeScript**
- 상태관리: Redux Toolkit + Redux Persist · Jotai · React Query v5
- 실시간: SignalR Client
- 스타일: SCSS Modules · CSS Variables · Tailwind · MUI · Radix UI
- 미디어: Shaka Player (DASH/HLS) · Google IMA SDK
- **Expo 53 / React Native** · EAS Build · Android Native Module (Java/Kotlin)

### Backend
- **.NET 8 / C#** · SignalR Hub · Google IAP · Apple IAP
- 외부 서비스: OneSignal · Cloudflare · DeepL · OpenAI / LangChain
- 보안: JWT · AES-GCM · NSFW 필터

### Game Client
- **Unity 2020 / 2021 / 2022 LTS** · C# · **URP**
- Addressables / AssetBundle · BlendShape · Spine 2D · NavMeshPlus
- ScriptableObject 기반 데이터 레이어

### 협업·도구
- Git · GitHub · Notion · Figma → 코드 자동화 · Claude Code Agent 자체 구축

### 외부 서비스 · 운영 콘솔 (개발 외 영역)
- **광고**: Google AdSense · AdMob · Google Ad Manager · IMA SDK · House Ad
- **스토어**: Google Play Console · App Store Connect · Apple Developer Portal
- **SEO**: Google Search Console · sitemap / robots / hreflang 자동화
- **결제 인프라**: Google Play RTDN · StoreKit · Stripe · GCP Pub/Sub
- **인증·키 관리**: p8 · Provisioning · OneSignal API Key Rotate
- **분석**: Firebase Analytics · Google Analytics 4 · AppsFlyer · Facebook SDK
- **자격·컴플라이언스**: 사업자 자격 인증 · Tax Interview · KMC 본인인증 · NSFW 정책

자세한 내역은 [operations-and-services.md](./operations-and-services.md) 참조.

---

## 핵심 사례 3건 (Highlights)

### 1. 백엔드와 프론트엔드를 동시에 손대서 SEO 인프라를 1주일 안에 안전 전환 (2026 Q2)
운영 중인 서비스에서 `'use client'` 남발로 SEO 약점이 있었으나, 한 번에 떼면 인증·하이드레이션·캐시 등 다발성 버그가 우려되는 상황. 7가지 안티패턴을 정리한 자체 가이드 문서를 만들고, 백엔드에 SEO 전용 서비스/컨트롤러를 신설하여 프론트와 백엔드를 동시에 한 명이 진행. 부수효과로 **production 콘솔에 JWT가 노출되던 P0 보안 이슈를 발견·차단**.

### 2. Android 네이티브 모듈 직접 작성으로 키보드 UX 문제 해결 (2026-05)
DM·채팅·댓글 화면마다 키보드 동작 요구가 달라서 일관된 RN 솔루션이 없었음. **`KeyboardModeModule`** 이라는 Android 네이티브 모듈을 직접 Java/Kotlin으로 작성해서 `windowSoftInputMode`를 화면별로 동적 토글. Expo Managed Workflow의 한계를 네이티브로 우회한 케이스.

### 3. 메타버스 아바타 빌더의 합성 엣지케이스 카탈로그 (2022-08)
LG U+ 메타버스 아바타 빌더에서 모자/수염/맨몸/컬러피커 충돌, 저장 직후 찰나 맨몸 로딩, 단색 배경 캐릭터 사라짐 등 **사용자 시나리오 기반 결함**을 한 달 동안 집중 잡아냄. 다대다 파츠 결합 시스템의 안정성을 본인이 주도해서 운영 가능한 수준으로 끌어올림.

---

## 협업·엔지니어링 가치관

- **단기 우회보다 산업 표준 본질안 선호**: sentinel 값 우회 같은 임시 코드보다 스키마 표준화 같은 근본 해결을 선택. 백엔드 협업 비용을 감수하더라도 옳은 길로 감
- **자기 도구화**: 반복되는 검증(미번역 텍스트 / 하드코딩 색상 / 공용 컴포넌트 / 인코딩 / 다국어 라우팅)을 자체 Agent 시스템으로 자동화
- **운영 의식**: prod와 stg를 구분하지 않는 환경에서 작업한다는 가정으로 항상 stg를 실사용자 트래픽 환경으로 다룸. 보안 로그·결제 검증·콘텐츠 필터를 우선순위 상단에 둠
- **수직 슬라이스 처리력**: 익숙하지 않은 외부 코드베이스(8-Bit Games SlimeHunter)에도 단일 영업일 내에 신규 스킬 기능 한 건을 깔끔하게 마무리한 경험

---

## 문서 구성

```
이 폴더/
├── README.md                       ← 이 파일
├── avatarplay-frontend.md          ← 종합 콘텐츠 플랫폼 — 웹
├── avatarplay-app.md               ← 종합 콘텐츠 플랫폼 — 모바일 앱
├── avatarplay-chat-api.md          ← 종합 콘텐츠 플랫폼 — 백엔드
├── BowwowDefence.md                ← 자체 IP 2D 디펜스 게임
├── uplus-avatar-client.md          ← LG U+ 메타버스 아바타 빌더
├── SlimeHunter.md                  ← 8-Bit Games 협업 (스팟 기여)
└── operations-and-services.md      ← 외부 서비스·운영 콘솔 작업 (개발 외)
```

각 문서는 다음 구조로 통일:
**개요 → 정량 기여도 → 기술 스택 → 도메인별 상세 기여 → 대표 사례(STAR) → 키워드**

---

## 연락처

- 이메일: gustjd8121@gmail.com

---

*문서 작성 기준일: 2026-05-21*
