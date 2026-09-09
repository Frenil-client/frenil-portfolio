# 정휘현 - Unity Client Programmer

모바일 RPG의 UI와 핵심 콘텐츠 시스템을 설계하고 런칭부터 라이브 운영까지 맡아 온 Unity 클라이언트 프로그래머입니다.
경력 6년 8개월. 상점·결제·재화·캐릭터 스탯·던전 진입을 구현하고,
기획팀과 아트팀이 코드 수정 없이 콘텐츠를 다룰 수 있는 에디터 툴을 만들어 왔습니다.

silsen@naver.com · [GitHub](https://github.com/Frenil-client)

## 실무 경험과 공개 작업물

| 프로젝트 / 회사 | 담당 경험 |
|---|---|
| 아야카시 라이즈 / 클로버게임즈 | 가챠·인벤토리·캐릭터 육성 UI와 서버 연동, 결제 상품·구매 흐름, 던전 진입, 스탯 합산·캐시, 카메라·조명 구조 |
| 트리 오브 세이비어M / IMC게임즈 | UI 콘텐츠, MVVM 바인딩, 재사용 스크롤, NGUI 셰이더 마스킹, Timeline·Inspector 연출 툴 |
| 애프터타임 | 퍼즐·전투 콘텐츠, Photon 멀티플레이, 플랫폼 서비스 연동과 공통 프레임워크 |

아래 저장소는 개인 작업물입니다. 실무에서 다룬 문제를 범용 시스템으로 재구현하거나,
런타임 제어와 렌더링 기법을 별도로 검증한 결과를 공개합니다.

## 먼저 볼 작업 세 가지

### 1. [통합 데모](https://github.com/Frenil-client/unity-integration-demo) - 독립 패키지를 하나의 화면으로 연결

![통합 데모 로비](docs/images/demo-lobby.gif)

모바일 RPG 로비에서 능력치 강화·소환·보상 확인·임무 수령이 동작합니다.
`stat-system`은 능력치와 변경 이벤트를, `mvvm`은 값·목록 바인딩을,
`reddot-system`은 알림 집계를 담당합니다.

패키지 사이의 타입 변환은 소비 프로젝트의 `Glue/` 두 파일에 모았습니다.
각 패키지가 다른 패키지를 참조하지 않고, 도메인과 ViewModel은 Canvas나 GameObject 없이 테스트됩니다.
실제로 조립해 봐야 드러나는 것들은 데모가 아니라 패키지 쪽에 반영했고, 무엇이 왜 바뀌었는지는
[데모 README](https://github.com/Frenil-client/unity-integration-demo#이-데모가-드러낸-것)에 남겼습니다.

**확인 방법:** Unity 6000.3.9f1에서 `Assets/Scenes/LobbyDemo.unity` 실행.
EditMode 테스트 21종이 로비의 흐름을 검증하며, 설치 버전은 manifest의 태그로 고정합니다.

### 2. [UI 스택 시스템](https://github.com/Frenil-client/unity-ui-system) - 게임에서 사용하는 UPM 패키지

레이어 캔버스, 정렬 순서 배정, 공유 Dim, 씬 소유권에 따른 UI 수명을 관리합니다.
뷰 타입이 레이어를 정하고, 뷰가 가진 캔버스 수만큼 정렬 구간을 예약했다가 닫을 때 반납합니다.
부트스트랩 설정을 갖추면 작업 중인 씬에서 바로 Play할 수 있습니다.

[DefenceGame](https://github.com/Frenil-client/DefenceGame)이 이 패키지를 UPM으로 설치해 사용합니다.
문자열 id로 팝업을 여는 호출을 `OpenAsync<ShopPopup>()`으로 바꿔 타입 이름 오타가 컴파일 단계에서 걸리고,
개별 backdrop은 공유 Dim 하나로 대체됩니다.

**확인 방법:** 패키지 저장소의 `SampleLobby` 씬 또는 DefenceGame의 상점·조합·결과 팝업.

### 3. [Spine FX 랩](https://github.com/Frenil-client/unity-spine-fx-lab) - 성능과 통합 투명 연출

Spine의 부위별 페이드에서 생기는 겹침을 RT 평탄화와 단일 알파 합성으로 처리하고,
화면 밖 캐릭터의 애니메이션·메시 갱신 비용을 컬링으로 줄였습니다.

**측정 조건:** spineboy 300체 중 화면 안 60체를 갱신하고 240체를 컬링한 에디터 계측에서
CPU 메인 프레임 4.29ms, 화면 약 129 FPS입니다. 드로우콜은 컬링 여부와 무관하게 77~78로 같아,
절약은 그리는 양이 아니라 화면 밖 인스턴스의 갱신 비용에서 나옵니다.

MaterialPropertyBlock으로 인스턴스별 연출 값을 전달해 머티리얼 복제를 줄였습니다.
SRP Batcher 호환을 포기하는 대가와 해당 장면에서의 비교 계측은
[성능 분석](https://github.com/Frenil-client/unity-spine-fx-lab/blob/main/Docs/analysis/multi-instance-perf.md)에 정리했습니다.

## 전체 저장소

| 저장소 | 역할 / 확인할 내용 |
|---|---|
| [unity-integration-demo](https://github.com/Frenil-client/unity-integration-demo) | 세 패키지의 연결, 로비 상태 변화, 구독 해제와 통합 테스트 |
| [unity-ui-system](https://github.com/Frenil-client/unity-ui-system) | UI 스택·정렬 구간·씬 소유권·풀링, DefenceGame 적용 |
| [unity-mvvm](https://github.com/Frenil-client/unity-mvvm) | `Observable<T>`와 델타 목록 바인딩, Unity 비의존 ViewModel, View 구독 수명 |
| [unity-stat-system](https://github.com/Frenil-client/unity-stat-system) | long 고정소수점 저장, 기본값·모디파이어 분리, 최종값 캐싱·변경 통지 |
| [unity-reddot-system](https://github.com/Frenil-client/unity-reddot-system) | 트리 카운트 집계, 잠금, enum 계층 진단과 EditorWindow |
| [unity-maplightdata-tool](https://github.com/Frenil-client/unity-maplightdata-tool) | 씬 조명 SO 캡처, Primary/Additive 적용·복원, Addressables 등록 도구 |
| [minigames](https://github.com/Frenil-client/minigames) | Additive 콘텐츠 진입, `IMiniGame` 계약, SO 등록, 재사용 스크롤, 미니게임 2종 |
| [unity-spine-fx-lab](https://github.com/Frenil-client/unity-spine-fx-lab) | HLSL 연출 제어, 컬링 성능 비교, RT 통합 페이드 |
| [unity-urp-shader-lab](https://github.com/Frenil-client/unity-urp-shader-lab) | NPR 셰이더 4종, 포스트 3종, SDF·스무딩 노멀 등 에디터 툴 6종 |
| [DefenceGame](https://github.com/Frenil-client/DefenceGame) | 진행 중인 조합 디펜스 프로토타입, 순수 C# Core와 실시간 전투의 경계 |

UI·MVVM·스탯·레드닷은 독립 UPM 패키지입니다. UI는 Unity 6000.3 이상,
나머지는 각 저장소에 적힌 Unity 최소 버전과 의존성을 따릅니다.
MapLightData도 UPM으로 설치되며 Addressables를 사용합니다.

## 검증 범위

CI 구성 기준입니다. 최신 실행 결과는 각 워크플로에서 확인할 수 있습니다.

| 저장소 | 자동 검증 | Unity에서 별도로 확인할 범위 |
|---|---|---|
| [UI Validate](https://github.com/Frenil-client/unity-ui-system/actions/workflows/validate.yml) | 패키지 경계·meta·JSON·CHANGELOG 정합성. 릴리스 시 태그·버전 대조 | 컴파일과 UI 동작, 씬 전환·입력·비동기 수명 |
| [MVVM CI](https://github.com/Frenil-client/unity-mvvm/actions/workflows/ci.yml) | 순수 C# 코어 빌드, 헤드리스 20종, 할당 벤치마크 | View 테스트 15종과 Unity 할당 테스트 3종 |
| [Stat CI](https://github.com/Frenil-client/unity-stat-system/actions/workflows/ci.yml) | 코어 빌드, 헤드리스 57종, 할당 벤치마크 | Unity 할당 테스트 6종, Mono·IL2CPP 실행 확인 |
| [RedDot CI](https://github.com/Frenil-client/unity-reddot-system/actions/workflows/ci.yml) | 코어 빌드, 트리·진단 로직 47종 | Icon·Manager·EditorWindow의 Unity 동작 |

MVVM·Stat·RedDot의 헤드리스 테스트는 합계 124종입니다. `Tests~/`가 `Tests/`의 같은 소스를 컴파일하므로
사본이 아니라 같은 테스트가 매 푸시마다 우분투 러너에서 돕니다.

스탯 벤치마크는 .NET 8 / Release에서 대상 40만 연산의 관리 힙 할당이 0B인지 검사합니다.
스탯 저장은 long, 곱셈·나눗셈의 중간 계산은 decimal이며, 같은 값과 같은 연산 순서를 전제로 합니다.

## 툴과 게임에서 확인할 설계

### 레드닷 트리 디버거

![레드닷 트리 디버거](docs/images/reddot-debugger.gif)

카운트를 자기와 자식으로 분해해 표시하고, 값 주입·잠금 토글·enum 계층 진단을 한 화면에 모았습니다.
표시 모델은 순수 C#이며 런타임과 같은 부모 계층 유도 함수를 사용합니다.

### DefenceGame - SYNTHESIS (가칭)

랜덤 조합 디펜스의 그레이박스 프로토타입입니다. 현재 뽑기·조합·선택권의 흐름을 검증하고 있고,
배치 칸과 선택권으로 결정을 만듭니다.

`Shared/Synthesis.Core`는 UnityEngine을 참조하지 않으며 코어 빌드·테스트·CSV 불변식 린터를 CI에서 실행합니다.
맵 생성·스폰·루프 순회 등 Core의 처리는 시드와 정수 틱을 기준으로 재현됩니다.

## 기술 스택

`Unity` `C#` `UGUI` `NGUI` `MVVM` `ScriptableObject` `Addressables` `Protobuf` `URP` `HLSL` `Spine` `UniTask` `DOTween` `GitHub Actions`
