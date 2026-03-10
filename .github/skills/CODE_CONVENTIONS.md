# Code Style & Conventions

This document defines the code style and conventions used across all Flutter module creation skills.

---

## Language Convention

> **All identifiers (variables, classes, functions, files, folders) and all comments must be written in English.**  
> This applies to: inline comments, TODO comments, documentation comments, and commit messages.

---

## Naming Conventions

### Files & Folders
- **Folders**: `snake_case` (e.g., `user`, `oauth`, `tic_tac_toe`)
- **Dart Files**: `snake_case` (e.g., `user_domain_repository.dart`)
- **Classes**: `PascalCase` (e.g., `UserDomainRepository`)
- **Variables**: `camelCase` (e.g., `userName`, `isActive`)
- **Constants**: `camelCase` (e.g., `maxRetries`, `defaultTimeout`)

> **All identifiers must use English words.** Do not use transliterated or non-English words.

```dart
// ✅ Correct
String userName;
bool isLoggedIn;
int retryCount;
class UserProfilePage {}

// ❌ Wrong — non-English identifiers
String tenNguoiDung;
bool dangNhap;
class TrangCaNhan {}
```

[//]: # (### Module Structure Naming)

[//]: # (```)

[//]: # (<module_name>/                           &#40;snake_case&#41;)

[//]: # (├── data/)

[//]: # (│   ├── model/)

[//]: # (│   │   ├── local_db/                    &#40;snake_case&#41;)

[//]: # (│   │   ├── res_api_remote/              &#40;snake_case&#41;)

[//]: # (│   │   └── web_socket/                  &#40;snake_case&#41;)

[//]: # (│   └── <module>_domain_repository_impl.dart  &#40;snake_case&#41;)

[//]: # (├── domain/)

[//]: # (│   ├── entity/                          &#40;snake_case&#41;)

[//]: # (│   ├── value_object/                    &#40;snake_case&#41;)

[//]: # (│   ├── <module>_domain_repository.dart  &#40;snake_case&#41;)

[//]: # (│   └── <module>_domain_service.dart     &#40;snake_case&#41;)

[//]: # (└── use_case/)

[//]: # (    └── <use_case_name>/                 &#40;snake_case&#41;)

[//]: # (        ├── <use_case>_use_case.dart     &#40;snake_case&#41;)

[//]: # (        └── <use_case>_use_case_output_entity.dart  &#40;snake_case&#41;)

[//]: # (```)

### Class Naming Patterns

[//]: # (- **Domain Repository**: `<Module>DomainRepository` &#40;e.g., `UserDomainRepository`&#41;)

[//]: # (- **Domain Service**: `<Module>DomainService` &#40;e.g., `UserDomainService`&#41;)

[//]: # (- **Data Repository**: `<Module>DomainRepositoryImpl` &#40;e.g., `UserDomainRepositoryImpl`&#41;)

[//]: # (- **Use Case**: `<UseCase>UseCase` &#40;e.g., `LoginUseCase`&#41;)

[//]: # (- **Use Case Input**: `<UseCase>UseCaseInputModel` &#40;e.g., `LoginUseCaseInputModel`&#41;)

[//]: # (- **Use Case Output**: `<UseCase>UseCaseOutputModel` &#40;e.g., `LoginUseCaseOutputModel`&#41;)

[//]: # (- **Output Entity**: `<UseCase>UseCaseOutputEntity` &#40;e.g., `LoginUseCaseOutputEntity`&#41;)

---

## Import Conventions

### Import Order
1. Dart SDK imports
2. Flutter framework imports
3. Package imports (alphabetically)
4. Project imports (alphabetically)
5. Relative imports

### Import Style
```dart
// Dart/Flutter imports
import 'dart:async';
import 'package:flutter/material.dart';

// Package imports
import 'package:dio/dio.dart';
import 'package:freezed_annotation/freezed_annotation.dart';

// Project imports
import 'package:forever_c_web/core/use_case/use_case.dart';
import 'package:forever_c_web/module/user/domain/user_domain_repository.dart';
import 'package:forever_c_web/module/user/domain/user_domain_service.dart';

// Relative imports
import 'user_use_case_output_entity.dart';
```

---

## Code Style

### Class Structure
```dart
class ExampleClass {
  // 1. Static constants
  static const int maxRetries = 3;
  
  // 2. Instance fields (final first, then non-final)
  final String name;
  final int age;
  int score;
  
  // 3. Constructor
  ExampleClass({
    required this.name,
    required this.age,
    this.score = 0,
  });
  
  // 4. Named constructors
  ExampleClass.empty()
      : name = '',
        age = 0,
        score = 0;
  
  // 5. Public methods
  void publicMethod() {
    // Implementation
  }
  
  // 6. Private methods
  void _privateMethod() {
    // Implementation
  }
}
```

### Method Structure
```dart
Future<void> methodName({
  required String param1,
  int param2 = 0,
}) async {
  // 1. Input validation
  if (param1.isEmpty) {
    throw ArgumentError('param1 cannot be empty');
  }
  
  // 2. Business logic
  final result = await _performOperation(param1);
  
  // 3. Return or update state
  return result;
}
```

---

## Comment Conventions

> **All comments must be written in English.** Do not use any other language in comments.

### TODO Comments
```dart
// ✅ Correct
/// TODO: Add implementation for user authentication
/// TODO: Handle edge case when network is unavailable
/// TODO: Add method declarations here

// ❌ Wrong — not in English
/// TODO: Thêm xử lý xác thực người dùng
```

### Documentation Comments
```dart
// ✅ Correct
/// Creates a new user in the system.
///
/// [name] must not be empty.
/// Returns [UserEntity] if successful, throws [Exception] otherwise.
Future<UserEntity> createUser(String name) async {
  // Implementation
}

// ❌ Wrong — not in English
/// Tạo người dùng mới trong hệ thống.
Future<UserEntity> createUser(String name) async {}
```

### Inline Comments
```dart
// ✅ Correct
// Validate input before processing
if (input.isEmpty) {
  return;
}

// Call domain service for business logic
final result = await service.processData(input);

// ❌ Wrong — not in English
// Kiểm tra đầu vào trước khi xử lý
if (input.isEmpty) {
  return;
}
```

---

## Freezed Conventions

### Freezed Class Pattern
```dart
import 'package:freezed_annotation/freezed_annotation.dart';

part 'entity_name.freezed.dart';
part 'entity_name.g.dart';

@freezed
class EntityName with _$EntityName {
  const EntityName._();

  const factory EntityName({
    required int id,
    required String name,
    String? optionalField,
    @Default(false) bool isActive,
  }) = _EntityName;

  factory EntityName.fromJson(Map<String, dynamic> json) =>
      _$EntityNameFromJson(json);
      
  // Custom methods
  bool get isValid => name.isNotEmpty;
}
```
---

## Architecture Conventions

[//]: # (### Domain Layer)

[//]: # (- **Repository Interface**: Always abstract, no implementation)

[//]: # (- **Domain Service**: Contains pure business logic, depends on repository interface)

[//]: # (- **Entities**: Immutable, use Freezed)

[//]: # (- **Value Objects**: Enums, simple validated types)

[//]: # ()
[//]: # (### Data Layer)

[//]: # (- **Repository Implementation**: Implements domain repository interface)

[//]: # (- **Models**: DTOs for API/DB, use Freezed)

[//]: # (- **Separation**: Keep API, DB, WebSocket models in separate folders)

[//]: # ()
[//]: # (### Use Case Layer)

[//]: # (- **Input Model**: Contains `UseCaseInputBinding` for reactive inputs)

[//]: # (- **Output Model**: Contains output entity and `setValue` callback)

[//]: # (- **Use Case**: Contains `businessLogic&#40;&#41;` method, uses domain service)

---

## Error Handling Conventions

### Use Case Error Handling
```dart
@override
Future<void> businessLogic() async {
  try {
    // Validate inputs
    service.validateInput(inputModel.value);
    
    // Execute business logic
    final result = await service.execute();
    
    // Update output
    outputModel.setValue(
      outputModel.output.copyWith(
        successful: true,
        data: result,
      ),
    );
  } on BusinessLogicException catch (e) {
    // Handle business logic errors
    outputModel.setValue(
      outputModel.output.copyWith(
        failed: true,
        baseErrorMessage: e.message,
      ),
    );
  } catch (e) {
    // Handle unexpected errors
    outputModel.setValue(
      outputModel.output.copyWith(
        failed: true,
        baseErrorMessage: 'Unexpected error: $e',
      ),
    );
  }
}
```

### Domain Service Error Handling
```dart
void validateInput({required String? input}) {
  if (input == null || input.isEmpty) {
    throw EmptyException(message: 'Input cannot be empty');
  }
  
  if (input.length < 3) {
    throw BusinessLogicException(
      message: 'Input must be at least 3 characters',
    );
  }
}
```

---

## Best Practices

### 1. Dependency Injection
```dart
// Constructor injection (preferred)
class MyService {
  final MyRepository repository;
  
  MyService({required this.repository});
}
```

### 2. Immutability
```dart
// Use final for fields
final String name;

// Use Freezed for data classes
@freezed
class User with _$User {
  const factory User({required String name}) = _User;
}
```

### 3. Null Safety
```dart
// Use required for non-nullable parameters
void method({required String name}) {}

// Use nullable types explicitly
String? optionalValue;

// Use null-aware operators
final value = optionalValue ?? 'default';
```

### 4. Async/Await
```dart
// Always use async/await for Future operations
Future<User> getUser(int id) async {
  final data = await repository.fetchUser(id);
  return User.fromJson(data);
}
```

---

## Package Import Paths

### Core Imports
```dart
// Use case framework
import 'package:forever_c_web/core/use_case/use_case.dart';
import 'package:forever_c_web/core/use_case/use_case_input_binding.dart';
import 'package:forever_c_web/core/use_case/use_case_input_model.dart';
import 'package:forever_c_web/core/use_case/use_case_output_model.dart';
import 'package:forever_c_web/core/use_case/use_case_output_entity.dart';

// Exceptions
import 'package:forever_c_web/core/use_case/business_logic_exception.dart';
import 'package:forever_c_web/core/use_case/empty_exception.dart';

// API
import 'package:forever_c_web/core/base_api_response/base_api_response.dart';
```

### Module Imports
```dart
// Domain
import 'package:forever_c_web/module/<module>/domain/<module>_domain_repository.dart';
import 'package:forever_c_web/module/<module>/domain/<module>_domain_service.dart';
import 'package:forever_c_web/module/<module>/domain/entity/<entity_name>.dart';

// Data
import 'package:forever_c_web/module/<module>/data/<module>_domain_repository_impl.dart';
import 'package:forever_c_web/module/<module>/data/model/res_api_remote/<model_name>.dart';

// Use Case
import 'package:forever_c_web/module/<module>/use_case/<use_case>/<use_case>_use_case.dart';
import 'package:forever_c_web/module/<module>/use_case/<use_case>/<use_case>_use_case_output_entity.dart';
```

---

[//]: # (## Version & Compatibility)

[//]: # ()
[//]: # (- **Dart Version**: 3.0+)

[//]: # (- **Flutter Version**: 3.10+)

[//]: # (- **Null Safety**: Enabled)

[//]: # (- **Freezed Version**: 2.0+)

[//]: # (- **Build Runner**: Required for code generation)

[//]: # ()
[//]: # (---)

**Last Updated**: January 2026  
**Version**: 1.0
