# 외부 서비스 · 운영 콘솔 작업 (Operations & External Services)

> 개발 외에 **광고 운영 · 스토어 콘솔 · SEO · 결제 인프라 · 분석 · 자격 인증**까지 본인이 직접 처리한 작업 모음. 단순 코드 작성을 넘어 **서비스 운영 전체 사이클**을 책임진 경험을 정리.

- **이름**: 배현성 (BHS)
- **활동 기간**: 2024 ~ 2026 (Talkain / StoryBeginz 운영 기간)
- **범위**: 본인이 직접 콘솔 접속하여 처리한 운영 작업

---

## 1. 광고 운영 (Ads)

### 1.1 Google AdSense
| 작업 | 내용 |
|------|------|
| **사이트 승인** | storybeginz.com / talkain 도메인 AdSense 사이트 승인 — pending 상태 트러블슈팅 후 통과 |
| **In-Feed 슬롯 생성** | 슬롯 ID `4687342740` — 피드 자연 삽입형 |
| **Display 슬롯 생성** | 슬롯 ID `2554784838` — 일반 디스플레이 |
| **Auto Ads 코드 적용** | 페이지 단위 자동 광고 코드 임베드 / 검증 |
| **운영 트러블슈팅** | staging 환경에서 placeholder 만 노출되던 이슈 (광고 ID 환경 분기) 해결 |

### 1.2 Google AdMob (모바일)
| 작업 | 내용 |
|------|------|
| **AdMob 앱 등록** | StoryBeginz / Talkain 듀얼 브랜드 각각 등록 |
| **광고 단위 생성** | 배너 / 전면 / 보상형 광고 단위 발급 |
| **브랜드 마이그레이션** | 기존 Talkain → StoryBeginz로 AdMob 구현 이전 |
| **내부 테스트 세팅** | 테스트 앱 / 테스트 광고 ID 분리 운영 |

### 1.3 Google Ad Manager (GAM, 영상 광고)
| 작업 | 내용 |
|------|------|
| **영상 광고 단위 발급** | `/23352908510/reels_video_instream` — Reels 인스트림 영상 광고 |
| **IMA SDK 연동** | 프론트엔드 IMA 클라이언트 적용 + 테스트 광고 검증 |
| **AFV(AdSense for Video) EOL 대응** | 2026-05-31 종료에 맞춰 GAM / 외부 SSP 마이그레이션 검토 |

### 1.4 House Ad (자체 광고)
- AdSense·IMA 단가 부족 구간을 위한 자체 광고 컴포넌트 설계
- Reels / Feed 자연 삽입

---

## 2. SEO · Google Search Console

### 2.1 사이트 색인 등록·관리
- storybeginz.com / talkain 양 도메인의 **Search Console 소유권 등록**
- **sitemap.xml 자동 생성 파이프라인** (빌드 시점에 SEO 파일 생성: `npm run generate-seo`)
- **robots.txt** 환경별 분기 (production / staging — staging은 noindex)
- 다국어 `hreflang` 태그 5개 언어 적용

### 2.2 색인 트러블슈팅
- Google 검색 결과에서 사이트가 차단되던 이슈 발견 → 공식 경로 검증 후 해결
- Search Console 다국어 색인 리포트 검토 + 미색인 페이지 우선순위 작업 계획
- noindex 헤더 + 도메인 리다이렉트 정책 정리

### 2.3 SEO 메타데이터·구조
- Feed / Reels SSR 메타데이터 + 본문 추가
- 백엔드에 `SeoService` 신규 작성, StoryBeginz 전용 SEO 컨트롤러 신설
- 웹툰·콘텐츠 페이지 SEO 개선 (Open Graph / Twitter Card / JSON-LD 검토)

---

## 3. Google Play Console (Android)

### 3.1 앱 등록·릴리스
- StoryBeginz / Talkain **각 브랜드별 앱 등록**
- 빌드 업로드 (EAS Build → AAB → Internal Testing → Production)
- 버전 정책 정착 — version "0.0.X" = versionCode X 동기화

### 3.2 인앱 상품·구독 등록
- 스타(가상 재화) 단품 상품 등록
- 구독 플랜 등록 (월간 / 연간 등)
- 상품 SKU 발급 + 가격 정책 / 국가별 통화 설정

### 3.3 결제 알림 인프라
- **Google Play Subscription Notification** RTDN 엔드포인트 등록
- Pub/Sub 토픽 연결 + 서버 검증 로직 (`GooglePlaySubscriptionNotificationService.cs`)
- 구독 갱신 / 취소 / 환불 이벤트 처리

### 3.4 기타 설정
- 데이터 보안 양식 작성
- 콘텐츠 등급 분류
- 광고 ID 권한 신청
- Google Services 설정 (FCM 등) — `setup-google-services.js` 스크립트로 브랜드별 자동 교체

---

## 4. Apple App Store Connect (iOS)

### 4.1 앱 등록·릴리스
- StoryBeginz / Talkain 각 브랜드별 앱 등록
- EAS Build → TestFlight → App Store 빌드 업로드
- Xcode 26 빌드 이미지 지정
- 빌드 심사 제출 / 거부 사유 대응

### 4.2 인앱 상품·구독 등록 (StoreKit)
- Consumable / Subscription 상품 등록
- 가격 단계(Price Tier) 설정 / 국가별 통화
- 구독 그룹 / 플랜 구성

### 4.3 인증·키 관리
- **p8 키** 발급 / 갱신 (StoreKit 서버 검증용)
- 인증서 / 프로비저닝 프로파일 관리
- ATT (App Tracking Transparency) 설정 + iPad 팝업 이슈 트러블슈팅

### 4.4 컴플라이언스
- 개인정보 처리방침 / 이용약관 URL 등록
- 데이터 사용 라벨 (App Privacy)
- 가족 공유 / 사인 인 위드 애플 설정

---

## 5. Apple Developer Portal

- **개발자 계정 등록** (조직 / 개인)
- Bundle ID 발급 (Talkain / StoryBeginz 분리)
- Capability 활성화 (Push / IAP / Sign in with Apple / Associated Domains)
- 인증서·프로비저닝 관리

---

## 6. GCP (Google Cloud Platform)

### 6.1 서비스 계정·권한
- 서비스 계정 발급 / 권한 설정
- 백엔드의 GCP 권한 없음 예외 처리 (런타임 안전장치)

### 6.2 Pub/Sub
- Google Play 구독 알림 Pub/Sub 토픽 / 구독 생성
- 메시지 처리 엔드포인트 연결

### 6.3 클라우드 스토리지
- 영상 업로드 버킷 운영 (AWS S3 + GCP 혼용 환경)
- Signed URL 발급 정책

### 6.4 API·키 발급
- Cloud Translation / Speech-to-Text 등 API 키 발급 (사용 시점에 따라)

---

## 7. OneSignal (Push)

| 작업 | 내용 |
|------|------|
| **앱 등록** | StoryBeginz / Talkain 각각 등록 |
| **API Key 발급·관리** | App ID + REST API Key |
| **키 Rotate** | 2026-04-17 OneSignal 키 무중단 교체 — Talkain 키 복구 포함 |
| **알림 다국어** | 알림 언어 validation 에러 (key 분리 부족) 트러블슈팅 |
| **알림 라우팅** | 채팅 / 팔로우 / 좋아요 이벤트별 알림 분기 |

---

## 8. Stripe (웹 결제)

- 결제 흐름 설정 검토
- **CORS 헤더 중복 이슈** 트러블슈팅 (`Access-Control-Allow-Origin` 중복 송신)
- (운영 채택 여부와 별개로 통합 코드 정리·검증)

---

## 9. 분석·트래킹

### 9.1 Firebase Analytics / Google Analytics
- Firebase Analytics vs Google Analytics 4 비교 검토
- 이벤트 트래킹 / 사용자 속성 / 퍼널 구성 계획

### 9.2 AppsFlyer (게임)
- BowwowDefence 시기에 AppsFlyer SDK 적용 (어트리뷰션 / 마케팅 캠페인 트래킹)

### 9.3 Facebook SDK
- 마케팅 이벤트 / 로그인 SDK 통합 (게임 프로젝트)

---

## 10. 자격·인증 / 컴플라이언스

### 10.1 본인인증 (KMC 등)
- 모바일 본인인증 통합 — 본인인증 버그 수정 다수
- 만 14세 이상 인증 / 청소년 보호 정책

### 10.2 사업자 자격 인증
- AdSense / AdMob / Play Console 의 **결제·지급 정보 등록**
- 사업자 자격 증빙 서류 제출 (Document submission verification)
- 세금 정보 (W-8/W-9 / Tax Interview)

### 10.3 NSFW / 검열 정책
- 콘텐츠 NSFW 필터 설정 / 해제 정책
- 신고 시스템

---

## 11. Google Sheets / 외부 데이터 연동

- **Localization Google Sheet** 운영 (다국어 텍스트 마스터)
- Google Sheets API 권한·키 관리
- Sheets → Localization.json 자동 동기화 파이프라인 (PowerShell)
- 한글 byte 변환 / 외부 API 한글 전송 대응

---

## 12. Notion / 협업 도구

- 버그 트래킹 Notion DB 운영 (MCP 서버 연동)
- 노션 API 토큰 관리
- 일일 보고 자동화 (git commit → Notion)

---

## 핵심 사례

### Case 1. AdSense 사이트 승인 통과
- **상황**: storybeginz.com AdSense 사이트 승인이 pending 상태로 장기간 머무름
- **행동**: 콘텐츠 / 사이트 구조 / 정책 페이지 점검, ads.txt 배치, 도메인 인증 보강
- **결과**: 승인 통과 → 후속 작업으로 In-Feed / Display 슬롯 발급 및 광고 게재 시작

### Case 2. 영상 광고 통합 파이프라인 구축
- **상황**: AdSense for Video(AFV) 2026-05-31 종료 발표 → 영상 광고 대안 시급
- **행동**: GAM에서 Reels 인스트림 광고 단위 발급(`/23352908510/reels_video_instream`), 프론트엔드에 IMA SDK 통합, AdSense In-Feed / Display 슬롯과 함께 자연 삽입
- **결과**: AdSense + GAM + House Ad 3단 광고 스택 완성. 광고 ID와 코드 변경, .env 환경변수 입력까지 한 사이클 마무리

### Case 3. Google Play 구독 인프라
- **상황**: 구독 갱신·취소 이벤트를 실시간으로 받아 서버 상태 동기화 필요
- **행동**: Play Console에서 RTDN(Real-Time Developer Notification) 설정, GCP Pub/Sub 토픽 생성, 백엔드 `GooglePlaySubscriptionNotificationService` 엔드포인트 연결
- **결과**: 결제 / 갱신 / 환불 모든 흐름이 서버 측 검증으로 안전하게 처리

---

## 키워드

`Google AdSense` · `Google AdMob` · `Google Ad Manager (GAM)` · `Google IMA SDK` · `Google Play Console` · `Google Play Subscription Notification` · `RTDN` · `Apple App Store Connect` · `Apple Developer Portal` · `StoreKit` · `p8 Key` · `Provisioning` · `TestFlight` · `EAS Build` · `Google Search Console` · `sitemap.xml` · `robots.txt` · `hreflang` · `OneSignal` · `Stripe` · `Firebase Analytics` · `Google Analytics 4` · `AppsFlyer` · `Facebook SDK` · `GCP Pub/Sub` · `GCP Service Account` · `Cloud Storage` · `KMC 본인인증` · `사업자 자격 인증` · `Tax Interview` · `Google Sheets API` · `Notion API`
