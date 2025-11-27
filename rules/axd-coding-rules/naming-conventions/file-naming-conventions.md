# 파일 명명규칙 (File Naming Conventions)

이 문서는 AI-Driven Development System에서 사용하는 소스코드 파일 명명규칙을 정의합니다.

## 📋 목차

1. [일반 원칙](#일반-원칙)
2. [언어별 파일 명명규칙](#언어별-파일-명명규칙)
3. [프레임워크별 파일 명명규칙](#프레임워크별-파일-명명규칙)
4. [디렉토리 명명규칙](#디렉토리-명명규칙)
5. [특수 파일 명명규칙](#특수-파일-명명규칙)

---

## 일반 원칙

### 1. 기본 원칙

- **일관성**: 프로젝트 전체에서 일관된 명명 규칙 사용
- **명확성**: 파일명만으로 파일의 목적과 내용을 파악 가능해야 함
- **간결성**: 불필요하게 긴 파일명 지양
- **영문 사용**: 파일명은 영문으로 작성 (한글, 특수문자 제외)
- **대소문자 구분**: OS에 따라 대소문자 구분 여부가 다를 수 있으므로 주의

### 2. 금지 사항

- 공백 문자 사용 금지 (하이픈 `-` 또는 언더스코어 `_` 사용)
- 특수문자 사용 금지 (`/`, `\`, `:`, `*`, `?`, `"`, `<`, `>`, `|` 등)
- 한글 및 기타 비영문 문자 사용 금지
- 연속된 하이픈 또는 언더스코어 사용 금지

### 3. 파일명 길이

- 권장: 50자 이내
- 최대: 255자 (OS 제한 고려)

---

## 언어별 파일 명명규칙

### Python

#### 파일명 규칙
- **형식**: `snake_case.py`
- **예시**:
  - `user_service.py`
  - `database_connection.py`
  - `api_client.py`
  - `test_user_service.py` (테스트 파일)

#### 특수 파일명
- `__init__.py`: 패키지 초기화 파일
- `__main__.py`: 모듈 실행 진입점
- `setup.py`: 패키지 설정 파일
- `requirements.txt`: 의존성 목록
- `conftest.py`: pytest 설정 파일

#### 클래스 파일
- 클래스명과 파일명 일치 권장
- 예: `UserService` 클래스 → `user_service.py`

### TypeScript / JavaScript

#### 파일명 규칙
- **형식**: `kebab-case.ts` 또는 `kebab-case.tsx`
- **예시**:
  - `user-service.ts`
  - `api-client.ts`
  - `user-profile.component.tsx`
  - `user-service.test.ts` (테스트 파일)

#### React 컴포넌트
- 컴포넌트 파일: `PascalCase.tsx` (선택적, 팀 규칙에 따라)
  - 예: `UserProfile.tsx`, `Button.tsx`
- 또는: `kebab-case.tsx`
  - 예: `user-profile.tsx`, `button.tsx`

#### 유틸리티 파일
- `utils.ts`, `helpers.ts`, `constants.ts`

### Java

#### 파일명 규칙
- **형식**: `PascalCase.java`
- **규칙**: 파일명은 반드시 public 클래스명과 일치해야 함
- **예시**:
  - `UserService.java`
  - `DatabaseConnection.java`
  - `UserServiceTest.java` (테스트 파일)

#### 패키지 구조
- 패키지명: `lowercase` (점으로 구분)
- 예: `com.example.userservice`

### C# / .NET

#### 파일명 규칙
- **형식**: `PascalCase.cs`
- **규칙**: 파일명은 반드시 public 클래스명과 일치해야 함
- **예시**:
  - `UserService.cs`
  - `DatabaseConnection.cs`
  - `UserServiceTests.cs` (테스트 파일)

#### 네임스페이스
- 네임스페이스명: `PascalCase` (점으로 구분)
- 예: `Company.Project.UserService`

### Go

#### 파일명 규칙
- **형식**: `snake_case.go`
- **예시**:
  - `user_service.go`
  - `database_connection.go`
  - `user_service_test.go` (테스트 파일)

#### 패키지명
- 패키지명: `lowercase` (단일 단어 권장)
- 예: `userservice`, `database`

### Rust

#### 파일명 규칙
- **형식**: `snake_case.rs`
- **예시**:
  - `user_service.rs`
  - `database_connection.rs`
  - `user_service_test.rs` (테스트 파일)

#### 모듈명
- 모듈명: `snake_case`
- 예: `user_service`, `database`

---

## 프레임워크별 파일 명명규칙

### Next.js

#### 페이지 파일
- **App Router**: `page.tsx`, `layout.tsx`, `loading.tsx`, `error.tsx`
- **Pages Router**: `index.tsx`, `[id].tsx`, `[...slug].tsx`

#### 컴포넌트 파일
- **형식**: `PascalCase.tsx` 또는 `kebab-case.tsx`
- **예시**:
  - `UserProfile.tsx`
  - `user-profile.tsx`
  - `Button.tsx`

#### API 라우트
- **App Router**: `route.ts` 또는 `route.tsx`
- **Pages Router**: `api/users/[id].ts`

#### 유틸리티 파일
- `utils.ts`, `lib.ts`, `constants.ts`

### React

#### 컴포넌트 파일
- **형식**: `PascalCase.tsx` (권장)
- **예시**:
  - `UserProfile.tsx`
  - `Button.tsx`
  - `UserProfile.test.tsx` (테스트 파일)

#### Hook 파일
- **형식**: `useHookName.ts`
- **예시**:
  - `useUser.ts`
  - `useApi.ts`

### Vue.js

#### 컴포넌트 파일
- **형식**: `PascalCase.vue` (권장)
- **예시**:
  - `UserProfile.vue`
  - `Button.vue`

#### 컴포지션 API
- **형식**: `useComposableName.ts`
- **예시**:
  - `useUser.ts`
  - `useApi.ts`

### Angular

#### 컴포넌트 파일
- **형식**: `component-name.component.ts`
- **예시**:
  - `user-profile.component.ts`
  - `user-profile.component.html`
  - `user-profile.component.scss`

#### 서비스 파일
- **형식**: `service-name.service.ts`
- **예시**:
  - `user.service.ts`
  - `api.service.ts`

### FastAPI

#### 라우터 파일
- **형식**: `router_name.py`
- **예시**:
  - `users.py`
  - `auth.py`
  - `api_v1.py`

#### 모델 파일
- **형식**: `model_name.py`
- **예시**:
  - `user.py`
  - `product.py`

### Django

#### 앱 구조
- **형식**: `snake_case`
- **예시**:
  - `users/`
  - `products/`
  - `orders/`

#### 뷰 파일
- **형식**: `views.py`, `urls.py`, `models.py`, `admin.py`

### Spring Boot

#### 클래스 파일
- **형식**: `PascalCase.java`
- **예시**:
  - `UserController.java`
  - `UserService.java`
  - `UserRepository.java`
  - `User.java` (엔티티)

#### 패키지 구조
- `com.example.project.controller`
- `com.example.project.service`
- `com.example.project.repository`
- `com.example.project.entity`

---

## 디렉토리 명명규칙

### 일반 원칙

- **형식**: `kebab-case` 또는 `snake_case` (프로젝트 일관성 유지)
- **예시**:
  - `user-service/`
  - `api-client/`
  - `database-connection/`

### 언어별 디렉토리 규칙

#### Python
- `snake_case`: `user_service/`, `api_client/`

#### TypeScript/JavaScript
- `kebab-case`: `user-service/`, `api-client/`

#### Java
- `lowercase`: `userservice/`, `apiclient/` (패키지 구조)

#### C#
- `PascalCase`: `UserService/`, `ApiClient/`

#### Go
- `lowercase`: `userservice/`, `apiclient/`

---

## 특수 파일 명명규칙

### 설정 파일

#### 일반 설정
- `.env`, `.env.local`, `.env.production`
- `config.json`, `config.yaml`, `config.yml`
- `package.json`, `requirements.txt`, `pom.xml`, `build.gradle`

#### IDE 설정
- `.vscode/`, `.idea/`
- `.editorconfig`, `.prettierrc`, `.eslintrc.json`

### 문서 파일

#### 프로젝트 문서
- `README.md`
- `CHANGELOG.md`
- `LICENSE`
- `CONTRIBUTING.md`

#### API 문서
- `api-documentation.md`
- `api-spec.yaml` 또는 `openapi.yaml`

### 테스트 파일

#### 일반 규칙
- 테스트 파일은 원본 파일명에 `test` 또는 `spec` 접미사 추가
- **예시**:
  - `user_service.py` → `test_user_service.py` 또는 `user_service_test.py`
  - `user-service.ts` → `user-service.test.ts` 또는 `user-service.spec.ts`

#### 테스트 디렉토리
- `tests/`, `__tests__/`, `spec/`

### 빌드 및 배포 파일

#### Docker
- `Dockerfile`, `docker-compose.yml`, `.dockerignore`

#### CI/CD
- `.github/workflows/`, `.gitlab-ci.yml`, `Jenkinsfile`

---

## 파일명 예시 모음

### Python 프로젝트
```
project/
├── src/
│   ├── user_service/
│   │   ├── __init__.py
│   │   ├── user_service.py
│   │   ├── user_model.py
│   │   └── user_repository.py
│   └── api_client/
│       ├── __init__.py
│       └── api_client.py
├── tests/
│   ├── test_user_service.py
│   └── test_api_client.py
├── requirements.txt
└── README.md
```

### TypeScript/Next.js 프로젝트
```
project/
├── app/
│   ├── page.tsx
│   ├── layout.tsx
│   └── users/
│       └── [id]/
│           └── page.tsx
├── components/
│   ├── UserProfile.tsx
│   └── Button.tsx
├── lib/
│   ├── api-client.ts
│   └── utils.ts
└── package.json
```

### Java/Spring Boot 프로젝트
```
project/
├── src/
│   └── main/
│       └── java/
│           └── com/
│               └── example/
│                   └── userservice/
│                       ├── controller/
│                       │   └── UserController.java
│                       ├── service/
│                       │   └── UserService.java
│                       └── repository/
│                           └── UserRepository.java
└── pom.xml
```

---

## 체크리스트

파일명을 작성할 때 다음 사항을 확인하세요:

- [ ] 파일명이 프로젝트의 명명 규칙을 따르는가?
- [ ] 파일명에 공백이나 특수문자가 없는가?
- [ ] 파일명이 너무 길지 않은가? (50자 이내 권장)
- [ ] 파일명만으로 파일의 목적을 파악할 수 있는가?
- [ ] 테스트 파일은 적절한 접미사를 사용하는가?
- [ ] 컴포넌트/클래스 파일명이 내부 클래스명과 일치하는가? (해당 언어의 규칙에 따라)

---

## 참고 자료

- [Python PEP 8](https://pep8.org/)
- [TypeScript Style Guide](https://www.typescriptlang.org/docs/handbook/declaration-files/do-s-and-don-ts.html)
- [Java Code Conventions](https://www.oracle.com/java/technologies/javase/codeconventions-contents.html)
- [C# Coding Conventions](https://docs.microsoft.com/en-us/dotnet/csharp/fundamentals/coding-style/coding-conventions)
- [Go Code Review Comments](https://github.com/golang/go/wiki/CodeReviewComments)

