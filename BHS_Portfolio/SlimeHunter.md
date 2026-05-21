# 배현성 (BHS) — SlimeHunter (8-Bit Games 협업)

> **외부 게임사(8-Bit Games)와의 협업 Unity 프로젝트**에 짧게 합류하여 멀티샷 스킬 한 건을 작업한 스팟 기여 사례.

- **이름**: 배현성 (BHS / BaeHyeonSeong)
- **이메일**: gustjd8121@gmail.com
- **포지션**: Unity 클라이언트 (스팟 컨트리뷰터)

---

## 1. 프로젝트 개요

| 항목 | 내용 |
|------|------|
| **프로젝트명** | SlimeHunter |
| **협업 구조** | ovencode 측 + **8-Bit Games(외부)** 공동 작업 — `*@8-bitgames.com` 도메인 컨트리뷰터 다수 참여 |
| **엔진** | Unity 2021.3.34f1 LTS |
| **렌더 파이프라인** | URP 12.1.13 |
| **3rd-Party** | Firebase, Addressables 1.19.19 |
| **저장소** | `github.com/ovencode-game/SlimeHunter` (private) |

---

## 2. 정량 기여도

| 항목 | 값 |
|------|-----|
| **활동 기간** | 2023년 8월 8일 (**단일 작업일**) |
| **BHS 커밋 수** | **2** |
| **저장소 내 비중** | 0.2% (전체 1,244 커밋 중) |
| **LOC** | +357 / -7 / 14 파일 |
| **역할** | 스팟 컨트리뷰터 — 단일 기능 작업 |

> 짧은 합류였지만, **외부 코드베이스에 빠르게 진입해서 신규 스킬 한 건을 깔끔하게 마무리**한 케이스.

---

## 3. 작업 내용 — 멀티샷(Multishot) 스킬 구현

### 커밋

| 일자 | 커밋 |
|------|------|
| 2023-08-08 | `멀티샷` |
| 2023-08-08 | `Skill. Multishor 리소스 적용` |

### 추가/수정 파일 (14개)

#### 신규 스크립트
- `Assets/Scripts/Core/Skill/Implements/SkillMultishot.cs` — **멀티샷 스킬 신규 클래스**

#### 수정 스크립트
- `Assets/Scripts/Core/Projectile/ProjectileBehavior.cs` — 발사체 공통 모듈 보강 (멀티샷 적용 시 정상 동작)
- `Assets/Scripts/Core/Weapon/WeaponBow.cs` — **활(Bow) 무기에 멀티샷 통합**

#### 신규 이펙트
- `Assets/Prefabs/Core/Projectile/MultShotFx.prefab` — 멀티샷 전용 이펙트
- `Assets/Prefabs/Core/Projectile/MultShotFx.prefab.meta`

#### 수정 발사체 프리팹 (9종)
- `CactusBullet.prefab` / `CactusBulletEvol.prefab`
- `ProjectileEgg.prefab`
- `ProjectileGravity.prefab`
- `ProjectileHoming.prefab`
- `ProjectileKnife.prefab` / `ThrowingKnife.prefab`
- `ProjectileRock.prefab`
- `ProjectileStraight.prefab`

> 활(Bow) 기반 멀티샷이지만 **기존 발사체 9종 전부에 영향**이 가는 구조였기 때문에, 단순 신규 추가가 아니라 **공통 발사체 인터페이스를 안전하게 확장**하는 작업이었음.

---

## 4. 기여 포인트

### 4.1 외부 코드베이스 빠른 진입
8-Bit Games 주도의 익숙하지 않은 게임 아키텍처에 합류하여, **단일 영업일 내에 신규 스킬 하나를 PR 완료**.

### 4.2 공통 발사체 모듈 안전 확장
멀티샷 도입 시 기존 발사체(직선·중력·호밍·관통·바위 등 9종)가 회귀하지 않도록 `ProjectileBehavior` 공통 모듈을 보강. 신규 기능이 기존 자산을 깨지 않게 하는 **호환성 우선** 접근.

### 4.3 스킬-무기-이펙트 한 세트
스크립트(스킬·발사체·무기) + 프리팹(이펙트·9종 발사체) + 리소스 적용을 한 작업 단위로 마무리. **기능 수직 슬라이스(Vertical Slice)** 단위 작업 능력 확인.

---

## 5. 키워드 / 태그

`Unity 2021 LTS` · `C#` · `URP` · `Skill System` · `Multishot` · `Projectile` · `Weapon System` · `Bow` · `Firebase` · `Addressables` · `외부 협업` · `8-Bit Games` · `Vertical Slice`

---

## 6. 메타 정보

- 작성 기준일: **2026-05-21**
- 데이터 출처: `ovencode-game/SlimeHunter` git log (`gustjd8121@gmail.com` 기준, 모든 브랜치 `--all`)
- 분석 환경: 읽기 전용 클론 (원본 저장소 쓰기 없음)
