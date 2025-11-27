# 실제 프롬프트 명령 사용 예시

## 개요

이 문서는 각 프로세스에서 실제로 사용할 수 있는 프롬프트 명령 예시를 제공합니다. 각 예시는 `@rules/` 파일을 참조하여 사용합니다.

## 사용 방법

### 기본 형식

```markdown
@rules/{프로세스파일명}.md를 사용하여 다음 작업을 수행하세요.

**프로세스 코드**: {프로세스코드}
**TASK ID**: {TASK ID}
**TASK 이름**: {TASK 이름}

**입력 데이터:**
- 입력 데이터 목록

**작업 수행 지침:**
1. 입력 데이터 확인 (필수)
2. 작업 수행 (필수)
3. 결과 파일 저장 (필수)
4. 검증 및 완료 (필수)

**출력 데이터:**
- 출력 데이터 목록
```

## 프로세스별 예시

### P01: 요구사항 분석

#### 예시 1: 배경 이해 (P01.1)

```markdown
@rules/P01-requirements-analysis.md를 사용하여 다음 작업을 수행하세요.

**프로세스 코드**: P01
**TASK ID**: P01.1
**TASK 이름**: 배경 이해

**입력 데이터:**
- 프로젝트 목표: "AI 기반 프로젝트 관리 시스템 개발"
- 비즈니스 요구사항: "프로젝트 생성, 관리, 협업 기능 필요"

**작업 수행 지침:**
1. 입력 데이터 확인 (필수)
2. 조직 프로세스 파악 (필수)
3. 협업 방식 이해 (필수)
4. 배경 이해 문서 작성 (필수)
5. 결과 파일 저장 (필수)
   - 파일명: `project-p01-1-background.md`
   - 저장 경로: `docs/P01-requirements/`
6. 검증 및 완료 (필수)

**출력 데이터:**
- 배경 이해 문서
- 저장 경로: `docs/P01-requirements/project-p01-1-background.md`
```

#### 예시 2: 요구사항 정보 분석 (P01.2)

```markdown
@rules/P01-requirements-analysis.md를 사용하여 다음 작업을 수행하세요.

**프로세스 코드**: P01
**TASK ID**: P01.2
**TASK 이름**: 요구사항 정보 분석

**입력 데이터:**
- README.md 파일
- 이전 단계 출력: `docs/P01-requirements/project-p01-1-background.md`

**작업 수행 지침:**
1. 입력 데이터 확인 (필수)
2. 요구사항 읽기 (필수)
3. 주요 요소 식별 (필수)
4. 카테고리 분류 (옵션)
5. 요구사항 분석 문서 작성 (필수)
6. 결과 파일 저장 (필수)
   - 파일명: `project-p01-2-analysis.md`
   - 저장 경로: `docs/P01-requirements/`
7. 검증 및 완료 (필수)

**출력 데이터:**
- 요구사항 분석 결과
- 저장 경로: `docs/P01-requirements/project-p01-2-analysis.md`
```

### P06: 시스템 아키텍처 설계

#### 예시: ADR 작성

```markdown
@rules/P06-system-architecture.md를 사용하여 다음 작업을 수행하세요.

**프로세스 코드**: P06
**TASK ID**: P06.1
**TASK 이름**: 아키텍처 드라이버 식별

**입력 데이터:**
- 요구사항 문서: `docs/P01-requirements/project-p01-requirements.md`
- 프로젝트 목표 및 제약사항

**작업 수행 지침:**
1. 입력 데이터 확인 (필수)
2. 제약 사항 식별 (필수)
3. 품질 특성 정의 (필수)
4. 아키텍처에 영향을 주는 기능 요구사항 식별 (필수)
5. ADR 문서 작성 (필수)
   - 파일명: `project-p06-adr.md`
   - 저장 경로: `docs/P06-architecture/`
6. 검증 및 완료 (필수)

**출력 데이터:**
- ADR 문서
- 저장 경로: `docs/P06-architecture/project-p06-adr.md`
```

### P11: 구현 생성

#### 예시 1: Level 1 (유닛) 구현 - Backend

```markdown
@rules/P11-implementation-generation.md를 사용하여 다음 작업을 수행하세요.

**프로세스 코드**: P11
**TASK ID**: P11.1
**TASK 이름**: 사용자 서비스 클래스 구현 (Level 1)

**입력 데이터:**
- 구현 계획서: `docs/P10-implementation-plan/project-p10-plan.md`
- 상세 설계 문서: `docs/P07-detailed-design/project-p07-design.md`

**작업 수행 지침:**
1. 입력 데이터 확인 (필수)
2. 서비스 클래스 구조 설계 (필수)
3. 사용자 조회 메서드 구현 (필수)
4. 사용자 생성 메서드 구현 (필수)
5. 코딩 표준 준수 확인 (필수)
   - Python 코딩 표준 준수
   - FastAPI 코딩 표준 준수
   - 파일명: `snake_case` (예: `user_service.py`)
6. 결과 파일 저장 (필수)
   - 파일명: `app/services/user_service.py`
   - 구현 문서: `docs/P11-implementation/project-p11-user-service.md`
7. 검증 및 완료 (필수)

**출력 데이터:**
- 구현 코드: `app/services/user_service.py`
- 구현 문서: `docs/P11-implementation/project-p11-user-service.md`
```

#### 예시 2: Level 1 (유닛) 구현 - Frontend

```markdown
@rules/P11-implementation-generation.md를 사용하여 다음 작업을 수행하세요.

**프로세스 코드**: P11
**TASK ID**: P11.2
**TASK 이름**: 사용자 목록 컴포넌트 구현 (Level 1)

**입력 데이터:**
- 구현 계획서: `docs/P10-implementation-plan/project-p10-plan.md`
- 상세 설계 문서: `docs/P07-detailed-design/project-p07-design.md`

**작업 수행 지침:**
1. 입력 데이터 확인 (필수)
2. 컴포넌트 구조 설계 (필수)
3. Props 타입 정의 (필수)
4. 컴포넌트 구현 (필수)
5. 코딩 표준 준수 확인 (필수)
   - TypeScript 코딩 표준 준수
   - Next.js 코딩 표준 준수
   - React 코딩 표준 준수
   - 파일명: `PascalCase` (예: `UserList.tsx`)
6. 결과 파일 저장 (필수)
   - 파일명: `components/users/UserList.tsx`
   - 구현 문서: `docs/P11-implementation/project-p11-user-list.md`
7. 검증 및 완료 (필수)

**출력 데이터:**
- 구현 코드: `components/users/UserList.tsx`
- 구현 문서: `docs/P11-implementation/project-p11-user-list.md`
```

## 에이전트 내부 자동 생성

에이전트가 작업을 수행할 때는 `PromptService`가 자동으로 다음을 수행합니다:

1. **프로세스 코드 추출**: TASK ID에서 프로세스 코드 추출
2. **룰 파일 로드**: 공통 룰 + 프로세스별 룰 로드
3. **시스템 프롬프트 생성**: 모든 룰 통합
4. **사용자 프롬프트 생성**: 입력 데이터 기반 생성
5. **AI 모델 호출**: 생성된 프롬프트로 호출

사용자는 위의 예시 형식으로 요청하면, 에이전트가 자동으로 적절한 프롬프트를 생성하여 작업을 수행합니다.

---

**참고**: 각 프로세스별 상세 예시는 해당 프로세스의 룰 파일(`P{번호}-{프로세스명}.md`)을 참고하세요.

