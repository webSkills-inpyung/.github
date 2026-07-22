# 🛠 운영자 메모 (내부용)

> 이 파일은 org 공개 페이지에 노출되지 않습니다. (공개 프로필은 `profile/README.md`)
> Owner만 참고하는 org 설정·운영 기록입니다.

## Org 권한 설정 현황 (Settings → Member privileges)

| 설정 | 값 | 목적 |
|---|---|---|
| **Base permissions** | `Read` | 전원이 모든 레포 **열람** 가능 (선배 기록 열람 목표) |
| **Repository creation** | Private 허용 | 부원이 본인 레포 생성 가능 (Public은 정책상 강제 on → 생성 시 Private 선택 안내) |
| **Repository deletion and transfer** | 비활성 | 레포 삭제·이전은 **Owner만** (본인 레포도 삭제 불가) |
| **Team creation** | 비활성 | 팀 생성은 Owner만 |
| **Repository discussions** | 비활성 | 토론 생성 제한 (댓글은 가능), 커뮤니티는 별도 앱으로 운영 예정 |
| **App access requests** | Members only | 외부 협력자는 앱 요청 불가 |
| **Repository visibility change** | 비활성 | Public↔Private 변경은 **Owner만** (대회 레포 유출 방지) |

### 핵심 원리
- 남의 레포 → base Read라 **열람만**, 수정·삭제 불가
- 본인 레포 → 생성자는 admin이지만, 삭제/공개변경은 org 설정으로 차단
- 대회 종료 → Owner가 **Archive** 처리해 읽기 전용으로 봉인

## 목표 접근 제어 모델 — 파트별 (현재는 base=Read로 임시 운영)

**원칙:** "선배 기록 열람" 목표를 **파트 단위로** 충족한다.

| 대상 | 열람 범위 |
|---|---|
| 웹 기능반 | 웹 관련 레포 (선배 웹 기록 포함) |
| 앱 기능반 | 앱 관련 레포 (선배 앱 기록 포함) |
| 교사 · 관리자(운영진) | **전체 레포** |

즉 웹 후배는 웹 선배 기록 전부를, 앱 후배는 앱 선배 기록 전부를 본다. 목표와 상충하지 않는다.

### 구현 방식
1. Base permissions → **`No permission`** (기본 접근 없음)
2. 팀별 Read 부여:

| 팀 | 접근 범위 |
|---|---|
| `@운영진` (교사·관리자) | 전체 레포 Read |
| `@web` | 웹 레포 Read |
| `@app` | 앱 레포 Read |

### ⚠️ 운영 비용 (전환 전 반드시 인지)
- `base = No permission`이면 **모든 레포를 해당 파트 팀에 Read로 배정**해야 그 파트가 볼 수 있다.
  배정 안 된 레포는 아무에게도(운영진 제외) 안 보인다.
- 따라서 **새 레포가 생길 때마다** `@web` 또는 `@app` 팀에 추가하는 절차가 필요하다.
  (네이밍의 `web`/`app` 토큰으로 어느 팀에 넣을지 판단)
- 지금의 `base = Read`는 이 배정 절차가 필요 없는 대신 전원이 전체를 본다.

### 전환 판단
- **파일럿(전국 4명) 동안은 `base = Read` 유지 권장** — 레포가 12개뿐이라 배정 관리 이득이 적다.
- 레포·기수가 쌓이고 파트 구분이 의미 있어지면 위 파트별 모델로 전환한다.

## 레포 네이밍 규칙 (요약)

```
{연도}-{nat|reg}-{web|app}-{이니셜}-{a|b|c}
예) 2026-nat-web-ytw-a
```
- `nat` = 전국(national) / `reg` = 지방(regional, 인천)
- 상세 안내는 `profile/README.md` 참고
