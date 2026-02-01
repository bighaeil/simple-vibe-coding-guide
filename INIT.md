# Project Initialization Document

## 프로젝트 개요
- **프로젝트명**: [프로젝트 이름]
- **설명**: [한 줄 설명]
- **시작일**: YYYY-MM-DD
- **주요 목표**: 
  - [핵심 목표 1]
  - [핵심 목표 2]
  - [핵심 목표 3]

---

## 기술 스택

### Backend
- **언어**: Java 17 (LTS)
- **프레임워크**: Spring Boot 3.2.x
- **빌드 도구**: Gradle 8.x (Kotlin DSL)
- **데이터베이스**: 
  - Primary: PostgreSQL 16.x
  - Cache: Redis 7.x
- **ORM**: Spring Data JPA (Hibernate 6.x)
- **인증/보안**: Spring Security 6.x + JWT
- **API 문서**: SpringDoc OpenAPI 3.x (Swagger)
- **테스트**: JUnit 5 + Mockito + TestContainers

### 주요 의존성
```gradle
dependencies {
    // Spring Boot Starters
    implementation 'org.springframework.boot:spring-boot-starter-web'
    implementation 'org.springframework.boot:spring-boot-starter-data-jpa'
    implementation 'org.springframework.boot:spring-boot-starter-security'
    implementation 'org.springframework.boot:spring-boot-starter-validation'
    implementation 'org.springframework.boot:spring-boot-starter-data-redis'
    
    // Database
    runtimeOnly 'org.postgresql:postgresql'
    
    // JWT
    implementation 'io.jsonwebtoken:jjwt-api:0.12.3'
    runtimeOnly 'io.jsonwebtoken:jjwt-impl:0.12.3'
    runtimeOnly 'io.jsonwebtoken:jjwt-jackson:0.12.3'
    
    // Lombok
    compileOnly 'org.projectlombok:lombok'
    annotationProcessor 'org.projectlombok:lombok'
    
    // MapStruct
    implementation 'org.mapstruct:mapstruct:1.5.5.Final'
    annotationProcessor 'org.mapstruct:mapstruct-processor:1.5.5.Final'
    
    // API Documentation
    implementation 'org.springdoc:springdoc-openapi-starter-webmvc-ui:2.3.0'
    
    // Testing
    testImplementation 'org.springframework.boot:spring-boot-starter-test'
    testImplementation 'org.springframework.security:spring-security-test'
    testImplementation 'org.testcontainers:postgresql:1.19.3'
}
```

### 개발 도구
- **IDE**: IntelliJ IDEA
- **코드 포매터**: Google Java Format
- **정적 분석**: SonarLint, CheckStyle
- **API 테스트**: Postman, REST Client
- **CI/CD**: GitHub Actions / Jenkins
- **컨테이너**: Docker + Docker Compose
- **모니터링**: Spring Boot Actuator + Prometheus + Grafana

---

## 프로젝트 구조

```
src/
├── main/
│   ├── java/
│   │   └── com/
│   │       └── company/
│   │           └── project/
│   │               ├── ProjectApplication.java
│   │               ├── common/              # 공통 유틸리티
│   │               │   ├── config/          # 설정 클래스
│   │               │   │   ├── SecurityConfig.java
│   │               │   │   ├── JpaConfig.java
│   │               │   │   ├── RedisConfig.java
│   │               │   │   └── SwaggerConfig.java
│   │               │   ├── exception/       # 예외 처리
│   │               │   │   ├── GlobalExceptionHandler.java
│   │               │   │   ├── BusinessException.java
│   │               │   │   └── ErrorCode.java
│   │               │   ├── util/            # 유틸리티
│   │               │   │   ├── JwtUtil.java
│   │               │   │   └── DateUtil.java
│   │               │   └── dto/             # 공통 DTO
│   │               │       ├── ApiResponse.java
│   │               │       └── PageResponse.java
│   │               │
│   │               ├── domain/              # 도메인 모듈
│   │               │   ├── user/
│   │               │   │   ├── controller/
│   │               │   │   │   └── UserController.java
│   │               │   │   ├── service/
│   │               │   │   │   ├── UserService.java
│   │               │   │   │   └── UserServiceImpl.java
│   │               │   │   ├── repository/
│   │               │   │   │   └── UserRepository.java
│   │               │   │   ├── entity/
│   │               │   │   │   └── User.java
│   │               │   │   ├── dto/
│   │               │   │   │   ├── UserCreateRequest.java
│   │               │   │   │   ├── UserUpdateRequest.java
│   │               │   │   │   └── UserResponse.java
│   │               │   │   └── mapper/
│   │               │   │       └── UserMapper.java
│   │               │   │
│   │               │   ├── auth/
│   │               │   │   ├── controller/
│   │               │   │   ├── service/
│   │               │   │   ├── dto/
│   │               │   │   └── filter/
│   │               │   │       └── JwtAuthenticationFilter.java
│   │               │   │
│   │               │   └── post/
│   │               │       ├── controller/
│   │               │       ├── service/
│   │               │       ├── repository/
│   │               │       ├── entity/
│   │               │       └── dto/
│   │               │
│   │               └── infrastructure/       # 인프라 계층
│   │                   ├── persistence/
│   │                   └── external/
│   │
│   └── resources/
│       ├── application.yml                  # 기본 설정
│       ├── application-dev.yml              # 개발 환경
│       ├── application-prod.yml             # 운영 환경
│       ├── application-test.yml             # 테스트 환경
│       └── db/
│           └── migration/                   # Flyway/Liquibase
│
└── test/
    └── java/
        └── com/
            └── company/
                └── project/
                    ├── domain/
                    │   └── user/
                    │       ├── controller/
                    │       │   └── UserControllerTest.java
                    │       ├── service/
                    │       │   └── UserServiceTest.java
                    │       └── repository/
                    │           └── UserRepositoryTest.java
                    └── common/
                        └── TestConfig.java
```

### 아키텍처 패턴
- **레이어드 아키텍처**: Controller → Service → Repository → Entity
- **도메인 주도 설계(DDD)**: 도메인별 패키지 구조
- **의존성 주입**: Spring IoC Container 활용
- **DTO 변환**: MapStruct를 통한 Entity ↔ DTO 매핑

---

## 코딩 컨벤션

### 네이밍 규칙

#### 패키지명
- 소문자 사용, 단수형
- 도메인별 구분: `com.company.project.domain.user`
- 계층별 구분: `controller`, `service`, `repository`, `entity`, `dto`

#### 클래스명
```java
// PascalCase
public class UserController {}
public class UserService {}
public class UserServiceImpl {}
public class UserRepository {}
public class User {}              // Entity
public class UserCreateRequest {} // Request DTO
public class UserResponse {}      // Response DTO
```

#### 인터페이스와 구현체
```java
// 인터페이스: 명사 또는 형용사
public interface UserService {}
public interface Readable {}

// 구현체: Impl 접미사
public class UserServiceImpl implements UserService {}
```

#### 메서드명
```java
// camelCase, 동사로 시작
public User findById(Long id) {}
public List<User> findAll() {}
public User create(UserCreateRequest request) {}
public User update(Long id, UserUpdateRequest request) {}
public void delete(Long id) {}
public boolean existsByEmail(String email) {}
public int countActiveUsers() {}
```

#### 변수명
```java
// camelCase
private String userName;
private Long userId;
private List<User> userList;
private Optional<User> optionalUser;
```

#### 상수명
```java
// SCREAMING_SNAKE_CASE
public static final int MAX_LOGIN_ATTEMPTS = 5;
public static final String DEFAULT_ROLE = "USER";
public static final Duration TOKEN_EXPIRATION = Duration.ofHours(24);
```

### Java 코드 스타일

#### Entity 작성
```java
@Entity
@Table(name = "users")
@Getter
@NoArgsConstructor(access = AccessLevel.PROTECTED)
@EntityListeners(AuditingEntityListener.class)
public class User {
    
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
    
    @Column(nullable = false, unique = true, length = 100)
    private String email;
    
    @Column(nullable = false, length = 100)
    private String name;
    
    @Column(nullable = false)
    private String password;
    
    @Enumerated(EnumType.STRING)
    @Column(nullable = false, length = 20)
    private UserRole role;
    
    @CreatedDate
    @Column(nullable = false, updatable = false)
    private LocalDateTime createdAt;
    
    @LastModifiedDate
    @Column(nullable = false)
    private LocalDateTime updatedAt;
    
    @Builder
    public User(String email, String name, String password, UserRole role) {
        this.email = email;
        this.name = name;
        this.password = password;
        this.role = role;
    }
    
    // 비즈니스 로직 메서드
    public void updateProfile(String name) {
        this.name = name;
    }
    
    public void changePassword(String newPassword) {
        this.password = newPassword;
    }
}
```

#### Controller 작성
```java
@RestController
@RequestMapping("/api/v1/users")
@RequiredArgsConstructor
@Tag(name = "User", description = "사용자 관리 API")
public class UserController {
    
    private final UserService userService;
    
    @GetMapping("/{id}")
    @Operation(summary = "사용자 조회", description = "ID로 사용자를 조회합니다.")
    public ResponseEntity<ApiResponse<UserResponse>> getUser(
            @PathVariable @NotNull Long id
    ) {
        UserResponse user = userService.findById(id);
        return ResponseEntity.ok(ApiResponse.success(user));
    }
    
    @GetMapping
    @Operation(summary = "사용자 목록 조회", description = "페이징된 사용자 목록을 조회합니다.")
    public ResponseEntity<ApiResponse<PageResponse<UserResponse>>> getUsers(
            @RequestParam(defaultValue = "0") int page,
            @RequestParam(defaultValue = "20") int size,
            @RequestParam(defaultValue = "id,desc") String sort
    ) {
        PageResponse<UserResponse> users = userService.findAll(page, size, sort);
        return ResponseEntity.ok(ApiResponse.success(users));
    }
    
    @PostMapping
    @Operation(summary = "사용자 생성", description = "새로운 사용자를 생성합니다.")
    public ResponseEntity<ApiResponse<UserResponse>> createUser(
            @RequestBody @Valid UserCreateRequest request
    ) {
        UserResponse user = userService.create(request);
        return ResponseEntity.status(HttpStatus.CREATED)
                .body(ApiResponse.success(user, "사용자가 생성되었습니다."));
    }
    
    @PatchMapping("/{id}")
    @Operation(summary = "사용자 수정", description = "사용자 정보를 수정합니다.")
    public ResponseEntity<ApiResponse<UserResponse>> updateUser(
            @PathVariable @NotNull Long id,
            @RequestBody @Valid UserUpdateRequest request
    ) {
        UserResponse user = userService.update(id, request);
        return ResponseEntity.ok(ApiResponse.success(user, "사용자가 수정되었습니다."));
    }
    
    @DeleteMapping("/{id}")
    @Operation(summary = "사용자 삭제", description = "사용자를 삭제합니다.")
    public ResponseEntity<ApiResponse<Void>> deleteUser(
            @PathVariable @NotNull Long id
    ) {
        userService.delete(id);
        return ResponseEntity.ok(ApiResponse.success(null, "사용자가 삭제되었습니다."));
    }
}
```

#### Service 작성
```java
public interface UserService {
    UserResponse findById(Long id);
    PageResponse<UserResponse> findAll(int page, int size, String sort);
    UserResponse create(UserCreateRequest request);
    UserResponse update(Long id, UserUpdateRequest request);
    void delete(Long id);
}

@Service
@RequiredArgsConstructor
@Transactional(readOnly = true)
@Slf4j
public class UserServiceImpl implements UserService {
    
    private final UserRepository userRepository;
    private final UserMapper userMapper;
    private final PasswordEncoder passwordEncoder;
    
    @Override
    public UserResponse findById(Long id) {
        User user = userRepository.findById(id)
                .orElseThrow(() -> new BusinessException(ErrorCode.USER_NOT_FOUND));
        
        return userMapper.toResponse(user);
    }
    
    @Override
    public PageResponse<UserResponse> findAll(int page, int size, String sort) {
        String[] sortParams = sort.split(",");
        Sort.Direction direction = Sort.Direction.fromString(sortParams[1]);
        Pageable pageable = PageRequest.of(page, size, Sort.by(direction, sortParams[0]));
        
        Page<User> userPage = userRepository.findAll(pageable);
        
        return PageResponse.of(
                userPage.map(userMapper::toResponse).getContent(),
                userPage.getNumber(),
                userPage.getSize(),
                userPage.getTotalElements()
        );
    }
    
    @Override
    @Transactional
    public UserResponse create(UserCreateRequest request) {
        // 이메일 중복 검증
        if (userRepository.existsByEmail(request.getEmail())) {
            throw new BusinessException(ErrorCode.EMAIL_ALREADY_EXISTS);
        }
        
        // 비밀번호 암호화
        String encodedPassword = passwordEncoder.encode(request.getPassword());
        
        // Entity 생성 및 저장
        User user = User.builder()
                .email(request.getEmail())
                .name(request.getName())
                .password(encodedPassword)
                .role(UserRole.USER)
                .build();
        
        User savedUser = userRepository.save(user);
        
        log.info("사용자 생성 완료: id={}, email={}", savedUser.getId(), savedUser.getEmail());
        
        return userMapper.toResponse(savedUser);
    }
    
    @Override
    @Transactional
    public UserResponse update(Long id, UserUpdateRequest request) {
        User user = userRepository.findById(id)
                .orElseThrow(() -> new BusinessException(ErrorCode.USER_NOT_FOUND));
        
        user.updateProfile(request.getName());
        
        log.info("사용자 수정 완료: id={}", id);
        
        return userMapper.toResponse(user);
    }
    
    @Override
    @Transactional
    public void delete(Long id) {
        if (!userRepository.existsById(id)) {
            throw new BusinessException(ErrorCode.USER_NOT_FOUND);
        }
        
        userRepository.deleteById(id);
        
        log.info("사용자 삭제 완료: id={}", id);
    }
}
```

#### Repository 작성
```java
public interface UserRepository extends JpaRepository<User, Long> {
    
    Optional<User> findByEmail(String email);
    
    boolean existsByEmail(String email);
    
    @Query("SELECT u FROM User u WHERE u.role = :role AND u.createdAt >= :startDate")
    List<User> findActiveUsersByRole(
            @Param("role") UserRole role,
            @Param("startDate") LocalDateTime startDate
    );
    
    @Modifying
    @Query("DELETE FROM User u WHERE u.createdAt < :cutoffDate")
    int deleteOldUsers(@Param("cutoffDate") LocalDateTime cutoffDate);
}
```

#### DTO 작성
```java
// Request DTO
@Getter
@NoArgsConstructor
@AllArgsConstructor
public class UserCreateRequest {
    
    @NotBlank(message = "이메일은 필수입니다.")
    @Email(message = "올바른 이메일 형식이 아닙니다.")
    @Size(max = 100, message = "이메일은 100자를 초과할 수 없습니다.")
    private String email;
    
    @NotBlank(message = "이름은 필수입니다.")
    @Size(min = 2, max = 50, message = "이름은 2~50자 사이여야 합니다.")
    private String name;
    
    @NotBlank(message = "비밀번호는 필수입니다.")
    @Pattern(
            regexp = "^(?=.*[A-Za-z])(?=.*\\d)(?=.*[@$!%*#?&])[A-Za-z\\d@$!%*#?&]{8,}$",
            message = "비밀번호는 8자 이상, 영문, 숫자, 특수문자를 포함해야 합니다."
    )
    private String password;
}

// Response DTO
@Getter
@Builder
@AllArgsConstructor
public class UserResponse {
    private Long id;
    private String email;
    private String name;
    private UserRole role;
    private LocalDateTime createdAt;
    private LocalDateTime updatedAt;
}
```

#### Mapper 작성 (MapStruct)
```java
@Mapper(componentModel = "spring")
public interface UserMapper {
    
    UserResponse toResponse(User user);
    
    List<UserResponse> toResponseList(List<User> users);
    
    @Mapping(target = "id", ignore = true)
    @Mapping(target = "createdAt", ignore = true)
    @Mapping(target = "updatedAt", ignore = true)
    User toEntity(UserCreateRequest request);
}
```

### 예외 처리

#### ErrorCode Enum
```java
@Getter
@RequiredArgsConstructor
public enum ErrorCode {
    
    // Common
    INVALID_INPUT_VALUE(400, "C001", "잘못된 입력값입니다."),
    METHOD_NOT_ALLOWED(405, "C002", "허용되지 않은 메서드입니다."),
    INTERNAL_SERVER_ERROR(500, "C003", "서버 오류가 발생했습니다."),
    
    // User
    USER_NOT_FOUND(404, "U001", "사용자를 찾을 수 없습니다."),
    EMAIL_ALREADY_EXISTS(409, "U002", "이미 존재하는 이메일입니다."),
    
    // Auth
    UNAUTHORIZED(401, "A001", "인증이 필요합니다."),
    FORBIDDEN(403, "A002", "권한이 없습니다."),
    INVALID_CREDENTIALS(401, "A003", "이메일 또는 비밀번호가 올바르지 않습니다."),
    TOKEN_EXPIRED(401, "A004", "토큰이 만료되었습니다."),
    ;
    
    private final int status;
    private final String code;
    private final String message;
}
```

#### BusinessException
```java
@Getter
public class BusinessException extends RuntimeException {
    
    private final ErrorCode errorCode;
    
    public BusinessException(ErrorCode errorCode) {
        super(errorCode.getMessage());
        this.errorCode = errorCode;
    }
    
    public BusinessException(ErrorCode errorCode, String message) {
        super(message);
        this.errorCode = errorCode;
    }
}
```

#### GlobalExceptionHandler
```java
@RestControllerAdvice
@Slf4j
public class GlobalExceptionHandler {
    
    @ExceptionHandler(BusinessException.class)
    public ResponseEntity<ApiResponse<Void>> handleBusinessException(BusinessException e) {
        log.error("BusinessException: {}", e.getMessage(), e);
        
        ErrorCode errorCode = e.getErrorCode();
        return ResponseEntity
                .status(errorCode.getStatus())
                .body(ApiResponse.error(errorCode.getCode(), e.getMessage()));
    }
    
    @ExceptionHandler(MethodArgumentNotValidException.class)
    public ResponseEntity<ApiResponse<Map<String, String>>> handleValidationException(
            MethodArgumentNotValidException e
    ) {
        log.error("ValidationException: {}", e.getMessage());
        
        Map<String, String> errors = new HashMap<>();
        e.getBindingResult().getFieldErrors().forEach(error ->
                errors.put(error.getField(), error.getDefaultMessage())
        );
        
        return ResponseEntity
                .status(HttpStatus.BAD_REQUEST)
                .body(ApiResponse.error(ErrorCode.INVALID_INPUT_VALUE.getCode(), 
                        ErrorCode.INVALID_INPUT_VALUE.getMessage(), errors));
    }
    
    @ExceptionHandler(Exception.class)
    public ResponseEntity<ApiResponse<Void>> handleException(Exception e) {
        log.error("Exception: {}", e.getMessage(), e);
        
        return ResponseEntity
                .status(HttpStatus.INTERNAL_SERVER_ERROR)
                .body(ApiResponse.error(
                        ErrorCode.INTERNAL_SERVER_ERROR.getCode(),
                        ErrorCode.INTERNAL_SERVER_ERROR.getMessage()
                ));
    }
}
```

### 응답 형식

#### ApiResponse
```java
@Getter
@Builder
@AllArgsConstructor
public class ApiResponse<T> {
    
    private boolean success;
    private T data;
    private String message;
    private String errorCode;
    private LocalDateTime timestamp;
    
    public static <T> ApiResponse<T> success(T data) {
        return ApiResponse.<T>builder()
                .success(true)
                .data(data)
                .timestamp(LocalDateTime.now())
                .build();
    }
    
    public static <T> ApiResponse<T> success(T data, String message) {
        return ApiResponse.<T>builder()
                .success(true)
                .data(data)
                .message(message)
                .timestamp(LocalDateTime.now())
                .build();
    }
    
    public static <T> ApiResponse<T> error(String errorCode, String message) {
        return ApiResponse.<T>builder()
                .success(false)
                .errorCode(errorCode)
                .message(message)
                .timestamp(LocalDateTime.now())
                .build();
    }
    
    public static <T> ApiResponse<T> error(String errorCode, String message, T data) {
        return ApiResponse.<T>builder()
                .success(false)
                .errorCode(errorCode)
                .message(message)
                .data(data)
                .timestamp(LocalDateTime.now())
                .build();
    }
}
```

#### PageResponse
```java
@Getter
@AllArgsConstructor
public class PageResponse<T> {
    
    private List<T> content;
    private int page;
    private int size;
    private long totalElements;
    private int totalPages;
    
    public static <T> PageResponse<T> of(List<T> content, int page, int size, long totalElements) {
        int totalPages = (int) Math.ceil((double) totalElements / size);
        return new PageResponse<>(content, page, size, totalElements, totalPages);
    }
}
```

---

## 환경 변수

### application.yml
```yaml
spring:
  application:
    name: project-name
  
  profiles:
    active: ${SPRING_PROFILES_ACTIVE:dev}
  
  datasource:
    driver-class-name: org.postgresql.Driver
    url: ${DATABASE_URL:jdbc:postgresql://localhost:5432/dbname}
    username: ${DATABASE_USERNAME:postgres}
    password: ${DATABASE_PASSWORD:password}
    hikari:
      maximum-pool-size: 10
      minimum-idle: 5
      connection-timeout: 30000
  
  jpa:
    hibernate:
      ddl-auto: ${DDL_AUTO:validate}
    properties:
      hibernate:
        format_sql: true
        show_sql: false
        default_batch_fetch_size: 100
    open-in-view: false
  
  data:
    redis:
      host: ${REDIS_HOST:localhost}
      port: ${REDIS_PORT:6379}
      password: ${REDIS_PASSWORD:}
  
  security:
    oauth2:
      client:
        registration:
          google:
            client-id: ${GOOGLE_CLIENT_ID}
            client-secret: ${GOOGLE_CLIENT_SECRET}

jwt:
  secret: ${JWT_SECRET:your-secret-key-change-in-production}
  expiration: ${JWT_EXPIRATION:86400000} # 24 hours
  refresh-expiration: ${JWT_REFRESH_EXPIRATION:604800000} # 7 days

logging:
  level:
    root: INFO
    com.company.project: ${LOG_LEVEL:DEBUG}
    org.hibernate.SQL: DEBUG
    org.hibernate.type.descriptor.sql.BasicBinder: TRACE

springdoc:
  api-docs:
    path: /api-docs
  swagger-ui:
    path: /swagger-ui.html
    tags-sorter: alpha
    operations-sorter: alpha
```

### application-dev.yml
```yaml
spring:
  jpa:
    hibernate:
      ddl-auto: update
    show-sql: true
  
  h2:
    console:
      enabled: true

logging:
  level:
    com.company.project: DEBUG
```

### application-prod.yml
```yaml
spring:
  jpa:
    hibernate:
      ddl-auto: validate
    show-sql: false

logging:
  level:
    com.company.project: INFO
```

---

## 데이터베이스 컨벤션

### 네이밍 규칙
- **테이블명**: 복수형 snake_case (`users`, `blog_posts`)
- **컬럼명**: snake_case (`created_at`, `user_id`)
- **인덱스명**: `idx_테이블명_컬럼명` (`idx_users_email`)
- **외래키명**: `fk_테이블명_참조테이블명` (`fk_posts_users`)
- **시퀀스명**: `seq_테이블명` (`seq_users`)

### JPA Auditing
```java
@MappedSuperclass
@EntityListeners(AuditingEntityListener.class)
@Getter
public abstract class BaseEntity {
    
    @CreatedDate
    @Column(nullable = false, updatable = false)
    private LocalDateTime createdAt;
    
    @LastModifiedDate
    @Column(nullable = false)
    private LocalDateTime updatedAt;
    
    @CreatedBy
    @Column(updatable = false)
    private String createdBy;
    
    @LastModifiedBy
    private String updatedBy;
}
```

---

## 테스트 전략

### 디렉토리 구조
```
src/test/java/
└── com/company/project/
    ├── domain/
    │   └── user/
    │       ├── controller/
    │       │   └── UserControllerTest.java
    │       ├── service/
    │       │   └── UserServiceTest.java
    │       └── repository/
    │           └── UserRepositoryTest.java
    └── integration/
        └── UserIntegrationTest.java
```

### 단위 테스트 (JUnit 5 + Mockito)
```java
@ExtendWith(MockitoExtension.class)
@DisplayName("UserService 테스트")
class UserServiceTest {
    
    @Mock
    private UserRepository userRepository;
    
    @Mock
    private UserMapper userMapper;
    
    @Mock
    private PasswordEncoder passwordEncoder;
    
    @InjectMocks
    private UserServiceImpl userService;
    
    @Test
    @DisplayName("사용자 조회 성공")
    void findById_Success() {
        // given
        Long userId = 1L;
        User user = User.builder()
                .email("test@example.com")
                .name("Test User")
                .password("encoded")
                .role(UserRole.USER)
                .build();
        
        UserResponse expected = UserResponse.builder()
                .id(userId)
                .email(user.getEmail())
                .name(user.getName())
                .build();
        
        when(userRepository.findById(userId)).thenReturn(Optional.of(user));
        when(userMapper.toResponse(user)).thenReturn(expected);
        
        // when
        UserResponse result = userService.findById(userId);
        
        // then
        assertThat(result).isNotNull();
        assertThat(result.getEmail()).isEqualTo("test@example.com");
        
        verify(userRepository, times(1)).findById(userId);
        verify(userMapper, times(1)).toResponse(user);
    }
    
    @Test
    @DisplayName("사용자 조회 실패 - 존재하지 않는 사용자")
    void findById_NotFound() {
        // given
        Long userId = 999L;
        when(userRepository.findById(userId)).thenReturn(Optional.empty());
        
        // when & then
        assertThatThrownBy(() -> userService.findById(userId))
                .isInstanceOf(BusinessException.class)
                .hasMessageContaining("사용자를 찾을 수 없습니다");
    }
}
```

### Repository 테스트 (TestContainers)
```java
@DataJpaTest
@AutoConfigureTestDatabase(replace = AutoConfigureTestDatabase.Replace.NONE)
@Testcontainers
@DisplayName("UserRepository 테스트")
class UserRepositoryTest {
    
    @Container
    static PostgreSQLContainer<?> postgres = new PostgreSQLContainer<>("postgres:16")
            .withDatabaseName("testdb")
            .withUsername("test")
            .withPassword("test");
    
    @Autowired
    private UserRepository userRepository;
    
    @Test
    @DisplayName("이메일로 사용자 조회")
    void findByEmail() {
        // given
        User user = User.builder()
                .email("test@example.com")
                .name("Test User")
                .password("password")
                .role(UserRole.USER)
                .build();
        userRepository.save(user);
        
        // when
        Optional<User> found = userRepository.findByEmail("test@example.com");
        
        // then
        assertThat(found).isPresent();
        assertThat(found.get().getName()).isEqualTo("Test User");
    }
}
```

### 통합 테스트
```java
@SpringBootTest
@AutoConfigureMockMvc
@Transactional
@DisplayName("User API 통합 테스트")
class UserIntegrationTest {
    
    @Autowired
    private MockMvc mockMvc;
    
    @Autowired
    private ObjectMapper objectMapper;
    
    @Test
    @DisplayName("사용자 생성 API")
    void createUser() throws Exception {
        // given
        UserCreateRequest request = new UserCreateRequest(
                "test@example.com",
                "Test User",
                "Password123!@#"
        );
        
        // when & then
        mockMvc.perform(post("/api/v1/users")
                        .contentType(MediaType.APPLICATION_JSON)
                        .content(objectMapper.writeValueAsString(request)))
                .andExpect(status().isCreated())
                .andExpect(jsonPath("$.success").value(true))
                .andExpect(jsonPath("$.data.email").value("test@example.com"))
                .andExpect(jsonPath("$.data.name").value("Test User"));
    }
}
```

---

## Git 컨벤션

### 브랜치 전략 (Git Flow)
- `main`: 프로덕션 배포 브랜치
- `develop`: 개발 통합 브랜치
- `feature/*`: 기능 개발 (예: `feature/user-login`)
- `bugfix/*`: 버그 수정 (예: `bugfix/login-error`)
- `hotfix/*`: 긴급 수정 (예: `hotfix/security-patch`)
- `release/*`: 배포 준비 (예: `release/v1.0.0`)

### 커밋 메시지 규칙
```
<type>(<scope>): <subject>

<body>

<footer>
```

#### 타입 (Type)
- `feat`: 새로운 기능 추가
- `fix`: 버그 수정
- `docs`: 문서 수정
- `style`: 코드 포맷팅 (기능 변경 없음)
- `refactor`: 코드 리팩토링
- `test`: 테스트 코드 추가/수정
- `chore`: 빌드, 설정 변경

#### 예시
```
feat(user): 사용자 회원가입 기능 구현

- UserController, UserService 추가
- 이메일 중복 검증 로직 구현
- 비밀번호 암호화 적용

Resolves: #123
```

---

## API 설계 원칙

### RESTful 규칙
```
GET    /api/v1/users          # 목록 조회
GET    /api/v1/users/{id}     # 단일 조회
POST   /api/v1/users          # 생성
PATCH  /api/v1/users/{id}     # 부분 수정
PUT    /api/v1/users/{id}     # 전체 수정
DELETE /api/v1/users/{id}     # 삭제

# 연관 리소스
GET    /api/v1/users/{id}/posts           # 사용자의 게시글 목록
POST   /api/v1/posts/{id}/comments        # 게시글에 댓글 작성
```

### 쿼리 파라미터
```
?page=0               # 페이지 번호 (0부터 시작)
?size=20              # 페이지 크기
?sort=createdAt,desc  # 정렬 (필드,방향)
?filter=role:ADMIN    # 필터링
?search=keyword       # 검색
```

### HTTP 상태 코드
- `200 OK`: 성공
- `201 Created`: 생성 성공
- `204 No Content`: 성공 (응답 본문 없음)
- `400 Bad Request`: 잘못된 요청
- `401 Unauthorized`: 인증 실패
- `403 Forbidden`: 권한 없음
- `404 Not Found`: 리소스 없음
- `409 Conflict`: 충돌 (중복 등)
- `422 Unprocessable Entity`: 유효성 검증 실패
- `500 Internal Server Error`: 서버 오류

---

## 보안 가이드라인

### 필수 적용 사항
1. **비밀번호 암호화**: BCryptPasswordEncoder 사용
2. **JWT 보안**:
   - 짧은 만료 시간 (액세스: 15분, 리프레시: 7일)
   - HttpOnly 쿠키 또는 Authorization 헤더
   - 서명 검증 필수
3. **입력 검증**: 
   - `@Valid` + `@NotNull`, `@NotBlank`, `@Email` 등
   - DTO에서 검증 로직 정의
4. **SQL 인젝션 방지**: 
   - JPA 사용 (JPQL, Named Parameter)
   - Native Query 사용 시 PreparedStatement
5. **CORS 설정**: 허용된 출처만 명시
6. **CSRF 방지**: Spring Security CSRF 토큰
7. **XSS 방지**: 
   - 응답 시 HTML 이스케이프
   - Content-Security-Policy 헤더
8. **민감 정보 로깅 금지**: 비밀번호, 토큰 등
9. **Rate Limiting**: Bucket4j 또는 Redis 활용

### SecurityConfig 예시
```java
@Configuration
@EnableWebSecurity
@EnableMethodSecurity
@RequiredArgsConstructor
public class SecurityConfig {
    
    private final JwtAuthenticationFilter jwtAuthenticationFilter;
    
    @Bean
    public SecurityFilterChain filterChain(HttpSecurity http) throws Exception {
        http
                .csrf(csrf -> csrf.disable())
                .cors(cors -> cors.configurationSource(corsConfigurationSource()))
                .sessionManagement(session -> 
                        session.sessionCreationPolicy(SessionCreationPolicy.STATELESS))
                .authorizeHttpRequests(auth -> auth
                        .requestMatchers("/api/v1/auth/**", "/api-docs/**", "/swagger-ui/**").permitAll()
                        .requestMatchers("/api/v1/admin/**").hasRole("ADMIN")
                        .anyRequest().authenticated()
                )
                .addFilterBefore(jwtAuthenticationFilter, UsernamePasswordAuthenticationFilter.class)
                .exceptionHandling(ex -> ex
                        .authenticationEntryPoint((request, response, authException) -> {
                            response.setStatus(HttpServletResponse.SC_UNAUTHORIZED);
                            response.setContentType("application/json;charset=UTF-8");
                            response.getWriter().write(
                                    "{\"success\":false,\"errorCode\":\"A001\",\"message\":\"인증이 필요합니다.\"}"
                            );
                        })
                );
        
        return http.build();
    }
    
    @Bean
    public PasswordEncoder passwordEncoder() {
        return new BCryptPasswordEncoder();
    }
    
    @Bean
    public CorsConfigurationSource corsConfigurationSource() {
        CorsConfiguration config = new CorsConfiguration();
        config.setAllowedOrigins(List.of("http://localhost:3000", "https://example.com"));
        config.setAllowedMethods(List.of("GET", "POST", "PUT", "PATCH", "DELETE", "OPTIONS"));
        config.setAllowedHeaders(List.of("*"));
        config.setAllowCredentials(true);
        
        UrlBasedCorsConfigurationSource source = new UrlBasedCorsConfigurationSource();
        source.registerCorsConfiguration("/api/**", config);
        return source;
    }
}
```

---

## 성능 최적화 가이드

### 데이터베이스
- **인덱스 추가**: 자주 조회되는 컬럼
- **N+1 문제 해결**: 
  - `@EntityGraph` 또는 `fetch join` 사용
  - `default_batch_fetch_size` 설정
- **페이징 필수**: 대량 데이터 조회 시
- **쿼리 최적화**: 
  - Select 절 최소화 (필요한 컬럼만)
  - Projection 활용

### 캐싱
```java
@Configuration
@EnableCaching
public class CacheConfig {
    
    @Bean
    public CacheManager cacheManager(RedisConnectionFactory connectionFactory) {
        RedisCacheConfiguration config = RedisCacheConfiguration.defaultCacheConfig()
                .entryTtl(Duration.ofHours(1))
                .serializeKeysWith(
                        RedisSerializationContext.SerializationPair.fromSerializer(
                                new StringRedisSerializer()
                        )
                )
                .serializeValuesWith(
                        RedisSerializationContext.SerializationPair.fromSerializer(
                                new GenericJackson2JsonRedisSerializer()
                        )
                );
        
        return RedisCacheManager.builder(connectionFactory)
                .cacheDefaults(config)
                .build();
    }
}

// Service에서 사용
@Cacheable(value = "users", key = "#id")
public UserResponse findById(Long id) {
    // ...
}

@CacheEvict(value = "users", key = "#id")
public void delete(Long id) {
    // ...
}
```

### 로깅
```java
@Slf4j
public class UserService {
    
    public UserResponse findById(Long id) {
        log.debug("사용자 조회 시작: id={}", id);
        
        // 비즈니스 로직
        
        log.info("사용자 조회 완료: id={}", id);
        return response;
    }
}
```

---

## AI에게 코드 요청 시 참조 방법

이 문서를 AI에게 제공할 때:

```
다음 INIT.md를 참고해서 코드를 작성해줘:

[INIT.md 내용 또는 파일 업로드]

요청사항:
- UserController에 프로필 조회 엔드포인트 추가
- 위 컨벤션을 정확히 따라줘
- Lombok, MapStruct 사용
- 예외 처리와 응답 형식도 문서대로 작성해줘
```

---

## 업데이트 이력
- 2024-01-01: 초기 작성
- 2024-01-15: Spring Security 6.x 반영
- 2024-02-01: TestContainers 설정 추가
