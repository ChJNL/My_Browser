# MyBrowser

## APK 다운로드

**[UI/UX 생성기 v0.2.0 프리뷰 APK 바로 다운로드](https://github.com/ChJNL/My_Browser/releases/download/v0.2.0-preview/UIUX-Generator-v0.2.0-preview.apk)** · [릴리스 상세 정보](https://github.com/ChJNL/My_Browser/releases/tag/v0.2.0-preview)

앱 이름은 `개발용 UI/UX 생성기`입니다. **기존 MyBrowser v0.1.0 프리뷰와 패키지명 및 서명이 같아, 설치하면 기존 앱을 업데이트하여 덮어쓸 수 있습니다.** 기기 설치 및 동작은 아직 검증되지 않았습니다.

- Android 8.0(API 26) 이상, ARM64·ARMv7·x86_64
- SHA-256: `6a9f994c3da2ac450ce5c0a81c654f4943f085cc55f42c9dd5af220290aeae7c`
- [이전 MyBrowser v0.1.0 프리뷰](https://github.com/ChJNL/My_Browser/releases/tag/v0.1.0-preview)

### GeckoView 기반 독립형 Android 웹 브라우저

MyBrowser는 Mozilla의 GeckoView 엔진을 활용하여 개발하는 독립형 Android 브라우저입니다.

기존 Chrome이나 Chromium 엔진에 의존하지 않고, Firefox와 동일한 Gecko 엔진 계열의 기술을 활용하여 웹사이트에 접속할 수 있는 독립적인 앱을 만드는 것을 목표로 합니다.

APK를 설치하려면 Android에서 다운로드에 사용한 앱의 알 수 없는 앱 설치를 허용해야 할 수 있습니다. 프리뷰 패키지 `io.github.chjnl.mybrowser.preview`는 일반 배포 패키지와 이름이 달라 기존 일반 배포 앱을 업데이트하지 않습니다.

현재 저장소에는 이 APK들의 앱 소스와 빌드 구성이 포함되어 있지 않습니다. 릴리스 태그는 APK와 일치하는 소스 버전을 보증하지 않습니다.

---

## 1. 프로젝트 소개

### 개발 목적

기존 브라우저에 의존하지 않는 나만의 독립적인 웹사이트 접속용 Android 앱을 개발합니다.

Mozilla GeckoView를 앱 내부에 통합하여 사용자가 URL을 입력하면 별도의 브라우저 앱을 실행하지 않고도 웹사이트에 직접 접속할 수 있도록 구현합니다.

### 핵심 개발 방향

- Chromium 및 Chrome 엔진 미사용
- Mozilla GeckoView 엔진 사용
- Android 네이티브 앱으로 개발
- 웹사이트 접속에 필요한 최소 기능만 구현
- 불필요한 브라우저 기능 및 복잡한 UI 배제
- 안정적이고 간결한 사용 환경 제공

---

## 2. 기술 스택

| 구분 | 사용 기술 |
|---|---|
| 플랫폼 | Android |
| 개발 언어 | Kotlin |
| 개발 환경 | Android Studio |
| 렌더링 엔진 | Mozilla GeckoView |
| UI 구성 | XML Layout |
| 빌드 시스템 | Gradle Kotlin DSL |
| 버전 관리 | Git / GitHub |

### GeckoView

Mozilla에서 제공하는 Android용 웹 렌더링 엔진입니다.

Firefox와 동일한 Gecko 엔진 계열을 사용하며, Android 애플리케이션 내부에서 웹페이지를 표시할 수 있도록 지원합니다.

공식 저장소: https://github.com/mozilla/geckoview

---

## 3. 핵심 기능

MyBrowser는 웹사이트 접속이라는 단일 목적에 집중합니다.

### 웹사이트 접속
- URL 주소 입력
- 웹사이트 접속 및 렌더링
- HTTP / HTTPS 지원
- URL 자동 보정
- 검색어 입력 시 검색 엔진 연동
- JavaScript 기반 웹사이트 지원

### 기본 페이지 제어
- 뒤로 가기
- 앞으로 가기
- 페이지 새로고침
- 페이지 로딩 상태 표시
- 로딩 진행률 표시
- 웹페이지 제목 표시

### 사용자 인터페이스
- 심플하고 미니멀한 디자인
- 다크 모드 기본 적용
- 직관적인 주소 입력창
- 웹페이지 표시 영역
- 기본 내비게이션 버튼
- 모바일 환경에 최적화된 화면 구성

---

## 4. UI / UX 설계

복잡한 브라우저 인터페이스를 지양하고 웹사이트 접속에 필요한 요소만 배치합니다.

### 기본 화면 구성

| 영역 | 구성 요소 |
|---|---|
| 상단 | URL 주소 입력창 |
| 중앙 | GeckoView 웹페이지 표시 영역 |
| 하단 | 뒤로 가기, 앞으로 가기, 새로고침 |

### 디자인 원칙

- 불필요한 장식과 메뉴 최소화
- 직관적인 화면 구성
- 모바일 조작 편의성 확보
- 일관된 아이콘 및 디자인
- 다크 테마 중심의 인터페이스

---

## 5. 개발 범위

MyBrowser는 웹사이트 접속 전용 앱이므로 다음 기능은 개발 범위에서 제외합니다.

- 다중 탭 시스템
- 즐겨찾기
- 방문 기록
- 다운로드 관리자
- 확장 프로그램
- 광고 차단 시스템
- 별도의 계정 시스템
- 복잡한 브라우저 설정
- 동기화 기능

---

## 6. 개발 환경 및 라이선스

### 개발 환경
- Windows
- Android Studio
- Kotlin
- Android SDK
- Gradle
- Git

### 라이선스 및 비용

GeckoView는 Mozilla Public License 2.0(MPL 2.0) 기반의 오픈소스 소프트웨어입니다.

- 엔진 사용료: 무료
- 개인 프로젝트 사용: 가능
- 상업적 이용: 가능
- 소스 코드 수정: 가능
- 앱 배포: 라이선스 조건 준수 시 가능

단, GeckoView 및 관련 구성 요소의 저작권과 라이선스 고지, 수정된 MPL 적용 파일의 소스 제공 등 MPL 2.0의 의무를 준수합니다.

라이선스: https://www.mozilla.org/en-US/MPL/2.0/

---

## 7. 프로젝트 개발 목표

최종 목표는 Mozilla GeckoView를 기반으로 작동하는 독립형 Android 웹사이트 접속 앱을 완성하는 것입니다.

사용자가 앱을 실행하고 URL을 입력하면 앱 내부에서 해당 웹사이트가 정상적으로 표시되는 것을 핵심 완성 기준으로 삼습니다.

**MyBrowser는 다양한 브라우저 기능을 제공하는 것이 아니라, 웹사이트 접속이라는 하나의 목적을 간결하고 안정적으로 수행하는 것을 지향합니다.**
