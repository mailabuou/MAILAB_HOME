# MAILAB Homepage

> Medical Artificial Intelligence Laboratory  
> Department of ICT Convergence · University of Ulsan

설명 가능하고 신뢰할 수 있는 의료 인공지능을 연구하는 **MAILAB**의 공식 연구실 홈페이지입니다. 의료 영상, 생체 신호, 뇌–컴퓨터 인터페이스와 임상 의사결정 지원 연구를 소개하며, 별도의 프레임워크나 데이터베이스 없이 하나의 HTML 파일로 운영됩니다.

## Live site

- Website: <https://mailabuou.github.io/MAILAB_HOME/>
- Repository: <https://github.com/mailabuou/MAILAB_HOME>

## 주요 구성

| 영역 | 내용 |
| --- | --- |
| Home | 연구실 소개, 연구 분야, 주요 실적 통계와 최근 소식 |
| Professor | 교수 프로필, 연구 관심사, 학력 및 주요 활동 |
| People | 박사·석사·학부 인턴·졸업생 구성원 정보 |
| News | 학회, 게재, 수상, 행사 등 연구실 소식 |
| Papers | 논문 검색, 연도 필터, 등급·태그·외부 링크 |
| Patents | 특허 검색, 연도 필터, 상태·태그·외부 링크 |
| Contact | 연구실 위치, 이메일, 지도와 문의 메일 작성 |

## 관리자 모드 사용법

1. 홈페이지 오른쪽 아래의 **관리 모드**를 선택합니다.
2. 허용된 공용 Google 계정으로 로그인합니다.
3. 원하는 항목을 추가하거나 `수정`, `삭제` 버튼으로 편집합니다.
4. 각 편집창의 `저장` 버튼을 누르면 Google Drive의 공용 데이터 파일이 갱신됩니다.
5. 다른 컴퓨터와 일반 방문자도 새로고침하면 같은 최신 데이터를 확인할 수 있습니다.

> [!IMPORTANT]
> Google Drive 설정값이 비어 있을 때만 기존 `localStorage` 저장 방식으로 동작합니다. 운영 배포에서는 아래 Drive 설정을 완료하세요.

### 외부 링크 입력

Papers와 Patents에서는 한 줄에 하나씩 다음 형식 중 하나로 링크를 입력할 수 있습니다.

```text
https://example.com/document
PDF|https://example.com/document.pdf
Google Patents|patents.google.com/patent/...
```

`https://`가 없는 일반 도메인은 자동으로 HTTPS 주소로 정규화됩니다.

## 로컬에서 실행하기

빌드나 패키지 설치는 필요하지 않습니다. `index.html`을 직접 열어도 되지만, 브라우저 보안 정책과 동작을 실제 배포 환경에 가깝게 확인하려면 간단한 로컬 서버 사용을 권장합니다.

```powershell
python -m http.server 8000
```

이후 <http://localhost:8000>에 접속합니다.

## GitHub Pages 배포

이 프로젝트는 GitHub Pages를 통해 정적 사이트로 배포됩니다. 일반적인 작업 흐름은 다음과 같습니다.

```text
기능 브랜치 생성
  → index.html 수정 및 확인
  → 커밋 및 push
  → main 브랜치에 병합
  → GitHub Pages 자동 배포
```

배포 상태는 GitHub 저장소의 **Deployments → github-pages** 또는 **Settings → Pages**에서 확인할 수 있습니다.

콘텐츠 수정은 Google Drive에 저장되므로 GitHub 재배포가 필요하지 않습니다. GitHub 커밋과 배포는 HTML 코드, 디자인 또는 Drive 설정값을 변경할 때만 필요합니다.

## Google Drive 동기화 설정

Google Drive에는 이미지 Data URL을 포함한 전체 홈페이지 데이터가 `mailab-site-data.json` 한 파일로 저장됩니다. 파일은 공개 읽기 전용으로 공유되고, 쓰기는 지정한 Google 계정의 OAuth 인증을 거친 관리자에게만 허용됩니다.

> [!CAUTION]
> Google Cloud 상단의 **Start your Free Trial**은 누르지 마세요. 무료 체험, 카드 등록, 결제 프로필과 본인인증은 이 홈페이지 설정에 필요하지 않습니다.

### 1단계: 결제 없이 Cloud 프로젝트 만들기

1. 공용 관리자 계정으로 <https://console.cloud.google.com/projectcreate>에 접속합니다.
2. 프로젝트 이름을 `MAILAB Homepage`로 입력하고 **Create**를 누릅니다.
3. 화면 상단 프로젝트 선택기가 `MAILAB Homepage`인지 확인합니다.

### 2단계: Google Drive API 활성화

1. 왼쪽 `☰` → **APIs & Services → Library**로 이동합니다.
2. `Google Drive API`를 검색합니다.
3. **Enable**을 누릅니다. 버튼이 **Manage**라면 이미 활성화된 상태입니다.
4. **APIs & Services → Enabled APIs & services** 목록에 `Google Drive API`가 있는지 확인합니다.

API Key에 Drive 제한을 거는 것과 Drive API를 활성화하는 것은 별개이므로 이 단계를 생략하면 안 됩니다.

### 3단계: OAuth 동의 화면과 테스트 사용자 설정

1. **Google Auth Platform → Branding**에서 앱 이름을 `MAILAB Homepage`로 설정하고 연락처 이메일을 입력합니다.
2. **Audience**의 User type이 `External`, Publishing status가 `Testing`인지 확인합니다.
3. **Test users → Add users**를 눌러 실제 관리에 사용할 공용 Google 계정을 추가합니다.
4. **Data Access → Add or remove scopes**에서 다음 권한을 검색해 추가하고 저장합니다.

```text
https://www.googleapis.com/auth/drive.file
```

전체 Drive 권한인 `https://www.googleapis.com/auth/drive`는 선택하지 않습니다. `drive.file`은 이 홈페이지 앱이 생성한 파일만 관리합니다.

### 4단계: OAuth Client ID 만들기

1. **Google Auth Platform → Clients → Create client**로 이동합니다.
2. Application type은 **Web application**을 선택합니다.
3. 이름은 `MAILAB Homepage Web`으로 입력합니다.
4. **Authorized JavaScript origins**에 아래 두 주소를 각각 추가합니다.

```text
https://mailabuou.github.io
http://localhost:8000
```

5. **Authorized redirect URIs**는 비워둡니다.
6. **Create**를 누르고 `...apps.googleusercontent.com`으로 끝나는 Client ID를 복사합니다.
7. Client Secret은 이 홈페이지에서 사용하지 않습니다.

### 5단계: 브라우저용 API Key 만들기

1. **APIs & Services → Credentials → Create credentials → API key**로 이동합니다.
2. Name은 `MAILAB Homepage API Key`로 입력합니다.
3. **Select API restrictions**에서 `Google Drive API`를 선택합니다.
4. **Authenticate API calls through a service account**는 체크하지 않습니다.
5. **Application restrictions**에서 `Websites`를 선택합니다.
6. Website restrictions에 아래 두 주소를 각각 추가합니다.

```text
https://mailabuou.github.io/*
http://localhost:8000/*
```

7. **Create**를 누르고 `AIza...`로 시작하는 API Key를 복사합니다.

### 6단계: 첫 번째 설정 배포

`index.html`의 `drive-config` 블록에 Client ID, API Key와 공용 관리자 이메일을 입력합니다. `dataFileId`는 아직 비워둡니다.

```js
const DRIVE_CONFIG = {
  clientId: "123456789-....apps.googleusercontent.com",
  apiKey: "AIza...",
  dataFileId: "",
  adminEmail: "mailab.uou@gmail.com"
};
```

이 변경을 커밋하고 `main`에 병합하여 GitHub Pages에 배포합니다.

### 7단계: 최초 Drive 데이터 파일 생성

1. 배포된 홈페이지에서 **관리 모드**를 누릅니다.
2. 반드시 Test users에 등록한 공용 관리자 계정을 선택합니다.
3. `Google hasn't verified this app` 화면이 나타나면 직접 만든 테스트 앱이므로 **Continue**를 누릅니다.
4. 다음 Drive 권한이 표시되는지 확인하고 허용합니다.

```text
See, edit, create, and delete only the specific Google Drive files you use with this app
```

5. 성공하면 Drive에 `mailab-site-data.json`이 생성되고 파일 ID가 클립보드에 복사됩니다.

클립보드를 놓쳤다면 Google Drive에서 `mailab-site-data.json`을 검색하고 **링크 복사**를 누릅니다. 다음 주소에서 `/d/`와 `/view` 사이 문자열이 파일 ID입니다.

```text
https://drive.google.com/file/d/1AbCdEfGhIjKlMn/view
                                ^^^^^^^^^^^^^^^
```

### 8단계: dataFileId 입력 후 마지막 배포

복사한 ID만 `dataFileId`에 입력합니다. Drive 링크 전체를 넣으면 안 됩니다.

```js
dataFileId: "1AbCdEfGhIjKlMn"
```

이 설정을 커밋하고 다시 `main`에 배포합니다. 이 두 번째 배포 이후에는 콘텐츠 수정 때 GitHub 커밋이 필요하지 않습니다.

### 최초 인증에서 403 insufficientPermissions가 발생할 때

Cloud 설정이 맞더라도 `drive.file`을 추가하기 전에 발급된 예전 액세스 토큰이 남아 있으면 다음 오류가 발생할 수 있습니다.

```text
403 · insufficientPermissions
ACCESS_TOKEN_SCOPE_INSUFFICIENT
```

다음 순서로 기존 권한을 지우고 다시 인증합니다.

1. 공용 관리자 계정으로 <https://myaccount.google.com/connections>에 접속합니다.
2. `MAILAB Homepage` 연결을 찾아 **모든 연결 삭제** 또는 **액세스 권한 삭제**를 누릅니다.
3. 홈페이지로 돌아와 `Ctrl + Shift + R`로 강력 새로고침합니다.
4. **관리 모드**를 다시 누르고 Drive 권한 동의를 새로 진행합니다.

그래도 실패하면 Chrome 개발자도구 `F12 → Network`에서 `files?uploadType=multipart...` 요청의 **Response**를 확인합니다. Response JSON의 `reason`과 `message`만 공유하고, Authorization 헤더나 액세스 토큰은 공유하지 마세요.

| 오류 reason | 의미 | 조치 |
| --- | --- | --- |
| `accessNotConfigured` | Drive API 미활성화 | Library에서 Google Drive API Enable |
| `insufficientPermissions` | 토큰에 `drive.file` 없음 | Google 계정 앱 연결 삭제 후 재동의 |
| `storageQuotaExceeded` | Drive 저장 공간 부족 | 공용 계정의 Drive/Gmail/Photos 용량 정리 |
| `origin_mismatch` | GitHub Pages 주소 미등록 | OAuth Client의 Authorized JavaScript origins 확인 |

### 동시 편집 보호

Drive 데이터에는 증가하는 `revision` 값이 포함됩니다. 저장 직전에 원격 revision을 다시 검사하며, 다른 관리자가 먼저 저장했다면 현재 저장을 중단하고 최신 데이터를 불러옵니다. 충돌 메시지가 나타나면 최신 내용을 확인한 뒤 수정을 다시 적용하세요.

### Drive 권한과 데이터 공개 범위

- OAuth 범위는 `drive.file`을 사용하여 이 앱이 생성한 파일에만 접근합니다.
- `mailab-site-data.json`은 홈페이지 방문자가 읽을 수 있도록 `anyone / reader` 권한이 설정됩니다.
- 공개 연구실 정보만 저장하고 민감한 정보, 비밀번호, API 비밀키는 데이터 파일에 넣지 마세요.
- OAuth Client ID와 제한된 브라우저용 API Key는 HTML에 포함되지만, Google 계정 쓰기 권한을 부여하지는 않습니다.
- `Client Secret`이나 Google 계정 비밀번호는 절대로 저장소에 넣지 마세요.

## 데이터와 저장 구조

홈페이지 데이터는 `index.html` 내부의 `script#data`에 JavaScript 객체로 포함됩니다.

- `NEWS`: 연구실 소식
- `PEOPLE`: 구성원
- `PAPERS`: 논문
- `PATENTS`: 특허
- `PROF`: 교수 정보

운영 환경에서는 관리자 모드에서 편집한 데이터가 Google Drive의 `mailab-site-data.json`에 저장됩니다. Drive 설정이 없는 개발·예비 환경에서만 `localStorage`의 `mailab_db`를 사용합니다. **백업 파일 저장** 기능으로 현재 데이터를 포함한 `index.html`을 내려받을 수도 있습니다.

업로드 이미지는 자동 리사이즈와 JPEG 압축을 거친 Data URL로 변환되어 Drive의 JSON 데이터에 함께 저장됩니다. 별도의 이미지 서버는 사용하지 않으며, 원본과 크롭 상태도 같은 데이터 파일에서 관리합니다. Drive 미설정 예비 모드에서는 브라우저 저장 한도가 적용될 수 있습니다.

## 프로젝트 구조

```text
MAILAB_HOME/
├── index.html   # 스타일, 콘텐츠 데이터, 관리자 UI 및 애플리케이션 로직
└── README.md    # 프로젝트 및 운영 문서
```

---

Built for **MAILAB · Medical Artificial Intelligence Laboratory, University of Ulsan**.
