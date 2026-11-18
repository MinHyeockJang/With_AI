# GitHub API 첫 조회

API는 프로그램이 다른 프로그램에 무엇을 요청할 수 있고, 어떤 형식으로 응답을 받는지 정한 규칙이다. 이번에는 PowerShell에서 GitHub API에 공개 저장소 `With_AI`의 정보를 요청했다.

## PowerShell에서 실습하기

입력 줄이 `PS C:\...>`로 시작하는지 확인한다. 명령 프롬프트(CMD)라면 `powershell`을 입력하고 Enter를 누른다. 아래 명령은 첫 글자인 `$`부터 한 줄씩 입력한다.

```powershell
$repo = Invoke-RestMethod -Method Get -Uri "https://api.github.com/repos/MinHyeockJang/With_AI"
$repo.name
```

첫 줄을 실행하면 GitHub가 보낸 JSON 응답을 PowerShell이 읽어 `$repo`에 저장한다. 저장만 하므로 화면에 출력이 없어도 정상이다. 같은 창에서 둘째 줄을 실행하면 저장소 이름인 `With_AI`가 출력된다.

| 명령의 부분 | 의미 |
| --- | --- |
| `$repo` | GitHub 응답을 담을 변수. `$`는 PowerShell에서 변수 이름 앞에 붙인다. |
| `=` | 오른쪽 명령의 실행 결과를 왼쪽 변수에 저장한다. |
| `Invoke-RestMethod` | 웹 API에 요청을 보내고 응답을 읽는 PowerShell 명령이다. |
| `-Method Get` | HTTP의 `GET` 방식으로 정보를 조회한다. |
| `-Uri "https://..."` | 요청을 보낼 주소를 지정한다. `/repos/소유자/저장소`에서 조회 대상을 고를 수 있다. |
| `$repo.name` | 응답에서 저장소 이름만 꺼낸다. |

## 응답에서 다른 항목 꺼내기

| 입력 | 이번 실습의 결과 | 의미 |
| --- | --- | --- |
| `$repo.name` | `With_AI` | 저장소 이름 |
| `$repo.visibility` | `public` | 공개 범위 |
| `$repo.default_branch` | `main` | 기본 브랜치 |
| `$repo.owner.login` | `MinHyeockJang` | 소유자의 로그인 이름 |

## 실습 중 자주 틀린 부분

- `Invoke=RestMethod` 대신 `Invoke-RestMethod`를 쓴다. `=`는 `$repo` 뒤의 대입 위치에 쓴다.
- `-Uri`는 하이픈과 `Uri`를 붙여 쓴다. 도메인은 `api.github.com`이다.
- “외부 명령, 실행할 수 있는 프로그램 또는 배치 파일이 아닙니다”라는 오류가 나오면 CMD에서 실행했을 수 있다. 입력 줄 앞에 `PS`가 있는지 확인한다.
- PowerShell에서 `$repo.name`으로 항목을 꺼낼 수 있는 이유는 응답을 이름과 값이 있는 데이터로 다루기 때문이다.

## 다른 곳에서도 요청할 수 있나?

인터넷에서 접근할 수 있는 API라면 다른 컴퓨터에서도 요청할 수 있다. [이번 실습의 API 주소](https://api.github.com/repos/MinHyeockJang/With_AI)를 브라우저로 열어 JSON 응답을 볼 수도 있고, Python에서도 같은 주소로 요청할 수 있다.

이 공개 저장소 조회에는 인증 토큰이 필요 없다. 비공개 저장소나 개인 일정처럼 접근이 제한된 데이터는 해당 서비스의 인증과 권한이 필요하다. 주소, 요청 방식, 인증 조건은 각 서비스의 API 문서에서 확인한다. [GitHub 저장소 조회 API 문서](https://docs.github.com/en/rest/repos/repos#get-a-repository)
