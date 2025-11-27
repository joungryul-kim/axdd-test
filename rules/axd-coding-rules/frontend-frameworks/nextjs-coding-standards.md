# Next.js 코딩표준 (Next.js Coding Standards)

이 문서는 AI-Driven Development System에서 Next.js 개발 시 준수해야 할 코딩 표준과 패턴을 정의합니다.

## 📋 목차

1. [프로젝트 구조](#프로젝트-구조)
2. [App Router 패턴](#app-router-패턴)
3. [컴포넌트 작성 규칙](#컴포넌트-작성-규칙)
4. [라우팅 규칙](#라우팅-규칙)
5. [데이터 페칭](#데이터-페칭)
6. [스타일링](#스타일링)
7. [성능 최적화](#성능-최적화)

---

## 프로젝트 구조

### 1. 권장 디렉토리 구조

```
project/
├── app/                      # App Router (Next.js 13+)
│   ├── (auth)/              # Route groups
│   │   └── login/
│   │       └── page.tsx
│   ├── api/                 # API routes
│   │   └── users/
│   │       └── route.ts
│   ├── layout.tsx           # Root layout
│   ├── page.tsx             # Home page
│   └── globals.css
├── components/              # React components
│   ├── ui/                  # UI components
│   ├── layout/              # Layout components
│   └── features/            # Feature-specific components
├── lib/                     # Utility functions
│   ├── api.ts
│   └── utils.ts
├── hooks/                   # Custom React hooks
├── types/                   # TypeScript types
│   └── index.ts
├── public/                  # Static assets
└── styles/                  # Global styles
```

### 2. 파일 명명 규칙

- 페이지: `page.tsx`, `layout.tsx`, `loading.tsx`, `error.tsx`
- 컴포넌트: `PascalCase.tsx` 또는 `kebab-case.tsx`
- 유틸리티: `kebab-case.ts`
- 타입: `kebab-case.ts`

---

## App Router 패턴

### 1. 페이지 컴포넌트

```typescript
// app/users/page.tsx
import { Metadata } from 'next';
import { UserList } from '@/components/features/users/user-list';

export const metadata: Metadata = {
  title: 'Users',
  description: 'User list page',
};

export default async function UsersPage() {
  // Server Component에서 직접 데이터 페칭
  const users = await fetchUsers();
  
  return (
    <div>
      <h1>Users</h1>
      <UserList users={users} />
    </div>
  );
}
```

### 2. 레이아웃 컴포넌트

```typescript
// app/layout.tsx
import type { Metadata } from 'next';
import { Inter } from 'next/font/google';
import { Header } from '@/components/layout/header';
import { Footer } from '@/components/layout/footer';
import './globals.css';

const inter = Inter({ subsets: ['latin'] });

export const metadata: Metadata = {
  title: 'My App',
  description: 'Application description',
};

export default function RootLayout({
  children,
}: {
  children: React.ReactNode;
}) {
  return (
    <html lang="ko">
      <body className={inter.className}>
        <Header />
        <main>{children}</main>
        <Footer />
      </body>
    </html>
  );
}
```

### 3. 로딩 및 에러 처리

```typescript
// app/users/loading.tsx
export default function Loading() {
  return <div>Loading users...</div>;
}

// app/users/error.tsx
'use client';

export default function Error({
  error,
  reset,
}: {
  error: Error & { digest?: string };
  reset: () => void;
}) {
  return (
    <div>
      <h2>Something went wrong!</h2>
      <button onClick={() => reset()}>Try again</button>
    </div>
  );
}
```

---

## 컴포넌트 작성 규칙

### 1. Server Component vs Client Component

#### Server Component (기본)
```typescript
// components/user-card.tsx
import { User } from '@/types/user';

interface UserCardProps {
  user: User;
}

export function UserCard({ user }: UserCardProps) {
  return (
    <div>
      <h3>{user.name}</h3>
      <p>{user.email}</p>
    </div>
  );
}
```

#### Client Component (필요한 경우만)
```typescript
// components/user-form.tsx
'use client';

import { useState } from 'react';

export function UserForm() {
  const [name, setName] = useState('');
  
  return (
    <form>
      <input
        value={name}
        onChange={(e) => setName(e.target.value)}
      />
    </form>
  );
}
```

### 2. 컴포넌트 구조

```typescript
// components/features/users/user-list.tsx
'use client';

import { User } from '@/types/user';
import { UserCard } from './user-card';

interface UserListProps {
  users: User[];
}

export function UserList({ users }: UserListProps) {
  if (users.length === 0) {
    return <div>No users found</div>;
  }
  
  return (
    <ul>
      {users.map((user) => (
        <li key={user.id}>
          <UserCard user={user} />
        </li>
      ))}
    </ul>
  );
}
```

---

## 라우팅 규칙

### 1. 동적 라우트

```typescript
// app/users/[id]/page.tsx
interface UserPageProps {
  params: {
    id: string;
  };
}

export default async function UserPage({ params }: UserPageProps) {
  const user = await getUserById(params.id);
  
  if (!user) {
    notFound();
  }
  
  return (
    <div>
      <h1>{user.name}</h1>
    </div>
  );
}
```

### 2. Catch-all 라우트

```typescript
// app/docs/[...slug]/page.tsx
interface DocsPageProps {
  params: {
    slug: string[];
  };
}

export default function DocsPage({ params }: DocsPageProps) {
  const slug = params.slug.join('/');
  // ...
}
```

### 3. Route Groups

```typescript
// app/(auth)/login/page.tsx
// app/(auth)/register/page.tsx
// URL에는 (auth)가 포함되지 않음
```

---

## 데이터 페칭

### 1. Server Component에서 데이터 페칭

```typescript
// app/users/page.tsx
async function fetchUsers(): Promise<User[]> {
  const res = await fetch('https://api.example.com/users', {
    cache: 'no-store', // 또는 'force-cache', { revalidate: 3600 }
  });
  
  if (!res.ok) {
    throw new Error('Failed to fetch users');
  }
  
  return res.json();
}

export default async function UsersPage() {
  const users = await fetchUsers();
  return <UserList users={users} />;
}
```

### 2. API Routes

```typescript
// app/api/users/route.ts
import { NextRequest, NextResponse } from 'next/server';

export async function GET(request: NextRequest) {
  const users = await getUsersFromDB();
  return NextResponse.json(users);
}

export async function POST(request: NextRequest) {
  const body = await request.json();
  const user = await createUser(body);
  return NextResponse.json(user, { status: 201 });
}
```

### 3. Client Component에서 데이터 페칭

```typescript
// hooks/use-users.ts
'use client';

import { useState, useEffect } from 'react';
import { User } from '@/types/user';

export function useUsers() {
  const [users, setUsers] = useState<User[]>([]);
  const [loading, setLoading] = useState(true);
  const [error, setError] = useState<Error | null>(null);
  
  useEffect(() => {
    fetch('/api/users')
      .then(res => res.json())
      .then(data => {
        setUsers(data);
        setLoading(false);
      })
      .catch(err => {
        setError(err);
        setLoading(false);
      });
  }, []);
  
  return { users, loading, error };
}
```

---

## 스타일링

### 1. Tailwind CSS 사용

```typescript
// components/button.tsx
interface ButtonProps {
  children: React.ReactNode;
  variant?: 'primary' | 'secondary';
  onClick?: () => void;
}

export function Button({ children, variant = 'primary', onClick }: ButtonProps) {
  const baseClasses = 'px-4 py-2 rounded font-medium';
  const variantClasses = {
    primary: 'bg-blue-600 text-white hover:bg-blue-700',
    secondary: 'bg-gray-200 text-gray-800 hover:bg-gray-300',
  };
  
  return (
    <button
      className={`${baseClasses} ${variantClasses[variant]}`}
      onClick={onClick}
    >
      {children}
    </button>
  );
}
```

### 2. CSS Modules

```typescript
// components/user-card.module.css
.card {
  padding: 1rem;
  border: 1px solid #e5e7eb;
  border-radius: 0.5rem;
}

.title {
  font-size: 1.25rem;
  font-weight: 600;
}
```

```typescript
// components/user-card.tsx
import styles from './user-card.module.css';

export function UserCard() {
  return (
    <div className={styles.card}>
      <h3 className={styles.title}>User</h3>
    </div>
  );
}
```

---

## 성능 최적화

### 1. 이미지 최적화

```typescript
import Image from 'next/image';

export function UserAvatar({ src, alt }: { src: string; alt: string }) {
  return (
    <Image
      src={src}
      alt={alt}
      width={100}
      height={100}
      priority // 중요 이미지인 경우
    />
  );
}
```

### 2. 동적 임포트

```typescript
import dynamic from 'next/dynamic';

const HeavyComponent = dynamic(() => import('./heavy-component'), {
  loading: () => <p>Loading...</p>,
  ssr: false, // 서버 사이드 렌더링 비활성화
});
```

### 3. 메타데이터 최적화

```typescript
export const metadata: Metadata = {
  title: 'Page Title',
  description: 'Page description',
  openGraph: {
    title: 'Page Title',
    description: 'Page description',
    images: ['/og-image.jpg'],
  },
};
```

---

## 참고 자료

- [Next.js Documentation](https://nextjs.org/docs)
- [Next.js App Router](https://nextjs.org/docs/app)
- [Next.js Best Practices](https://nextjs.org/docs/app/building-your-application/routing/loading-ui-and-streaming)

