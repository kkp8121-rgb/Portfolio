# 배현성 (BHS) — LG U+ 메타버스 아바타 빌더 (`uplus-avatar-client`)

> **메타버스 플랫폼 3D 아바타 커스터마이징 클라이언트** — LG U+ 메타버스 사업의 아바타 빌더 모듈. 5개월간 단일 컨트리뷰터로서 약 1/3 비중을 차지한 메인 개발자급 기여.

- **이름**: 배현성 (BHS / BaeHyeonSeong)
- **이메일**: gustjd8121@gmail.com
- **소속 GitHub Org**: ovencode-new
- **포지션**: Unity 클라이언트 개발자

---

## 1. 프로젝트 개요

| 항목 | 내용 |
|------|------|
| **프로젝트명** | uplus-avatar-client |
| **클라이언트** | LG U+ (메타버스플랫폼기술팀과 협업, `*@lgupluspartners.co.kr` 컨트리뷰터 참여) |
| **장르 / 도메인** | 3D 아바타 빌더 / 메타버스 클라이언트 모듈 |
| **엔진** | Unity 2020.3.14f1 LTS |
| **렌더 파이프라인** | URP 10.5.0 |
| **타깃 플랫폼** | Android / iOS (모바일 메타버스 앱 내 모듈) |
| **저장소** | `github.com/ovencode-new/uplus-avatar-client` (private) |

### 사용 패키지·SDK

| 분류 | 라이브러리 |
|------|----------|
| 리소스 로딩 | **Addressables 1.16.19** → **AssetBundle 시스템**으로 마이그레이션 |
| 렌더링 | URP 10.5.0, **lilToon**(셀쉐이딩 셰이더, 후 제거) |
| UI | TextMeshPro 3.0.6, UGUI |
| 기타 | Burst Compiler 1.4.11, Timeline 1.4.8, 2D Sprite Shape 5.1.7 |
| 컬러 피커 | UnityUIColorPicker (3rd-party) |
| 의존성 | ExternalDependencyManager (Google Play Plugins) |

---

## 2. 정량 기여도

| 항목 | 값 |
|------|-----|
| **활동 기간** | 2022년 5월 24일 ~ 10월 25일 (**약 5개월**) |
| **BHS 커밋 수** | **294** |
| **저장소 내 비중** | **32.5%** (전체 905 커밋 중) |
| **LOC** | +946,948 / -328,463 (Unity 메타·에셋 포함) |
| **변경 파일** | 3,141 |

> 13명 컨트리뷰터 중 **단일 개발자로 약 1/3 기여**, 아바타 객체 관리·UI·페이스 에디터·에셋번들 등 클라이언트 코어를 폭넓게 담당.

---

## 3. 도메인별 상세 기여

### 3.1 아바타 객체 관리 시스템 — 시그니처 영역
**`ObjectManager_Avatar.cs` 29회 수정 (최다)**

- 아바타 파츠(헤어 · 얼굴 · 의상 · 악세서리 · 신발) 슬롯 기반 결합 / 교체
- 모자 ↔ 헤어 충돌 처리, 맨몸 아바타 폴백
- 저장 직후 찰나 맨몸 로딩 이슈 대응
- Animator Rebind, LOD 거리 조절
- 단색 배경에서 캐릭터 사라짐 버그 수정

### 3.2 아바타 빌더 메인 UI
**`UIBuilder.cs` 24회 + `Game/UIBuilder.cs` 18회 — 두 모듈 모두 BHS가 메인 담당**

- 메인 빌더 화면 — 카테고리 / 서브카테고리 / 색상 / 아이템 그리드
- `UIBuilderScrollView.cs` 12회, `UIBuilderScrollItem.cs` 7회 — 무한 스크롤 그리드 컴포넌트
- `UIBuilderSubCategory.cs` 6회 — 카테고리 탭 전환
- `UIGender.cs` 8회 — 성별 선택
- `UIBGChange.cs` 13회 — 배경 변경
- `UIGesture.cs` 16회 — 아바타 포즈/제스처
- `UILobbyScene.cs` 12회 — 로비 씬 진입

### 3.3 마이룸 (개인 공간)
**`UIMyRoom.cs` 11회 + 4회, `ScreenshotManager.cs` 8회**

- 마이룸 화면 구성 / 사진 촬영 기능 (2022-06-20 1차 완성)
- 아바타 스크린샷 캡처 → 썸네일 생성
- 단색 배경 + 캐릭터 합성, 썸네일 로딩 속도 개선
- `ScreenShotAvatar on/off` 토글

### 3.4 페이스 에디터 (Face Editor)
**`FaceEditor/ContentManager.cs` 11회 + 10회, `FaceEditManager.cs` 9회 + 9회**

- **BlendShape 기반 얼굴 커스터마이징** — 눈/코/입/턱 형태 슬라이더 편집
- 수염 BlendShape 충돌 이슈 (모자 / 헤어와의 결합) 해결
- 모자 착용 시 컬러피커 적용 충돌 해결

### 3.5 컬러피커 시스템
**`ColorPickerController.cs` 8회, `ColorPickerUnityUI.cs` 10회, `ChangeColor.cs` 8회**

- UnityUI 기반 색상 피커 + 머티리얼 색상 실시간 반영
- 모자 / 의상 / 헤어 컬러 변경 → BlendShape 결합 시 충돌 다수 해결
- 모자 쓰면 기존 컬러피커 적용 안 됨 현상 수정 (2022-08-30)

### 3.6 에셋번들 & 다운로드 매니저
**`AssetBundleManager.cs` 16회 + 8회**

- **Addressables → AssetBundle 시스템 전환** (2022-05-30, BHS 단독 작업)
- 다운로드 진행률, 안드로이드 외부 저장소 권한 처리
- Key 기반 아바타 생성 — 서버에서 받은 키로 로컬 번들 매칭
- 동일 패킷 중복 송신 방지 (`CheckOverlapSendPacket`)
- `UILoadResources.cs` 10회 — 리소스 로딩 화면

### 3.7 서버 연동
**`WebManager.cs` 9회, `AvatarBuilderAPI.cs` 6회**

- LG U+ 백엔드 API 통신 (REST)
- 아바타 데이터 저장 / 로드
- Android 플랫폼 판별 코드, 권한 부여

### 3.8 디버그 / 운영 편의
- DebugConsole (Shift + ` 단축키로 토글)
- 팝업 시스템 정리 (UI 일관화)
- lilToon 셰이더 제거 (성능·번들 사이즈 이슈로 추정)

---

## 4. 기술적 특이점

### 4.1 Addressables → AssetBundle 1주일 마이그레이션
프로젝트 초기 Addressables로 설계되었으나, 운영 요구사항(번들 분할 / 다운로드 제어 / 캐싱 정책)에 맞추어 **AssetBundle 시스템으로 본인이 단독 마이그레이션**.
- 2022-05-24 어드레서블 적용 → 2022-05-27 다운로드 성공·안드로이드 권한 부여 → 2022-05-30 에셋번들 시스템 전환 완료
- **1주일 내 인프라 교체** 완수

### 4.2 아바타 합성 엣지케이스 카탈로그
모자/수염/맨몸/컬러피커 충돌, 저장 직후 찰나 맨몸 로딩, 단색 배경 캐릭터 사라짐 등 **사용자 시나리오 기반 결함**을 8월 한 달간 집중 잡아냄(8월 한 달 **84 커밋**). 다대다 파츠 결합 시스템의 안정성을 BHS가 주도하여 끌어올림.

### 4.3 BlendShape × 머티리얼 컬러피커 동시 제어
얼굴 형태(BlendShape)와 머티리얼 컬러를 같이 변경할 때 발생하는 셰이더 변수 충돌을 정리. 컬러피커가 BlendShape 영향 받는 파츠(수염·헤어·모자)에서 누락되지 않도록 일관화.

---

## 5. 시기별 작업 흐름

| 시기 | 커밋 | 주력 작업 |
|------|------|----------|
| 2022-05 | 12 | 어드레서블 / 에셋번들 인프라, 다운로드, 안드로이드 권한 |
| 2022-06 | 32 | 아바타 로더, Key 기반 아바타 생성, 마이룸 사진찍기 1차 |
| 2022-07 | 47 | 컬러피커, 블렌드쉐이프, Android 플랫폼 판별 |
| **2022-08** | **84** | **아바타 합성 엣지케이스 집중 대응** (모자/수염/맨몸/썸네일) |
| 2022-09 | 85 | Animator Rebind, LOD 조절, lilToon 제거, 팝업 정리 |
| 2022-10 | 34 | 디버그 콘솔, 스크린샷 토글, 아바타 빌더 머지 마무리 |

---

## 6. 키워드 / 태그

`Unity 2020 LTS` · `C#` · `URP` · `Addressables` · `AssetBundle 마이그레이션` · `3D Avatar Builder` · `BlendShape` · `Face Editor` · `Color Picker` · `UnityUIColorPicker` · `Animator Rebind` · `LOD` · `lilToon` · `Screenshot` · `Metaverse Client` · `LG U+` · `Android 권한` · `Asset Pipeline`

---

## 7. 메타 정보

- 작성 기준일: **2026-05-21**
- 데이터 출처: `ovencode-new/uplus-avatar-client` git log (`gustjd8121@gmail.com` 기준, 모든 브랜치 `--all`)
- 분석 환경: 읽기 전용 클론 (원본 저장소 쓰기 없음)
