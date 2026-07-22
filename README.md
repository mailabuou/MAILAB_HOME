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

### 1. Google Cloud 프로젝트 준비

1. 공용 관리자 계정으로 [Google Cloud Console](https://console.cloud.google.com/)에 접속합니다.
2. 새 프로젝트를 만들고 **Google Drive API**를 활성화합니다.
3. **Google Auth Platform → Branding / Audience**에서 OAuth 동의 화면을 설정합니다.
4. 앱이 테스트 상태라면 공용 관리자 이메일을 테스트 사용자로 추가합니다.
5. **Clients**에서 `Web application` 유형의 OAuth Client ID를 만듭니다.
6. 승인된 JavaScript 원본에 다음 주소를 추가합니다.

```text
https://mailabuou.github.io
http://localhost:8000
```

7. API Key를 만들고 가능하면 HTTP referrer를 위 주소로, API 사용 범위를 Google Drive API로 제한합니다.

### 2. HTML 설정값 입력

`index.html`의 `drive-config` 블록에 Client ID, API Key와 관리자 이메일을 입력합니다. 첫 설정에서는 `dataFileId`를 비워 둡니다.

```js
const DRIVE_CONFIG = {
  clientId: "123456789-....apps.googleusercontent.com",
  apiKey: "AIza...",
  dataFileId: "",
  adminEmail: "shared-admin@example.com"
};
```

이 변경을 `main`에 배포한 뒤 홈페이지에서 **관리 모드**를 누르고 공용 계정으로 인증합니다. 홈페이지가 최초 `mailab-site-data.json` 파일을 만들고 공개 읽기 권한을 설정한 뒤 파일 ID를 클립보드에 복사합니다.

복사된 ID를 `dataFileId`에 넣고 한 번 더 배포합니다.

```js
dataFileId: "1AbCdEf..."
```

이 두 번째 배포 이후에는 콘텐츠를 수정할 때 GitHub 커밋이 필요하지 않습니다.

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

업로드 이미지는 Data URL로 HTML 내부에 저장됩니다. 이미지가 많거나 용량이 크면 브라우저 저장 한도를 초과할 수 있으므로 업로드 과정에서 자동 리사이즈와 JPEG 압축을 수행합니다.

## 프로젝트 구조

```text
MAILAB_HOME/
├── index.html   # 스타일, 콘텐츠 데이터, 관리자 UI 및 애플리케이션 로직
└── README.md    # 프로젝트 및 운영 문서
```

---

Built for **MAILAB · Medical Artificial Intelligence Laboratory, University of Ulsan**.
