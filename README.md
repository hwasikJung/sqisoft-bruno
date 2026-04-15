# Bruno API Collections

SEF-2026 공통프레임워크의 API 테스트를 위한 [Bruno](https://www.usebruno.com/) 컬렉션 저장소입니다.

## 저장소 구조

```
Bruno/
└── sef/
    └── 공통프레임워크/
        ├── bruno.json              # Bruno 컬렉션 설정
        ├── collection.bru          # 공통 헤더/인증 설정
        ├── environments/           # 환경별 변수 정의
        │   ├── local.bru
        │   └── dev.bru
        ├── 공공/                   # 공공 프로젝트 API
        │   ├── 01_인증
        │   ├── 02_사용자
        │   ├── 03_게시판
        │   ├── 04_메뉴
        │   ├── 05_메뉴권한
        │   ├── 06_역할
        │   ├── 07_코드
        │   ├── 08_약관
        │   ├── 09_시스템
        │   ├── 10_파기
        │   └── 11_보관
        └── 민간/                   # 민간 프로젝트 API
```

## 사전 준비

1. [Bruno 설치](https://www.usebruno.com/downloads)
2. 본 저장소 클론

```bash
git clone <repository-url>
cd Bruno
```

## 사용 방법

### 컬렉션 열기

1. Bruno 실행
2. **Open Collection** 선택
3. `sef/공통프레임워크` 폴더 선택

### 환경 설정

우측 상단 환경 선택 드롭다운에서 사용할 환경을 고릅니다.

| 환경 | baseUrl | 용도 |
|------|---------|------|
| `local` | 로컬 개발 서버 | 개인 개발 환경 |
| `dev` | `http://52.78.238.167:8199` | 공용 개발 서버 |

### 인증 토큰 설정

1. `공공/01_인증/로그인` 요청 실행
2. 응답에서 `accessToken`, `refreshToken` 복사
3. 환경 변수(`environments/*.bru`)의 `accessToken`, `refreshToken` 값에 반영
4. 이후 요청은 `collection.bru`의 Bearer 인증이 자동 적용됨

> 토큰 갱신은 `공공/01_인증/토큰갱신` 요청을 사용합니다.

## 공통 설정

컬렉션 전역 설정은 `collection.bru`에 정의되어 있습니다.

- **Content-Type**: `application/json`
- **Accept**: `application/json`
- **Auth**: Bearer Token (`{{accessToken}}`)

## API 분류

### 공공 (eGovFrame 기반)
- **01_인증**: 로그인, 로그아웃, 토큰 갱신
- **02_사용자**: 계정/관리자/일반 사용자, 통계, 파기
- **03_게시판**: 게시글(관리자/일반), 댓글, 파일/통계
- **04_메뉴 · 05_메뉴권한 · 06_역할 · 07_코드 · 08_약관**: 관리자/일반 API
- **09_시스템**: API 로그, 감사 로그, 로그인 이력, 방문 로그/통계, 에러 로그
- **10_파기 · 11_보관**: 데이터 수명 주기 관리

### 민간 (Spring Boot 3.x + JPA)
민간 프로젝트용 API 컬렉션이 순차적으로 추가될 예정입니다.

## 기여 방법

1. 새 요청은 기존 분류 폴더 규칙(`##_도메인/하위분류`)을 따라 추가합니다.
2. URL은 하드코딩하지 않고 `{{baseUrl}}` 변수로 작성합니다.
3. 커밋 메시지는 프로젝트 컨벤션(`feat:`, `fix:` 등)을 따릅니다.
