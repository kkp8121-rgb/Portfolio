# 배현성 (BHS) — Talkain / StoryBeginz Frontend (`avatarplay-frontend`)

> **Next.js 15 기반 종합 콘텐츠 플랫폼 메인 프론트엔드** — 영상·웹툰·소설·캐릭터 챗·쇼츠·커뮤니티 포스트를 통합한 멀티 콘텐츠 서비스의 웹 클라이언트. 단일 코드베이스에서 환경변수 분기로 Talkain·StoryBeginz 두 브랜드 동시 운영.

- **이름**: 배현성 (BHS / BaeHyeonSeong)
- **이메일**: gustjd8121@gmail.com
- **포지션**: 프론트엔드 메인 컨트리뷰터

---

## 1. 프로젝트 개요

| 항목 | 내용 |
|------|------|
| **저장소** | `avatarplay-frontend` |
| **서비스** | **Talkain** / **StoryBeginz** (멀티 테넌트) |
| **분기 방식** | `NEXT_PUBLIC_SERVICE_ID` 환경변수 (`talkain` \| `default`) |
| **콘텐츠 타입** | 영상(시리즈/싱글) · 웹툰 · 소설 · 캐릭터 챗(AI) · 쇼츠(릴스) · 커뮤니티 포스트 · 공모전 |
| **사용자 타입** | 일반 사용자 / 캐릭터 / 채널 / PD(프로듀서) |
| **수익화** | 구독 · 인앱결제(스타 재화) · 광고(AdSense/IMA/AdMob/House Ad) |

---

## 2. 정량 기여도

| 항목 | 값 |
|------|-----|
| **활동 기간** | 2024년 9월 20일 ~ 2026년 5월 20일 (**20개월 진행 중**) |
| **BHS 커밋 수** | **2,690** |
| **저장소 내 비중** | **37.5%** (전체 7,173 커밋 중) |
| **LOC** | **+321,779 / -137,763** |
| **변경 파일** | 8,974 |

> 단일 컨트리뷰터로서 **약 40%에 가까운 기여**, 누적 약 **32만 줄 코드 추가**.

---

## 3. 기술 스택

| 분류 | 라이브러리·도구 |
|------|----------------|
| 프레임워크 | **Next.js 15** (App Router, RSC, Middleware) · React 18 |
| 언어 | TypeScript 5.6 |
| 전역 상태 | **Redux Toolkit + Redux Persist** (user/session/currency/content 등) |
| 로컬 상태 | **Jotai** (auth 팝업, drawer, post 작성 등) |
| 데이터 페칭 | **React Query v5** + Axios 인스턴스 |
| 실시간 | `@microsoft/signalr` (SignalR Client) |
| 인증 | **Supabase Auth** + JWT + OAuth (Google / Apple) |
| 스타일 | SCSS Modules · CSS Variables(디자인 토큰) · Tailwind v3 · MUI v6 · Radix UI · Emotion |
| 미디어 | **Shaka Player** (DASH/HLS) · Google IMA SDK |
| 광고 | Google AdSense · IMA · House Ad |
| 에디터 | CodeMirror 6 (다중 언어) · DnD Kit |
| 결제 | 자체 결제 검증 + 백엔드 IAP 서버 검증 |
| i18n | 자체 `getLocalizedText` + Google Sheet 자동 동기화 (5개 언어) |

---

## 4. 도메인별 상세 기여

### 4.1 콘텐츠 생성·뷰어 시스템
- **시리즈 / 에피소드 / 싱글 / 웹툰 / 영상** 통합 CRUD
- 에피소드 **분기 트리거 시스템** (`ChangeBehaviour.tsx` 41회)
- 대화 템플릿, 드롭다운 UI, 에피소드 복사 / 순서 변경 등 작가 도구
- **Shaka Player 기반 영상 뷰어** — `ViewerContent.tsx` 79회 · `ShakaPlayerWrapper.tsx` 59회
- 미디어 업로드 — iOS 크래시 / 비디오 / 웹툰 / 이미지 멀티 포맷
- PD(프로듀서) 모드: 콘텐츠 제작 권한, 초안 저장, 공개 범위

**대표 파일**: `CreateSeriesContent.tsx`, `CreateContentEpisode.tsx`, `SeriesDetail.tsx`, `ViewerContent.tsx`, `ShakaPlayerWrapper.tsx`, `VideoContentUpload.tsx`, `WebtoonContentUpload.tsx`

### 4.2 홈피드 & Reels (영상 숏폼) — 시그니처 영역
- **`ReelsContent.tsx` 195회 / `ReelsLayout.tsx` 144회** — 단일 컴포넌트로 압도적 최다 수정
- 무한 스크롤 + 자동 재생 + 일시 mute + 인터랙션 최적화
- 광고 자연 삽입 (AdSense `<ins>` 중복 push 방지, IMA 테스트 광고, 자체 House Ad)
- 노치(세이프에리어) 대응, 핀치 줌 방지
- 콘텐츠 visibility / NSFW / 차단 필터

### 4.3 프로필 시스템
- **`ProfileBase.tsx` 149회** — 다층 프로필(일반/캐릭터/채널/PD) 통합 컴포넌트
- 탭별 비공개 항목 서버 필터링
- `SelectProfile` 드로어 기반 활성 프로필 전환 시 탭/권한 자동 갱신
- 팔로우 / 친구(맞팔) / 차단 / 추천 / 북마크
- `PostCard.tsx` 64회 — 게시물 카드

### 4.4 채팅 시스템 (실시간)
- **캐릭터 챗 (AI)** + **DM 채팅 (1:1 실시간)**
- **SignalR Hub** 클라이언트(`useSignalR` 23회) 연동
- DM **음성 녹음**, 채팅방 레드닷 정렬
- **키보드/스크롤 OS 분기** — `@hooks/platform` 훅으로 격리
- `ChatBar.tsx` 52회, `FooterChat.tsx` 43회, `ChatPage.tsx` 41회

### 4.5 결제 & 구독
- **`SubscriptionPlan.tsx` 49회**, `Shop.tsx` 61회
- 구독 갱신, 결제 검증, 본인 콘텐츠 유료 결제 시 스타 차감 방지
- 구독 플랜 등급 제한, 결제 내역, 지갑 / 카드 등록 UI

### 4.6 게이미피케이션
- 상점(`Shop.tsx` 61회), 스타(가상 재화), 시간 보상, 데일리 리워드
- 구독 플랜별 혜택, 상점 알람 / 알림

### 4.7 SEO & SSR/CSR 최적화 (2026 Q2 주력)
- **Feed / Reels SSR SEO** 메타데이터 + 본문 추가
- **`'use client'` 제거 / SSR ↔ CSR 전환 가이드** 자체 문서화 — 7가지 안티패턴 정리:
  1. 이중 호출 · 2. 권한 미스매치 · 3. 하이드레이션 · 4. 토큰 캐시 오염 · 5. 환경변수 · 6. 브라우저 API · 7. ISR stale
- character / content/single / content/series — SSR fetch 제거 후 CSR-only 전환
- Feed / Reels — SSR 메타데이터 + 본문만 추가, 인터랙션은 CSR 유지
- sitemap / robots 자동 생성, 다국어 `hreflang`

### 4.8 보안 강화
- **P0 보안 패치**: production SignalR LogLevel을 Warning으로 강제 (JWT 콘솔 노출 차단)
- XSS 방지: `innerHTML` 제거 (CharacterIntroBubble 등)
- Axios 401 인터셉터 + Supabase 세션 기반 자동 토큰 갱신, 중복 요청 방지(5초)
- NSFW 필터, 검열 강화, 신고 시스템, 본인인증
- 빈 `img/video` src 로 인한 페이지 재요청 방지

### 4.9 다국어(i18n)
- 5개 언어(ko/en/ja/zh-CN/zh-TW) URL 라우팅 — `/[lang]/...`
- `getLocalizedText('(&)텍스트')` 패턴 + `(&)` 접두어 미번역 자동 탐지
- **`pushLocalizedRoute`** 헬퍼 — 모든 페이지 이동 시 언어 자동 보정
- **Google Sheet → Localization.json 자동 동기화 파이프라인** (PowerShell, 한글 byte 변환 대응)

### 4.10 광고 시스템
- AdSense `<ins>` 중복 push 방지 + sponsored 라벨 통일
- IMA SDK 테스트 광고 자연 삽입(피드 / 릴스)
- House Ad 자체 광고 컴포넌트
- **AdSense for Video(AFV) 2026-05-31 종료** 대응 → GAM / 외부 SSP 마이그레이션 검토

### 4.11 WebView 브릿지 (앱-웹 통신)
- **`useWebview.tsx` 102회** — 앱-웹 통합 진입점
- 결제 / 푸시 / 키보드 / 노치 / 스크롤 락 / OAuth 콜백 / 권한 요청 통합 프로토콜

### 4.12 검색
- `SearchBoardV2MainPage.tsx` 37회 — 통합 검색
- `ChatSearchMain.tsx` 65회 — 채팅 내 검색

---

## 5. 시기별 작업 흐름

| 시기 | 월평균 커밋 | 주력 작업 |
|------|------------|----------|
| 2024 Q4 | ~75 | 초기 세팅, 에피소드 / 트리거 시스템, 콘텐츠 생성 UI |
| 2025 Q1 | ~78 | 피드 / 댓글 / 콘텐츠 확장, iOS 대응 |
| 2025 Q2 | ~135 | 채널, 상점, 구독 |
| 2025 Q3 | ~174 | **DM(SignalR) 1차 완성**, 캐릭터 챗, 차단 / 회원탈퇴 / 추천인 |
| 2025 Q4 | ~167 | QA, 본인인증, 결제 검증, 채널 다국어 |
| 2026 Q1 | ~120 | 노치 대응, WebView 정비, 결제 검증 |
| **2026 Q2** | **~192** | **SEO/SSR 전환, JWT 보안 강화, AdSense/IMA 통합** — 역대 최고치 |

---

## 6. 대표 케이스 — SSR/CSR 안전 전환 + SEO 강화 (2026 Q2)

- **상황**: `'use client'` 남발로 SEO 약점. 봇이 본문을 인덱싱하지 못해 검색 노출 저조.
- **과제**: 한 번에 `'use client'`를 떼면 권한 미스매치 / 하이드레이션 / 토큰 캐시 오염 등 다발성 버그 발생 우려.
- **행동**:
  - **자체 가이드 문서화**: `'use client'` 제거 시 7가지 안티패턴 정리 → `.claude/skills/use-client-removal/` 스킬로 정형화
  - **점진적 전환**: character / single / series — SSR fetch 제거하고 CSR-only로 안전 전환
  - Feed / Reels — SSR 메타데이터 + 본문만 추가하고 인터랙션은 클라이언트로 유지
  - sitemap fallback을 StoryBeginz로 전환 + 다국어 hreflang
  - 안전성 점검: id=0 차단, Public 필터, profile CSR-only 전환
- **결과**: 1주일 내 핵심 페이지 SSR 메타데이터 전면 적용. 보안 부수효과로 **JWT가 production 콘솔에 노출되던 P0 이슈도 함께 발견·차단**.

---

## 7. 키워드 / 태그

`Next.js 15` · `App Router` · `RSC` · `React 18` · `TypeScript` · `SSR/CSR` · `SEO` · `Redux Toolkit` · `Jotai` · `React Query` · `SignalR Client` · `Supabase` · `Shaka Player` · `Google IMA` · `AdSense` · `Tailwind` · `MUI` · `Radix UI` · `i18n 5개 언어` · `Localization Pipeline` · `Multi-Tenant` · `JWT 보안` · `Claude Agent`

---

## 8. 메타 정보

- 작성 기준일: **2026-05-21**
- 데이터 출처: `avatarplay-frontend` git log (`gustjd8121@gmail.com` 기준, 모든 브랜치 `--all`)
- 관련 문서: [avatarplay-app.md](./avatarplay-app.md), [avatarplay-chat-api.md](./avatarplay-chat-api.md)
