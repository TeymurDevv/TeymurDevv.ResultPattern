# TeymurDevv.ResultPattern

*A lightweight and elegant Result Pattern implementation for handling success and failure scenarios in C#.*

![NuGet](https://img.shields.io/nuget/v/TeymurDevv.ResultPattern) ![License](https://img.shields.io/badge/license-MIT-green) ![.NET](https://img.shields.io/badge/.NET-9.0-blue)

## 🚀 Introduction

`TeymurDevv.ResultPattern` is a simple yet powerful library that provides a structured way to handle operations that can either **succeed** or **fail**, reducing reliance on exceptions and improving code clarity.

## ✨ Features

- Encapsulates **success** and **failure** outcomes in a single result type.
- Eliminates excessive `if-else` checks.
- Improves readability and maintainability of business logic.
- Avoids using exceptions for expected errors.
- Works seamlessly with **ASP.NET Core**, **CQRS**, and **MediatR**.

## 📦 Installation

Install via NuGet Package Manager:
```sh
Install-Package TeymurDevv.ResultPattern
```

Or via .NET CLI:
```sh
dotnet add package TeymurDevv.ResultPattern
```

## 🛠 Usage

### 1️⃣ Basic Success & Failure Handling

```csharp
using TeymurDevv.ResultPattern;

var successResult = Result<string>.Success("Operation successful");
Console.WriteLine(successResult.Value); // Output: Operation successful

var failureResult = Result<string>.Failure("Something went wrong");
Console.WriteLine(failureResult.Error); // Output: Something went wrong
```

### 2️⃣ Using Result Without a Return Value

```csharp
var operationResult = Result.Success();
if (operationResult.IsSuccess)
{
    Console.WriteLine("Operation succeeded");
}
else
{
    Console.WriteLine($"Error: {operationResult.Error}");
}
```

### 3️⃣ Using Result in a Service Layer

```csharp
public class UserService
{
    public Result<User> GetUserById(int id)
    {
        var user = _userRepository.GetById(id);
        if (user == null)
        {
            return Result<User>.Failure("User not found");
        }
        return Result<User>.Success(user);
    }
}
```

### 4️⃣ Handling Result in an API Controller (ASP.NET Core)

```csharp
[ApiController]
[Route("api/users")]
public class UserController : ControllerBase
{
    private readonly UserService _userService;

    public UserController(UserService userService)
    {
        _userService = userService;
    }

    [HttpGet("{id}")]
    public IActionResult GetUser(int id)
    {
        var result = _userService.GetUserById(id);
        
        if (result.IsFailure)
            return NotFound(new { message = result.Error });

        return Ok(result.Value);
    }
}
```

## 🔥 Why Use TeymurDevv.ResultPattern?

✅ **Explicit error handling** – No more guessing where exceptions might occur.  
✅ **Improves performance** – Avoids costly exceptions for expected failures.  
✅ **Increases maintainability** – Cleaner and more structured error handling.  
✅ **Works with CQRS & MediatR** – Perfect for modern backend architectures.  

## ⚡ Roadmap
- [ ] Add logging integration
- [ ] Extend support for `Result<T>` chaining
- [ ] Improve compatibility with LINQ expressions

## 📜 License

This project is licensed under the **MIT License** - see the [LICENSE](LICENSE) file for details.

## 🤝 Contributing

Contributions are welcome! Feel free to submit **issues**, **feature requests**, or **pull requests** on [GitHub](https://github.com/TeymurDevv/ResultPattern).

## 🌟 Support & Feedback

If you find this package useful, please ⭐ it on [GitHub](https://github.com/TeymurDevv/ResultPattern)! 😊

