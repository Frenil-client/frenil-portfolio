# 정휘현 — Unity Client Programmer

모바일 수집형 RPG / MMORPG에서 UI 시스템과 핵심 콘텐츠 시스템을 설계해 온 Unity 클라이언트 프로그래머입니다.
가챠, 인앱결제, 캐릭터 스탯, 던전 진입 등 핵심 시스템을 라이브 서비스까지 운영했고,
아트팀과 기획팀이 코드 없이 쓸 수 있는 에디터 툴을 만드는 일에 강점이 있습니다.

경력 6년 8개월 (애프터타임 -> IMC게임즈 트리오브세이비어M -> 클로버게임즈 아야카시라이즈)

silsen@naver.com

---

## UI / 시스템

실무에서 설계했던 구조를 범용 모듈로 다시 구현한 라이브러리입니다.
각 저장소는 UPM 패키지 형태로 배포되어 있고 EditMode 단위 테스트를 포함합니다.

| 프로젝트 | 설명 |
|---|---|
| [unity-mvvm](https://github.com/Frenil-client/unity-mvvm) | UGUI 환경을 위한 경량 MVVM 프레임워크. Observable 기반 데이터 바인딩을 외부 라이브러리 없이 구현. View는 UI 조작만, ViewModel은 Unity 비의존 로직만 담당하도록 분리 |
| [unity-reddot-system](https://github.com/Frenil-client/unity-reddot-system) | 트리 구조 기반 레드닷 시스템. enum 노드 타입, 자동 상위 전파, 카운트 아이콘 지원 |
| [unity-stat-system](https://github.com/Frenil-client/unity-stat-system) | 제네릭 기반 RPG 스탯 시스템. StatId enum, 버전 기반 캐시 무효화, MaxValue 무결성 검사 |
| [unity-maplightdata-tool](https://github.com/Frenil-client/unity-maplightdata-tool) | 씬별 조명 환경을 ScriptableObject로 관리. Primary/Additive 스택 기반 자동 복원, Addressables 에디터 자동화 |

## 아키텍처

| 프로젝트 | 설명 |
|---|---|
| [minigames](https://github.com/Frenil-client/minigames) | 확장형 씬 로딩 플랫폼 아키텍처. 허브 씬에서 콘텐츠를 Additive 로드/언로드하고, 폴더 1개와 데이터 에셋 1개만 추가하면 코드 수정 없이 확장되는 구조. IMiniGame 생명주기 계약, ScriptableObject 데이터 드리븐 등록, UIStackManager, RecycleScrollView. 구조 실증용으로 콘텐츠 2종 구현 |

## 렌더링 / 셰이더

| 프로젝트 | 설명 |
|---|---|
| [unity-spine-fx-lab](https://github.com/Frenil-client/unity-spine-fx-lab) | Spine 2D 런타임 + 셰이더 제어 시스템. 디졸브, 히트플래시, 상태이상, 아웃라인을 MaterialPropertyBlock으로 머티리얼 증식 없이 일원 제어. 다중 인스턴스 성능 문제(58 -> 129 FPS)와 통합 투명 고스팅 두 건을 원인 분석부터 해결, 계측까지 정리 |
| [unity-urp-shader-lab](https://github.com/Frenil-client/unity-urp-shader-lab) | URP 기반 서브컬처 스타일 NPR 렌더링 랩. Shader Graph 없이 HLSL 직접 작성 - 셀 셰이딩, SDF 페이스 셰도우, 헤어 이방성, 아웃라인. SDF/스무딩 노멀 베이커 등 아트 파이프라인 툴 6종 자작 |

## 기술 스택

`Unity` `C#` `UGUI` `NGUI` `MVVM` `ScriptableObject` `Addressables` `Protobuf` `URP` `HLSL` `Spine` `UniTask` `DOTween`
