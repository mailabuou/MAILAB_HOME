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
2. 관리자 비밀번호로 로그인합니다.
3. 원하는 항목을 추가하거나 `수정`, `삭제` 버튼으로 편집합니다.
4. 각 편집창의 `저장` 버튼을 눌러 현재 브라우저에 임시 저장합니다.
5. 편집이 끝나면 **사이트 파일로 저장**을 눌러 갱신된 `index.html`을 내려받습니다.
6. 내려받은 파일을 이 저장소의 `index.html`과 교체하고 GitHub에 반영합니다.

> [!IMPORTANT]
> 편집창의 `저장`은 현재 브라우저의 `localStorage`에만 저장합니다. 공개 홈페이지를 변경하려면 새 `index.html`을 커밋하고 GitHub Pages 배포 브랜치에 push해야 합니다.

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

## 데이터와 저장 구조

홈페이지 데이터는 `index.html` 내부의 `script#data`에 JavaScript 객체로 포함됩니다.

- `NEWS`: 연구실 소식
- `PEOPLE`: 구성원
- `PAPERS`: 논문
- `PATENTS`: 특허
- `PROF`: 교수 정보

관리자 모드에서 편집한 데이터는 먼저 `localStorage`의 `mailab_db`에 저장됩니다. **사이트 파일로 저장**을 실행하면 현재 데이터를 직렬화하여 새로운 `index.html` 안에 포함합니다.

업로드 이미지는 Data URL로 HTML 내부에 저장됩니다. 이미지가 많거나 용량이 크면 브라우저 저장 한도를 초과할 수 있으므로 업로드 과정에서 자동 리사이즈와 JPEG 압축을 수행합니다.

## 프로젝트 구조

```text
MAILAB_HOME/
├── index.html   # 스타일, 콘텐츠 데이터, 관리자 UI 및 애플리케이션 로직
└── README.md    # 프로젝트 및 운영 문서
```

---

Built for **MAILAB · Medical Artificial Intelligence Laboratory, University of Ulsan**.
