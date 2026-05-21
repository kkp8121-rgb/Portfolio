# 배현성 (BHS) — Talkain / StoryBeginz Backend API (`avatar_play_chat_api`)

> **.NET 8 / C# 기반 백엔드 API** — 프론트엔드(`avatarplay-frontend`)와 모바일 앱(`avatarplay-app`)에 데이터·실시간 메시징·결제 검증·SEO 페이지를 제공하는 통합 API 서버. 프론트엔드 메인 개발자가 백엔드까지 직접 손대는 풀스택 협업 형태.

- **이름**: 배현성 (BHS / BaeHyeonSeong)
- **이메일**: gustjd8121@gmail.com
- **포지션**: 백엔드 보조 컨트리뷰터 (프론트와 결합되는 영역 직접 수정)

---

## 1. 프로젝트 개요

| 항목 | 내용 |
|------|------|
| **저장소** | `avatar_play_chat_api` |
| **프레임워크** | **.NET 8 / C#** |
| **실시간** | **SignalR Hub** (DM 채팅 / 알림) |
| **결제** | Google Play Subscription · Google IAP · Apple IAP |
| **알림** | OneSignal |
| **인프라** | GCP, Azure (배포), Cloudflare |
| **운영 환경** | stg = 실사용자 트래픽 (별도 prod 없음) |

### 주요 컨트롤러(BHS 작업 영역 중심)

| 컨트롤러 | BHS 수정 횟수 |
|----------|--------------|
| `PostController.cs` | **20회** |
| `ProfileController.cs` | 13회 |
| `IapController.cs` | 8회 |
| `CommonController.cs` | 7회 |
| `CharacterController.cs` | 6회 |
| `StoryBeginzMainPageController.cs` | 6회 |
| `StoryBeginzExploreController.cs` | 5회 |
| `FeedController.cs` | 5회 |
| `ChatMessageController.cs` | 5회 |
| `UniverseController.cs` / `FriendController.cs` / `ContentController.cs` | 각 4회 |

### 주요 서비스

`SeoService.cs` · `GoogleIapService.cs` · `AppleIapService.cs` · `GooglePlaySubscriptionNotificationService.cs` · `OneSignalService.cs` · `DataService.cs` · `JwtTokenService.cs` · `AesGcmEncryptService.cs` · `DeepLService.cs` · `LangChainService` · `OpenAiService.cs` · `FeedScoringService.cs` · `CloudflareService.cs` · `AdMobService.cs`

---

## 2. 정량 기여도

| 항목 | 값 |
|------|-----|
| **활동 기간** | 2024년 11월 18일 ~ 2026년 5월 20일 (약 18개월) |
| **BHS 커밋 수** | **162** |
| **저장소 내 비중** | 4% (전체 4,029 커밋 중) |
| **LOC** | +8,899 / -1,209 (양보다 정확도) |
| **변경 파일** | 238 |

> 양은 작지만 **프론트엔드 변경에 필요한 API 수정·신규 엔드포인트·SEO·결제 검증**을 본인이 직접 처리. 백엔드팀과의 라운드트립 비용을 줄임.

---

## 3. 도메인별 상세 기여

### 3.1 SEO 시스템 (2026 Q2 주력)
**`SeoService.cs` + `StoryBeginzMainPageController.cs` + `StoryBeginzExploreController.cs` 신설**

- Feed / Reels SEO 전용 엔드포인트 추가
- StoryBeginz 전용 컨트롤러 (메인 / Explore / SEO)
- 다국어 hreflang 대응
- 프론트엔드 SSR 메타데이터 + 본문 공급
- sitemap fallback을 StoryBeginz로 전환

### 3.2 포스트 & 커뮤니티 (가장 많이 작업)
**`PostController.cs` 20회**

- `post - share api`, `view api` 신규 (2026-02-02)
- `feed get api` 추가
- **PostInfo** — `isFollow` / `commentCount` / `dislike` 여부 / `LanguageType`
- 리포스트 카운트 차감, 원본 포스트 삭제 시 추천 안 함
- 비공개 포스트 제외 필터, 콘텐츠 포스트 결격사유(NSFW / 삭제 / 비활성화) 처리
- 공모전 랜덤 추출 API
- `CommunityCategoryType` 받아오기
- 포스트 유니버스 작업, 한줄 요약 (한줄 요약 번역 버그 수정 포함)

### 3.3 프로필 시스템
**`ProfileController.cs` 13회**

- **프로필 탭 비공개 항목 `isSelectProfile` 기준 서버 필터링** (2026-05-20)
- 캐릭터 채널 URL 링크 키 수정
- `updatePdInfo` 버그 수정, 회원가입 버그
- 댓글 프로필 타입 분류

### 3.4 결제 시스템 (IAP)
**`IapController.cs` 8회 + 결제 서비스 `Service/PaymentAppService/`**

- `GoogleIapService.cs` 6회 — Google IAP 검증
- `GooglePlaySubscriptionNotificationService.cs` 7회 — 구독 알림 서버
- `AppleIapService.cs` 2회 — Apple IAP 검증
- **본인 콘텐츠 유료 결제 시 스타 차감 방지** (노션 #57 — 2026-05-04)
- iOS IAP 단품 구매 버그 수정
- 구독 갱신 관련, stg 앱 세팅 변경

### 3.5 실시간 채팅 (SignalR)
**`SignalR/RealtimeHubService_DmChat.cs` 6회 + `ChatMessageController.cs` 5회**

- DM Hub 메시지 프로토콜
- DM ID 내려주기, DM 마이크 작업 (음성 녹음)
- DM 친구(맞팔) 제한 해제

### 3.6 데이터·인프라
**`Data/Packet.cs` 23회 (최다), `Data/Data.cs` 13회, `Data/Enum.cs` 7회, `Data/Schema.cs` 6회**

- 패킷 / DTO 정의 (프론트와 동기화)
- 스키마 추가·확장
- `DataService.cs` 10회 — 데이터 액세스 레이어
- 서비스 ID 버그 수정 (멀티 테넌트)

### 3.7 보안·필터링
- **NSFW 필터**, 검열 강화 / 해제 정책
- 차단된 콘텐츠 / 비활성 계정 비노출 (임시조치 → 정책화)
- Share API 401 예외처리
- GCP 권한 없음 예외처리

### 3.8 친구 / 팔로우
**`FriendController.cs` 4회**

- 팔로우 → 언팔 → 팔로우 시 follow insert 데이터 여러 개 생기는 이슈 수정
- Friend 북마크 PD 프로필 통일, url_link_key 발급/중복검사 개선

### 3.9 피드 & Explore
- 인기 대화 캐릭터 챗봇만 노출
- 피드 소스 episode / content 우선 매핑
- 릴스 피드에 visibility / NSFW / 차단 필터 적용
- 릴스 콘텐츠 비디오 URL에 StreamUrl prefix 누락 수정

### 3.10 알림 (OneSignal)
**`OneSignalService.cs` 3회**

- 2026-04-17 OneSignal 키 변경 (Talkain 키 복구 포함)
- SEO·OneSignal 신고 작업
- 레드닷 정렬 / DM 방목록 시 체크

### 3.11 환경 설정 (멀티 테넌트)
- `appsettings.Development.json` 6회
- `appsettings.Staging.json` 6회
- `appsettings.StorybeginzDev.json` 3회
- `appsettings.json` 5회
- v2 → v3 마이그레이션, stg 앱 세팅

---

## 4. 시기별 작업 흐름

| 시기 | 커밋 | 주력 작업 |
|------|------|----------|
| 2024-11 ~ 2025-07 | 9 | 토큰 / 초기 패치 (간헐적) |
| **2025-08** | **24** | iOS IAP 단품 / import 버그 |
| 2025-09 | 16 | 회원가입 / 팔로우 / DM 레드닷 / 마이크 / 주소록 |
| 2025-10 | 12 | v2→v3, gcp 권한 예외, p8 업데이트, stg storybeginz |
| 2025-11 | 6 | 구독 갱신, 결제 앱세팅 토카인 |
| 2025-12 | 1 | (최소) |
| 2026-01 | 3 | 포스트 유니버스, 홈포스트 댓글 카운트 |
| **2026-02** | **17** | **post share/view API, feed get API, 리포스트, 공유, 캐릭터 채널 URL** |
| 2026-03 | 19 | 키 일부 적용, 서비스 아이디 버그, 메인 컨텐츠 조건 |
| **2026-04** | **28** | **OneSignal 키 변경, 공모전 API, NSFW 필터, DM 친구 제한 해제, 영상 업로드 우회** |
| **2026-05** | **26** | **SEO 엔드포인트 / SeoService 신설, 릴스 필터, 본인 콘텐츠 차감 방지, isSelectProfile 필터링** |

---

## 5. 대표 케이스 — 백엔드 SEO 인프라 신설 (2026-05)

- **상황**: 프론트엔드가 SSR로 전환되려면 SEO 메타데이터·본문을 백엔드가 공급해줘야 함.
- **과제**: 기존 컨트롤러를 건드리면 사이드이펙트 가능 → **StoryBeginz 전용 분리**.
- **행동**:
  - `SeoService.cs` 신규 — SEO 메타·본문 생성 로직 일원화
  - `StoryBeginzMainPageController.cs` + `StoryBeginzExploreController.cs` 신설
  - Feed / Reels SEO 엔드포인트 추가
  - 다국어 hreflang 지원
- **결과**: 프론트엔드 SSR 전환이 백엔드 변경 라운드트립 없이 진행됨. **프론트·백 동시 개발자라서 가능한 속도**.

---

## 6. 협업 특징

- **프론트엔드 메인 + 백엔드 보조**라는 1인 풀스택 협업 패턴
- 백엔드의 다른 메인 컨트리뷰터(`forbm1234`, `winpro`, `tr8425` 등)와 분업
- BHS는 본인 프론트 작업에 필요한 **수직 슬라이스 작업**을 백엔드까지 직접 처리하여 라운드트립 비용 제거
- **단기 우회보다 산업 표준 본질안 선호** — sentinel 값 우회 대신 스키마 표준화 같은 근본 해결

---

## 7. 키워드 / 태그

`.NET 8` · `C#` · `SignalR Hub` · `Google IAP` · `Apple IAP` · `Google Play Subscription Notification` · `OneSignal` · `JWT` · `AES-GCM` · `DeepL` · `OpenAI` · `LangChain` · `Cloudflare` · `Multi-Tenant` · `SEO Service` · `NSFW Filter` · `REST API` · `Schema Design` · `IAP Verification`

---

## 8. 메타 정보

- 작성 기준일: **2026-05-21**
- 데이터 출처: `avatar_play_chat_api` git log (`gustjd8121@gmail.com` 기준, 모든 브랜치 `--all`)
- 관련 문서: [avatarplay-frontend.md](./avatarplay-frontend.md), [avatarplay-app.md](./avatarplay-app.md)
