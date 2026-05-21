# 배현성 (Bae Hyeon Seong) — 통합 포트폴리오

> Unity 게임 클라이언트에서 시작해 Web Frontend, Mobile App, Backend API, 서비스 운영 콘솔까지 확장한 풀스택 엔지니어입니다.  
> 현재는 종합 콘텐츠 플랫폼 **Talkain / StoryBeginz**에서 메인 프론트엔드 개발과 모바일 앱 운영, 필요한 백엔드 API 개발을 함께 담당하고 있습니다.

- **이름**: 배현성 (Bae Hyeon Seong)
- **이메일**: gustjd8121@gmail.com
- **경력 흐름**: Unity Client → Web/App/Backend Full-stack
- **작성 기준일**: 2026-05-21

---

## 1. 한눈에 보기

| 항목 | 내용 |
|------|------|
| **주요 경력** | 약 4년, 6개 프로덕트 참여 |
| **현재 역할** | 종합 콘텐츠 플랫폼 풀스택 엔지니어 |
| **주력 분야** | Next.js 웹, Expo 모바일 앱, Unity 게임 클라이언트, .NET 백엔드 |
| **강점** | 프론트·앱·백엔드·운영 콘솔을 한 기능 단위로 끝까지 연결 |
| **대표 경험** | SEO/SSR 전환, 실시간 채팅, WebView 앱, 인앱결제, 3D 아바타 빌더, 2D 게임 스킬 시스템 |

---

## 2. 핵심 강점

### 풀스택 수직 슬라이스 처리

한 화면이나 기능을 프론트엔드에서 끝내지 않고, 필요한 API, 모바일 앱 브릿지, 결제 검증, 푸시 알림, 운영 콘솔까지 연결합니다.  
예를 들어 DM 채팅은 프론트 SignalR 클라이언트, 백엔드 Hub, 모바일 마이크 권한, 읽음 표시, 알림 흐름까지 함께 다뤘습니다.

### 운영 중인 서비스의 안전한 개선

새 프로젝트를 만드는 것뿐 아니라 이미 사용자가 있는 서비스의 구조를 안전하게 바꾸는 경험이 많습니다.

- CSR 중심 페이지에 SEO용 SSR 메타데이터와 본문을 점진 적용
- 모바일 WebView 크래시와 키보드 UX 문제 해결
- Addressables / AssetBundle, 스킬 사용 모델, 결제 검증 흐름 등 운영 중 구조 전환

### 개발 외 운영 영역까지 담당

광고, 스토어 출시, 검색 노출, 결제 상품, 구독 알림, 인증, 분석 도구까지 직접 설정하고 운영했습니다.

- Google AdSense / AdMob / Google Ad Manager
- Google Play Console / App Store Connect / Apple Developer Portal
- Google Search Console / sitemap / robots / hreflang
- GCP Pub/Sub / OneSignal / Stripe / Firebase Analytics

---

## 3. 프로젝트 이력

| 기간 | 프로젝트 | 역할 | 주요 성과 | 상세 |
|------|---------|------|----------|------|
| 2022.05 ~ 2022.10 | **LG U+ 메타버스 아바타 빌더** | Unity 클라이언트 | 3D 아바타 파츠 결합, Face Editor, 컬러피커, 에셋 로딩 구조 전환 | [상세](./uplus-avatar-client.md) |
| 2023.08 | **SlimeHunter** | Unity 클라이언트 | 외부 코드베이스에서 멀티샷 스킬과 발사체 확장 구현 | [상세](./SlimeHunter.md) |
| 2024.06 ~ 2024.08 | **BowwowDefence** | Unity 클라이언트 | 스킬/발사체 시스템, 데이터 레이어, 가챠 연출, 인게임 UI 구현 | [상세](./BowwowDefence.md) |
| 2024.09 ~ 현재 | **Talkain / StoryBeginz Web** | 메인 프론트엔드 | 콘텐츠 플랫폼 웹 클라이언트, Reels, 채팅, 결제, SEO/SSR, 다국어 | [상세](./avatarplay-frontend.md) |
| 2024.11 ~ 현재 | **Talkain / StoryBeginz Backend** | 백엔드 협업 | SEO API, 포스트/프로필 API, IAP 검증, SignalR DM, 필터링 | [상세](./avatarplay-chat-api.md) |
| 2025.08 ~ 현재 | **Talkain / StoryBeginz Mobile App** | 앱 메인 운영 | WebView 앱, Android 네이티브 모듈, IAP, 푸시, 듀얼 브랜드 빌드 | [상세](./avatarplay-app.md) |
| 2024 ~ 현재 | **운영 콘솔 / 외부 서비스** | 운영·수익화 | 광고, 앱스토어, SEO, 결제, 인증, 분석 도구 설정과 운영 | [상세](./operations-and-services.md) |

---

## 4. 기술 스택

| 분야 | 기술 |
|------|------|
| **Frontend** | Next.js 15, React 18, TypeScript, App Router, RSC, Redux Toolkit, Jotai, React Query |
| **Mobile** | Expo 53, React Native, expo-router, EAS Build, WebView, Android Native Module |
| **Backend** | .NET 8, C#, REST API, SignalR, JWT, IAP Validation, OneSignal |
| **Game Client** | Unity 2020/2021/2022 LTS, C#, URP, Addressables, AssetBundle, Spine 2D, BlendShape |
| **Operation** | AdSense, AdMob, Google Ad Manager, Google Play Console, App Store Connect, GCP, Search Console |
| **Automation** | GitHub, Notion, Figma, Google Sheet localization, custom agent workflow |

---

## 5. 대표 사례

### 5.1 SEO / SSR 전환을 프론트와 백엔드에서 동시에 처리

Talkain / StoryBeginz는 콘텐츠가 많은 서비스였지만, 클라이언트 렌더링 중심 구조 때문에 검색 노출에 한계가 있었습니다.  
프론트에서는 Next.js SSR 메타데이터와 본문 렌더링을 점진 적용하고, 백엔드에서는 SEO 전용 API와 다국어 hreflang 데이터를 제공하도록 구조를 만들었습니다.

**결과**
- 핵심 페이지의 SEO 기반을 1주일 내 구축
- 운영 중 페이지를 큰 장애 없이 점진 전환
- 작업 중 production 콘솔에 JWT가 노출되는 보안 이슈를 발견하고 차단

관련 문서:
- [웹 프론트엔드](./avatarplay-frontend.md)
- [백엔드 API](./avatarplay-chat-api.md)

### 5.2 모바일 WebView 앱의 네이티브 문제 해결

Expo / React Native 기반 앱에서 WebView를 중심으로 웹 서비스를 감싸는 구조를 운영했습니다. 채팅, 댓글, DM 화면마다 키보드 동작이 달라야 했고, 일반적인 React Native 처리만으로는 한계가 있었습니다.

**해결**
- Android `KeyboardModeModule` 네이티브 모듈 직접 작성
- 화면별 `windowSoftInputMode` 동적 전환
- WebView 백그라운드 복귀 크래시 복구
- Talkain / StoryBeginz 듀얼 브랜드 빌드 설정 정리

관련 문서:
- [모바일 앱](./avatarplay-app.md)

### 5.3 3D 아바타 빌더의 복잡한 파츠 결합 안정화

LG U+ 메타버스 아바타 빌더에서 헤어, 얼굴, 의상, 악세서리, 모자, 수염, 컬러피커, BlendShape가 함께 얽히는 3D 아바타 커스터마이징을 담당했습니다.

**해결**
- 모자/헤어/수염 충돌 처리
- 저장 직후 맨몸 상태로 보이는 로딩 이슈 수정
- 컬러피커와 BlendShape 동시 적용 이슈 해결
- Addressables에서 AssetBundle 기반 로딩 구조로 전환

관련 문서:
- [LG U+ 메타버스 아바타 빌더](./uplus-avatar-client.md)

### 5.4 2D 디펜스 게임의 스킬/발사체 코어 구현

BowwowDefence에서 게임플레이 핵심인 스킬 시스템과 발사체 구조를 담당했습니다.

**해결**
- 단일, 연쇄, 관통, 광역, 부채꼴, 잔류 효과 발사체 구현
- 스킬 사용 모델을 ChargeCount에서 CoolDown 기반으로 재설계
- ScriptableObject 기반 데이터 레이어와 유닛/스킬 보드 UI 구현
- 보물상자 가챠 연출과 결과 보상 흐름 구현

관련 문서:
- [BowwowDefence](./BowwowDefence.md)

---

## 6. 현재 가장 잘할 수 있는 일

| 영역 | 설명 |
|------|------|
| **콘텐츠 플랫폼 프론트엔드** | 피드, Reels, 콘텐츠 뷰어, 프로필, 채팅, 결제, 다국어, SEO를 실제 운영 수준으로 구현 |
| **하이브리드 모바일 앱** | WebView 앱, 앱-웹 브릿지, IAP, 푸시, 권한, 네이티브 모듈, EAS 빌드 운영 |
| **프론트 연계 백엔드** | 프론트 기능을 완성하기 위한 API, DTO, SignalR, 결제 검증, 필터링, SEO API 구현 |
| **Unity 클라이언트** | 아바타 커스터마이징, 스킬/전투 시스템, 데이터 테이블, 가챠 연출, Addressables/AssetBundle |
| **서비스 운영** | 광고, 앱스토어, 검색 노출, 결제 상품, 푸시, 분석, 인증/컴플라이언스 연결 |

---

## 7. 키워드

`Next.js 15` · `React` · `TypeScript` · `SSR/CSR` · `SEO` · `React Native` · `Expo` · `WebView Bridge` · `Android Native Module` · `.NET 8` · `SignalR` · `Unity` · `C#` · `URP` · `AssetBundle` · `BlendShape` · `IAP` · `AdSense` · `AdMob` · `Google Play Console` · `App Store Connect` · `OneSignal` · `Multi-Tenant` · `i18n`

---

## 8. 문서 링크

| 문서 | 설명 |
|------|------|
| [README.md](./README.md) | 포트폴리오 인덱스 |
| [avatarplay-frontend.md](./avatarplay-frontend.md) | Talkain / StoryBeginz 웹 프론트엔드 |
| [avatarplay-app.md](./avatarplay-app.md) | Talkain / StoryBeginz 모바일 앱 |
| [avatarplay-chat-api.md](./avatarplay-chat-api.md) | Talkain / StoryBeginz 백엔드 API |
| [BowwowDefence.md](./BowwowDefence.md) | 2D 디펜스 게임 |
| [uplus-avatar-client.md](./uplus-avatar-client.md) | LG U+ 메타버스 아바타 빌더 |
| [SlimeHunter.md](./SlimeHunter.md) | SlimeHunter 협업 |
| [operations-and-services.md](./operations-and-services.md) | 운영 콘솔 / 외부 서비스 |

