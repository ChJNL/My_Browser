# 개발 계획과 구현 상태

## 승인 범위

GeckoView, Kotlin, XML Layout, Gradle Kotlin DSL로 단일 화면·단일 세션 Android 브라우저를 구현합니다. GitHub를 통해 APK를 배포합니다.

다중 탭, 즐겨찾기, 방문 기록 관리, 다운로드 관리자, 확장 프로그램, 광고 차단, 계정, 동기화는 구현 범위에서 제외합니다.

## 작업 스텝

| 작업 스텝 | 산출물 | 상태 |
|---|---|---|
| 1. 빌드 기반 구성 | Android 프로젝트, Gradle Wrapper, 고정 의존성 버전 | 구성 완료, 전체 빌드 검증 대기 |
| 2. GeckoView 통합 | 프로세스별 런타임, 단일 세션, 활성 상태 처리 | 코드 작성 완료, 기기 검증 대기 |
| 3. 주소·검색 처리 | HTTPS 보정, 검색어 인코딩, URL 검증 | 단위 테스트 8개 통과 |
| 4. 화면과 페이지 제어 | 다크 테마, 주소, 제목, 진행률, 뒤로·앞으로·새로고침 | 코드 작성 완료, 기기 검증 대기 |
| 5. 안정성 검증 | 접속 오류 안내, 재시도, 회전·복귀 처리 | 코드 작성 완료, 통합 검증 대기 |
| 6. 문서 및 배포 | 빌드·검증·배포 문서, GitHub Actions, 서명한 APK 배포 절차 | 구성 완료, 실제 배포 대기 |

## 초기 결정

- 앱 식별자는 `io.github.chjnl.mybrowser`입니다.
- 최소 지원 버전은 Android 8.0(API 26)입니다. 초기 검증 대상을 제한하기 위한 선택입니다.
- 컴파일 SDK와 대상 SDK는 36입니다.
- 검색 엔진은 DuckDuckGo입니다. API 키 없이 검색어를 URL로 전달합니다.
- 앱 화면은 기본 다크 테마입니다. 웹사이트의 화면 색상을 강제로 변경하지 않습니다.
- 스킴이 없는 주소는 HTTPS로 엽니다. HTTP는 사용자가 명시한 경우 지원합니다.
- 서명한 배포 APK는 모든 포함 아키텍처를 묶은 단일 APK로 생성합니다.
- 배포 키가 없으면 배포 빌드가 실패하도록 구성합니다.
- 사용자 정보 입력창이 있는 페이지에서 카메라·마이크·위치·파일 선택 등의 기능은 초기 구현에 포함하지 않습니다.
- 화면 회전에서는 같은 세션을 유지합니다. 프로세스가 종료되면 현재 주소만 다시 엽니다.

## 기술 참고 문서

- GeckoView 시작 안내: https://firefox-source-docs.mozilla.org/mobile/android/geckoview/consumer/geckoview-quick-start.html
- GeckoView API: https://mozilla.github.io/geckoview/javadoc/mozilla-central/
- AGP 8.13 호환성: https://developer.android.com/build/releases/agp-8-13-0-release-notes
- Gradle 배포 체크섬: https://gradle.org/release-checksums/
- GitHub Actions 비밀값: https://docs.github.com/en/actions/how-tos/write-workflows/choose-what-workflows-do/use-secrets

GeckoView 배포 저장소를 이 환경에서 직접 조회하지 못했습니다. 고정한 버전의 실제 해석과 API 호환성은 첫 온라인 빌드에서 반드시 확인해야 합니다.
