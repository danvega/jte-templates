# Spring Boot & JTE Templates

Welcome to the Spring Boot & JTE Templates project! This repository demonstrates how to integrate Java Template Engine (JTE) with Spring Boot, providing a powerful and efficient way to render dynamic web pages in your Java applications.

## Introduction

JTE is a modern and lightweight templating engine for Java that offers excellent performance and type-safe templates. By combining it with Spring Boot, we create a robust foundation for building web applications with clean separation of concerns and improved developer productivity.

## Project Requirements

- Java 23
- Maven 3.6+
- Spring Boot 3.3.4
- JTE 3.1.12

## Dependencies

This project relies on the following key dependencies:

- `spring-boot-starter-web`: For building web applications with Spring MVC
- `jte`: The core JTE library

## Getting Started

To get started with this project, ensure you have Java 23 and Maven installed on your system. Then, follow these steps:

1. Navigate to the project root directory
2. Build the project using Maven:

```bash
mvn clean install
```

3. Run the application:

```bash
mvn spring-boot:run
```

The application will start, and you can access it at `http://localhost:8080`.

## How to Run the Application

After building the project, you can run it using the following command:

```bash
java -jar target/jte-templates-0.0.1-SNAPSHOT.jar
```

This will start the Spring Boot application, and you can access the web pages through your browser.

## Project Structure

The project follows a standard Spring Boot structure with additional JTE-specific configurations:

- `src/main/java`: Java source files
- `src/main/jte`: JTE template files
- `src/test`: Test files

## Relevant Code Examples

### Controller

Here's an example of how a controller is set up to work with JTE templates:

```java
@Controller
public class TemplateController {

    @GetMapping("/")
    public String home(Model model) {
        model.addAttribute("username", "John Doe");
        return "pages/home";
    }

    @GetMapping("/team")
    public String team(Model model) {
        List<String> teamMembers = Arrays.asList("Alice", "Bob", "Charlie", "David");
        model.addAttribute("teamMembers", teamMembers);
        return "pages/team";
    }
}
```

In this example, the controller methods return the name of the JTE template to render, and add attributes to the model which can be accessed in the templates.

### JTE Template

JTE templates are located in the `src/main/jte/pages` directory. Here's a simple example of what a JTE template might look like:

```html
@param String username

@template.layout.main(content = @`
<div class="bg-white shadow rounded-lg p-6">
    <h1 class="text-2xl font-bold mb-4">Welcome, ${username}!</h1>
    <p class="text-gray-600">This is your dashboard. Here you can view your recent activity and manage your account.</p>
</div>
`)
```

This template takes a `username` parameter and renders it within the HTML. This template declares that it is using the `main` layout.


## JTE Content and Layouts

### Understanding Content in JTE

In JTE, `gg.jte.Content` is a special parameter type used to pass template code to other templates, similar to lambdas in Java. This feature is particularly useful for sharing structures between different templates and creating reusable layouts.

### Main Layout

The main layout for this project is located at `/src/main/jte/layout/main.jte`. This layout serves as the base structure for other pages in the application. Here's an example of how a main layout might look:

```jte
@import gg.jte.Content

@param String title
@param Content content

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>${title}</title>
</head>
<body>
    <header>
        <h1>${title}</h1>
    </header>
    
    <main>
        ${content}
    </main>
    
    <footer>
        <p>&copy; 2024 Spring Boot & JTE Templates</p>
    </footer>
</body>
</html>
```

### Using Content Blocks

To use content blocks within JTE templates, you can use the shorthand syntax of `@` followed by two backticks. Here's an example of how you might use the main layout in another template:

```jte
@import dev.danvega.jte.TemplateController

@param String username

@template.layout.main(
    title = "Welcome",
    content = @`
        <p>Welcome, ${username}!</p>
        <p>This is a JTE template rendered by Spring Boot.</p>
    `
)
```

This approach allows for clean separation of concerns, making your templates more modular and easier to maintain.


## Conclusion

The Spring Boot & JTE Templates project provides a solid foundation for building web applications with a modern, type-safe templating engine. By leveraging the strengths of both Spring Boot and JTE, you can create robust, efficient, and maintainable web applications.

We encourage you to explore the codebase, experiment with the templates, and build upon this foundation to create your own amazing web applications. If you have any questions or suggestions, please feel free to open an issue or submit a pull request. 

Happy coding!