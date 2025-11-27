# TypeScript 코딩표준 (TypeScript Coding Standards)

이 문서는 AI-Driven Development System에서 TypeScript 개발 시 준수해야 할 코딩 표준과 패턴을 정의합니다.

## 📋 목차

1. [일반 원칙](#일반-원칙)
2. [코딩 컨벤션](#코딩-컨벤션)
3. [명명 규칙](#명명-규칙)
4. [타입 시스템](#타입-시스템)
5. [코드 구조](#코드-구조)
6. [에러 처리](#에러-처리)
7. [테스트](#테스트)

---

## 일반 원칙

### 1. TypeScript 스타일 가이드 준수

- TypeScript 공식 스타일 가이드를 기본으로 따릅니다.
- 프로젝트별 ESLint 및 Prettier 설정을 준수합니다.

### 2. 타입 안전성 우선

- `any` 타입 사용을 최소화합니다.
- 명시적 타입 선언을 우선합니다.
- 타입 추론이 명확한 경우에만 생략합니다.

### 3. 모던 TypeScript 기능 활용

- 최신 TypeScript 기능을 적극 활용합니다.
- 유니온 타입, 제네릭, 타입 가드 등을 적절히 사용합니다.

---

## 코딩 컨벤션

### 1. 들여쓰기 및 공백

- **2개의 공백** 또는 **4개의 공백** 사용 (프로젝트 일관성 유지)
- 최대 줄 길이: **100자** 또는 **120자**

### 2. 세미콜론

- 세미콜론 사용 여부는 프로젝트 설정에 따릅니다.
- 일관성 유지가 중요합니다.

### 3. 따옴표

- **작은따옴표(`'`)** 또는 **큰따옴표(`"`)** 사용 (프로젝트 일관성 유지)
- 템플릿 리터럴은 백틱(`` ` ``) 사용

### 4. 임포트 (Imports)

#### 임포트 순서
1. Node.js 내장 모듈
2. 외부 라이브러리
3. 내부 모듈 (절대 경로)
4. 상대 경로 모듈

#### 예시
```typescript
// Node.js 내장 모듈
import { readFile } from 'fs';
import { join } from 'path';

// 외부 라이브러리
import React from 'react';
import { NextRequest, NextResponse } from 'next/server';
import axios from 'axios';

// 내부 모듈 (절대 경로)
import { UserService } from '@/services/user-service';
import { User } from '@/types/user';

// 상대 경로 모듈
import { helper } from './helper';
import { constants } from '../constants';
```

#### 임포트 스타일
- 명명된 임포트(named imports) 우선 사용
- 기본 임포트(default imports)는 필요한 경우만 사용

---

## 명명 규칙

### 1. 변수 및 함수

- **camelCase** 사용
- 예: `userName`, `getUserData()`, `calculateTotal()`

### 2. 클래스 및 인터페이스

- **PascalCase** 사용
- 예: `UserService`, `DatabaseConnection`, `ApiClient`

### 3. 타입 및 인터페이스

- **PascalCase** 사용
- 타입 별칭(type alias)은 `T` 접두사 사용 가능
- 예: `User`, `ApiResponse`, `TUserData`

### 4. 상수

- **UPPER_SNAKE_CASE** 사용
- 예: `MAX_RETRY_COUNT`, `DEFAULT_TIMEOUT`, `API_BASE_URL`

### 5. 비공개 멤버

- 단일 언더스코어(`_`) 접두사 사용
- 예: `_privateMethod()`, `_privateVariable`

### 6. 파일명

- **kebab-case** 사용
- 예: `user-service.ts`, `api-client.ts`

---

## 타입 시스템

### 1. 타입 선언

```typescript
// 명시적 타입 선언
function calculateTotal(price: number, quantity: number): number {
  return price * quantity;
}

// 타입 추론 활용 (명확한 경우)
const userName = 'John'; // string으로 추론
const userCount = 10; // number로 추론
```

### 2. 인터페이스 vs 타입 별칭

#### 인터페이스 사용 (확장 가능한 구조)
```typescript
interface User {
  id: number;
  name: string;
  email: string;
}

interface AdminUser extends User {
  role: 'admin';
  permissions: string[];
}
```

#### 타입 별칭 사용 (유니온, 교집합 등)
```typescript
type Status = 'pending' | 'approved' | 'rejected';

type ApiResponse<T> = {
  data: T;
  status: number;
  message: string;
};
```

### 3. 제네릭

```typescript
// 함수 제네릭
function getItem<T>(items: T[], index: number): T | undefined {
  return items[index];
}

// 클래스 제네릭
class Repository<T> {
  private items: T[] = [];
  
  add(item: T): void {
    this.items.push(item);
  }
  
  find(id: number): T | undefined {
    return this.items.find(item => (item as any).id === id);
  }
}

// 인터페이스 제네릭
interface Service<TRequest, TResponse> {
  execute(request: TRequest): Promise<TResponse>;
}
```

### 4. 타입 가드

```typescript
// 타입 가드 함수
function isString(value: unknown): value is string {
  return typeof value === 'string';
}

function processValue(value: unknown): void {
  if (isString(value)) {
    // 이 블록에서 value는 string 타입
    console.log(value.toUpperCase());
  }
}
```

### 5. 옵셔널 및 기본값

```typescript
// 옵셔널 파라미터
function greet(name: string, title?: string): string {
  return title ? `${title} ${name}` : name;
}

// 기본값
function createUser(
  name: string,
  email: string,
  role: string = 'user'
): User {
  return { name, email, role };
}

// 옵셔널 체이닝
const userName = user?.profile?.name ?? 'Unknown';
```

---

## 코드 구조

### 1. 모듈 구조

```typescript
/**
 * 모듈 설명
 * @module user-service
 */

// 임포트
import { User } from '@/types/user';
import { Database } from '@/lib/database';

// 상수
const DEFAULT_LIMIT = 100;
const MAX_RETRY_COUNT = 3;

// 타입/인터페이스
interface UserServiceConfig {
  db: Database;
  cacheEnabled: boolean;
}

// 클래스
export class UserService {
  // ...
}

// 함수
export function createUserService(config: UserServiceConfig): UserService {
  return new UserService(config);
}
```

### 2. 클래스 구조

```typescript
export class UserService {
  // 정적 상수
  private static readonly DEFAULT_LIMIT = 100;
  
  // 인스턴스 변수
  private _db: Database;
  private _cache: Map<number, User>;
  
  // 생성자
  constructor(db: Database) {
    this._db = db;
    this._cache = new Map();
  }
  
  // 공개 메서드
  public async getUser(userId: number): Promise<User> {
    // 캐시 확인
    if (this._cache.has(userId)) {
      return this._cache.get(userId)!;
    }
    
    // 데이터베이스 조회
    const user = await this._db.findUser(userId);
    if (!user) {
      throw new UserNotFoundError(`User ${userId} not found`);
    }
    
    // 캐시 저장
    this._cache.set(userId, user);
    return user;
  }
  
  // 비공개 메서드
  private _validateUser(user: User): boolean {
    return user.id > 0 && !!user.email;
  }
  
  // 정적 메서드
  public static createDefault(): UserService {
    return new UserService(Database.createDefault());
  }
}
```

### 3. 함수 구조

```typescript
/**
 * 사용자 데이터를 처리합니다.
 * 
 * @param userId - 사용자 ID
 * @param options - 처리 옵션
 * @returns 처리된 사용자 데이터
 * @throws {UserNotFoundError} 사용자를 찾을 수 없는 경우
 */
export async function processUserData(
  userId: number,
  options: {
    includeProfile?: boolean;
    includeHistory?: boolean;
  } = {}
): Promise<ProcessedUserData> {
  // 파라미터 검증
  if (userId <= 0) {
    throw new Error('userId must be positive');
  }
  
  // 기본값 설정
  const {
    includeProfile = true,
    includeHistory = false
  } = options;
  
  // 함수 본문
  const user = await getUser(userId);
  const result: ProcessedUserData = {
    id: user.id,
    name: user.name
  };
  
  if (includeProfile) {
    result.profile = await getUserProfile(userId);
  }
  
  if (includeHistory) {
    result.history = await getUserHistory(userId);
  }
  
  return result;
}
```

---

## 에러 처리

### 1. 예외 처리 원칙

- 구체적인 에러 클래스 사용
- 에러 메시지는 명확하고 유용하게 작성
- 비동기 함수는 Promise rejection 처리

### 2. 커스텀 에러 클래스

```typescript
// 기본 에러 클래스
export class AppError extends Error {
  constructor(
    message: string,
    public readonly code: string,
    public readonly statusCode: number = 500
  ) {
    super(message);
    this.name = this.constructor.name;
    Error.captureStackTrace(this, this.constructor);
  }
}

// 구체적인 에러 클래스
export class UserNotFoundError extends AppError {
  constructor(userId: number) {
    super(
      `User with ID ${userId} not found`,
      'USER_NOT_FOUND',
      404
    );
  }
}

export class ValidationError extends AppError {
  constructor(message: string, public readonly fields: string[]) {
    super(message, 'VALIDATION_ERROR', 400);
  }
}
```

### 3. 에러 처리 패턴

```typescript
// try-catch 사용
async function fetchUser(userId: number): Promise<User> {
  try {
    const user = await api.getUser(userId);
    return user;
  } catch (error) {
    if (error instanceof UserNotFoundError) {
      throw error;
    // 재사용 가능한 에러는 그대로 전파
    }
    
    // 예상치 못한 에러는 로깅하고 변환
    logger.error('Unexpected error fetching user', { userId, error });
    throw new AppError(
      'Failed to fetch user',
      'FETCH_USER_ERROR',
      500
    );
  }
}

// Result 패턴 (선택적)
type Result<T, E = Error> = 
  | { success: true; data: T }
  | { success: false; error: E };

async function fetchUserSafe(userId: number): Promise<Result<User>> {
  try {
    const user = await api.getUser(userId);
    return { success: true, data: user };
  } catch (error) {
    return { success: false, error: error as Error };
  }
}
```

---

## 테스트

### 1. 테스트 파일 구조

- 테스트 파일명: `*.test.ts` 또는 `*.spec.ts`
- 테스트는 원본 파일과 같은 디렉토리 또는 `__tests__` 디렉토리에 위치

### 2. 테스트 예시

```typescript
import { describe, it, expect, beforeEach, vi } from 'vitest';
import { UserService } from './user-service';
import { UserNotFoundError } from './errors';

describe('UserService', () => {
  let userService: UserService;
  let mockDb: any;
  
  beforeEach(() => {
    mockDb = {
      findUser: vi.fn(),
    };
    userService = new UserService(mockDb);
  });
  
  describe('getUser', () => {
    it('should return user when found', async () => {
      // Given
      const userId = 1;
      const expectedUser = { id: userId, name: 'Test User' };
      mockDb.findUser.mockResolvedValue(expectedUser);
      
      // When
      const result = await userService.getUser(userId);
      
      // Then
      expect(result).toEqual(expectedUser);
      expect(mockDb.findUser).toHaveBeenCalledWith(userId);
    });
    
    it('should throw UserNotFoundError when user not found', async () => {
      // Given
      const userId = 999;
      mockDb.findUser.mockResolvedValue(null);
      
      // When & Then
      await expect(userService.getUser(userId)).rejects.toThrow(
        UserNotFoundError
      );
    });
  });
});
```

---

## 패턴 및 베스트 프랙티스

### 1. 비동기 처리

```typescript
// async/await 사용 (권장)
async function fetchData(): Promise<Data> {
  const response = await fetch('/api/data');
  return response.json();
}

// Promise 체이닝 (필요한 경우)
function fetchData(): Promise<Data> {
  return fetch('/api/data')
    .then(response => response.json())
    .catch(error => {
      console.error('Failed to fetch data', error);
      throw error;
    });
}
```

### 2. 옵셔널 체이닝 및 Nullish Coalescing

```typescript
// 옵셔널 체이닝
const userName = user?.profile?.name;
const userCount = users?.length ?? 0;

// Nullish coalescing
const timeout = config.timeout ?? 5000;
const apiUrl = process.env.API_URL || 'http://localhost:3000';
```

### 3. 구조 분해 할당

```typescript
// 객체 구조 분해
const { name, email, role } = user;
const { name: userName, email: userEmail } = user;

// 배열 구조 분해
const [first, second, ...rest] = items;

// 함수 파라미터 구조 분해
function processUser({ id, name, email }: User): void {
  // ...
}
```

### 4. 제네릭 유틸리티 타입

```typescript
// Partial: 모든 속성을 옵셔널로
type PartialUser = Partial<User>;

// Pick: 특정 속성만 선택
type UserName = Pick<User, 'name'>;

// Omit: 특정 속성 제외
type UserWithoutId = Omit<User, 'id'>;

// Record: 키-값 타입 매핑
type UserRoles = Record<string, string[]>;
```

---

## 도구 및 설정

### 1. 린터 및 포맷터

- **ESLint**: 코드 품질 검사
- **Prettier**: 코드 포맷팅
- **TypeScript Compiler**: 타입 체크

### 2. 설정 파일 예시

#### `tsconfig.json`
```json
{
  "compilerOptions": {
    "target": "ES2020",
    "module": "ESNext",
    "lib": ["ES2020", "DOM"],
    "moduleResolution": "node",
    "strict": true,
    "esModuleInterop": true,
    "skipLibCheck": true,
    "forceConsistentCasingInFileNames": true,
    "resolveJsonModule": true,
    "isolatedModules": true,
    "noEmit": true,
    "jsx": "react-jsx",
    "baseUrl": ".",
    "paths": {
      "@/*": ["./src/*"]
    }
  },
  "include": ["src"],
  "exclude": ["node_modules", "dist"]
}
```

---

## 참고 자료

- [TypeScript Handbook](https://www.typescriptlang.org/docs/handbook/intro.html)
- [TypeScript Style Guide](https://github.com/basarat/typescript-book)
- [Google TypeScript Style Guide](https://google.github.io/styleguide/tsguide.html)

