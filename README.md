# Kotlin Cybersecurity Examples

This repository contains examples demonstrating how to enhance the security of your Kotlin applications. The examples cover various aspects of cybersecurity, such as null safety, input validation, immutable data classes, exception handling, and access control.

## Table of Contents

- [Overview](#overview)
- [Examples](#examples)
  - [Null Safety](#null-safety)
  - [Input Validation](#input-validation)
  - [Immutable Data Classes](#immutable-data-classes)
  - [Exception Handling](#exception-handling)
  - [Access Control](#access-control)
- [Usage](#usage)
- [Contributing](#contributing)
- [License](#license)

## Overview

In this repository, you'll find practical examples that showcase how to implement various cybersecurity best practices using Kotlin. These examples can be executed directly in Kotlin Playground, allowing you to experiment and learn how to write more secure code.

## Examples

### Null Safety

Kotlin's null safety feature helps you avoid `NullPointerException` (NPE) by handling nullable types safely.

### Input Validation

Always validate and sanitize user input to prevent injection attacks (SQL, XSS, etc.). Kotlin makes this task easier with extension functions.

### Immutable Data Classes

Immutability helps prevent unexpected data modifications, improving the security and stability of your application.

### Exception Handling

Proper exception handling is crucial for maintaining the security and stability of your application. Kotlin provides robust exception handling mechanisms.

### Access Control

Encapsulation and access control are demonstrated to ensure that your code is structured securely, even in a simplified environment like Kotlin Playground.

## Usage

To run the examples, copy and paste the code into [Kotlin Playground](https://pl.kotl.in/LoiTF-418) and execute it. Each function demonstrates a specific cybersecurity practice.


### Full Code Example

```kotlin
// Example 1: Null Safety
fun demonstrateNullSafety() {
    val name: String? = null
    
    // Using safe call to avoid NPE
    println("The length of the name is: ${name?.length ?: "Name not provided"}")
}

// Example 2: Validate and Sanitize User Input
fun String.isValidEmail(): Boolean {
    return this.contains("@") && this.contains(".")
}

fun demonstrateEmailValidation() {
    val email = "user@example.com"
    
    if (email.isValidEmail()) {
        println("The email is valid")
    } else {
        println("The email is not valid")
    }
}

// Example 3: Use Immutable Data Classes
data class User(val name: String, val email: String)

fun demonstrateImmutableDataClasses() {
    val user = User("Juan Pérez", "juan.perez@example.com")
    println("User: $user")
}

// Example 4: Handle Exceptions Safely
fun divide(a: Int, b: Int): Int {
    require(b != 0) { "The divisor cannot be zero" }
    return a / b
}

fun demonstrateExceptionHandling() {
    try {
        println(divide(10, 0))
    } catch (e: IllegalArgumentException) {
        println("Error: ${e.message}")
    }
}

// Example 5: Access Control and Authorization
class UserRepository {
    private val users = mutableListOf<User>()

    fun registerUser(name: String, email: String, password: String) {
        require(name.isNotBlank()) { "The name cannot be empty" }
        require(email.isValidEmail()) { "Invalid email" }
        require(password.length >= 6) { "The password must be at least 6 characters long" }

        val user = User(name, email)
        users.add(user)
    }

    fun getUserByEmail(email: String): User? {
        return users.find { it.email == email }
    }
}

fun demonstrateAccessControl() {
    val repository = UserRepository()

    try {
        repository.registerUser("Juan Pérez", "juan.perez@example.com", "password123")
        repository.registerUser("Ana Gómez", "ana.gomez@example.com", "password456")
        repository.registerUser("Invalid", "invalid_email", "pass")
    } catch (e: IllegalArgumentException) {
        println("Error registering user: ${e.message}")
    }

    val user = repository.getUserByEmail("juan.perez@example.com")
    user?.let {
        println("User found: Name: ${it.name}, Email: ${it.email}")
    } ?: run {
        println("User not found")
    }
}

fun main() {
    demonstrateNullSafety()
    demonstrateEmailValidation()
    demonstrateImmutableDataClasses()
    demonstrateExceptionHandling()
    demonstrateAccessControl()
}

```

### Contributing
Contributions are welcome! Please open an issue or submit a pull request for any improvements or new examples related to Kotlin and cybersecurity.

### License
This repository is licensed under the MIT License. See the LICENSE file for details.
