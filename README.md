# 🛠 운영자 메모 (내부용)

> 이 파일은 org 공개 페이지에 노출되지 않습니다. (공개 프로필은 `profile/README.md`)
> Owner만 참고하는 org 설정·운영 기록입니다.

## Org 권한 설정 현황 (Settings → Member privileges)

| 설정 | 값 | 목적 |
|---|---|---|
| **Base permissions** | `Read` (→ `No permission` 전환 예정) | 파트별 모델 세팅 시 No permission으로 내림 (아래 참고) |
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

## 접근 제어 모델 — 파트별 (✅ 채택, 세팅은 다음 진행)

**결정:** 아래 파트별 모델을 정식 채택한다. "선배 기록 열람" 목표를 **파트 단위로** 충족한다
(웹 후배는 웹 선배 기록 전부, 앱 후배는 앱 선배 기록 전부). 목표와 상충하지 않는다.
기존 레포는 없으므로 마이그레이션 없이 파일럿부터 이 모델로 시작한다.

### 원칙

| 대상 | 열람 범위 | 구현 |
|---|---|---|
| 웹 기능반 학생 | 웹 레포 (선배 웹 포함) | `@web` 팀 Read |
| 앱 기능반 학생 | 앱 레포 (선배 앱 포함) | `@app` 팀 Read |
| 교사 | 전체(웹+앱), **삭제권 없음** | `@web`·`@app` **둘 다** 가입 |
| 총괄관리자(나) | 전체 | Owner (자동) |

> 교사를 Owner로 올리지 않는 이유: 삭제·설정 권한은 총괄관리자만 갖기 위함.
> 두 팀에 모두 넣으면 전체 열람은 되되 삭제권은 없다.

### 세팅 순서 (다음에 진행)
1. Teams → New team 으로 `web`, `app` 생성 (base가 Read인 지금/전환 전에 먼저)
2. 팀 배정 — 교사: `@web`·`@app` 둘 다 / 학생: 본인 파트 팀
3. Settings → Member privileges → Base permissions → **`No permission`**
4. 각 레포 → Settings → Collaborators and teams → Add team → 해당 파트 팀, Role: **Read**

### 운영 루틴 (레포 ↔ 팀 배정) — 핵심 비용
- `base = No permission`이면 **팀에 배정된 레포만** 그 파트가 본다. 배정 안 된 레포는 안 보임.
- **레포 생성자(=본인 레포 admin)가 직접** 본인 레포에 `@web`/`@app`을 Read로 추가하도록 규칙화
  → 운영자 부담 최소화. (네이밍의 `web`/`app` 토큰으로 어느 팀인지 자명)
- Owner는 빠뜨린 레포 없는지 감사만.

## 레포 네이밍 규칙 (요약)

```
{연도}-{nat|reg}-{web|app}-{이니셜}-{a|b|c}
예) 2026-nat-web-ytw-a
```
- `nat` = 전국(national) / `reg` = 지방(regional, 인천)
- 상세 안내는 `profile/README.md` 참고
