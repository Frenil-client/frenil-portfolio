# 정휘현 - Unity Client Programmer

UI 시스템과 핵심 콘텐츠 시스템을 설계하고 라이브 서비스까지 운영해 온 Unity 클라이언트 프로그래머입니다.
상점, 결제, 재화, 캐릭터 스탯, 던전 진입 같은 시스템을 런칭부터 운영까지 맡았고,
기획팀과 아트팀이 코드 없이 쓸 수 있는 에디터 툴을 만드는 일에 강점이 있습니다.

경력 6년 8개월 - 애프터타임, IMC게임즈(트리 오브 세이비어M), 클로버게임즈(아야카시 라이즈).
세 프로젝트 모두 런칭과 라이브 운영을 함께 겪었습니다.

silsen@naver.com

---

## 먼저 볼 것 - 통합 데모

### [unity-integration-demo](https://github.com/Frenil-client/unity-integration-demo)

![통합 데모 로비](docs/images/demo-lobby.gif)

아래 UPM 패키지 세 개가 **서로를 모르는 채로** 하나의 화면에서 맞물리는 것을 보여주는 프로젝트입니다.
소재는 모바일 RPG 로비입니다.

`stat-system`은 `Observable`을 모르고, `mvvm`은 `Stat`을 모르며, `reddot-system`은 둘 다 모릅니다.
**한 패키지의 출력을 다른 패키지의 입력 타입으로 바꾸는 코드는 `Glue/` 두 파일뿐**이고,
그 둘을 지우면 세 패키지는 완전한 남남으로 돌아갑니다.
각 패키지 README가 "외부 의존 없는 드롭인"이라고 주장하기 때문에 세운 제약입니다.
연결 코드를 패키지 안에 넣는 순간 그 주장이 깨집니다.

Canvas도 GameObject도 만들지 않는 테스트 **21종**이 로비의 흐름 전체를 검증합니다.
`mvvm`이 ViewModel을 MonoBehaviour로 만들지 않은 이유가 여기서 증명됩니다.

패키지를 실제로 조립하는 과정에서 **패키지 쪽 결함 세 건**이 드러났고, 셋 다 데모가 아니라 패키지를
고쳐 해결했습니다. git URL 설치에서만 터지는 `.meta` 누락, 씬 오브젝트 순서에 따라 죽는 초기화 의존,
목록 항목 View가 프레임워크 기본 경로를 못 쓰던 문제입니다. 원인과 해결은
[데모 README](https://github.com/Frenil-client/unity-integration-demo#이-데모가-드러낸-것)에 정리했습니다.

---

## 재사용 패키지 (UPM)

실무에서 설계했던 구조를 범용 모듈로 다시 구현했습니다. 셋 다 git URL로 설치되고,
**Unity 라이선스 없이 도는 CI**가 매 푸시마다 컴파일, 테스트, 할당 회귀를 검증합니다.

| 프로젝트 | 설명 | 테스트 | CI |
|---|---|---|---|
| [unity-mvvm](https://github.com/Frenil-client/unity-mvvm) | UGUI용 경량 MVVM. 외부 라이브러리 없이 `Observable<T>` 값 바인딩과 `ObservableList<T>` **델타 기반 목록 바인딩**. ViewModel은 Unity 비의존이라 화면 없이 테스트되고, 구독 수명은 베이스가 관리 | 38 | ![CI](https://github.com/Frenil-client/unity-mvvm/actions/workflows/ci.yml/badge.svg) |
| [unity-stat-system](https://github.com/Frenil-client/unity-stat-system) | 캐릭터 스탯 시스템. long 고정소수점 값 타입으로 결정적 연산, **기본값 + 모디파이어(장비/버프) 2층 구조**, 최종값 캐싱과 변경 통지 | 63 | ![CI](https://github.com/Frenil-client/unity-stat-system/actions/workflows/ci.yml/badge.svg) |
| [unity-reddot-system](https://github.com/Frenil-client/unity-reddot-system) | 트리 기반 레드닷. enum 숫자 규칙에서 계층 자동 유도, 델타 전파로 읽기 O(1), **트리 디버거 EditorWindow** 포함 | 47 | ![CI](https://github.com/Frenil-client/unity-reddot-system/actions/workflows/ci.yml/badge.svg) |

### 수치로 남긴 것

**할당 19.07MB -> 0B** (stat-system)

`FieldInfo.GetValue()`가 struct를 호출마다 boxing하던 경로를 배열 인덱싱으로 재설계했습니다.
반복당 200바이트가 40바이트 박스 5개와 정확히 일치합니다.
[벤치마크 코드](https://github.com/Frenil-client/unity-stat-system/tree/main/Benchmarks~)가 리팩토링 전후
구현을 나란히 돌려 매번 다시 재고, **CI가 0바이트를 강제**하므로 문서가 낡을 수 없습니다.
Unity가 물결로 끝나는 폴더를 임포트하지 않기 때문에 벤치마크는 패키지 사용자에게 딸려가지 않습니다.

**boxed 열거자 40 B/회** (mvvm)

`ObservableList<T>`가 `List<T>.Enumerator`를 그대로 반환하는 이유를 인터페이스 경유 열거와
나란히 재서 숫자로 남겼습니다.

**float 대신 long 고정소수점** (stat-system)

부동소수점 결과는 플랫폼과 최적화 옵션에 따라 마지막 자리가 갈립니다. 표시용으로 끝나면 문제가
없지만 같은 계산을 서로 다른 곳에서 돌려 같은 답이 나와야 하는 순간부터는 재현 불가능한 불일치가
됩니다. 그래서 모든 산술을 정수 연산으로 닫아, 같은 입력이면 어느 환경에서든 비트 단위로 같습니다.

### CI 구성

Unity Personal 라이선스는 `.ulf`에 MAC 주소가 박힌 **하드웨어 바인딩**이라 매번 새로 만들어지는
GitHub 러너에서 활성화되지 않습니다. 자체 호스팅 러너는 공개 저장소에서 포크 PR이 임의 코드를
실행할 수 있어 선택지가 아니고요.

그래서 "CI에서 Unity를 돌린다"를 포기하는 대신 **테스트를 Unity 없이 돌 수 있게** 만들었습니다.
`Tests~/`의 dotnet 프로젝트가 `Tests/`의 소스를 **그대로 컴파일**하므로 사본이 아니라 같은 테스트이고,
패키지 세 개의 테스트 148종 중 **124종이 CI에서 실행**됩니다. 초록 뱃지가 실제로 무언가를 증명합니다.

빠지는 24종은 성격이 분명합니다. 할당을 재는 9종은 판정자(`Is.Not.AllocatingGCMemory`)가
`UnityEngine.TestTools` 소속이고, 나머지 15종은 실제로 `GameObject`를 만들어 View를 붙입니다.
둘 다 Unity 없이는 의미가 없어서 Test Runner에 남겼습니다.
CI가 검증하지 못하는 범위를 숨기지 않기 위해 적어 둡니다.

---

## 툴, 자동화, 구조 설계

| 프로젝트 | 설명 |
|---|---|
| [unity-maplightdata-tool](https://github.com/Frenil-client/unity-maplightdata-tool) | 씬별 조명 환경을 ScriptableObject로 관리. Primary/Additive 스택 기반 자동 복원, Addressables 에디터 자동화 |
| [minigames](https://github.com/Frenil-client/minigames) | 확장형 씬 로딩 플랫폼. 허브 씬에서 콘텐츠를 Additive 로드/언로드하고, 폴더 1개와 데이터 에셋 1개만 추가하면 코드 수정 없이 확장되는 구조. `IMiniGame` 생명주기 계약, ScriptableObject 데이터 드리븐 등록, UIStackManager, RecycleScrollView |

### 레드닷 트리 디버거

![레드닷 트리 디버거](docs/images/reddot-debugger.gif)

레드닷 버그는 대부분 "왜 안 켜지지" 또는 "왜 안 꺼지지" 한 문장으로 들어오는데, 원인은 셋 중 하나입니다.
값이 안 들어왔거나, 노드가 잠겨 있거나, enum 값을 잘못 매겨 부모에 안 붙었거나. 셋 다 런타임에서는
같은 증상으로만 드러납니다.

그래서 실효 카운트를 **자기와 자식으로 분해**해 보여주고(`5 (0/5)`는 내 값은 0인데 자식 때문에 켜졌다는
뜻입니다), 값 주입과 잠금 토글로 서버 응답 없이 UI 반응을 확인할 수 있게 하고, enum 계층의 구조적
실수까지 한 화면에 모았습니다.

표시 내용은 순수 C#이 만들고 창은 그리기만 하며, **런타임과 같은 계층 유도 함수를 쓴다는 전제를
테스트로 고정**했습니다. 툴과 실행 결과가 어긋나는 건 디버깅 도구가 만들 수 있는 최악의 실패라서입니다.

---

## 성능 최적화 사례

| 프로젝트 | 설명 |
|---|---|
| [unity-spine-fx-lab](https://github.com/Frenil-client/unity-spine-fx-lab) | Spine 2D 런타임과 셰이더 제어. 디졸브, 히트플래시, 상태이상, 아웃라인을 MaterialPropertyBlock으로 머티리얼 증식 없이 일원 제어. **다중 인스턴스 58 -> 129 FPS**와 통합 투명 고스팅 두 건을 원인 분석부터 해결과 계측까지 정리. 오프스크린 컬링 기반 개선 포함 |
| [unity-urp-shader-lab](https://github.com/Frenil-client/unity-urp-shader-lab) | URP 기반 NPR 렌더링 랩. Shader Graph 없이 HLSL 직접 작성. 셀 셰이딩, SDF 페이스 셰도우, 헤어 이방성, 아웃라인. SDF/스무딩 노멀 베이커 등 아트 파이프라인 툴 6종 자작 |

---

## 기술 스택

`Unity` `C#` `UGUI` `NGUI` `MVVM` `ScriptableObject` `Addressables` `Protobuf` `URP` `HLSL` `Spine` `UniTask` `DOTween` `GitHub Actions`
