# React 코딩표준 (React Coding Standards)

이 문서는 AI-Driven Development System에서 React 개발 시 준수해야 할 코딩 표준과 패턴을 정의합니다.

## 📋 목차

1. [컴포넌트 작성 규칙](#컴포넌트-작성-규칙)
2. [Hooks 사용 규칙](#hooks-사용-규칙)
3. [상태 관리](#상태-관리)
4. [성능 최적화](#성능-최적화)

---

## 컴포넌트 작성 규칙

### 1. 함수형 컴포넌트 사용

```typescript
// 좋은 예
interface UserCardProps {
  user: User;
  onEdit?: (user: User) => void;
}

export function UserCard({ user, onEdit }: UserCardProps) {
  return (
    <div>
      <h3>{user.name}</h3>
      {onEdit && (
        <button onClick={() => onEdit(user)}>Edit</button>
      )}
    </div>
  );
}
```

### 2. Props 타입 정의

```typescript
// 명시적 Props 인터페이스
interface ButtonProps {
  children: React.ReactNode;
  variant?: 'primary' | 'secondary';
  onClick?: () => void;
  disabled?: boolean;
}

export function Button({ 
  children, 
  variant = 'primary', 
  onClick,
  disabled = false 
}: ButtonProps) {
  return (
    <button
      className={`btn btn-${variant}`}
      onClick={onClick}
      disabled={disabled}
    >
      {children}
    </button>
  );
}
```

---

## Hooks 사용 규칙

### 1. Hooks 규칙 준수

- Hooks는 최상위 레벨에서만 호출
- 조건문, 반복문, 중첩 함수 내에서 호출 금지

### 2. Custom Hooks

```typescript
// hooks/use-user.ts
import { useState, useEffect } from 'react';
import { User } from '@/types/user';

export function useUser(userId: number) {
  const [user, setUser] = useState<User | null>(null);
  const [loading, setLoading] = useState(true);
  const [error, setError] = useState<Error | null>(null);
  
  useEffect(() => {
    async function fetchUser() {
      try {
        setLoading(true);
        const data = await fetchUserById(userId);
        setUser(data);
      } catch (err) {
        setError(err as Error);
      } finally {
        setLoading(false);
      }
    }
    
    fetchUser();
  }, [userId]);
  
  return { user, loading, error };
}
```

---

## 상태 관리

### 1. 로컬 상태

```typescript
// useState 사용
const [count, setCount] = useState(0);
const [name, setName] = useState('');
```

### 2. 전역 상태

- Context API 또는 상태 관리 라이브러리 사용
- Zustand, Redux, Jotai 등

---

## 성능 최적화

### 1. React.memo

```typescript
export const UserCard = React.memo(function UserCard({ user }: UserCardProps) {
  return <div>{user.name}</div>;
});
```

### 2. useMemo, useCallback

```typescript
const expensiveValue = useMemo(() => {
  return computeExpensiveValue(data);
}, [data]);

const handleClick = useCallback(() => {
  doSomething(id);
}, [id]);
```

---

## 참고 자료

- [React Documentation](https://react.dev/)
- [React Hooks](https://react.dev/reference/react)

