# P11: 구현 생성 프로세스 지침

## 프로세스 개요
- **프로세스 코드**: P11
- **프로세스 이름**: 구현 생성
- **설명**: 코드를 구현하고 생성합니다
- **입력 데이터**: 구현 계획서, 상세 설계 문서
- **출력 데이터**: 구현 코드

## 프로세스 성격
이 프로세스는 **코드 구현 및 생성** 중심의 프로세스입니다. 상세 설계 문서와 구현 계획서를 기반으로 실제 코드를 생성하는 것이 목적입니다.

## TASK 목록
각 프로세스별로 필요한 TASK를 정의하고, TASK 단위로 작업을 수행합니다.

## TASK별 작업 수행 프롬프트
공통 작업 지침(`00-common-guidelines.md`)과 작업 수행 프롬프트 중요 내용(`04-task-execution-prompt.md`)을 참고하여 작성합니다.

## 프로세스별 특수 지침
- **Level별 구현 전략 적용**: Level 1 (유닛) → Level 2 (통합) → Level 3 (E2E)
- **언어별 코딩 표준 준수**: Python/FastAPI, TypeScript/Next.js
- **프레임워크별 코딩 표준 준수**: FastAPI, Next.js, React
- **파일 명명규칙 준수**: snake_case (Python), kebab-case/PascalCase (TypeScript)

## 실제 프롬프트 명령 사용 예시

### 예시 1: Level 1 (유닛) 구현 - Backend

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
   - 린터 오류 확인
   - 기능 동작 확인

**출력 데이터:**
- 구현 코드: `app/services/user_service.py`
- 구현 문서: `docs/P11-implementation/project-p11-user-service.md`
```

### 예시 2: Level 1 (유닛) 구현 - Frontend

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
   - 린터 오류 확인
   - 컴포넌트 렌더링 확인

**출력 데이터:**
- 구현 코드: `components/users/UserList.tsx`
- 구현 문서: `docs/P11-implementation/project-p11-user-list.md`
```

### 예시 3: Level 2 (통합) 구현

```markdown
@rules/P11-implementation-generation.md를 사용하여 다음 작업을 수행하세요.

**프로세스 코드**: P11
**TASK ID**: P11.3
**TASK 이름**: API와 DB 연동 처리 (Level 2)

**입력 데이터:**
- Level 1 구현 결과
- API 명세서: `docs/P04-api-spec/project-p04-api.md`
- DB 설계 문서: `docs/P03-database/project-p03-ddl.md`

**작업 수행 지침:**
1. 입력 데이터 확인 (필수)
2. API 엔드포인트 구현 (필수)
3. DB 연동 처리 (필수)
4. 트랜잭션 처리 (필수)
5. 통합 테스트 (필수)
6. 결과 파일 저장 (필수)
7. 검증 및 완료 (필수)

**출력 데이터:**
- 구현 코드
- 통합 테스트 결과
```

## 검증 기준
- [ ] 모든 필수 TASK가 완료되었는가?
- [ ] 각 TASK의 완료 기준을 충족했는가?
- [ ] Level별 구현 전략이 적용되었는가?
- [ ] 코딩 표준을 준수했는가?
- [ ] 파일 명명규칙을 준수했는가?
- [ ] 결과 파일이 올바른 위치에 저장되었는가?

---
**참고**: 공통 작업 지침과 작업 수행 프롬프트 중요 내용을 반드시 준수해야 합니다.
