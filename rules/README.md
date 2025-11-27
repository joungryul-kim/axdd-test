# 프로세스별 시스템 프롬프트 사용 가이드

## 개요

이 폴더(`rules/`)에는 AXDD 시스템의 **모든 룰 정보**가 통합 관리됩니다:
- 14단계 프로세스별 시스템 프롬프트와 작업 지침
- AXD 코딩 규칙 (코딩 표준, 명명 규칙, 프레임워크별 규칙)
- 프로세스별 룰 기준 및 사용 예시

각 프로세스는 TASK 단위로 세분화되어 있으며, 각 TASK별로 작업 계획 수립 프롬프트와 작업 수행 프롬프트가 제공됩니다.

> **중요**: 
> - 모든 룰 정보는 이 `rules/` 폴더에서만 관리됩니다.
> - **우선순위**: `backend/rules/` 위치의 룰 파일이 최우선 적용됩니다.
> - 다른 위치의 룰 파일(예: `.cursor/axd-coding-rules/`)은 더 이상 사용하지 않으며, 중복을 제거했습니다.

## 폴더 구조

```
rules/
├── 00-common-guidelines.md          # 공통 작업 지침 (모든 프로세스 공통 적용)
├── 01-process-rule-standards.md     # 프로세스별 룰 기준 설정 (신규)
├── 02-prompt-command-examples.md     # 실제 프롬프트 명령 사용 예시 (신규)
├── 03-result-file-storage.md        # 수행 결과 파일 저장 지침
├── 04-task-execution-prompt.md      # 작업 수행 프롬프트 중요 내용
├── P01-requirements-analysis.md     # P01: 요구사항 분석
├── P02-information-collection.md    # P02: 정보 수집
├── P03-result-presentation.md       # P03: 결과 제시
├── P04-ui-design-review.md          # P04: UI 설계 검토
├── P05-final-instruction.md         # P05: 최종 지시
├── P06-system-architecture.md       # P06: 시스템 아키텍처 설계
├── P07-detailed-design.md           # P07: 상세 설계
├── P08-design-review.md             # P08: 설계 검토
├── P09-prototype-analysis.md        # P09: 프로토타입 분석
├── P10-implementation-plan.md       # P10: 구현 계획 수립
├── P11-implementation-generation.md # P11: 구현 생성
├── P12-quality-assurance.md         # P12: 품질 검증
├── P13-deployment-preparation.md    # P13: 배포 준비
├── P14-operation-maintenance.md     # P14: 운영 및 유지보수
├── axd-coding-rules/                # AXD 코딩 규칙 (통합 관리)
│   ├── README.md
│   ├── naming-conventions/          # 파일 명명규칙
│   ├── languages/                   # 언어별 코딩표준
│   ├── frontend-frameworks/          # 프론트엔드 프레임워크별 코딩표준
│   ├── backend-frameworks/           # 백엔드 프레임워크별 코딩표준
│   └── process-guidelines/           # 14단계 프로세스 적용 지침
└── README.md                         # 이 파일
```

## 최근 개선 사항 (2024)

### 1. 프로세스별 룰 기준 설정
- **파일**: `01-process-rule-standards.md`
- **내용**: 각 프로세스별로 적용되는 룰 기준을 명확히 정의
- **주요 기능**:
  - 프로세스별 룰 적용 우선순위 명시
  - 룰 파일 로딩 규칙 정의
  - 프로세스별 특수 지침 정리

### 2. 실제 프롬프트 명령 사용 예시 추가
- **파일**: `02-prompt-command-examples.md`
- **내용**: 각 프로세스에서 실제로 사용할 수 있는 프롬프트 명령 예시
- **주요 기능**:
  - 프로세스별 실제 사용 예시 제공
  - TASK별 상세 프롬프트 예시
  - 에이전트 내부 자동 생성 프로세스 설명

### 3. 에이전트 내부 시스템 프롬프트 자동 생성
- **구현**: `app/services/prompt_service.py`
- **내용**: 프로세스별 룰을 기반으로 동적으로 시스템 프롬프트 생성
- **주요 기능**:
  - 프로세스별 룰 파일 자동 로드
  - 공통 룰 + 프로세스별 룰 + TASK별 지침 통합
  - 작업 계획 수립 및 작업 수행 프롬프트 자동 생성
  - 캐싱을 통한 성능 최적화

## 사용 방법

### 1. 공통 지침 확인

작업을 시작하기 전에 반드시 다음 파일을 확인하세요:

- **`00-common-guidelines.md`**: 모든 프로세스에 공통으로 적용되는 작업 지침
- **`04-task-execution-prompt.md`**: TASK별 작업 수행 시 필수로 준수해야 하는 내용

### 2. 프로세스별 룰 기준 확인

각 프로세스의 룰 적용 기준을 확인하세요:

- **`01-process-rule-standards.md`**: 프로세스별 룰 기준 및 적용 우선순위

### 3. 실제 사용 예시 확인

프롬프트 명령 사용 예시를 확인하세요:

- **`02-prompt-command-examples.md`**: 프로세스별 실제 프롬프트 명령 사용 예시

### 4. 프로세스별 지침 확인

각 프로세스를 수행할 때 해당 프로세스의 지침 파일을 확인하세요:

- **`P01-requirements-analysis.md`**: 요구사항 분석 프로세스
- **`P02-information-collection.md`**: 정보 수집 프로세스
- ... (기타 프로세스)

### 5. 결과 파일 저장 지침 확인

작업 결과를 저장할 때 다음 파일을 참고하세요:

- **`03-result-file-storage.md`**: 파일 저장 위치, 파일명 규칙, 저장 절차

## 에이전트 내부 시스템 프롬프트 자동 생성 (개선 사항)

에이전트는 `PromptService`를 통해 프로세스별 룰을 기반으로 **동적으로** 시스템 프롬프트를 생성합니다. 이는 하드코딩된 프롬프트를 제거하고, 프로세스별 룰 파일을 기반으로 자동으로 프롬프트를 생성하는 개선 사항입니다.

### 시스템 프롬프트 생성 프로세스

1. **TASK ID 분석**: TASK ID (예: `P01.1`)에서 프로세스 코드 (`P01`) 추출
2. **공통 룰 로드**: `00-common-guidelines.md`
3. **작업 수행 프롬프트 룰 로드**: `04-task-execution-prompt.md`
4. **결과 파일 저장 룰 로드**: `03-result-file-storage.md`
5. **프로세스별 룰 로드**: `P{번호}-{프로세스명}.md`
6. **TASK별 특수 지침 추출**: 프로세스 룰에서 해당 TASK 부분 추출
7. **최종 시스템 프롬프트 생성**: 모든 룰을 통합하여 생성

### 사용자 프롬프트 생성

에이전트는 `PromptService`를 통해 작업 계획 수립 또는 작업 수행에 맞는 사용자 프롬프트를 생성합니다.

- **작업 계획 수립**: TASK 분해, 의존성 파악, 우선순위 결정
- **작업 수행**: TASK 목표 확인, 입력 데이터 확인, 작업 수행, 결과 저장

### 개선 전후 비교

#### 개선 전
- 하드코딩된 프롬프트 템플릿 사용
- 프로세스별 룰 변경 시 코드 수정 필요
- TASK별 특수 지침 반영 어려움

#### 개선 후
- 프로세스별 룰 파일 기반 동적 생성
- 룰 파일 수정만으로 프롬프트 업데이트 가능
- TASK별 특수 지침 자동 추출 및 적용
- 캐싱을 통한 성능 최적화

## 프롬프트 사용 예시

### 예시 1: 요구사항 분석 프로세스 (P01)

#### 1단계: 작업 계획 수립

```markdown
@rules/P01-requirements-analysis.md를 사용하여 다음 작업의 계획을 수립하세요.

**입력 데이터:**
- 프로젝트 목표: "AI 기반 프로젝트 관리 시스템 개발"
- 비즈니스 요구사항: "프로젝트 생성, 관리, 협업 기능 필요"

**요청 사항:**
- TASK 1: 배경 이해 작업 계획 수립
- 각 TASK별 목표, 범위, 완료 기준 정의
```

#### 2단계: 작업 수행

```markdown
@rules/P01-requirements-analysis.md를 사용하여 다음 작업을 수행하세요.

**입력 데이터:**
- 프로젝트 목표 문서
- 비즈니스 요구사항 문서

**요청 사항:**
- TASK 1: 배경 이해 작업 수행
- 결과 파일 저장: `docs/P01-requirements/project-p01-1-background.md`
```

### 예시 2: 구현 생성 프로세스 (P11)

#### 1단계: 작업 계획 수립

```markdown
@rules/P11-implementation-generation.md를 사용하여 다음 작업의 계획을 수립하세요.

**프로세스 코드**: P11
**TASK ID**: P11.1
**입력 데이터:**
- 구현 계획서: `docs/P10-implementation-plan/project-p10-plan.md`
- 상세 설계 문서: `docs/P07-detailed-design/project-p07-design.md`

**요청 사항:**
- Level 1 (유닛) 구현 계획 수립
- 각 TASK별 목표, 범위, 완료 기준 정의
- TASK별 우선순위 및 의존성 파악

**출력 형식**: JSON 배열 형식
```

#### 2단계: 작업 수행

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
6. 결과 파일 저장 (필수)
   - 파일명: `app/services/user_service.py`
   - 구현 문서: `docs/P11-implementation/project-p11-user-service.md`
7. 검증 및 완료 (필수)

**출력 데이터:**
- 구현 코드: `app/services/user_service.py`
- 구현 문서: `docs/P11-implementation/project-p11-user-service.md`
```

### 예시 3: 에이전트 내부 시스템 프롬프트 생성 (자동)

에이전트가 작업을 수행할 때, `PromptService`가 자동으로 다음을 수행합니다:

1. **프로세스 코드 추출**: TASK ID (예: P01.1)에서 프로세스 코드 (P01) 추출
2. **룰 파일 로드**: 해당 프로세스의 룰 파일 로드
3. **시스템 프롬프트 생성**: 공통 룰 + 프로세스별 룰 + TASK별 지침 통합
4. **사용자 프롬프트 생성**: 입력 데이터 기반 사용자 프롬프트 생성
5. **AI 모델 호출**: 생성된 프롬프트로 AI 모델 호출

**예시 코드 (에이전트 내부)**:
```python
# PromptService를 통해 시스템 프롬프트 생성
system_prompt = prompt_service.build_system_prompt(
    task_id='P01.1',
    prompt_type='execution',
    input_data=input_data,
)

# 사용자 프롬프트 생성
user_prompt = prompt_service.build_user_prompt(
    task_id='P01.1',
    prompt_type='execution',
    input_data=input_data,
    task_info=task_info,
)

# AI 모델 호출
result = await ai_model_service.generate_completion(
    prompt=user_prompt,
    system_prompt=system_prompt,
    ...
)
```

## 주요 원칙

### 1. TASK 단위 작업
- 모든 작업은 TASK 단위로 분리하여 진행
- 각 TASK는 명확한 목표와 완료 기준을 가져야 함
- 한 번에 하나의 TASK만 처리

### 2. 단계별 진행
- 작업 계획 수립 → 작업 수행 → 검증 및 완료
- 각 단계를 순차적으로 진행
- 검증 없이 다음 단계로 진행하지 않음

### 3. 결과 파일 저장
- 모든 산출물은 `docs/` 폴더에 저장
- 파일명 규칙 준수
- 저장 경로를 출력 데이터에 포함

### 4. 코딩 표준 준수
- 언어별 코딩 표준 준수
- 프레임워크별 코딩 표준 준수
- 명명 규칙 준수

## 프로세스별 특수 지침

각 프로세스는 고유한 특성을 가지고 있으므로, 해당 프로세스의 지침 파일을 확인하여 프로세스별 특수 지침을 준수하세요.

### P01: 요구사항 분석
- 문서 작성 규칙 준수
- 질의 생성 규칙 준수
- 답변 수집 규칙 준수

### P02-P05: 설계 단계
- 문서 작성 규칙 준수
- 설계 원칙 준수
- 검토 프로세스 준수

### P06-P08: 상세 설계 및 검토
- 4+1 뷰 모델 작성
- 설계 검토 체크리스트 활용
- 개선 사항 문서화

### P09-P10: 분석 및 계획
- 프로토타입 분석 기준 적용
- 구현 계획 수립 프로세스 준수
- WBS 표준 형식 준수

### P11-P12: 구현 및 테스트
- 언어별/프레임워크별 코딩 표준 준수
- Level별 구현 전략 적용
- 테스트 커버리지 기준 준수

### P13-P14: 배포 및 운영
- 배포 준비 체크리스트 활용
- 운영 가이드 작성
- 유지보수 계획 수립

## 검증 기준

각 프로세스 완료 시 다음 기준을 확인하세요:

- [ ] 모든 필수 TASK가 완료되었는가?
- [ ] 각 TASK의 완료 기준을 충족했는가?
- [ ] 결과 파일이 올바른 위치에 저장되었는가?
- [ ] 코딩 표준을 준수했는가?
- [ ] 린터 오류가 없는가?

## 문제 해결

### 문제 1: TASK 분해가 어려운 경우
- 큰 작업을 더 작은 단위로 분해
- 각 TASK는 최대 1-2개 파일 수정 범위로 제한
- 공통 작업 지침(`00-common-guidelines.md`) 참고

### 문제 2: 결과 파일 저장 위치가 불명확한 경우
- 결과 파일 저장 지침(`03-result-file-storage.md`) 참고
- 파일명 규칙 준수 확인
- 저장 경로를 출력 데이터에 포함

### 문제 3: 코딩 표준 준수 여부 확인
- 언어별/프레임워크별 코딩 표준 파일 참고
- 린터 도구 사용
- 코드 리뷰 수행

## 추가 리소스

### rules 폴더 내 리소스

이 `rules/` 폴더 내에서 관리되는 모든 룰 정보입니다:

- **`axd-coding-rules/`**: AXD 코딩 규칙 (통합 관리)
  - `languages/`: 언어별 코딩 표준 (Python, TypeScript, Java 등)
  - `frontend-frameworks/`: 프론트엔드 프레임워크 코딩 표준 (Next.js, React 등)
  - `backend-frameworks/`: 백엔드 프레임워크 코딩 표준 (FastAPI 등)
  - `naming-conventions/`: 파일 명명 규칙
  - `process-guidelines/`: 14단계 프로세스 가이드라인

### 프로젝트 내 참조 리소스 (선택적, 참고용)

> **참고**: 모든 룰 정보는 `rules/` 폴더에서 통합 관리됩니다. 아래 리소스는 참고용이며, 우선순위는 `rules/` 폴더의 룰 파일이 높습니다.

- **`../../.cursor/common_rule.md`**: 공통 작업 규칙 (참고용)

- **`../../.cursor/doc01-requirements.md` ~ `../../.cursor/doc14-ai-task-failure-analysis.md`**: 상세 프로세스 문서 (참고용)
  - 이 문서들은 프로세스 이해를 위한 참고 자료입니다
  - 실제 작업 시에는 `rules/P01-requirements-analysis.md` ~ `rules/P14-operation-maintenance.md`를 우선 참조하세요

### 백엔드 서비스 (rules 폴더 기준 상대 경로)

- **`../app/services/prompt_service.py`**: 프롬프트 서비스 (프로세스별 룰 기반 프롬프트 생성)
- **`../app/services/agent_orchestrator.py`**: 에이전트 오케스트레이터 (PromptService 통합)

### rules 폴더 내 관련 문서

#### 프로세스 지침 파일
- **`00-common-guidelines.md`**: 공통 작업 지침
- **`01-process-rule-standards.md`**: 프로세스별 룰 기준 상세 설명
- **`02-prompt-command-examples.md`**: 실제 프롬프트 명령 사용 예시 모음
- **`03-result-file-storage.md`**: 결과 파일 저장 지침
- **`04-task-execution-prompt.md`**: 작업 수행 프롬프트 중요 내용
- **`P01-requirements-analysis.md` ~ `P14-operation-maintenance.md`**: 프로세스별 지침 파일

#### 코딩 규칙 파일
- **`axd-coding-rules/README.md`**: AXD 코딩 규칙 개요
- **`axd-coding-rules/languages/`**: 언어별 코딩 표준
- **`axd-coding-rules/frontend-frameworks/`**: 프론트엔드 프레임워크별 코딩 표준
- **`axd-coding-rules/backend-frameworks/`**: 백엔드 프레임워크별 코딩 표준
- **`axd-coding-rules/naming-conventions/`**: 파일 명명 규칙
- **`axd-coding-rules/process-guidelines/`**: 14단계 프로세스 적용 지침

## 에이전트 내부 시스템 프롬프트 자동 생성

에이전트가 작업을 수행할 때, `PromptService`가 자동으로 프로세스별 룰을 기반으로 시스템 프롬프트를 생성합니다.

### 자동 생성 프로세스

1. **TASK ID 분석**: TASK ID (예: `P01.1`)에서 프로세스 코드 (`P01`) 추출
2. **룰 파일 로드**: 다음 순서로 룰 파일 로드
   - 공통 룰 (`00-common-guidelines.md`)
   - 작업 수행 프롬프트 룰 (`04-task-execution-prompt.md`)
   - 결과 파일 저장 룰 (`03-result-file-storage.md`)
   - 프로세스별 룰 (`P{번호}-{프로세스명}.md`)
3. **TASK별 지침 추출**: 프로세스 룰에서 해당 TASK의 특수 지침 추출
4. **시스템 프롬프트 생성**: 모든 룰을 통합하여 최종 시스템 프롬프트 생성
5. **사용자 프롬프트 생성**: 입력 데이터 기반 사용자 프롬프트 생성

### 코드 예시

```python
from app.services.prompt_service import PromptService

# PromptService 초기화
prompt_service = PromptService()

# 시스템 프롬프트 생성
system_prompt = prompt_service.build_system_prompt(
    task_id='P01.1',  # TASK ID
    prompt_type='execution',  # 'planning' or 'execution'
    input_data={
        'summary': '프로젝트 목표 및 비즈니스 요구사항',
        'previous_step_files': []
    }
)

# 사용자 프롬프트 생성
user_prompt = prompt_service.build_user_prompt(
    task_id='P01.1',
    prompt_type='execution',
    input_data={
        'summary': '프로젝트 목표 및 비즈니스 요구사항',
        'previous_step_files': []
    },
    task_info={
        'name': '배경 이해',
        'description': 'AXD 조직의 AI 기반 개발 프로세스와 협업 방식을 자세히 파악'
    }
)

# AI 모델 호출
result = await ai_model_service.generate_completion(
    prompt=user_prompt,
    system_prompt=system_prompt,
    project_id=project_id,
    process_step_id=process_step_id,
    task_type='execution',
    temperature=0.4,
)
```

### 프롬프트 생성 결과

생성된 시스템 프롬프트는 다음 구조를 가집니다:

```
# 공통 작업 지침
[00-common-guidelines.md 내용]

---

# 작업 수행 프롬프트 중요 내용
[04-task-execution-prompt.md 내용]

---

# 결과 파일 저장 지침
[03-result-file-storage.md 내용]

---

# P01 프로세스 지침
[P01-requirements-analysis.md 내용]

---

# TASK P01.1 특수 지침
[TASK별 특수 지침 내용]

---

# 최종 지침
[통합 지침]
```

## GitHub 연동

이 `rules/` 폴더는 프로젝트의 GitHub 저장소에 포함되어야 합니다. 

### Git 설정 확인
```bash
# .gitignore에 rules 폴더가 제외되지 않았는지 확인
cat .gitignore | grep rules

# rules 폴더가 Git에 추가되었는지 확인
git status rules/
```

### GitHub에 Push
```bash
# rules 폴더 추가
git add rules/

# 커밋
git commit -m "Add process-specific system prompts and guidelines"

# Push
git push origin main
```

## 기술적 구현 세부사항

### PromptService 구조

`PromptService`는 다음 메서드를 제공합니다:

- `build_system_prompt(task_id, prompt_type, input_data)`: 시스템 프롬프트 생성
- `build_user_prompt(task_id, prompt_type, input_data, task_info)`: 사용자 프롬프트 생성
- `_load_rule_file(filename)`: 룰 파일 로드 (캐싱 지원)
- `_extract_task_specific_guidance(process_rule, task_id, prompt_type)`: TASK별 지침 추출

### AgentOrchestrator 통합

`AgentOrchestrator`는 작업 계획 수립 및 작업 수행 시 `PromptService`를 사용하여 프롬프트를 생성합니다:

- 작업 계획 수립: `prompt_type='planning'`
- 작업 수행: `prompt_type='execution'`

### 성능 최적화

- 룰 파일 캐싱: 한 번 로드된 룰 파일은 메모리에 캐시
- 지연 로딩: 필요한 룰 파일만 로드
- 효율적인 문자열 조작: 최소한의 문자열 복사

## 변경 이력

### 2024년 개선 사항
- ✅ 프로세스별 룰 기준 설정 (`01-process-rule-standards.md`)
- ✅ 실제 프롬프트 명령 사용 예시 추가 (`02-prompt-command-examples.md`)
- ✅ 에이전트 내부 시스템 프롬프트 자동 생성 (`PromptService` 구현)
- ✅ 하드코딩된 프롬프트 제거 및 동적 생성으로 전환
- ✅ 프로세스별 룰 파일 기반 프롬프트 관리 체계 구축

---

**중요**: 모든 작업은 공통 작업 지침과 프로세스별 지침을 반드시 준수해야 합니다.

