# C# Code Style Guide

## File Header

All C# files must include the standard header template. See `.clinerules/templates/header-csharp.cs`.

## Naming Conventions

### General Rules
| Element | Convention | Example |
|---------|------------|---------|
| Namespace | PascalCase | `MyCompany.MyProduct` |
| Class | PascalCase | `UserService` |
| Interface | IPascalCase | `IUserRepository` |
| Method | PascalCase | `GetUserById` |
| Property | PascalCase | `FirstName` |
| Field (private) | _camelCase | `_userRepository` |
| Field (public) | PascalCase | `MaxRetryCount` |
| Parameter | camelCase | `userId` |
| Local variable | camelCase | `currentUser` |
| Constant | PascalCase | `DefaultTimeout` |
| Enum | PascalCase | `UserStatus` |
| Enum value | PascalCase | `Active` |

### Variables and Fields
```csharp
// Private fields - underscore prefix
private readonly IUserRepository _userRepository;
private readonly ILogger<UserService> _logger;
private int _retryCount;

// Public constants
public const int MaxRetryCount = 3;
public static readonly TimeSpan DefaultTimeout = TimeSpan.FromSeconds(30);

// Local variables
var currentUser = await GetUserAsync(userId);
var isActive = user.Status == UserStatus.Active;
```

### Methods and Properties
```csharp
// Methods - PascalCase, verb phrases
public async Task<User> GetUserByIdAsync(string userId)
public void ProcessOrder(Order order)
public bool ValidateInput(string input)

// Properties - PascalCase, noun phrases
public string FirstName { get; set; }
public bool IsActive { get; private set; }
public int Count => _items.Count;
```

### Interfaces
- Always prefix with `I`

```csharp
public interface IUserRepository
{
    Task<User?> FindByIdAsync(string id);
    Task SaveAsync(User user);
}

public interface INotificationService
{
    Task SendAsync(Notification notification);
}
```

### Async Methods
- Suffix async methods with `Async`

```csharp
// Good
public async Task<User> GetUserAsync(string id)
public async Task SendNotificationAsync(Notification notification)

// Bad
public async Task<User> GetUser(string id)
```

## Formatting

### Indentation and Braces
- Use 4 spaces for indentation
- Opening brace on new line (Allman style)

```csharp
// Good - Allman style
public class UserService
{
    public async Task<User?> GetUserAsync(string id)
    {
        if (string.IsNullOrEmpty(id))
        {
            throw new ArgumentException("Id cannot be empty", nameof(id));
        }

        return await _repository.FindByIdAsync(id);
    }
}

// Bad - K&R style (not C# convention)
public class UserService {
    public async Task<User?> GetUserAsync(string id) {
        // ...
    }
}
```

### Line Length
- Maximum 120 characters per line
- Break long lines at logical points

```csharp
// Good - break at logical points
public async Task<Result<User>> CreateUserAsync(
    string firstName,
    string lastName,
    string email,
    CancellationToken cancellationToken = default)
{
    // ...
}
```

### Spacing
```csharp
// Operators
var result = a + b;
var isValid = count > 0 && count < 100;

// Method calls - no space before parentheses
GetUser(userId);
await ProcessAsync();

// Control statements - space before parentheses
if (condition)
for (var i = 0; i < count; i++)
while (isRunning)
```

## Classes and Structures

### Class Organization
Order members as follows:
1. Constants
2. Static fields
3. Instance fields
4. Constructors
5. Properties
6. Public methods
7. Private methods
8. Nested types

```csharp
public class UserService : IUserService
{
    // 1. Constants
    private const int MaxRetries = 3;

    // 2. Static fields
    private static readonly TimeSpan CacheDuration = TimeSpan.FromMinutes(5);

    // 3. Instance fields
    private readonly IUserRepository _repository;
    private readonly ILogger<UserService> _logger;

    // 4. Constructors
    public UserService(IUserRepository repository, ILogger<UserService> logger)
    {
        _repository = repository ?? throw new ArgumentNullException(nameof(repository));
        _logger = logger ?? throw new ArgumentNullException(nameof(logger));
    }

    // 5. Properties
    public int CacheSize { get; private set; }

    // 6. Public methods
    public async Task<User?> GetUserAsync(string id)
    {
        _logger.LogDebug("Getting user {UserId}", id);
        return await _repository.FindByIdAsync(id);
    }

    // 7. Private methods
    private void ValidateId(string id)
    {
        if (string.IsNullOrEmpty(id))
        {
            throw new ArgumentException("Id cannot be empty", nameof(id));
        }
    }
}
```

### Records
- Use records for immutable data transfer objects

```csharp
// Simple record
public record User(string Id, string Name, string Email);

// Record with additional members
public record UserDto
{
    public required string Id { get; init; }
    public required string Name { get; init; }
    public string? Email { get; init; }

    public string DisplayName => $"{Name} ({Id})";
}
```

### Structs
- Use structs for small, immutable value types
- Prefer `readonly struct`

```csharp
public readonly struct Point
{
    public double X { get; }
    public double Y { get; }

    public Point(double x, double y)
    {
        X = x;
        Y = y;
    }

    public double DistanceTo(Point other)
    {
        var dx = X - other.X;
        var dy = Y - other.Y;
        return Math.Sqrt(dx * dx + dy * dy);
    }
}
```

## Null Handling

### Nullable Reference Types
- Enable nullable reference types
- Use `?` for nullable types
- Use `!` sparingly and with comment

```csharp
#nullable enable

public class UserService
{
    // Non-nullable - must be initialized
    private readonly IUserRepository _repository;

    // Nullable return type
    public async Task<User?> FindUserAsync(string id)
    {
        return await _repository.FindByIdAsync(id);
    }

    // Handle nullability
    public async Task<string> GetUserNameAsync(string id)
    {
        var user = await FindUserAsync(id);
        return user?.Name ?? "Unknown";
    }
}
```

### Null Checks
```csharp
// Guard clauses
public void ProcessUser(User user)
{
    ArgumentNullException.ThrowIfNull(user);
    // or
    _ = user ?? throw new ArgumentNullException(nameof(user));
}

// Null conditional operators
var name = user?.Profile?.DisplayName ?? "Anonymous";
user?.Notify();

// Pattern matching
if (user is not null)
{
    ProcessUser(user);
}

if (result is { Success: true, Data: var data })
{
    ProcessData(data);
}
```

## LINQ

### Query vs Method Syntax
- Prefer method syntax for simple queries
- Use query syntax for complex queries with multiple joins

```csharp
// Method syntax - preferred for simple queries
var activeUsers = users
    .Where(u => u.IsActive)
    .OrderBy(u => u.Name)
    .Select(u => new UserDto(u.Id, u.Name));

// Query syntax - for complex joins
var orderDetails =
    from order in orders
    join customer in customers on order.CustomerId equals customer.Id
    join product in products on order.ProductId equals product.Id
    where order.Date >= startDate
    select new
    {
        OrderId = order.Id,
        CustomerName = customer.Name,
        ProductName = product.Name,
        order.Quantity
    };
```

### Deferred Execution
- Be aware of deferred execution
- Use `.ToList()` or `.ToArray()` when immediate execution needed

```csharp
// Deferred - query not executed yet
var query = users.Where(u => u.IsActive);

// Immediate - executed now
var activeUsers = users.Where(u => u.IsActive).ToList();
```

## Async/Await

### Async Best Practices
```csharp
// Always use async suffix
public async Task<User> GetUserAsync(string id)

// Use ConfigureAwait(false) in libraries
public async Task<User> GetUserAsync(string id)
{
    return await _repository.FindByIdAsync(id).ConfigureAwait(false);
}

// Support cancellation
public async Task<User> GetUserAsync(string id, CancellationToken cancellationToken = default)
{
    return await _repository.FindByIdAsync(id, cancellationToken);
}

// Avoid async void except for event handlers
// Bad
public async void ProcessData() { }

// Good
public async Task ProcessDataAsync() { }
```

### Exception Handling
```csharp
public async Task<Result<User>> GetUserSafeAsync(string id)
{
    try
    {
        var user = await _repository.FindByIdAsync(id);
        return user is not null
            ? Result<User>.Success(user)
            : Result<User>.Failure("User not found");
    }
    catch (Exception ex) when (ex is not OperationCanceledException)
    {
        _logger.LogError(ex, "Error getting user {UserId}", id);
        return Result<User>.Failure(ex.Message);
    }
}
```

## Dependency Injection

### Constructor Injection
```csharp
public class UserService : IUserService
{
    private readonly IUserRepository _repository;
    private readonly ILogger<UserService> _logger;
    private readonly UserServiceOptions _options;

    public UserService(
        IUserRepository repository,
        ILogger<UserService> logger,
        IOptions<UserServiceOptions> options)
    {
        _repository = repository ?? throw new ArgumentNullException(nameof(repository));
        _logger = logger ?? throw new ArgumentNullException(nameof(logger));
        _options = options?.Value ?? throw new ArgumentNullException(nameof(options));
    }
}
```

### Registration
```csharp
// Program.cs or Startup.cs
services.AddScoped<IUserRepository, UserRepository>();
services.AddScoped<IUserService, UserService>();
services.Configure<UserServiceOptions>(configuration.GetSection("UserService"));
```

## Documentation

### XML Documentation
```csharp
/// <summary>
/// Retrieves a user by their unique identifier.
/// </summary>
/// <param name="id">The user's unique identifier.</param>
/// <param name="cancellationToken">Cancellation token for the operation.</param>
/// <returns>The user if found; otherwise, null.</returns>
/// <exception cref="ArgumentException">Thrown when id is null or empty.</exception>
/// <example>
/// <code>
/// var user = await userService.GetUserAsync("user-123");
/// if (user is not null)
/// {
///     Console.WriteLine(user.Name);
/// }
/// </code>
/// </example>
public async Task<User?> GetUserAsync(string id, CancellationToken cancellationToken = default)
{
    // ...
}
```

## Testing

### Test Naming
- Use descriptive names: `MethodName_Scenario_ExpectedBehavior`

```csharp
[Fact]
public async Task GetUserAsync_WithValidId_ReturnsUser()
{
    // Arrange
    var userId = "user-123";
    var expectedUser = new User(userId, "John");
    _repositoryMock.Setup(r => r.FindByIdAsync(userId))
        .ReturnsAsync(expectedUser);

    // Act
    var result = await _sut.GetUserAsync(userId);

    // Assert
    Assert.NotNull(result);
    Assert.Equal(expectedUser.Id, result.Id);
}

[Fact]
public async Task GetUserAsync_WithInvalidId_ThrowsArgumentException()
{
    // Arrange & Act & Assert
    await Assert.ThrowsAsync<ArgumentException>(
        () => _sut.GetUserAsync(string.Empty));
}
```

### Test Organization
```csharp
public class UserServiceTests
{
    private readonly Mock<IUserRepository> _repositoryMock;
    private readonly Mock<ILogger<UserService>> _loggerMock;
    private readonly UserService _sut; // System Under Test

    public UserServiceTests()
    {
        _repositoryMock = new Mock<IUserRepository>();
        _loggerMock = new Mock<ILogger<UserService>>();
        _sut = new UserService(_repositoryMock.Object, _loggerMock.Object);
    }
}
```
