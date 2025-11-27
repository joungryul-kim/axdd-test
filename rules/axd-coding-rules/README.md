# AXD 코딩 규칙 (AXD Coding Rules)

이 디렉토리는 AI-Driven Development System에서 사용하는 코딩 표준, 패턴, 명명 규칙을 정의합니다.

> **참고**: 이 폴더는 `backend/rules/axd-coding-rules/`에 위치하며, 모든 룰 정보는 `rules/` 폴더에서 통합 관리됩니다.

## 📁 디렉토리 구조

```
axd-coding-rules/
├── README.md                          # 이 파일
├── naming-conventions/                # 파일 명명규칙
│   └── file-naming-conventions.md
├── languages/                         # 프로그래밍 언어별 코딩표준
│   ├── python-coding-standards.md
│   ├── typescript-coding-standards.md
│   ├── java-coding-standards.md
│   ├── csharp-coding-standards.md
│   ├── go-coding-standards.md
│   └── ...
├── frontend-frameworks/               # 프론트엔드 프레임워크별 코딩표준
│   ├── nextjs-coding-standards.md
│   ├── react-coding-standards.md
│   ├── vue-coding-standards.md
│   ├── angular-coding-standards.md
│   └── ...
├── backend-frameworks/                # 백엔드 프레임워크별 코딩표준
│   ├── fastapi-coding-standards.md
│   ├── django-coding-standards.md
│   ├── spring-boot-coding-standards.md
│   ├── nestjs-coding-standards.md
│   └── ...
└── process-guidelines/                # 14단계 프로세스 적용 지침
    └── 14-step-process-guidelines.md
```

## 📋 규칙 파일 사용 방법

### 1. 프로젝트에 적용하기

프로젝트 루트에 `.cursor` 파일을 생성하고 필요한 규칙을 참조하세요:

```markdown
# 프로젝트 코딩 규칙

## 파일 명명규칙
@backend/rules/axd-coding-rules/naming-conventions/file-naming-conventions.md

## 언어별 코딩표준
@backend/rules/axd-coding-rules/languages/python-coding-standards.md
@backend/rules/axd-coding-rules/languages/typescript-coding-standards.md

## 프레임워크별 코딩표준
@backend/rules/axd-coding-rules/frontend-frameworks/nextjs-coding-standards.md
@backend/rules/axd-coding-rules/backend-frameworks/fastapi-coding-standards.md

## 14단계 프로세스 적용
@backend/rules/axd-coding-rules/process-guidelines/14-step-process-guidelines.md
```

또는 rules 폴더 기준으로 참조:

```markdown
# 프로젝트 코딩 규칙

## 파일 명명규칙
@rules/axd-coding-rules/naming-conventions/file-naming-conventions.md

## 언어별 코딩표준
@rules/axd-coding-rules/languages/python-coding-standards.md
@rules/axd-coding-rules/languages/typescript-coding-standards.md

## 프레임워크별 코딩표준
@rules/axd-coding-rules/frontend-frameworks/nextjs-coding-standards.md
@rules/axd-coding-rules/backend-frameworks/fastapi-coding-standards.md

## 14단계 프로세스 적용
@rules/axd-coding-rules/process-guidelines/14-step-process-guidelines.md
```

### 2. 규칙 파일 확장자

모든 규칙 파일은 `.md` (Markdown) 확장자를 사용합니다.

### 3. 규칙 우선순위

1. **프로젝트별 규칙** (프로젝트 `.cursor`)
2. **프레임워크별 규칙** (frontend-frameworks, backend-frameworks)
3. **언어별 규칙** (languages)
4. **명명규칙** (naming-conventions)
5. **프로세스 지침** (process-guidelines)

## 🔄 규칙 업데이트

규칙은 프로젝트 요구사항에 따라 지속적으로 업데이트됩니다.

## 📚 참고 자료

- **우선순위**: 이 폴더(`rules/axd-coding-rules/`)의 룰 파일이 최우선 적용됩니다.
- **중복 제거**: `.cursor/axd-coding-rules/` 폴더는 더 이상 사용하지 않으며, 모든 룰은 `rules/axd-coding-rules/`에서 관리됩니다.

