# 14단계 프로세스 적용 지침

이 문서는 AI-Driven Development System의 14단계 프로세스에 따라 코딩 규칙을 적용하는 방법을 설명합니다.

## 📋 목차

1. [14단계 프로세스 개요](#14단계-프로세스-개요)
2. [단계별 코딩 규칙 적용](#단계별-코딩-규칙-적용)
3. [프로세스별 체크리스트](#프로세스별-체크리스트)
4. [통합 적용 가이드](#통합-적용-가이드)

---

## 14단계 프로세스 개요

### 프로세스 단계

1. **P01: 요구사항 정의** 👤
2. **P02: ADR 작성** 👤
3. **P03: DB 설계** 🤖
4. **P04: API 명세** 🤖
5. **P05: UI 프로토타입** 👤
6. **P06: 상세 설계** 👤
7. **P07: 설계 검토** 👤
8. **P08: 프로토타입 분석** 🤖
9. **P09: 구현 계획** 👤
10. **P10: 구현 생성** 🤖
11. **P11: 테스트 생성** 🤖
12. **P12: 품질 보증** 🤖
13. **P13: 디버그** 👤
14. **P14: 실패 분석** 👤

---
## 최우선규칙
- 각 단계 진행시 기존 생성된 파일에 대해 재현행화 진행 한다. 

## 단계별 코딩 규칙 적용

### P01: 요구사항 정의 👤

#### 적용 규칙
- 문서 작성 규칙 준수
- 파일명 규칙: `{프로젝트명}-P01-requirements.md`
- Markdown 형식 준수

#### 체크리스트
- [ ] 요구사항 문서가 명확하게 작성되었는가?
- [ ] 기능/비기능 요구사항이 구분되었는가?
- [ ] 파일명 규칙을 준수하는가?

---

### P02: ADR 작성 👤

#### 적용 규칙
- ADR 템플릿 준수
- 파일명 규칙: `{프로젝트명}-P02-adr.md`
- 기술 스택 결정 사유 명시

#### 체크리스트
- [ ] ADR 형식이 표준을 따르는가?
- [ ] 대안 분석이 포함되었는가?
- [ ] 결정 사유가 명확한가?

---

### P03: DB 설계 🤖

#### 적용 규칙
- 파일명 규칙: `{프로젝트명}-P03-database.md`
- 데이터베이스 명명 규칙 준수
- 테이블명: `snake_case`
- 컬럼명: `snake_case`
- 인덱스명: `idx_{테이블명}_{순번}`

#### 체크리스트
- [ ] ERD가 작성되었는가?
- [ ] DDL이 생성되었는가?
- [ ] 명명 규칙을 준수하는가?

#### 예시
```sql
-- 테이블 생성
CREATE TABLE users (
    id SERIAL PRIMARY KEY,
    email VARCHAR(255) NOT NULL UNIQUE,
    name VARCHAR(100) NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- 인덱스 생성
CREATE INDEX idx_users_email ON users(email);
```

---

### P04: API 명세 🤖

#### 적용 규칙
- RESTful API 설계 원칙 준수
- OpenAPI 3.0 스펙 준수
- 파일명 규칙: `{프로젝트명}-P04-api-spec.md`

#### 체크리스트
- [ ] OpenAPI 스펙이 작성되었는가?
- [ ] 엔드포인트 명명 규칙을 준수하는가?
- [ ] 요청/응답 스키마가 정의되었는가?

#### 엔드포인트 명명 규칙
- 리소스명: `kebab-case` 또는 `snake_case`
- 예: `/api/users`, `/api/user-profiles`

---

### P05: UI 프로토타입 👤

#### 적용 규칙
- 파일명 규칙: `{프로젝트명}-P05-prototype.md`
- 프론트엔드 프레임워크 코딩표준 준수
- 컴포넌트 명명 규칙 준수
- 파일명 규칙: 프로젝트 구조에 따라

#### 체크리스트
- [ ] 컴포넌트 구조가 명확한가?
- [ ] 파일명 규칙을 준수하는가?
- [ ] 스타일링 규칙을 준수하는가?

#### Next.js 예시
```
prototype/
├── app/
│   ├── page.tsx
│   └── layout.tsx
├── components/
│   ├── ui/
│   └── layout/
└── lib/
```

---

### P06: 상세 설계 👤

#### 적용 규칙
- 4+1 뷰 모델 작성
- 컴포넌트 설계 일관성 유지
- 파일명 규칙: `{프로젝트명}-P06-detailed-design.md`

#### 체크리스트
- [ ] 논리 뷰가 작성되었는가?
- [ ] 개발 뷰가 작성되었는가?
- [ ] 프로세스 뷰가 작성되었는가?
- [ ] 물리 뷰가 작성되었는가?
- [ ] 유스케이스 뷰가 작성되었는가?

---

### P07: 설계 검토 👤

#### 적용 규칙
- 검토 체크리스트 활용
- 개선 사항 문서화
- 파일명 규칙: `{프로젝트명}-P07-review-results.md`

#### 체크리스트
- [ ] 설계 품질 평가가 수행되었는가?
- [ ] 개선 사항이 문서화되었는가?
- [ ] 일관성 검증이 완료되었는가?

---

### P08: 프로토타입 분석 🤖

#### 적용 규칙
- 보안/성능/가용성 평가 기준 적용
- 갭 분석 수행
- 파일명 규칙: `{프로젝트명}-P08-analysis-report.md`

#### 체크리스트
- [ ] 보안 평가가 완료되었는가?
- [ ] 성능 평가가 완료되었는가?
- [ ] 가용성 평가가 완료되었는가?
- [ ] 갭 분석이 수행되었는가?

---

### P09: 구현 계획 👤

#### 적용 규칙
- WBS 표준 형식 준수
- 작업 분해 명확성
- 파일명 규칙: `{프로젝트명}-P09-implementation-plan.md`

#### 체크리스트
- [ ] 작업 분해가 명확한가?
- [ ] 우선순위가 지정되었는가?
- [ ] 공수 추정이 포함되었는가?

---

### P10: 구현 생성 🤖

#### 적용 규칙
- 파일명 규칙: `{프로젝트명}-P10-implementation.md`
- **언어별 코딩표준 준수**
- **프레임워크별 코딩표준 준수**
- **파일 명명규칙 준수**
- Level별 구현 전략 적용

#### 체크리스트
- [ ] Level 1 (유닛) 구현이 완료되었는가?
- [ ] Level 2 (통합) 구현이 완료되었는가?
- [ ] Level 3 (E2E) 구현이 완료되었는가?
- [ ] 코딩 스타일을 준수하는가?
- [ ] 파일명 규칙을 준수하는가?

#### 적용 예시

##### Python/FastAPI 프로젝트
```python
# 파일명: user_service.py (snake_case)
# 코딩표준: python-coding-standards.md 준수

from typing import List, Optional
from app.models.user import User
from app.schemas.user import UserCreate, UserResponse

class UserService:
    """사용자 서비스 클래스"""
    
    async def get_users(self, skip: int = 0, limit: int = 100) -> List[User]:
        """사용자 목록 조회"""
        # 구현
        pass
```

##### TypeScript/Next.js 프로젝트
```typescript
// 파일명: user-service.ts (kebab-case)
// 코딩표준: typescript-coding-standards.md, nextjs-coding-standards.md 준수

import { User } from '@/types/user';

export class UserService {
  async getUsers(skip: number = 0, limit: number = 100): Promise<User[]> {
    // 구현
  }
}
```

---

### P11: 테스트 생성 🤖

#### 적용 규칙
- 파일명 규칙: `{프로젝트명}-P10-test.md`
- 테스트 파일 명명 규칙 준수
- 테스트 커버리지 기준 준수
- Level별 테스트 전략 적용

#### 체크리스트
- [ ] Level 1 (유닛) 테스트가 작성되었는가?
- [ ] Level 2 (통합) 테스트가 작성되었는가?
- [ ] Level 3 (E2E) 테스트가 작성되었는가?
- [ ] 테스트 커버리지가 기준을 만족하는가?

#### 테스트 파일 명명 규칙
- Python: `test_*.py` 또는 `*_test.py`
- TypeScript: `*.test.ts` 또는 `*.spec.ts`

---

### P12: 품질 보증 🤖

#### 적용 규칙
- 품질 게이트 기준 적용
- 정합성 검증 수행
- 코딩 스타일 검증

#### 체크리스트
- [ ] 정합성 검증이 완료되었는가?
- [ ] 품질 게이트를 통과했는가?
- [ ] 코딩 스타일 검증이 완료되었는가?

#### 검증 도구
- Python: `flake8`, `pylint`, `mypy`
- TypeScript: `ESLint`, `Prettier`, `TypeScript Compiler`

---

### P13: 디버그 👤

#### 적용 규칙
- 역산 사고 방법론 적용
- 체계적 원인 분석 수행
- 파일명 규칙: `{프로젝트명}-P13-debug-results.md`

#### 체크리스트
- [ ] 원인 분석이 수행되었는가?
- [ ] 해결 방안이 제시되었는가?
- [ ] 수정 코드가 작성되었는가?

---

### P14: 실패 분석 👤

#### 적용 규칙
- 근본 원인 분석(RCA) 방법론 적용
- 학습 자료 표준 형식 준수
- 파일명 규칙: `{프로젝트명}-P14-failure-analysis.md`

#### 체크리스트
- [ ] 근본 원인이 분석되었는가?
- [ ] 개선책이 제시되었는가?
- [ ] 재발 방지 대책이 수립되었는가?
- [ ] 학습 자료가 생성되었는가?

---

## 프로세스별 체크리스트

### 구현 단계 (P10) 체크리스트

#### 파일 명명규칙
- [ ] 파일명이 언어별 규칙을 따르는가?
- [ ] 파일명이 프레임워크별 규칙을 따르는가?
- [ ] 파일명에 공백이나 특수문자가 없는가?

#### 코딩표준
- [ ] 언어별 코딩표준을 준수하는가?
- [ ] 프레임워크별 코딩표준을 준수하는가?
- [ ] 명명 규칙을 준수하는가?

#### 코드 품질
- [ ] 타입 힌팅/타입 선언이 적절한가?
- [ ] 에러 처리가 적절한가?
- [ ] 문서화가 충분한가?

---

## 통합 적용 가이드

### 1. 프로젝트 초기 설정

프로젝트 루트에 `.cursor` 파일을 생성하고 필요한 규칙을 참조합니다 (우선순위: `rules/axd-coding-rules/`):

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

### 2. 단계별 규칙 적용

각 프로세스 단계에서 해당하는 규칙을 적용합니다:

- **P01-P09**: 문서 작성 규칙, 파일명 규칙
- **P10**: 언어별/프레임워크별 코딩표준, 파일 명명규칙
- **P11**: 테스트 파일 명명규칙, 테스트 작성 규칙
- **P12**: 코드 품질 검증 규칙
- **P13-P14**: 문서 작성 규칙

### 3. 규칙 우선순위

1. **프로젝트별 규칙** (프로젝트 `.cursor`)
2. **프레임워크별 규칙** (frontend-frameworks, backend-frameworks)
3. **언어별 규칙** (languages)
4. **명명규칙** (naming-conventions)
5. **프로세스 지침** (process-guidelines)

---