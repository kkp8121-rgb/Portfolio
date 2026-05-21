# Talkain / StoryBeginz — 모바일 앱

> Expo 53 / React Native 기반 모바일 앱. 웹 클라이언트를 WebView로 감싸고 네이티브 영역(결제·푸시·권한·광고·키보드 제어)을 브릿지로 연결한 하이브리드 구조. 단일 코드베이스에서 **Talkain × StoryBeginz × iOS × Android**의 4종 빌드를 운영한다.

- **재직 형태**: 자체 서비스 (현직)
- **활동 기간**: 2025년 8월 ~ 진행 중 (약 9개월)
- **역할**: **모바일 앱 단독 운영자급 컨트리뷰터**

---

## 1. 앱 개요

| 항목 | 내용 |
|------|------|
| **앱 타입** | Expo 53 / React Native 하이브리드 앱 (WebView 컨테이너) |
| **빌드 매트릭스** | Talkain × StoryBeginz × iOS × Android |
| **빌드 도구** | EAS Build (Xcode 26 이미지) |
| **스토어** | Google Play / App Store |
| **자체 운영 스크립트** | google-services.json 자동 교체, 버전 동기화, 패키지명 동기화 |

---

## 2. 정량 기여도

| 항목 | 값 |
|------|-----|
| **활동 기간** | 약 9개월 |
| **개인 커밋 수** | **59** |
| **저장소 내 비중** | **57%** (전체 약 104 커밋 중) — 메인 컨트리뷰터 |
| **코드 라인** | +30K / -18K |
| **변경 파일** | 642 |

> 모바일 앱 저장소의 **과반(57%)을 단독 기여**, 출시·운영·네이티브 모듈 작성까지 전담.

---

## 3. 기술 스택

| 분류 | 라이브러리 |
|------|----------|
| 프레임워크 | Expo 53 · React Native · expo-router 5 · React 19 |
| 빌드 | EAS Build · Xcode 26 |
| 결제 | expo-iap (Google Play · App Store) |
| 인증 | Google · Apple · Kakao OAuth |
| 푸시 | OneSignal + expo-notifications |
| 광고 | Google AdMob |
| WebView | react-native-webview (자체 브릿지 프로토콜) |
| 미디어 | expo-av · expo-image · expo-media-library |
| 권한 | expo-contacts · expo-tracking-transparency (ATT) |
| 상태관리 | Jotai |
| **네이티브** | Android Module 자체 작성 (Java / Kotlin) |

---

## 4. 담당 영역

### 4.1 WebView 컨테이너 — 핵심 컴포넌트
앱의 메인 컨테이너. 앱-웹 양방향 메시지 프로토콜 자체 설계.

- 결제 / 푸시 / 키보드 / 노치 / 스크롤 락 / OAuth 콜백 / 권한 요청 통합 처리
- 장시간 백그라운드 후 복귀 시 WebView 크래시 자동 복원 로직 추가
- 빈 src 요청 차단, 콘솔 노이즈 정리

### 4.2 Android 네이티브 모듈 자체 작성
`KeyboardModeModule` — `windowSoftInputMode`를 화면별로 동적 토글하는 네이티브 모듈을 Java/Kotlin으로 직접 작성. Expo Managed Workflow의 한계를 네이티브 영역으로 우회한 사례 ([대표 사례 1](#대표-사례-1-android-네이티브-모듈-직접-작성으로-키보드-ux-문제-해결) 참조).

### 4.3 iOS 안정화
- 화면별 swipe-back 제스처 ON/OFF 토글 (영상·채팅 화면에서 제스처 충돌 방지)
- iPad에서 ATT 팝업이 안 뜨던 이슈 수정
- iOS Adaptive Splash 2-layer 적용
- 접근성 폰트 확대 방지 (앱 UI 깨짐 방지)
- iOS 영상·사진 업로드 크래시 수정

### 4.4 듀얼 브랜드 빌드 시스템
환경별 config 파일을 분리하여 **하나의 코드베이스에서 두 브랜드의 앱**을 각각 빌드.

- 브랜드별 번들 ID / 아이콘 / 스플래시 / Google Services 설정 분리
- 아이콘 5단계 해상도 + Adaptive 2-layer 일괄 갱신
- `google-services.json` 브랜드별 자동 교체 스크립트
- 버전 동기화 자동화 — version "0.0.X"와 buildNumber/versionCode X 항상 일치시키는 규칙 정착

### 4.5 결제 (인앱결제)
expo-iap 기반 통합 결제 훅. Google Play 단품·구독 / Apple StoreKit 단품·구독 모두 처리. 가격 동적 로딩, 서버 검증 연동.

### 4.6 로그인 / 인증
Google · Apple · Kakao 3종 OAuth 통합. 로그인 튕김 이슈 디버깅·해결.

### 4.7 푸시 알림 (OneSignal)
OneSignal Player ID 발급·갱신. 2026-04-17 OneSignal 키 Rotate 무중단 대응.

### 4.8 광고 (AdMob)
AdMob 통합 훅. 브랜드별 광고 ID 분기.

### 4.9 권한 처리
연락처(Contacts), 마이크(DM 음성녹음용), ATT(App Tracking Transparency).

### 4.10 빌드·릴리스 운영
EAS Build 빌드 매트릭스 유지, 스토어 제출, 버전 정책 운영.

---

## 대표 사례 1. Android 네이티브 모듈 직접 작성으로 키보드 UX 문제 해결

**Situation** — DM, 채팅, 댓글 화면마다 키보드가 컨텐츠를 가리거나 가리지 않아야 하는 동작 요구가 달랐음. React Native의 `KeyboardAvoidingView`로는 모든 시나리오를 해결할 수 없었고, Android의 `windowSoftInputMode`를 화면별로 다르게 적용할 방법이 필요했음.

**Task** — Expo Managed Workflow에서 가능한 경로 + Eject 없이 해결.

**Action**
- **`KeyboardModeModule`** Android 네이티브 모듈을 Java/Kotlin으로 직접 작성
- `windowSoftInputMode`를 런타임에 토글하는 메서드 노출
- React Native ↔ Android Native 브릿지로 연결
- 화면별로 적절한 모드를 호출하도록 훅화

**Result** — 화면 진입/이탈 시 자동으로 키보드 모드 전환되어 디자인팀이 요구한 모든 시나리오 충족. Expo 환경의 한계를 네이티브 모듈로 안전하게 확장한 사례.

---

## 대표 사례 2. 모바일 앱 안정화 (2026-05)

**Situation** — 사용자가 앱을 장시간 백그라운드에 두고 돌아오면 WebView가 화이트 스크린 또는 크래시 상태로 진입하는 빈도 발생.

**Task** — 네이티브 영역을 최소 수정하면서 복구.

**Action**
- WebView 라이프사이클 이벤트를 감지해서 장시간 백그라운드 복귀 시 자동 복원 로직 추가
- iOS swipe-back 토글로 영상·채팅 화면에서 제스처 충돌 차단
- Android KeyboardModeModule 자체 네이티브 모듈로 키보드 동작 정상화
- 듀얼 브랜드 빌드 config를 분리하여 두 브랜드 모두 안정 빌드 운영

**Result** — StoryBeginz 0.0.43까지 안정 빌드 운영. version = buildNumber 동기화 규칙 정착으로 빌드 식별 가능성 개선.

---

## 키워드

`Expo 53` · `React Native` · `EAS Build` · `iOS / Android` · `WebView 브릿지` · `Android Native Module` · `Java/Kotlin` · `expo-iap` · `Google IAP` · `Apple IAP` · `OneSignal` · `AdMob` · `OAuth (Google/Apple/Kakao)` · `ATT` · `Adaptive Splash` · `Multi-Brand Build` · `Jotai`
