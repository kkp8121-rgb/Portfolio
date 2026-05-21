# 배현성 (BHS) — 개발자 포트폴리오 인덱스

> **풀스택 개발자**. Unity 클라이언트(2022~2024) → Web/App/Backend 풀스택(2024~현재). 6개 저장소에 걸쳐 **누적 3,300+ 커밋, +40만 LOC** 기여.

- **이름**: 배현성 (BHS / BaeHyeonSeong)
- **이메일**: gustjd8121@gmail.com
- **작성 기준일**: 2026-05-21

> 전체 이력을 한 파일로 빠르게 보려면 [integrated-portfolio.md](./integrated-portfolio.md)를 먼저 확인.

---

## 프로젝트 목록 (시간순)

| # | 시기 | 프로젝트 | 영역 | 커밋 | 비중 | 문서 |
|---|------|---------|------|------|------|------|
| 1 | 2022-05 ~ 2022-10 | **LG U+ 메타버스 아바타 빌더** | Unity 2020 / 3D 아바타 | 294 | 32.5% | [uplus-avatar-client.md](./uplus-avatar-client.md) |
| 2 | 2023-08 | **SlimeHunter** (8-Bit Games 협업) | Unity 2021 / 스킬 | 2 | 0.2% | [SlimeHunter.md](./SlimeHunter.md) |
| 3 | 2024-06 ~ 2024-08 | **BowwowDefence** (자체 IP) | Unity 2022 / 2D 디펜스 | 71 | 24.7% | [BowwowDefence.md](./BowwowDefence.md) |
| 4 | 2024-09 ~ 진행 중 | **Talkain / StoryBeginz** Frontend | Next.js 15 / React 18 | 2,690 | 37.5% | [avatarplay-frontend.md](./avatarplay-frontend.md) |
| 5 | 2025-08 ~ 진행 중 | **Talkain / StoryBeginz** Mobile App | Expo 53 / React Native | 59 | **57%** | [avatarplay-app.md](./avatarplay-app.md) |
| 6 | 2024-11 ~ 진행 중 | **Talkain / StoryBeginz** Backend API | .NET 8 / C# | 162 | 4% | [avatarplay-chat-api.md](./avatarplay-chat-api.md) |
| ★ | 2024 ~ 진행 중 | **외부 서비스 · 운영 콘솔 작업** | 광고 / 스토어 / SEO / 결제 / 인증 | — | — | [operations-and-services.md](./operations-and-services.md) |

---

## 누적 정량 지표

| 영역 | 저장소 수 | 총 커밋 | LOC 추가 | LOC 삭제 |
|------|----------|---------|----------|----------|
| **Unity** | 3 | 367 | +39,900,625 (메타 포함) | -640,914 |
| **Web (Next.js)** | 1 | 2,690 | +321,779 | -137,763 |
| **Mobile App (Expo)** | 1 | 59 | +30,279 | -18,111 |
| **Backend (.NET)** | 1 | 162 | +8,899 | -1,209 |
| **합계** | **6** | **3,278** | **+40,261,582** | **-797,997** |

> Unity 쪽 LOC가 큰 이유는 `.meta` 파일 / 에셋 자동 생성 결과 포함. **순수 C#/TS 코드 기준으로도 누적 +37만 줄 이상** 기여.

---

## 기술 스택 (전체)

### 클라이언트
- **Unity** 2020 / 2021 / 2022 LTS · C# · URP · Addressables / AssetBundle · Shader (lilToon) · BlendShape · Spine 2D
- **Next.js 15** (App Router · RSC) · React 18 · TypeScript · Redux Toolkit · Jotai · React Query
- **Expo 53 / React Native** · expo-router · EAS Build · Android Native Module (Java/Kotlin)

### 백엔드
- **.NET 8 / C#** · SignalR Hub · Google IAP · Apple IAP · OneSignal · JWT · AES-GCM
- 외부 서비스: GCP · Cloudflare · DeepL · OpenAI · LangChain

### 협업·도구
- Git · GitHub · Notion · Figma → 코드 자동화 · Claude Code Agent 시스템
- 자체 워크플로우: Plan → Explore → Execute → Verify

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

## 키워드 클라우드

`Unity` · `C#` · `Next.js 15` · `React Native` · `Expo` · `.NET 8` · `TypeScript` · `SignalR` · `Shaka Player` · `Google IMA` · `AdSense` · `AdMob` · `Google IAP` · `Apple IAP` · `OneSignal` · `Addressables` · `BlendShape` · `Avatar Builder` · `Tower Defense` · `Multi-Tenant` · `SSR/CSR` · `SEO` · `WebView Bridge` · `Android Native Module` · `i18n` · `Metaverse` · `LG U+`

---

## 캐리어 라인 요약

```
[3년차 Unity 클라이언트]
2022 ─── 2023 ─── 2024
  │       │       │
  uplus   SlimeHunter  BowwowDefence
  (LG U+) (협업)       (자체 IP)
                       │
                       ↓ 풀스택 전환
                       
[풀스택 — 진행 중]
2024-09 ─────────────── 2026-05
   │
   Talkain / StoryBeginz
   ├─ avatarplay-frontend (Next.js)
   ├─ avatarplay-app      (Expo)
   └─ avatar_play_chat_api (.NET 8)
```

---

## 파일 구조

```
BHS_Portfolio/
├── README.md                       ← 이 파일 (인덱스)
├── integrated-portfolio.md         ← 통합 포트폴리오 (한눈에 보기)
├── uplus-avatar-client.md          ← LG U+ 메타버스 아바타 빌더
├── SlimeHunter.md                  ← 8-Bit Games 협업
├── BowwowDefence.md                ← 자체 IP 2D 디펜스
├── avatarplay-frontend.md          ← 메인 웹 클라이언트 (Next.js)
├── avatarplay-app.md               ← 모바일 앱 (Expo)
├── avatarplay-chat-api.md          ← 백엔드 API (.NET)
└── operations-and-services.md      ← 외부 서비스·운영 콘솔 작업 (개발 외)
```
