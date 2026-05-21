# 배현성 (BHS) — Unity 게임 개발 경력서

> **Unity 2D 디펜스 게임 클라이언트 개발** — `BowwowDefence` 프로젝트의 게임플레이 코어(스킬/발사체/전투), 가챠 연출, 인게임 UI를 담당.

- **이름**: 배현성 (BHS / BaeHyeonSeong)
- **이메일**: gustjd8121@gmail.com
- **소속 GitHub Org**: ovencode-game
- **포지션**: Unity 클라이언트 개발자

---

## 1. 프로젝트 개요

| 항목 | 내용 |
|------|------|
| **프로젝트명** | BowwowDefence (가칭) |
| **장르** | 2D 디펜스 / 캐주얼 모바일 게임 |
| **엔진** | Unity 2022.3.14f1 LTS |
| **렌더 파이프라인** | URP 14.0.9 (Universal Render Pipeline) |
| **타깃 플랫폼** | Android / iOS (모바일) |
| **저장소** | `github.com/ovencode-game/BowwowDefence` (private) |

### 사용 패키지·SDK

**Unity 공식**
- Addressables 1.21.21 (애셋 관리)
- 2D Feature Set 2.0.0
- NavMeshPlus (2D NavMesh, h8man/NavMeshPlus GitHub 패키지)
- TextMeshPro 3.0.6, Timeline 1.7.6, Recorder 4.0.2
- Newtonsoft Json 3.2.1
- Burst Compiler 1.8.10

**3rd-Party SDK**
- AppsFlyer (어트리뷰션 / 마케팅)
- Facebook SDK
- Google Play Plugins (IAP / Authentication)
- 광고 ADSDK
- Spine (2D 스켈레톤 애니메이션) — 보물상자 / 캐릭터

---

## 2. 정량 기여도

| 항목 | 값 |
|------|-----|
| **활동 기간** | 2024년 6월 26일 ~ 8월 19일 (약 2개월 집중 개발) |
| **BHS 커밋 수** | **71** |
| **저장소 내 비중** | **24.7%** (전체 288 커밋 중) |
| **LOC** | +38,953,321 / -312,444 (Unity 메타·에셋 포함) |
| **변경 파일** | 29,259 |
| **주력 모듈** | 스킬 시스템 · 발사체 · 데이터 매니저 · 보물상자 · 보드 UI |

> 6명 컨트리뷰터 중 단일 개발자로서 **약 25% 기여**, 게임플레이 코어 로직(스킬/전투/UI)을 담당.

---

## 3. 도메인별 상세 기여

### 3.1 스킬 시스템 — 가장 깊이 작업한 영역
**`SkillManager.cs` 14회 수정 (최다)**

#### 발사체(Projectile) 시스템 구축
6종 발사체 패턴을 모듈형으로 설계하여 신규 스킬 추가 비용을 최소화.

| 발사체 | 메커니즘 |
|--------|---------|
| `Missile` | 기본 단일 타격 |
| `Missile_Chain` | 연쇄 타격 (조건부 분기) + **연사 기능** |
| `Missile_Pierce` | **관통**, 관통 횟수에 따른 데미지 감산 처리 |
| `Fire_Splash` | 광역 폭발 |
| `Projectile` (Chain / Fan) | 부채꼴 다중 발사 |
| `ActionObject` / `Explosion` | 발사체 사후 효과 (잔류 / 폭발) |

#### 스킬 모듈 / 공식
- `SkillModuleDamageAround` — 광역 데미지 모듈 + **타원 영역** 추가 (원형 한정 → 타원으로 확장)
- **데미지 공식 정형화** (`데미지 공식 적용` 커밋)
- 스킬 기본 데미지 + 각도 기능 + 공격 속도 적용
- **스킬 자동 장착** 로직 + 정렬
- **사용 모델 변경**: 충전 카운트(`ChargeCount`) → 쿨다운(`CoolDown`) 기반으로 재설계
- 스킬 데이터 구조 변경 + 마이그레이션
- 발사체 잔류 버그 수정 (객체 풀 / 라이프사이클)

**관련 파일**
`SkillManager.cs`, `SkillBase.cs`, `Projectile.cs`, `Missile.cs`, `Missile_Chain.cs`, `Missile_Pierce.cs`, `Fire_Splash.cs`, `SkillModuleDamageAround.cs`, `ActionObject.cs`, `Explosion.cs`, `SkillItemManager.cs`

---

### 3.2 데이터 관리 & 테이블 시스템
**`DataManager.cs` 12회 수정**

- ScriptableObject 기반 데이터 관리자 설계·유지보수
- `LocalDataTable` (`Assets/Scripts/Common/LocalDataTable.cs` 7회) — 정적 게임 데이터 로딩
- `UserDataManager.cs` — 유저 진행도 / 재화 / 인벤토리
- `EquipItemData.cs` (5회) — 장착 아이템 스키마
- `UnitItemManager.cs` (9회) — 유닛 인벤토리 / 슬롯 / 해금
- 데이터 테이블 오류 수정, 인덱스 검증 로직 (`UnitData.Ind 10nn %10 != 1 == continue`)

---

### 3.3 보물상자 가챠 시스템
**`PopupTreasureBox.cs` 9회 수정**

- 보물상자 **연출 시퀀스** 구현 (Treasure Anim → Card 등장 → 결과 카드)
- `TreasureCard.cs`, `TreasureResultCard.cs` — 카드 컴포넌트
- **재화 타입 보상 추가** (`RewardType Add Currency`)
- 보물상자 스킵 처리 + Off Block 안전장치
- 보물상자 스파인 애니메이션 오류 수정
- `PopupSummonReward.cs` — 소환 결과 팝업

---

### 3.4 유닛 & 스킬 보드 UI
**`PanelSkill.cs` 8회, `PanelUnit.cs` 6회 수정**

- 보드 패널 매니저 (`BoardPanelManager.cs`) — 유닛 / 스킬 / 축복 탭 컨트롤
- **유닛 슬롯 해금 / 탈부착** (UI + 데이터)
- 유닛·스킬 **자동 장착** + 자동 정렬
- `UI_SelectSkillObject`, `UI_SkillItem`, `UI_SelectUnitObject`, `UI_UnitItem`
- 슬라이더, Fill 색상, 프리팹 정리
- `PopupUnit.cs`, `PopupSkill.cs`, `PopupGuard.cs` — 상세 팝업 (StarIter, Owned value 표시)
- BottomTab — 하단 네비게이션 임시 조치 + 복구
- 프리팹 Missing Reference 에러 수정

---

### 3.5 축복(Bless) 시스템
- `BlessingItem.cs` — 축복 아이템 (5회)
- `PopupBlessLevelUp.cs` — 레벨업 팝업
- Bless ExpBar, Bless 프리팹, **레벨업 보너스 수치 적용**
- 축복 UI 정리

---

### 3.6 전투 핵심 로직
- `BattleRule.cs` 7회 — 전투 규칙 / 페이즈 / 승패 판정
- `ActiveUnit.cs` 7회 — 아군 유닛 베이스
- `EnemyCharacter.cs` 4회 — 적 캐릭터
- `GameManager.cs` 9회 — 게임 흐름 / 상태 머신
- Bullet Speed, 공격 속도, **PopupGuard Arrow Button Active** (보호기 방향 입력)

---

### 3.7 Addressables / 빌드 환경 세팅
- Addressables 패키지 도입 및 초기 세팅
- `Install Packages` — 사용 패키지 결정 / 의존성 정리
- `Game Package` — 빌드 출력 정비
- 프리팹 미싱 에러 정리, 데이터 정리(Cleaning), 초기 구조 마이그레이션(`Move Project`)

---

## 4. 게임플레이 시스템 다이어그램 (요약)

```
[GameManager] ─ 상태/페이즈 관리
   ├─ [BattleRule] ─ 승패/페이즈 판정
   ├─ [BoardPanelManager] ─ 인게임 보드 UI 전환
   │     ├─ PanelUnit  → UI_SelectUnitObject / UI_UnitItem / PopupUnit
   │     └─ PanelSkill → UI_SelectSkillObject / UI_SkillItem / PopupSkill
   ├─ [SkillManager] ─ 스킬 사용/쿨다운/자동장착
   │     └─ SkillBase
   │          └─ SkillModule(SkillModuleDamageAround …)
   │                └─ Projectile
   │                     ├─ Missile / Missile_Chain / Missile_Pierce
   │                     ├─ Fire_Splash
   │                     └─ ActionObject / Explosion (사후 효과)
   ├─ [UnitItemManager] ─ 유닛 인벤토리/장착
   └─ [DataManager + LocalDataTable + UserDataManager] ─ 데이터 계층
         └─ EquipItemData

[PopupTreasureBox] ─ 가챠 연출 시퀀스
   └─ TreasureCard → TreasureResultCard → PopupSummonReward
```

---

## 5. 기술적 특이점·기여 포인트

### 5.1 모듈형 스킬·발사체 구조
**Strategy + Decorator 패턴**으로 발사체를 모듈화. 베이스 `Projectile` + 행동 모듈(Chain / Pierce / Splash / Fan) 조합으로 6종을 처리하여, 신규 발사체 추가 시 기존 코드를 건드리지 않고 모듈만 조립.

### 5.2 ChargeCount → CoolDown 재설계
초기 충전식 스킬 사용 모델(`ChargeCount`)을 운영 도중 쿨다운 기반(`CoolDown`)으로 전환. 데이터 마이그레이션 + UI(슬라이더, 색상) + 자동 사용 로직 동시 수정.

### 5.3 ScriptableObject 기반 데이터 레이어
정적 게임 데이터를 ScriptableObject로 관리 → 디자이너가 코드 빌드 없이 밸런스를 조정. `DataManager` + `LocalDataTable` + `UserDataManager` 3계층으로 정적/동적 데이터 분리.

### 5.4 Addressables 도입
대용량 2D 아트 / Spine / 프리팹을 Addressables로 비동기 로드 → 초기 로딩 단축 + 메모리 풋프린트 최적화 기반 마련.

### 5.5 가챠 연출 파이프라인
보물상자 → 카드 등장 → 결과 카드 → 보상 적용까지의 **Spine 애니메이션 동기화 + 스킵 가능 시퀀스** 구현. 스킵 시 발생하던 NRE / 잔여 연출 버그를 안전장치(Off Block)로 차단.

---

## 6. 시기별 작업 흐름

| 시기 | 주력 작업 |
|------|----------|
| **2024-06** (4 커밋) | 프로젝트 이관(Move Project), 데이터·구조 정리 |
| **2024-07** (37 커밋) | 유닛 보드, 스킬 보드, 보물상자, 데이터 테이블, 데미지 공식, 발사체 6종, Bless 시스템 |
| **2024-08** (30 커밋) | Addressables 설치, 스킬 모듈 확장(타원·관통·연사), 가챠 연출, 프리팹 안정화, 게임 패키지 출력 |

---

## 7. 키워드 / 태그

`Unity 2022 LTS` · `C#` · `URP` · `2D Game` · `NavMeshPlus` · `Addressables` · `Spine 2D` · `TextMeshPro` · `Timeline` · `ScriptableObject` · `Object Pool` · `Strategy Pattern` · `Module Composition` · `Gacha System` · `Skill System` · `Projectile System` · `Battle Logic` · `In-Game UI` · `Tower Defense` · `AppsFlyer` · `Facebook SDK` · `Google Play Plugins`

---

## 8. 메타 정보

- 작성 기준일: **2026-05-21**
- 데이터 출처: `ovencode-game/BowwowDefence` git log (`gustjd8121@gmail.com` 기준, 모든 브랜치 `--all`)
- 분석 환경: 읽기 전용 클론 (원본 저장소에 쓰기 없음)
