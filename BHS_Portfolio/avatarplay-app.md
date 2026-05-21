# 배현성 (BHS) — Talkain / StoryBeginz Mobile App (`avatarplay-app`)

> **Expo 53 / React Native 기반 모바일 앱** — 웹 클라이언트를 WebView로 감싸고, 네이티브 영역(결제·푸시·권한·광고·키보드 제어)을 브릿지로 연결한 하이브리드 앱. 단일 코드베이스에서 Talkain·StoryBeginz 듀얼 빌드.

- **이름**: 배현성 (BHS / BaeHyeonSeong)
- **이메일**: gustjd8121@gmail.com
- **포지션**: 모바일 앱 메인 컨트리뷰터

---

## 1. 프로젝트 개요

| 항목 | 내용 |
|------|------|
| **저장소** | `avatarplay-app` |
| **타입** | Expo 53 / React Native **하이브리드 앱** (WebView 컨테이너) |
| **빌드 매트릭스** | **Talkain × StoryBeginz × iOS × Android** (4 빌드) |
| **빌드 도구** | EAS Build (Xcode 26 이미지) |
| **자체 스크립트** | `setup-google-services.js`, `bump-version.js`, `sync-package-name.js` |

---

## 2. 정량 기여도

| 항목 | 값 |
|------|-----|
| **활동 기간** | 2025년 8월 14일 ~ 2026년 5월 11일 (**약 9개월**) |
| **BHS 커밋 수** | **59** |
| **저장소 내 비중** | **57%** (전체 104 커밋 중) — 메인 컨트리뷰터 |
| **LOC** | +30,279 / -18,111 |
| **변경 파일** | 642 |

> **앱 저장소 과반(57%) 기여**, 사실상 단독 운영자급. 출시·운영·네이티브 모듈 작성까지 전담.

---

## 3. 기술 스택

| 분류 | 라이브러리 |
|------|----------|
| 프레임워크 | **Expo 53** · React Native (`react@19`) · expo-router 5 |
| 빌드 | **EAS Build** (iOS / Android), Xcode 26 |
| 결제 | **expo-iap 2.4.2** (Google Play / Apple App Store) |
| 인증 | `@react-native-google-signin/google-signin` · `@react-native-kakao/user` · Apple Authentication |
| 푸시 | `expo-notifications` + **OneSignal** (`onesignal-expo-plugin`) |
| 광고 | Google **AdMob** |
| WebView | `react-native-webview` (자체 브릿지) |
| 미디어 | `expo-av`, `expo-image`, `expo-media-library` |
| 파일 | `expo-file-system`, `expo-image-picker` |
| 권한 | `expo-contacts`, `expo-tracking-transparency` (ATT) |
| 상태 | **Jotai** 2.x |
| 햅틱 / UX | `expo-haptics`, `expo-blur`, `expo-navigation-bar` |

---

## 4. 도메인별 상세 기여

### 4.1 WebView 컨테이너 — 시그니처 영역
**`components/Webview/Webview.tsx` 36회 수정 (최다)**

- 앱-웹 양방향 메시지 프로토콜 자체 설계
- 결제 / 푸시 / 키보드 / 노치 / 스크롤 락 / OAuth 콜백 / 권한 요청 통합 처리
- **WebView 크래시 / 장시간 백그라운드 복귀 자동 복원** (2026-05)
- 빈 src 요청 차단, 콘솔 노이즈 정리

### 4.2 Android 네이티브 모듈 — `KeyboardModeModule`
**자체 작성 네이티브 모듈** (2026-05-11)

- **`windowSoftInputMode` 동적 토글** — Java/Kotlin
- DM / 채팅 / 댓글 화면에서 키보드 동작이 다르게 필요한 시나리오 대응
- React Native ↔ Android Native 브릿지 직접 구현

### 4.3 iOS 안정화
- **iOS swipe-back 토글** (화면별 ON/OFF) — 영상 / 채팅 화면에서 제스처 충돌 방지
- ATT (App Tracking Transparency) iPad 팝업 안나옴 이슈 수정
- iOS Adaptive Splash 2-layer 적용
- 휴대폰 접근성 폰트 확장 대응 (텍스트 확대 방지)
- iOS 영상 업로드 크래시 / 사진 업로드 크래시 수정

### 4.4 듀얼 브랜드 빌드 (Talkain ↔ StoryBeginz)
- **`config/app.talkain.ts` / `config/app.storybeginz.ts`** — 환경별 설정 분리
- **`app.config.ts` 19회 수정** — Expo 동적 config (브랜드별 번들 ID / 아이콘 / 스플래시)
- 앱 아이콘 (mipmap-hdpi ~ xxxhdpi 5단계) + adaptive 2-layer 스플래시 9회 일괄 갱신
- `setup-google-services.js` 자체 스크립트 — google-services.json 브랜드별 자동 교체
- `bump-version.js` — version "0.0.X" = buildNumber/versionCode X 동기화 자동화

### 4.5 결제 (인앱결제)
- **`hooks/usePurchase.tsx` 10회** — expo-iap 기반 통합 결제 훅
- Google Play Subscription / Apple StoreKit 단품 / 구독
- iOS IAP 단품 구매 버그 수정
- 스토어에서 가격 가져오기 (Server-side validation 연동)

### 4.6 로그인 / 인증
- **`hooks/useLogin.tsx` 9회**
- **Google / Apple / Kakao** OAuth 통합
- 로그인 튕김 이슈 디버깅 / 수정

### 4.7 푸시 알림 (OneSignal)
- `hooks/useOneSignal.tsx` — OneSignal Player ID 발급 / 갱신
- 2026-04-17 OneSignal 키 Rotate 대응 (Talkain 키 복구 포함)

### 4.8 광고 (AdMob)
- `hooks/useAds.tsx` — AdMob 통합 훅
- StoryBeginz / Talkain 별 광고 ID 분기

### 4.9 권한 처리
- `hooks/useContacts.tsx` — 연락처 (`expo-contacts`)
- 마이크 권한 (DM 음성녹음 연동)
- ATT (App Tracking Transparency)

### 4.10 빌드·릴리스 운영
- StoryBeginz 0.0.43까지 안정 빌드 운영
- EAS Build iOS 빌드 이미지 (xcode-26) 지정
- 빌드 버전 자동 동기화 정책 정착

---

## 5. 시기별 작업 흐름

| 시기 | 커밋 | 주력 작업 |
|------|------|----------|
| 2025-08 | 8 | 앱 초기 세팅, ATT iPad 이슈, 폰트 확장 대응 |
| 2025-09 | 8 | Contacts, 마이크 권한, talkain → storybeginz 브랜드 분기 |
| 2025-10 | 7 | usePurchase, 스토어 가격, 빌드 작업 |
| 2025-11 | 14 | 구글 로그인, 아이콘 / 브랜드 변경, 빌드 |
| 2025-12 | 1 | (활동 적음) |
| 2026-02 | 4 | 작업 재개 |
| 2026-03 | 3 | WIP |
| 2026-04 | 7 | 스플래시, 앱 아이콘, AdMob 테스트, 로그인 튕김 |
| **2026-05** | **7** | **WebView 크래시 복구, KeyboardModeModule(Android Native), 도메인 변경, 0.0.43 빌드** |

---

## 6. 대표 케이스 — 모바일 앱 안정화 (2026-05)

- **상황**: WebView가 장시간 백그라운드 후 복귀 시 화이트 스크린 / 크래시. 키보드 모드가 화면별로 다르게 요구되는 시나리오.
- **과제**: Expo Managed Workflow에서 네이티브 영역을 최소 손대고 해결할 경로 찾기.
- **행동**:
  - WebView 크래시 / 장시간 백그라운드 복귀 자동 복원 로직 추가
  - iOS swipe-back 토글 (화면별 ON/OFF)
  - **Android `KeyboardModeModule` 자체 네이티브 모듈 작성** — windowSoftInputMode 동적 토글 (Java/Kotlin 브릿지)
  - Talkain ↔ StoryBeginz 듀얼 빌드 config 분리 (`app.config.ts` 19회)
- **결과**: StoryBeginz 0.0.43까지 안정 빌드 운영. **version = buildNumber 동기화 규칙** 정착.

---

## 7. 키워드 / 태그

`Expo 53` · `React Native` · `EAS Build` · `iOS / Android` · `WebView 브릿지` · `Android Native Module` · `Java/Kotlin` · `expo-iap` · `Google IAP` · `Apple IAP` · `OneSignal` · `AdMob` · `OAuth (Google/Apple/Kakao)` · `ATT` · `Adaptive Splash` · `Multi-Brand Build` · `Jotai`

---

## 8. 메타 정보

- 작성 기준일: **2026-05-21**
- 데이터 출처: `avatarplay-app` git log (`gustjd8121@gmail.com` 기준, 모든 브랜치 `--all`)
- 관련 문서: [avatarplay-frontend.md](./avatarplay-frontend.md), [avatarplay-chat-api.md](./avatarplay-chat-api.md)
