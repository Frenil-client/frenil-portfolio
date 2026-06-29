# 정휘현 — Unity Client Programmer

Unity / C# 기반 클라이언트 프로그래머입니다.
렌더링 구조 설계, 에디터 툴 개발, 시스템 설계를 주로 다룹니다.

📧 silsen@naver.com

---

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
<td>URP 기반 서브컬쳐(애니메이션) 스타일 NPR 렌더링 랩. Shader Graph 없이 HLSL 직접 작성 — 셀 셰이딩·SDF 페이스 셰도우·헤어 이방성·아웃라인 구현 + SDF/스무딩 노멀 베이커 등 NPR 아트 파이프라인 툴 직접 설계</td>
</tr>
<tr>
<td><a href="https://github.com/Frenil-client/unity-spine-fx-lab">unity-spine-fx-lab</a></td>
<td style="white-space: nowrap;">렌더링 / 런타임 시스템</td>
<td>Unity 6 URP 2D 기반 Spine 2D 런타임 + 셰이더 제어 시스템 랩. Shader Graph 없이 HLSL 직접 작성 — 디졸브·히트플래시·상태이상·아웃라인을 MaterialPropertyBlock 으로 일원 제어(머티리얼 증식 없이). 다중 인스턴스 성능(오프스크린 컬링 58→129 FPS)·통합 투명 고스팅(RT 평탄화) 두 실무 문제를 원인 분석→해결→증거로 정리</td>
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
<td>미니게임 플랫폼. 허브 씬에서 게임을 Additive 로드/언로드하는 확장형 구조 — IMiniGame 생명주기 계약, ScriptableObject 데이터 드리븐 게임 등록, 타워 디펜스·타이밍 게임 2종 구현</td>
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

## 기술 스택

`Unity` `C#` `URP` `HLSL` `Spine` `UGUI` `Addressables` `ScriptableObject` `MVVM`
