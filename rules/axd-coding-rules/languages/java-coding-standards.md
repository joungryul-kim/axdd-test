# Java 코딩표준 (Java Coding Standards)

이 문서는 AI-Driven Development System에서 Java 개발 시 준수해야 할 코딩 표준과 패턴을 정의합니다.

## 📋 목차

1. [일반 원칙](#일반-원칙)
2. [코딩 컨벤션](#코딩-컨벤션)
3. [명명 규칙](#명명-규칙)
4. [클래스 구조](#클래스-구조)
5. [에러 처리](#에러-처리)
6. [테스트](#테스트)

---

## 일반 원칙

### 1. Java Code Conventions 준수

- Oracle의 [Java Code Conventions](https://www.oracle.com/java/technologies/javase/codeconventions-contents.html)를 기본으로 따릅니다.
- 프로젝트별로 일부 규칙을 조정할 수 있으나, 기본 원칙은 유지합니다.

### 2. 모던 Java 기능 활용

- Java 11+ 기능을 적극 활용합니다.
- Optional, Stream API, Lambda 표현식 등을 적절히 사용합니다.

---

## 코딩 컨벤션

### 1. 들여쓰기

- **4개의 공백** 사용 (탭 사용 금지)
- 최대 줄 길이: **120자**

### 2. 중괄호

- K&R 스타일 사용
- 제어문이 한 줄이더라도 중괄호 사용

```java
// 좋은 예
if (condition) {
    doSomething();
}

// 나쁜 예
if (condition) doSomething();
```

### 3. 임포트

- 와일드카드 임포트(`import java.util.*;`) 사용 금지
- 정적 임포트는 필요한 경우만 사용

---

## 명명 규칙

### 1. 클래스 및 인터페이스

- **PascalCase** 사용
- 예: `UserService`, `DatabaseConnection`, `ApiClient`

### 2. 메서드 및 변수

- **camelCase** 사용
- 예: `getUserData()`, `userName`, `calculateTotal()`

### 3. 상수

- **UPPER_SNAKE_CASE** 사용
- 예: `MAX_RETRY_COUNT`, `DEFAULT_TIMEOUT`, `API_BASE_URL`

### 4. 패키지

- **lowercase** 사용 (점으로 구분)
- 예: `com.example.userservice`

---

## 클래스 구조

### 1. 클래스 구조 순서

```java
package com.example.userservice;

// 임포트
import java.util.List;
import java.util.Optional;

/**
 * 사용자 서비스 클래스
 */
public class UserService {
    
    // 상수
    private static final int DEFAULT_LIMIT = 100;
    private static final int MAX_RETRY_COUNT = 3;
    
    // 인스턴스 변수
    private final UserRepository userRepository;
    private final CacheService cacheService;
    
    // 생성자
    public UserService(UserRepository userRepository, CacheService cacheService) {
        this.userRepository = userRepository;
        this.cacheService = cacheService;
    }
    
    // 공개 메서드
    public Optional<User> getUser(Long userId) {
        // 구현
        return userRepository.findById(userId);
    }
    
    // 비공개 메서드
    private void validateUser(User user) {
        // 구현
    }
}
```

---

## 에러 처리

### 1. 예외 처리 원칙

- 구체적인 예외 타입 사용
- 체크 예외는 필요한 경우만 사용
- 예외 메시지는 명확하고 유용하게 작성

### 2. 커스텀 예외

```java
public class UserServiceException extends RuntimeException {
    public UserServiceException(String message) {
        super(message);
    }
    
    public UserServiceException(String message, Throwable cause) {
        super(message, cause);
    }
}

public class UserNotFoundException extends UserServiceException {
    public UserNotFoundException(Long userId) {
        super("User with ID " + userId + " not found");
    }
}
```

---

## 참고 자료

- [Java Code Conventions](https://www.oracle.com/java/technologies/javase/codeconventions-contents.html)
- [Google Java Style Guide](https://google.github.io/styleguide/javaguide.html)

