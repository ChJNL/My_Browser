# GitHub APK 배포

배포 대상 저장소는 https://github.com/ChJNL/My_Browser 입니다. 일반 사용자는 저장소의 **Releases**에서 서명된 APK를 내려받습니다.

## 배포 구조

| 발생 조건 | 검사 및 산출물 |
|---|---|
| 브랜치 푸시, 풀 리퀘스트, 수동 빌드 | 단위 테스트, 정적 검사, 디버그 APK를 실행·생성합니다. APK는 Actions 산출물로 14일 보관합니다. |
| `v0.1.0` 형식의 태그 푸시 | 태그와 앱 버전을 대조하고 검사한 뒤, 서명한 APK·SHA-256·서명 인증서 정보·외부 구성 요소 고지를 GitHub Releases에 올립니다. |

디버그 앱의 패키지는 `io.github.chjnl.mybrowser.debug`입니다. 배포 앱의 패키지는 `io.github.chjnl.mybrowser`입니다. 두 앱은 함께 설치할 수 있습니다.

## 최초 배포 준비

1. 오프라인에서 보관할 배포용 서명 키를 준비합니다. 키 파일과 비밀번호를 저장소에 커밋하지 않습니다.
2. GitHub 저장소의 **Settings → Secrets and variables → Actions**에 다음 비밀값을 등록합니다.

| 비밀값 이름 | 내용 |
|---|---|
| `ANDROID_KEYSTORE_BASE64` | 배포 키 저장소 파일을 Base64로 변환한 값입니다. |
| `ANDROID_KEYSTORE_PASSWORD` | 키 저장소 비밀번호입니다. |
| `ANDROID_KEY_ALIAS` | 서명 키 별칭입니다. |
| `ANDROID_KEY_PASSWORD` | 서명 키 비밀번호입니다. |

3. `APK 빌드 및 검사` 워크플로가 통과하는지 확인합니다.
4. 디버그 APK로 `docs/VERIFICATION.md`의 기기 검증을 수행합니다.
5. 첫 배포 전에 패키지 이름, 앱 소스 라이선스, 외부 구성 요소 고지를 검토합니다.

키 생성 예시는 다음과 같습니다. 명령이 비밀번호를 대화형으로 요청합니다.

```powershell
keytool -genkeypair -v -keystore mybrowser-release.jks -alias mybrowser -keyalg RSA -keysize 4096 -validity 10000
```

서명 키는 이후 업데이트에도 동일하게 사용해야 합니다. 안전한 별도 위치에 백업합니다. 키를 분실하면 기존 설치본 위에 같은 서명으로 업데이트할 수 없습니다.

## 버전 배포

1. `version.properties`의 `versionName`을 변경하고 `versionCode`를 이전 배포보다 큰 정수로 올립니다.
2. 변경 사항을 커밋하고 브랜치 빌드가 통과하는지 확인합니다.
3. 버전과 같은 태그를 푸시합니다. 예를 들어 `versionName=0.1.0`이면 태그는 `v0.1.0`입니다.
4. 배포 워크플로가 완료되면 Releases에서 APK와 고지 파일을 확인합니다.
5. 배포 APK를 기기에 설치하고 핵심 동작 및 기존 버전에서의 업데이트를 검증합니다.

태그는 `v숫자.숫자.숫자` 형식만 지원합니다. 사전 배포 태그는 현재 지원하지 않습니다. 워크플로는 서명 비밀값이 없으면 실패하며, 서명되지 않은 APK를 배포하지 않습니다.

## 로컬 배포 빌드

다음 환경 변수를 현재 셸에 설정하고 `./gradlew.bat assembleRelease`를 실행합니다.

| 환경 변수 | 값 |
|---|---|
| `MYBROWSER_KEYSTORE_PATH` | 서명 키 저장소의 절대 경로입니다. |
| `MYBROWSER_KEYSTORE_PASSWORD` | 키 저장소 비밀번호입니다. |
| `MYBROWSER_KEY_ALIAS` | 서명 키 별칭입니다. |
| `MYBROWSER_KEY_PASSWORD` | 서명 키 비밀번호입니다. |

산출물은 `app/build/outputs/apk/release/app-release.apk`입니다. 비밀값은 명령 이력이나 로그에 남기지 않도록 별도로 입력합니다.

## 설치 및 확인

1. GitHub Releases에서 `MyBrowser-v버전.apk`를 내려받습니다.
2. 필요한 경우 Android에서 해당 다운로드 앱의 알 수 없는 앱 설치를 허용합니다.
3. APK를 설치합니다.
4. 파일 확인이 필요하면 Windows에서 `Get-FileHash 파일.apk -Algorithm SHA256` 결과를 `SHA256SUMS.txt`와 대조합니다.

현재 저장소에는 자동 업데이트 기능이 없습니다. 새 버전 APK를 내려받아 기존 앱 위에 설치합니다.
