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

## 향후 옵션 — 파트별 접근 제어 (지금은 미적용)

현재 `base = Read`라 전원이 모든 레포를 본다. 파트별로 **가리고 싶어지면** 아래로 전환:

1. Base permissions → **`No permission`** 으로 변경 (기본 접근 없음)
2. 팀을 만들고 팀별로 Read 부여:

| 팀 | 접근 범위 |
|---|---|
| `@운영진` | 전체 레포 Read |
| `@web` | 웹 관련 레포만 Read |
| `@app` | 앱 관련 레포만 Read |

> ⚠️ 이 방식은 "전원이 선배 기록 다 열람"이라는 원래 목표와 상충한다.
> 특정 레포를 특정 파트에게만 보이게 할 필요가 생겼을 때만 전환할 것.

## 레포 네이밍 규칙 (요약)

```
{연도}-{nat|reg}-{web|app}-{이니셜}-{a|b|c}
예) 2026-nat-web-ytw-a
```
- `nat` = 전국(national) / `reg` = 지방(regional, 인천)
- 상세 안내는 `profile/README.md` 참고
