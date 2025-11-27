# FastAPI 코딩표준 (FastAPI Coding Standards)

이 문서는 AI-Driven Development System에서 FastAPI 개발 시 준수해야 할 코딩 표준과 패턴을 정의합니다.

## 📋 목차

1. [프로젝트 구조](#프로젝트-구조)
2. [라우터 작성 규칙](#라우터-작성-규칙)
3. [모델 및 스키마](#모델-및-스키마)
4. [의존성 주입](#의존성-주입)
5. [에러 처리](#에러-처리)
6. [데이터베이스](#데이터베이스)
7. [테스트](#테스트)

---

## 프로젝트 구조

### 1. 권장 디렉토리 구조

```
project/
├── app/
│   ├── __init__.py
│   ├── main.py              # FastAPI 앱 진입점
│   ├── config.py            # 설정
│   ├── dependencies.py      # 의존성
│   ├── routers/             # API 라우터
│   │   ├── __init__.py
│   │   ├── users.py
│   │   └── auth.py
│   ├── models/              # 데이터베이스 모델
│   │   ├── __init__.py
│   │   └── user.py
│   ├── schemas/             # Pydantic 스키마
│   │   ├── __init__.py
│   │   └── user.py
│   ├── services/             # 비즈니스 로직
│   │   ├── __init__.py
│   │   └── user_service.py
│   ├── repositories/         # 데이터 접근 계층
│   │   ├── __init__.py
│   │   └── user_repository.py
│   └── exceptions/           # 커스텀 예외
│       ├── __init__.py
│       └── errors.py
├── tests/
│   ├── __init__.py
│   ├── test_users.py
│   └── conftest.py
├── requirements.txt
└── README.md
```

---

## 라우터 작성 규칙

### 1. 기본 라우터 구조

```python
# app/routers/users.py
from fastapi import APIRouter, Depends, HTTPException, status
from typing import List
from app.schemas.user import UserCreate, UserResponse
from app.services.user_service import UserService
from app.dependencies import get_user_service

router = APIRouter(
    prefix="/users",
    tags=["users"]
)

@router.get("/", response_model=List[UserResponse])
async def get_users(
    skip: int = 0,
    limit: int = 100,
    user_service: UserService = Depends(get_user_service)
):
    """사용자 목록 조회"""
    users = await user_service.get_users(skip=skip, limit=limit)
    return users

@router.get("/{user_id}", response_model=UserResponse)
async def get_user(
    user_id: int,
    user_service: UserService = Depends(get_user_service)
):
    """사용자 상세 조회"""
    user = await user_service.get_user(user_id)
    if not user:
        raise HTTPException(
            status_code=status.HTTP_404_NOT_FOUND,
            detail=f"User {user_id} not found"
        )
    return user

@router.post("/", response_model=UserResponse, status_code=status.HTTP_201_CREATED)
async def create_user(
    user_data: UserCreate,
    user_service: UserService = Depends(get_user_service)
):
    """사용자 생성"""
    user = await user_service.create_user(user_data)
    return user
```

### 2. 라우터 등록

```python
# app/main.py
from fastapi import FastAPI
from app.routers import users, auth

app = FastAPI(
    title="My API",
    description="API description",
    version="1.0.0"
)

app.include_router(users.router)
app.include_router(auth.router)
```

---

## 모델 및 스키마

### 1. Pydantic 스키마

```python
# app/schemas/user.py
from pydantic import BaseModel, EmailStr, Field
from typing import Optional
from datetime import datetime

class UserBase(BaseModel):
    """사용자 기본 스키마"""
    email: EmailStr
    name: str = Field(..., min_length=1, max_length=100)

class UserCreate(UserBase):
    """사용자 생성 스키마"""
    password: str = Field(..., min_length=8)

class UserUpdate(BaseModel):
    """사용자 업데이트 스키마"""
    name: Optional[str] = Field(None, min_length=1, max_length=100)
    email: Optional[EmailStr] = None

class UserResponse(UserBase):
    """사용자 응답 스키마"""
    id: int
    created_at: datetime
    updated_at: datetime
    
    class Config:
        from_attributes = True  # Pydantic v2
```

### 2. 데이터베이스 모델

```python
# app/models/user.py
from sqlalchemy import Column, Integer, String, DateTime
from sqlalchemy.ext.declarative import declarative_base
from datetime import datetime

Base = declarative_base()

class User(Base):
    __tablename__ = "users"
    
    id = Column(Integer, primary_key=True, index=True)
    email = Column(String, unique=True, index=True, nullable=False)
    name = Column(String, nullable=False)
    hashed_password = Column(String, nullable=False)
    created_at = Column(DateTime, default=datetime.utcnow)
    updated_at = Column(DateTime, default=datetime.utcnow, onupdate=datetime.utcnow)
```

---

## 의존성 주입

### 1. 의존성 정의

```python
# app/dependencies.py
from fastapi import Depends
from sqlalchemy.ext.asyncio import AsyncSession
from app.database import get_db
from app.services.user_service import UserService
from app.repositories.user_repository import UserRepository

async def get_user_repository(
    db: AsyncSession = Depends(get_db)
) -> UserRepository:
    """UserRepository 의존성"""
    return UserRepository(db)

async def get_user_service(
    repository: UserRepository = Depends(get_user_repository)
) -> UserService:
    """UserService 의존성"""
    return UserService(repository)
```

### 2. 인증 의존성

```python
# app/dependencies.py
from fastapi import Depends, HTTPException, status
from fastapi.security import OAuth2PasswordBearer
from app.services.auth_service import AuthService

oauth2_scheme = OAuth2PasswordBearer(tokenUrl="auth/login")

async def get_current_user(
    token: str = Depends(oauth2_scheme),
    auth_service: AuthService = Depends(get_auth_service)
):
    """현재 사용자 조회"""
    user = await auth_service.get_current_user(token)
    if not user:
        raise HTTPException(
            status_code=status.HTTP_401_UNAUTHORIZED,
            detail="Invalid authentication credentials"
        )
    return user
```

---

## 에러 처리

### 1. 커스텀 예외

```python
# app/exceptions/errors.py
class AppException(Exception):
    """애플리케이션 기본 예외"""
    def __init__(self, message: str, status_code: int = 500):
        self.message = message
        self.status_code = status_code
        super().__init__(self.message)

class UserNotFoundError(AppException):
    """사용자를 찾을 수 없을 때 발생하는 예외"""
    def __init__(self, user_id: int):
        super().__init__(
            f"User {user_id} not found",
            status_code=404
        )

class ValidationError(AppException):
    """유효성 검증 실패 예외"""
    def __init__(self, message: str):
        super().__init__(message, status_code=400)
```

### 2. 예외 핸들러

```python
# app/main.py
from fastapi import FastAPI, Request, status
from fastapi.responses import JSONResponse
from app.exceptions.errors import AppException, UserNotFoundError

app = FastAPI()

@app.exception_handler(AppException)
async def app_exception_handler(request: Request, exc: AppException):
    """애플리케이션 예외 핸들러"""
    return JSONResponse(
        status_code=exc.status_code,
        content={"detail": exc.message}
    )

@app.exception_handler(UserNotFoundError)
async def user_not_found_handler(request: Request, exc: UserNotFoundError):
    """사용자 없음 예외 핸들러"""
    return JSONResponse(
        status_code=exc.status_code,
        content={"detail": exc.message}
    )
```

---

## 데이터베이스

### 1. 데이터베이스 연결

```python
# app/database.py
from sqlalchemy.ext.asyncio import AsyncSession, create_async_engine, async_sessionmaker
from app.config import settings

engine = create_async_engine(
    settings.DATABASE_URL,
    echo=settings.DEBUG
)

AsyncSessionLocal = async_sessionmaker(
    engine,
    class_=AsyncSession,
    expire_on_commit=False
)

async def get_db() -> AsyncSession:
    """데이터베이스 세션 의존성"""
    async with AsyncSessionLocal() as session:
        try:
            yield session
            await session.commit()
        except Exception:
            await session.rollback()
            raise
        finally:
            await session.close()
```

### 2. Repository 패턴

```python
# app/repositories/user_repository.py
from sqlalchemy.ext.asyncio import AsyncSession
from sqlalchemy import select
from app.models.user import User
from app.schemas.user import UserCreate

class UserRepository:
    def __init__(self, db: AsyncSession):
        self.db = db
    
    async def get_user(self, user_id: int) -> User | None:
        """사용자 조회"""
        result = await self.db.execute(
            select(User).where(User.id == user_id)
        )
        return result.scalar_one_or_none()
    
    async def get_user_by_email(self, email: str) -> User | None:
        """이메일로 사용자 조회"""
        result = await self.db.execute(
            select(User).where(User.email == email)
        )
        return result.scalar_one_or_none()
    
    async def create_user(self, user_data: UserCreate) -> User:
        """사용자 생성"""
        user = User(**user_data.dict())
        self.db.add(user)
        await self.db.commit()
        await self.db.refresh(user)
        return user
```

---

## 테스트

### 1. 테스트 설정

```python
# tests/conftest.py
import pytest
from fastapi.testclient import TestClient
from sqlalchemy.ext.asyncio import create_async_engine, AsyncSession, async_sessionmaker
from app.main import app
from app.database import get_db
from app.models import Base

TEST_DATABASE_URL = "sqlite+aiosqlite:///:memory:"

@pytest.fixture
async def db_session():
    """테스트용 데이터베이스 세션"""
    engine = create_async_engine(TEST_DATABASE_URL, echo=True)
    async with engine.begin() as conn:
        await conn.run_sync(Base.metadata.create_all)
    
    async_session = async_sessionmaker(engine, class_=AsyncSession)
    async with async_session() as session:
        yield session
    
    async with engine.begin() as conn:
        await conn.run_sync(Base.metadata.drop_all)

@pytest.fixture
def client(db_session):
    """테스트 클라이언트"""
    def override_get_db():
        yield db_session
    
    app.dependency_overrides[get_db] = override_get_db
    yield TestClient(app)
    app.dependency_overrides.clear()
```

### 2. 테스트 예시

```python
# tests/test_users.py
import pytest
from fastapi import status

def test_get_users(client):
    """사용자 목록 조회 테스트"""
    response = client.get("/users/")
    assert response.status_code == status.HTTP_200_OK
    assert isinstance(response.json(), list)

def test_get_user_not_found(client):
    """존재하지 않는 사용자 조회 테스트"""
    response = client.get("/users/999")
    assert response.status_code == status.HTTP_404_NOT_FOUND

def test_create_user(client):
    """사용자 생성 테스트"""
    user_data = {
        "email": "test@example.com",
        "name": "Test User",
        "password": "password123"
    }
    response = client.post("/users/", json=user_data)
    assert response.status_code == status.HTTP_201_CREATED
    assert response.json()["email"] == user_data["email"]
```

---

## 참고 자료

- [FastAPI Documentation](https://fastapi.tiangolo.com/)
- [FastAPI Best Practices](https://fastapi.tiangolo.com/tutorial/)
- [SQLAlchemy Async](https://docs.sqlalchemy.org/en/20/orm/extensions/asyncio.html)

