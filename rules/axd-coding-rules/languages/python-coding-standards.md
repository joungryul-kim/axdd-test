# Python 코딩표준 (Python Coding Standards)

이 문서는 AI-Driven Development System에서 Python 개발 시 준수해야 할 코딩 표준과 패턴을 정의합니다.

## 📋 목차

1. [일반 원칙](#일반-원칙)
2. [코딩 컨벤션](#코딩-컨벤션)
3. [명명 규칙](#명명-규칙)
4. [코드 구조](#코드-구조)
5. [에러 처리](#에러-처리)
6. [테스트](#테스트)
7. [문서화](#문서화)

---

## 일반 원칙

### 1. PEP 8 준수

- Python 공식 스타일 가이드인 [PEP 8](https://pep8.org/)을 기본으로 따릅니다.
- 프로젝트별로 일부 규칙을 조정할 수 있으나, 기본 원칙은 유지합니다.

### 2. Pythonic 코드 작성

- Python의 관용구(idioms)를 활용합니다.
- 간결하고 읽기 쉬운 코드를 작성합니다.
- 명시적이 좋고 암시적보다 낫습니다 (Explicit is better than implicit).

### 3. 타입 힌팅 사용

- Python 3.5+ 타입 힌팅을 적극 활용합니다.
- `typing` 모듈을 사용하여 타입을 명시합니다.

---

## 코딩 컨벤션

### 1. 들여쓰기

- **4개의 공백**을 사용합니다 (탭 사용 금지).
- 최대 줄 길이: **88자** (Black 포맷터 기본값) 또는 **79자** (PEP 8).

### 2. 빈 줄

- 최상위 함수와 클래스 정의 사이: **2줄**
- 클래스 내부 메서드 정의 사이: **1줄**
- 함수 내부 논리적 섹션 구분: **1줄**

### 3. 임포트 (Imports)

#### 임포트 순서
1. 표준 라이브러리
2. 서드파티 라이브러리
3. 로컬 애플리케이션/라이브러리

#### 예시
```python
# 표준 라이브러리
import os
import sys
from typing import List, Dict, Optional

# 서드파티 라이브러리
import requests
from fastapi import FastAPI
from sqlalchemy import Column, Integer, String

# 로컬 애플리케이션
from app.models import User
from app.services import UserService
```

#### 임포트 스타일
- 절대 임포트 사용 권장
- 와일드카드 임포트(`from module import *`) 금지

### 4. 따옴표

- 문자열은 **작은따옴표(`'`)**를 기본으로 사용합니다.
- 문자열 내부에 작은따옴표가 있을 경우 큰따옴표(`"`) 사용.

### 5. 연산자 및 구분자

- 이항 연산자 주변에 공백 사용
- 함수 호출 시 쉼표 뒤 공백 사용

```python
# 좋은 예
result = a + b
function(arg1, arg2, arg3)

# 나쁜 예
result=a+b
function(arg1,arg2,arg3)
```

---

## 명명 규칙

### 1. 변수 및 함수

- **snake_case** 사용
- 예: `user_name`, `get_user_data()`, `calculate_total()`

### 2. 클래스

- **PascalCase** 사용
- 예: `UserService`, `DatabaseConnection`, `ApiClient`

### 3. 상수

- **UPPER_SNAKE_CASE** 사용
- 예: `MAX_RETRY_COUNT`, `DEFAULT_TIMEOUT`, `API_BASE_URL`

### 4. 비공개 변수/함수

- 단일 언더스코어(`_`) 접두사 사용
- 예: `_internal_method()`, `_private_variable`

### 5. 특수 메서드

- 더블 언더스코어(`__`) 사용 (매직 메서드)
- 예: `__init__`, `__str__`, `__repr__`

### 6. 모듈 및 패키지

- **snake_case** 사용
- 짧고 소문자 권장
- 예: `user_service`, `api_client`, `database`

---

## 코드 구조

### 1. 모듈 구조

```python
"""
모듈 docstring: 모듈의 목적과 사용법을 설명합니다.
"""

# 표준 라이브러리 임포트
import os
from typing import Optional

# 서드파티 라이브러리 임포트
import requests

# 로컬 임포트
from app.models import User

# 모듈 레벨 상수
DEFAULT_TIMEOUT = 30
MAX_RETRY_COUNT = 3

# 클래스 정의
class UserService:
    """UserService 클래스 docstring"""
    pass

# 함수 정의
def get_user(user_id: int) -> Optional[User]:
    """함수 docstring"""
    pass

# 모듈 실행 시 동작 (선택적)
if __name__ == "__main__":
    pass
```

### 2. 클래스 구조

```python
class UserService:
    """클래스 docstring"""
    
    # 클래스 변수
    DEFAULT_LIMIT = 100
    
    def __init__(self, db_connection: DatabaseConnection):
        """초기화 메서드"""
        self._db = db_connection
        self._cache = {}
    
    def public_method(self, param: str) -> str:
        """공개 메서드"""
        return self._private_method(param)
    
    def _private_method(self, param: str) -> str:
        """비공개 메서드"""
        return param.upper()
    
    @classmethod
    def create_instance(cls, config: dict) -> 'UserService':
        """클래스 메서드"""
        return cls(DatabaseConnection(config))
    
    @staticmethod
    def validate_email(email: str) -> bool:
        """정적 메서드"""
        return '@' in email
```

### 3. 함수 구조

```python
def process_user_data(
    user_id: int,
    include_profile: bool = True,
    include_history: bool = False
) -> Dict[str, Any]:
    """
    사용자 데이터를 처리합니다.
    
    Args:
        user_id: 사용자 ID
        include_profile: 프로필 포함 여부
        include_history: 히스토리 포함 여부
    
    Returns:
        처리된 사용자 데이터 딕셔너리
    
    Raises:
        ValueError: user_id가 유효하지 않은 경우
    """
    if user_id <= 0:
        raise ValueError("user_id must be positive")
    
    # 함수 본문
    result = {}
    
    if include_profile:
        result['profile'] = get_user_profile(user_id)
    
    if include_history:
        result['history'] = get_user_history(user_id)
    
    return result
```

---

## 에러 처리

### 1. 예외 처리 원칙

- 구체적인 예외 타입 사용
- 일반적인 `Exception` 사용 지양
- 예외 메시지는 명확하고 유용하게 작성

### 2. 예외 처리 패턴

```python
# 좋은 예
try:
    user = get_user(user_id)
except UserNotFoundError as e:
    logger.error(f"User not found: {user_id}")
    raise
except DatabaseConnectionError as e:
    logger.error(f"Database connection failed: {e}")
    raise ServiceUnavailableError("Service temporarily unavailable")
except Exception as e:
    logger.exception(f"Unexpected error: {e}")
    raise

# 나쁜 예
try:
    user = get_user(user_id)
except Exception as e:  # 너무 일반적
    pass  # 예외를 무시
```

### 3. 커스텀 예외

```python
class UserServiceError(Exception):
    """UserService 관련 기본 예외"""
    pass

class UserNotFoundError(UserServiceError):
    """사용자를 찾을 수 없을 때 발생하는 예외"""
    pass

class InvalidUserDataError(UserServiceError):
    """유효하지 않은 사용자 데이터일 때 발생하는 예외"""
    pass
```

---

## 테스트

### 1. 테스트 파일 구조

- 테스트 파일명: `test_*.py` 또는 `*_test.py`
- 테스트 클래스명: `Test*`
- 테스트 메서드명: `test_*`

### 2. 테스트 예시

```python
import pytest
from unittest.mock import Mock, patch
from app.services import UserService
from app.models import User

class TestUserService:
    """UserService 테스트 클래스"""
    
    @pytest.fixture
    def user_service(self):
        """UserService 인스턴스 fixture"""
        db_mock = Mock()
        return UserService(db_mock)
    
    def test_get_user_success(self, user_service):
        """사용자 조회 성공 테스트"""
        # Given
        user_id = 1
        expected_user = User(id=user_id, name="Test User")
        user_service._db.get_user.return_value = expected_user
        
        # When
        result = user_service.get_user(user_id)
        
        # Then
        assert result == expected_user
        user_service._db.get_user.assert_called_once_with(user_id)
    
    def test_get_user_not_found(self, user_service):
        """사용자 조회 실패 테스트"""
        # Given
        user_id = 999
        user_service._db.get_user.return_value = None
        
        # When & Then
        with pytest.raises(UserNotFoundError):
            user_service.get_user(user_id)
```

### 3. 테스트 원칙

- **AAA 패턴**: Arrange (Given), Act (When), Assert (Then)
- 각 테스트는 독립적으로 실행 가능해야 함
- 테스트명은 명확하고 설명적이어야 함

---

## 문서화

### 1. Docstring 스타일

- **Google 스타일** 또는 **NumPy 스타일** 사용 권장

#### Google 스타일 예시
```python
def calculate_total(items: List[Dict[str, float]], tax_rate: float = 0.1) -> float:
    """
    아이템 목록의 총액을 계산합니다.
    
    Args:
        items: 아이템 목록 (각 아이템은 'price' 키를 포함)
        tax_rate: 세율 (기본값: 0.1)
    
    Returns:
        세금 포함 총액
    
    Raises:
        ValueError: items가 비어있거나 tax_rate가 음수인 경우
    
    Example:
        >>> items = [{'price': 100.0}, {'price': 200.0}]
        >>> calculate_total(items, tax_rate=0.1)
        330.0
    """
    if not items:
        raise ValueError("items cannot be empty")
    if tax_rate < 0:
        raise ValueError("tax_rate must be non-negative")
    
    subtotal = sum(item['price'] for item in items)
    return subtotal * (1 + tax_rate)
```

### 2. 타입 힌팅

```python
from typing import List, Dict, Optional, Union, Any

def process_data(
    items: List[Dict[str, Any]],
    filter_func: Optional[callable] = None
) -> Dict[str, List[Any]]:
    """타입 힌팅이 포함된 함수"""
    pass
```

---

## 패턴 및 베스트 프랙티스

### 1. 리스트 컴프리헨션

```python
# 좋은 예
squares = [x**2 for x in range(10) if x % 2 == 0]

# 나쁜 예
squares = []
for x in range(10):
    if x % 2 == 0:
        squares.append(x**2)
```

### 2. 컨텍스트 매니저

```python
# 파일 처리
with open('file.txt', 'r') as f:
    content = f.read()

# 데이터베이스 연결
with database.get_connection() as conn:
    conn.execute(query)
```

### 3. 제너레이터

```python
def read_large_file(file_path: str):
    """대용량 파일을 메모리 효율적으로 읽기"""
    with open(file_path, 'r') as f:
        for line in f:
            yield line.strip()
```

### 4. 데코레이터

```python
from functools import wraps

def log_execution_time(func):
    """함수 실행 시간을 로깅하는 데코레이터"""
    @wraps(func)
    def wrapper(*args, **kwargs):
        import time
        start = time.time()
        result = func(*args, **kwargs)
        end = time.time()
        print(f"{func.__name__} took {end - start:.2f} seconds")
        return result
    return wrapper

@log_execution_time
def slow_function():
    """느린 함수"""
    time.sleep(1)
```

---

## 도구 및 설정

### 1. 포맷터

- **Black**: 코드 포맷팅
- **isort**: 임포트 정렬

### 2. 린터

- **flake8**: PEP 8 검사
- **pylint**: 코드 품질 검사
- **mypy**: 타입 체크

### 3. 설정 파일 예시

#### `.flake8`
```ini
[flake8]
max-line-length = 88
exclude = .git,__pycache__,venv
```

#### `pyproject.toml` (Black)
```toml
[tool.black]
line-length = 88
target-version = ['py39', 'py310', 'py311']
```

---

## 참고 자료

- [PEP 8 -- Style Guide for Python Code](https://pep8.org/)
- [PEP 484 -- Type Hints](https://www.python.org/dev/peps/pep-0484/)
- [Google Python Style Guide](https://google.github.io/styleguide/pyguide.html)
- [Real Python - Python Code Quality](https://realpython.com/python-code-quality/)

