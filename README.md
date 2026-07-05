# 정휘현 - Unity Client Programmer

모바일 수집형 RPG에서 가챠, 인앱 결제, 스탯, 던전 등 핵심 시스템을 설계하고 운영해 온 Unity C# 클라이언트 프로그래머입니다.
렌더링 구조 설계, 에디터 툴 개발, 시스템 설계를 주로 다룹니다.

📧 silsen@naver.com

---

## Highlights

- **Spine 2D 300체 스트레스 테스트: CPU 13.07ms → 4.29ms(약 3배), 58 FPS → 129 FPS** - 드로우콜 변화 없이 오프스크린 스켈레톤의 애니메이션 갱신 비용 제거가 본질임을 프로파일링으로 규명
- **서브컬처 스타일 NPR 렌더링 6종 기법 + 에디터 툴 6종** - Shader Graph 없이 HLSL 직접 작성, 비개발자도 운용 가능한 아트 파이프라인 구성
- **EditMode/NUnit 단위 테스트 34개, UPM 패키지 4종 배포** - 실무 시스템을 설치/테스트 가능한 범용 라이브러리로 재구현
- **Spec-Driven Development 워크플로우 공개 실증** - SPEC.md 명세 작성, 태스크 분해, 구현, 검증을 기능 단위 커밋으로 공개

## Featured

<table>
<tr>
<td width="50%">
<img src="https://raw.githubusercontent.com/Frenil-client/unity-spine-fx-lab/main/Docs/gifs/Benchmark.gif" alt="Spine 2D 300체 벤치마크" width="100%">
</td>
<td width="50%">
<img src="https://raw.githubusercontent.com/Frenil-client/unity-urp-shader-lab/main/Docs/gifs/Demo_Full.gif" alt="서브컬처 스타일 NPR 렌더링 데모" width="100%">
</td>
</tr>
<tr>
<td>
<b><a href="https://github.com/Frenil-client/unity-spine-fx-lab">unity-spine-fx-lab</a></b><br>
Spine 2D 다중 인스턴스 성능 문제를 spine-unity 4.3 구조에서 원인 규명 후 해결.
300체 기준 <b>CPU 13.07ms → 4.29ms, 58 → 129 FPS</b>.
PMA 블렌딩 누적 알파 손실로 인한 투명 고스팅을 RT 평탄화 후 단일 알파 합성으로 해결.
</td>
<td>
<b><a href="https://github.com/Frenil-client/unity-urp-shader-lab">unity-urp-shader-lab</a></b><br>
자작 VRoid 모델 위에 HLSL 직접 작성으로 재현한 서브컬처 스타일 NPR 렌더링.
램프 셀 셰이딩, SDF 페이스 셰도우, Kajiya-Kay 헤어 하이라이트, 림라이트, 인버티드 헐 아웃라인, 하프톤 포스트.
<b>SDF 베이커 등 에디터 툴 6종</b>으로 파이프라인 구성.
</td>
</tr>
</table>

## Projects

<table>
<thead>
<tr>
<th width="200">프로젝트</th>
<th width="170">분류</th>
<th>설명</th>
</tr>
</thead>
<tbody>
<tr>
<td><a href="https://github.com/Frenil-client/unity-urp-shader-lab">unity-urp-shader-lab</a></td>
<td style="white-space: nowrap;">렌더링 / 셰이더</td>
<td>URP 기반 서브컬처(애니메이션) 스타일 NPR 렌더링 랩. Shader Graph 없이 HLSL 직접 작성 - 셀 셰이딩, SDF 페이스 셰도우, 헤어 이방성, 아웃라인 구현 + SDF/스무딩 노멀 베이커 등 NPR 아트 파이프라인 툴 직접 설계</td>
</tr>
<tr>
<td><a href="https://github.com/Frenil-client/unity-spine-fx-lab">unity-spine-fx-lab</a></td>
<td style="white-space: nowrap;">렌더링 / 런타임 시스템</td>
<td>Unity 6 URP 2D 기반 Spine 2D 런타임 + 셰이더 제어 시스템 랩. Shader Graph 없이 HLSL 직접 작성 - 디졸브, 히트플래시, 상태이상, 아웃라인을 MaterialPropertyBlock으로 일원 제어(머티리얼 증식 없이). 다중 인스턴스 성능(오프스크린 컬링 <b>58 → 129 FPS</b>), 통합 투명 고스팅(RT 평탄화) 두 실무 문제를 원인 분석 → 해결 → 증거로 정리</td>
</tr>
<tr>
<td><a href="https://github.com/Frenil-client/unity-maplightdata-tool">unity-maplightdata-tool</a></td>
<td style="white-space: nowrap;">렌더링 / 에디터 툴</td>
<td>씬별 조명 환경을 ScriptableObject로 관리. Primary/Additive 스택 기반 자동 복원, Addressables 에디터 자동화 포함</td>
</tr>
<tr>
<td><a href="https://github.com/Frenil-client/unity-mvvm">unity-mvvm</a></td>
<td style="white-space: nowrap;">UI 시스템</td>
<td>Unity UGUI 환경을 위한 경량 MVVM 프레임워크. Observable 기반 데이터 바인딩, 외부 라이브러리 없이 구현</td>
</tr>
<tr>
<td><a href="https://github.com/Frenil-client/minigames">minigames</a></td>
<td style="white-space: nowrap;">게임플레이 / 아키텍처</td>
<td>미니게임 플랫폼. 허브 씬에서 게임을 Additive 로드/언로드하는 확장형 구조 - IMiniGame 생명주기 계약, ScriptableObject 데이터 드리븐 게임 등록, 타워 디펜스/타이밍 게임 2종 구현</td>
</tr>
<tr>
<td><a href="https://github.com/Frenil-client/unity-stat-system">unity-stat-system</a></td>
<td style="white-space: nowrap;">시스템 설계</td>
<td>제네릭 기반 RPG 스탯 시스템. StatId enum, Reflection 캐싱, MaxValue 무결성 검사 포함</td>
</tr>
<tr>
<td><a href="https://github.com/Frenil-client/unity-reddot-system">unity-reddot-system</a></td>
<td style="white-space: nowrap;">UI 시스템</td>
<td>트리 구조 기반 레드닷 시스템. enum 노드 타입, 자동 상위 전파, 카운트 아이콘 지원</td>
</tr>
</tbody>
</table>

위 4종(stat/reddot/mvvm/maplightdata)은 실무에서 설계한 구조를 범용 재사용 라이브러리로 재구현한 것으로, 모두 **EditMode/NUnit 단위 테스트(총 34개)** 를 포함해 **UPM 패키지** 형태로 설치할 수 있습니다.

## Background

모바일 수집형 RPG 클라이언트 개발을 중심으로 세 프로젝트를 거쳤습니다.

- **아야카시라이즈**(모바일 수집형 RPG) - 신작 풀사이클(CBT, 런칭, 라이브 서비스) 참여. 가챠/인앱 결제 상태 머신, 7종 소스 스탯 캐시(버전 기반 무효화), 조명/카메라 아키텍처, UI 리소스 파이프라인 에디터 툴
- **트리오브세이비어 M**(모바일 MMORPG) - 출시 안정화부터 정식 런칭, 라이브 서비스 운영 참여. NGUI 핵심 콘텐츠 전담, 커스텀 타임라인 연출 툴, NGUI 환경 Particle System Clipping용 HLSL 커스텀 셰이더
- **모바일 퍼즐 RPG 2종** - 퍼즐/전투 로직, Photon Network 멀티플레이, 공통 개발 프레임워크 구축

## Workflow

Claude Code 기반 **Spec-Driven Development**를 개인 프로젝트 전반에 적용하고 있습니다. SPEC.md/CLAUDE.md 명세 작성 → 태스크 분해 → 구현 → 검증의 전 과정을 기능 단위 커밋으로 공개했으며, 단위 테스트 작성, UPM 패키지화, 라이선스 정리까지 포함한 품질 관리 체계를 함께 운용합니다. 과정은 [unity-urp-shader-lab](https://github.com/Frenil-client/unity-urp-shader-lab)과 [unity-spine-fx-lab](https://github.com/Frenil-client/unity-spine-fx-lab)의 커밋 히스토리에서 확인할 수 있습니다.

## Tech Stack

`Unity` `C#` `URP` `HLSL` `Spine` `UGUI` `Addressables` `ScriptableObject` `MVVM`

---

📧 silsen@naver.com
