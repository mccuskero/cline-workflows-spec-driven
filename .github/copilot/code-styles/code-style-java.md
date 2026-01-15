# Java Code Style Guide

## File Header

All Java files must include the standard header template. See `.clinerules/templates/header-java.java`.

## Naming Conventions

### General Rules
| Element | Convention | Example |
|---------|------------|---------|
| Package | lowercase | `com.company.project` |
| Class | PascalCase | `UserService` |
| Interface | PascalCase | `UserRepository` |
| Method | camelCase | `getUserById` |
| Variable | camelCase | `userName` |
| Constant | UPPER_SNAKE_CASE | `MAX_RETRY_COUNT` |
| Type Parameter | Single uppercase | `T`, `E`, `K`, `V` |
| Enum | PascalCase | `UserStatus` |
| Enum constant | UPPER_SNAKE_CASE | `ACTIVE`, `INACTIVE` |

### Variables and Fields
```java
// Constants
public static final int MAX_RETRY_COUNT = 3;
public static final Duration DEFAULT_TIMEOUT = Duration.ofSeconds(30);

// Instance fields
private final UserRepository userRepository;
private final Logger logger;
private int retryCount;

// Local variables
var currentUser = getUserById(userId);
var isActive = user.getStatus() == UserStatus.ACTIVE;

// Boolean naming
boolean isValid;
boolean hasPermission;
boolean canExecute;
boolean shouldRetry;
```

### Methods
```java
// Methods - camelCase, verb phrases
public User getUserById(String userId)
public void processOrder(Order order)
public boolean validateInput(String input)

// Getters and setters
public String getFirstName()
public void setFirstName(String firstName)
public boolean isActive()  // boolean getter
public void setActive(boolean active)
```

### Packages
```java
// Use lowercase, reverse domain notation
package com.company.project.service;
package com.company.project.repository;
package com.company.project.model;
package com.company.project.util;
```

## Formatting

### Indentation and Braces
- Use 4 spaces for indentation
- Opening brace on same line (K&R style)

```java
// Good - K&R style
public class UserService {

    public User getUserById(String id) {
        if (id == null || id.isEmpty()) {
            throw new IllegalArgumentException("Id cannot be empty");
        }

        return repository.findById(id).orElse(null);
    }
}

// Bad - Allman style (not Java convention)
public class UserService
{
    public User getUserById(String id)
    {
        // ...
    }
}
```

### Line Length
- Maximum 120 characters per line
- Break long lines at logical points

```java
// Good - break at logical points
public CompletableFuture<Result<User>> createUserAsync(
        String firstName,
        String lastName,
        String email,
        UserRole role) {
    // ...
}

// Method chaining
var result = users.stream()
        .filter(User::isActive)
        .map(User::getName)
        .sorted()
        .collect(Collectors.toList());
```

### Blank Lines
```java
public class UserService {

    private static final Logger logger = LoggerFactory.getLogger(UserService.class);

    private final UserRepository repository;
    private final NotificationService notificationService;

    public UserService(UserRepository repository, NotificationService notificationService) {
        this.repository = Objects.requireNonNull(repository);
        this.notificationService = Objects.requireNonNull(notificationService);
    }

    public User getUserById(String id) {
        logger.debug("Getting user: {}", id);
        return repository.findById(id).orElse(null);
    }

    public void deleteUser(String id) {
        logger.debug("Deleting user: {}", id);
        repository.deleteById(id);
    }
}
```

## Classes and Interfaces

### Class Organization
Order members as follows:
1. Static fields (constants first)
2. Instance fields
3. Constructors
4. Static methods
5. Public methods
6. Protected methods
7. Private methods
8. Inner classes/interfaces

```java
public class UserService implements IUserService {

    // 1. Static fields
    private static final Logger logger = LoggerFactory.getLogger(UserService.class);
    private static final int MAX_RETRIES = 3;

    // 2. Instance fields
    private final UserRepository repository;
    private final EventPublisher eventPublisher;

    // 3. Constructors
    public UserService(UserRepository repository, EventPublisher eventPublisher) {
        this.repository = Objects.requireNonNull(repository);
        this.eventPublisher = Objects.requireNonNull(eventPublisher);
    }

    // 4. Static methods
    public static UserService createDefault() {
        return new UserService(new DefaultRepository(), new DefaultPublisher());
    }

    // 5. Public methods
    @Override
    public User getUserById(String id) {
        validateId(id);
        return repository.findById(id).orElse(null);
    }

    public User createUser(CreateUserRequest request) {
        var user = mapToUser(request);
        repository.save(user);
        publishUserCreatedEvent(user);
        return user;
    }

    // 6. Protected methods
    protected void publishUserCreatedEvent(User user) {
        eventPublisher.publish(new UserCreatedEvent(user));
    }

    // 7. Private methods
    private void validateId(String id) {
        if (id == null || id.isBlank()) {
            throw new IllegalArgumentException("Id cannot be empty");
        }
    }

    private User mapToUser(CreateUserRequest request) {
        return new User(
            UUID.randomUUID().toString(),
            request.firstName(),
            request.lastName(),
            request.email()
        );
    }
}
```

### Records (Java 16+)
- Use records for immutable data classes

```java
// Simple record
public record User(String id, String name, String email) {}

// Record with validation
public record UserId(String value) {
    public UserId {
        Objects.requireNonNull(value, "User ID cannot be null");
        if (value.isBlank()) {
            throw new IllegalArgumentException("User ID cannot be blank");
        }
    }
}

// Record with additional methods
public record Point(double x, double y) {
    public double distanceTo(Point other) {
        var dx = x - other.x;
        var dy = y - other.y;
        return Math.sqrt(dx * dx + dy * dy);
    }
}
```

### Interfaces
```java
// Functional interface
@FunctionalInterface
public interface UserValidator {
    ValidationResult validate(User user);
}

// Service interface
public interface UserRepository {
    Optional<User> findById(String id);
    List<User> findAll();
    void save(User user);
    void deleteById(String id);
}
```

## Null Handling

### Optional
- Use `Optional` for return values that may be absent
- Never use `Optional` for fields or parameters

```java
// Good - Optional for return type
public Optional<User> findById(String id) {
    return Optional.ofNullable(userMap.get(id));
}

// Using Optional
public String getUserName(String id) {
    return findById(id)
            .map(User::getName)
            .orElse("Unknown");
}

public User getRequiredUser(String id) {
    return findById(id)
            .orElseThrow(() -> new UserNotFoundException(id));
}

// Bad - Optional as parameter
public void processUser(Optional<User> user) { } // Don't do this
```

### Null Checks
```java
// Constructor validation
public UserService(UserRepository repository, Logger logger) {
    this.repository = Objects.requireNonNull(repository, "repository must not be null");
    this.logger = Objects.requireNonNull(logger, "logger must not be null");
}

// Method parameter validation
public void processUser(User user) {
    Objects.requireNonNull(user, "user must not be null");
    // process...
}

// Null-safe operations
var name = user != null ? user.getName() : "Unknown";

// With Optional
var name = Optional.ofNullable(user)
        .map(User::getName)
        .orElse("Unknown");
```

## Streams and Lambdas

### Stream Operations
```java
// Simple transformations
var names = users.stream()
        .map(User::getName)
        .collect(Collectors.toList());

// Filtering and mapping
var activeUserEmails = users.stream()
        .filter(User::isActive)
        .map(User::getEmail)
        .filter(Objects::nonNull)
        .distinct()
        .sorted()
        .collect(Collectors.toList());

// Grouping
var usersByStatus = users.stream()
        .collect(Collectors.groupingBy(User::getStatus));

// Reducing
var totalAge = users.stream()
        .mapToInt(User::getAge)
        .sum();
```

### Lambda Best Practices
```java
// Prefer method references when possible
users.forEach(System.out::println);
users.stream().map(User::getName);
users.stream().filter(Objects::nonNull);

// Use lambdas for simple operations
users.stream().filter(u -> u.getAge() > 18);

// Extract complex lambdas to methods
users.stream()
        .filter(this::isEligibleForPromotion)
        .forEach(this::sendPromotionEmail);

private boolean isEligibleForPromotion(User user) {
    return user.isActive()
            && user.getAge() >= 21
            && user.getAccountAge().toDays() > 365;
}
```

## Exception Handling

### Checked vs Unchecked Exceptions
```java
// Custom unchecked exception (preferred for business logic)
public class UserNotFoundException extends RuntimeException {
    private final String userId;

    public UserNotFoundException(String userId) {
        super("User not found: " + userId);
        this.userId = userId;
    }

    public String getUserId() {
        return userId;
    }
}

// Using exceptions
public User getRequiredUser(String id) {
    return repository.findById(id)
            .orElseThrow(() -> new UserNotFoundException(id));
}
```

### Try-with-Resources
```java
// Always use try-with-resources for AutoCloseable
public String readFile(Path path) throws IOException {
    try (var reader = Files.newBufferedReader(path)) {
        return reader.lines().collect(Collectors.joining("\n"));
    }
}

public void processData(Connection connection) throws SQLException {
    try (var statement = connection.prepareStatement(SQL);
         var resultSet = statement.executeQuery()) {
        while (resultSet.next()) {
            processRow(resultSet);
        }
    }
}
```

### Exception Best Practices
```java
// Don't swallow exceptions
try {
    riskyOperation();
} catch (Exception e) {
    logger.error("Operation failed", e);
    throw e; // or handle appropriately
}

// Catch specific exceptions
try {
    parseData(input);
} catch (JsonParseException e) {
    throw new InvalidInputException("Invalid JSON format", e);
} catch (IOException e) {
    throw new DataAccessException("Failed to read input", e);
}
```

## Dependency Injection

### Constructor Injection
```java
@Service
public class UserService {

    private final UserRepository repository;
    private final EventPublisher eventPublisher;
    private final UserValidator validator;

    @Autowired // Optional in Spring if single constructor
    public UserService(
            UserRepository repository,
            EventPublisher eventPublisher,
            UserValidator validator) {
        this.repository = repository;
        this.eventPublisher = eventPublisher;
        this.validator = validator;
    }
}
```

### Avoid Field Injection
```java
// Bad - field injection
@Service
public class UserService {
    @Autowired
    private UserRepository repository; // Avoid this
}

// Good - constructor injection
@Service
public class UserService {
    private final UserRepository repository;

    public UserService(UserRepository repository) {
        this.repository = repository;
    }
}
```

## Documentation

### Javadoc
```java
/**
 * Service for managing user operations.
 *
 * <p>This service provides CRUD operations for users and handles
 * associated business logic such as validation and event publishing.
 *
 * @author John Doe
 * @since 1.0.0
 * @see UserRepository
 * @see User
 */
public class UserService {

    /**
     * Retrieves a user by their unique identifier.
     *
     * @param id the user's unique identifier, must not be {@code null} or blank
     * @return an {@link Optional} containing the user if found, or empty if not found
     * @throws IllegalArgumentException if the id is null or blank
     *
     * @example
     * <pre>{@code
     * Optional<User> user = userService.findById("user-123");
     * user.ifPresent(u -> System.out.println(u.getName()));
     * }</pre>
     */
    public Optional<User> findById(String id) {
        // ...
    }
}
```

## Testing

### Test Naming
- Use descriptive method names
- Pattern: `methodName_scenario_expectedBehavior`

```java
class UserServiceTest {

    @Mock
    private UserRepository repository;

    @InjectMocks
    private UserService userService;

    @BeforeEach
    void setUp() {
        MockitoAnnotations.openMocks(this);
    }

    @Test
    void getUserById_withValidId_returnsUser() {
        // Arrange
        var userId = "user-123";
        var expectedUser = new User(userId, "John", "john@example.com");
        when(repository.findById(userId)).thenReturn(Optional.of(expectedUser));

        // Act
        var result = userService.getUserById(userId);

        // Assert
        assertNotNull(result);
        assertEquals(expectedUser.getId(), result.getId());
        verify(repository).findById(userId);
    }

    @Test
    void getUserById_withNullId_throwsIllegalArgumentException() {
        // Act & Assert
        assertThrows(IllegalArgumentException.class,
                () -> userService.getUserById(null));

        verifyNoInteractions(repository);
    }

    @Test
    void getUserById_withNonExistentId_returnsNull() {
        // Arrange
        when(repository.findById(anyString())).thenReturn(Optional.empty());

        // Act
        var result = userService.getUserById("non-existent");

        // Assert
        assertNull(result);
    }
}
```

### Test Organization
```java
@ExtendWith(MockitoExtension.class)
class UserServiceTest {

    @Mock
    private UserRepository repository;

    @Mock
    private EventPublisher eventPublisher;

    private UserService sut; // System Under Test

    @BeforeEach
    void setUp() {
        sut = new UserService(repository, eventPublisher);
    }

    @Nested
    class GetUserById {

        @Test
        void returnsUser_whenFound() { }

        @Test
        void returnsNull_whenNotFound() { }

        @Test
        void throwsException_whenIdIsNull() { }
    }

    @Nested
    class CreateUser {

        @Test
        void savesUser_withValidRequest() { }

        @Test
        void publishesEvent_afterSave() { }
    }
}
```
