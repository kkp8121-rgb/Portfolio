# 외부 서비스 · 운영 콘솔 작업 (Operations & External Services)

> 개발 외에 **광고 운영 · 스토어 콘솔 · SEO · 결제 인프라 · 분석 · 자격 인증**까지 본인이 직접 처리해온 영역. 단순한 코드 작성을 넘어, 한 명이 **서비스의 전체 운영 라이프사이클**을 책임질 수 있다는 점을 보여주는 별도 섹션.

> 보통 이런 작업은 마케팅 / 운영 / DevOps 담당자가 나누어 처리하지만, 본 프로덕트는 한 명이 클라이언트 코드와 콘솔 운영을 함께 다루는 구조로 진행됨.

---

## 1. 광고 운영 (Ads)

### Google AdSense
- **사이트 승인** — 운영 도메인의 AdSense 사이트 승인 완료 (pending 상태 트러블슈팅 후 통과)
- **광고 슬롯 생성** — In-Feed 슬롯 / Display 슬롯 발급 및 코드 배치
- **Auto Ads 코드 적용** — 페이지 단위 자동 광고 배치 및 검증
- **환경별 운영 트러블슈팅** — staging 환경에서 광고가 placeholder만 표시되던 이슈를 환경변수·광고 ID 분기 정책으로 정리

### Google AdMob (모바일)
- 듀얼 브랜드 각각 앱 등록 및 광고 단위(배너 / 전면 / 보상형) 발급
- 기존 브랜드에서 신규 브랜드로 AdMob 구현 안전 마이그레이션
- 내부 테스트용 광고 ID와 운영 ID 분리 정책 수립

### Google Ad Manager (영상 광고)
- Reels(영상 숏폼) 인스트림 광고 단위 발급
- IMA SDK 클라이언트 통합 및 테스트 광고로 검증
- **AdSense for Video 2026-05-31 EOL 대응** — GAM / 외부 SSP 마이그레이션 검토 및 실행

### 자체 House Ad
- AdSense·GAM 단가가 부족한 구간을 위한 자체 광고 컴포넌트를 함께 운영

---

## 2. SEO · Google Search Console

### 사이트 색인 등록·관리
- 운영 도메인의 Search Console 소유권 등록
- **sitemap.xml 자동 생성 파이프라인** 구축 (빌드 시 자동 생성)
- **robots.txt 환경별 분기** — production은 색인 허용, staging은 noindex
- 5개 언어 `hreflang` 태그 적용

### 색인 트러블슈팅
- Google 검색 결과에서 사이트가 부분적으로 차단되던 이슈 진단·해결
- Search Console 다국어 색인 리포트를 검토해서 미색인 페이지 우선순위 작업 계획 수립
- noindex 헤더·도메인 리다이렉트 정책 일관화

### SEO 메타데이터·구조
- Feed / Reels 페이지 SSR 메타데이터·본문 추가
- 백엔드에 SEO 전용 서비스·컨트롤러를 신설하여 프론트와 함께 안전 전환
- Open Graph / Twitter Card / JSON-LD 검토

---

## 3. Google Play Console (Android)

### 앱 등록·릴리스
- 듀얼 브랜드 각각 앱 등록 / 빌드 업로드 / 내부 테스트 → 프로덕션 배포
- 버전 정책 정착 — version과 versionCode 자동 동기화 규칙

### 인앱 상품·구독 등록
- 가상 재화 단품 상품 등록
- 구독 플랜 등록 (월간 / 연간)
- SKU·가격 정책·국가별 통화 설정

### 결제 알림 인프라 (RTDN)
- **Google Play Subscription Real-Time Developer Notification** 엔드포인트 등록
- GCP Pub/Sub 토픽 연결 + 서버 검증 로직 구현
- 구독 갱신 / 취소 / 환불 이벤트 처리

### 컴플라이언스
- 데이터 보안 양식, 콘텐츠 등급 분류, 광고 ID 권한, FCM 설정

---

## 4. Apple App Store Connect · Developer Portal (iOS)

### 앱 등록·릴리스
- 듀얼 브랜드 각각 앱 등록 / TestFlight → App Store 빌드 업로드
- Xcode 26 빌드 이미지 지정 (EAS Build)
- 빌드 심사 제출 및 거부 사유 대응

### 인앱 상품·구독 등록 (StoreKit)
- Consumable / Subscription 상품 등록
- 가격 단계·국가별 통화 설정
- 구독 그룹 및 플랜 구성

### 인증·키 관리
- p8 키 발급·갱신 (StoreKit 서버 검증용)
- 인증서·프로비저닝 프로파일 관리
- ATT (App Tracking Transparency) 설정 및 iPad 팝업 이슈 해결

### Developer Portal 측
- Bundle ID 발급 (브랜드별 분리), Capability 활성화 (Push / IAP / Sign in with Apple), Associated Domains

### 컴플라이언스
- 개인정보 처리방침 / 이용약관 URL, App Privacy 라벨, Sign in with Apple

---

## 5. GCP (Google Cloud Platform)

- **서비스 계정** 발급·권한 설정 (백엔드의 GCP 권한 예외 처리까지 포함)
- **Pub/Sub** — Google Play 구독 알림 토픽·구독 생성 및 백엔드 엔드포인트 연결
- **클라우드 스토리지** — 영상 업로드 버킷 운영 (AWS S3 혼용 환경에서 자격증명 정책 수립)
- Cloud Translation / Speech 등 API 키 발급 관리

---

## 6. OneSignal (Push)

- 듀얼 브랜드 각각 OneSignal 앱 등록 및 App ID / REST API Key 발급
- **API Key 무중단 Rotate 운영** — 운영 중 키 교체 후 백엔드·앱 양쪽 갱신
- 알림 다국어 validation 에러 트러블슈팅 (이벤트별 키 분리)
- 채팅 / 팔로우 / 좋아요 이벤트별 알림 라우팅 설계

---

## 7. Stripe (웹 결제)

- 결제 흐름 통합 검토 및 CORS 헤더 중복 이슈 트러블슈팅
- 운영 채택 여부와 별개로 통합 코드 정리·검증

---

## 8. 분석·트래킹

- **Firebase Analytics vs Google Analytics 4** 비교 검토 및 이벤트 / 사용자 속성 / 퍼널 설계
- **AppsFlyer** SDK 적용 (게임 프로젝트) — 어트리뷰션 / 마케팅 캠페인 트래킹
- **Facebook SDK** — 마케팅 이벤트·로그인 SDK 통합

---

## 9. 자격·인증 / 컴플라이언스

### 본인인증
- 모바일 본인인증(KMC 등) 통합
- 만 14세 이상 인증 / 청소년 보호 정책

### 사업자 자격 인증
- AdSense / AdMob / Google Play / App Store **결제·지급 정보 등록**
- 사업자 자격 증빙 서류 제출
- 세금 정보 (W-8 / W-9 / Tax Interview)

### 콘텐츠 정책
- NSFW 필터 정책 설계 및 운영, 신고 시스템

---

## 10. 외부 데이터 / 협업 도구

- **Localization Google Sheet** 운영 — 마스터 시트 + Google Sheets API 권한 / 동기화 파이프라인
- 한글 → byte 변환 / 외부 API 한글 전송 대응
- **Notion** — 버그 트래킹 DB 운영, MCP 서버 연동, 일일 보고 자동화 (git → Notion)

---

## 핵심 사례

### 사례 1. AdSense 사이트 승인 통과
**Situation** — 운영 도메인의 AdSense 사이트 승인이 pending 상태로 장기간 진행되지 않음.

**Task** — 광고 매출 라인 오픈 필요. 거부 사유를 사전에 차단.

**Action** — 콘텐츠 / 사이트 구조 / 정책 페이지 점검, `ads.txt` 배치, 도메인 인증 보강.

**Result** — 승인 통과 후 In-Feed / Display 슬롯을 즉시 발급하여 광고 게재 시작.

### 사례 2. 영상 광고 통합 파이프라인 구축
**Situation** — Google이 AdSense for Video(AFV)를 2026-05-31 종료한다고 발표하여 영상 광고 대안이 시급해짐.

**Task** — 종료 시점 전에 GAM / 외부 SSP로 마이그레이션하면서, AdSense·House Ad와의 광고 우선순위를 정리.

**Action**
- Google Ad Manager에서 영상 광고 단위 발급
- 프론트엔드에 IMA SDK 통합 + 테스트 광고로 검증
- AdSense In-Feed / Display 슬롯과 함께 자연 삽입 위치 기획
- 광고 ID / 환경변수 / 코드 변경 / 슬롯 등록을 한 사이클로 마무리

**Result** — AdSense + GAM + House Ad **3단 광고 스택**으로 운영. EOL 이전에 매끄럽게 전환 완료.

### 사례 3. Google Play 구독 알림 인프라 구축
**Situation** — 구독 갱신 / 취소 / 환불 이벤트를 실시간으로 받아 서버 상태와 동기화할 필요.

**Task** — Play Console - GCP - 백엔드 3개 시스템을 연결.

**Action**
- Play Console에서 RTDN(Real-Time Developer Notification) 설정
- GCP에서 Pub/Sub 토픽·구독 생성
- 백엔드에 검증 서비스 엔드포인트 작성 및 연결

**Result** — 결제 모든 흐름이 서버 검증을 거쳐 처리되어, 클라이언트 의존 없는 안전한 구독 운영 가능.

---

## 의의

대부분의 개발자 포트폴리오는 코드 영역에 집중되지만, 실제 서비스 운영은 **위 작업들이 안 되어 있으면 매출이 발생하지 않고 사용자가 찾아오지 않는다.** 본 섹션은 다음을 보여준다.

- **풀라이프사이클 책임**: 코드만 짜는 게 아니라 매출·유입·결제·인증까지 한 명이 끌고 갈 수 있음
- **콘솔 친화도**: AdSense / Play Console / App Store Connect / GCP / Search Console / OneSignal — 각 콘솔의 흐름을 익숙하게 다룸
- **트러블슈팅 능력**: 사이트 승인 pending / staging placeholder / CORS / API Key Rotate / 다국어 색인 등 **외부 시스템 문제도 직접 해결**
- **컴플라이언스 의식**: 자격 인증 / 세금 정보 / 본인인증 / 콘텐츠 정책까지 운영 가능한 수준으로 처리

---

## 키워드

`Google AdSense` · `Google AdMob` · `Google Ad Manager` · `Google IMA SDK` · `Google Play Console` · `RTDN` · `App Store Connect` · `Apple Developer Portal` · `StoreKit` · `p8 Key` · `Provisioning` · `TestFlight` · `EAS Build` · `Google Search Console` · `sitemap.xml` · `robots.txt` · `hreflang` · `OneSignal` · `Stripe` · `Firebase Analytics` · `Google Analytics 4` · `AppsFlyer` · `Facebook SDK` · `GCP Pub/Sub` · `GCP Service Account` · `Cloud Storage` · `KMC 본인인증` · `사업자 자격 인증` · `Tax Interview` · `Google Sheets API` · `Notion API`
