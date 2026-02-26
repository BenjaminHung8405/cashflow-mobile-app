# CashFlow Mobile App - Project Structure

## Architecture Overview

This project follows **Clean Architecture** with a **Feature-First** approach and uses **Riverpod** for state management.

## Folder Structure

```
lib/
├── core/                           # Shared functionality across features
│   ├── constants/                  # App-wide constants
│   ├── errors/                     # Error handling classes
│   ├── network/                    # Network configuration (API client, etc.)
│   ├── router/                     # App routing configuration
│   ├── theme/                      # App theme and styling
│   └── utils/                      # Utility functions and helpers
│
├── features/                       # Feature modules
│   ├── auth/                       # Authentication feature
│   │   ├── data/
│   │   │   ├── datasources/        # Remote & Local data sources
│   │   │   ├── models/             # Data models (JSON serialization)
│   │   │   └── repositories/       # Repository implementations
│   │   ├── domain/
│   │   │   ├── entities/           # Business entities
│   │   │   ├── repositories/       # Repository contracts (interfaces)
│   │   │   └── usecases/           # Business logic use cases
│   │   └── presentation/
│   │       ├── pages/              # UI screens/pages
│   │       ├── providers/          # Riverpod providers (state management)
│   │       └── widgets/            # Reusable UI components
│   │
│   └── transactions/               # Transactions feature
│       ├── data/
│       │   ├── datasources/
│       │   ├── models/
│       │   └── repositories/
│       ├── domain/
│       │   ├── entities/
│       │   ├── repositories/
│       │   └── usecases/
│       └── presentation/
│           ├── pages/
│           ├── providers/
│           └── widgets/
│
└── main.dart                       # App entry point with ProviderScope
```

## Clean Architecture Layers

### 1. **Presentation Layer** (`presentation/`)
- **Pages**: Full screen UI components
- **Widgets**: Reusable UI components
- **Providers**: Riverpod state management (StateNotifier, FutureProvider, etc.)
- **Responsibility**: Display data and handle user interactions

### 2. **Domain Layer** (`domain/`)
- **Entities**: Pure Dart business objects (no dependencies)
- **Repositories**: Abstract interfaces defining data operations
- **Use Cases**: Business logic operations (e.g., LoginUser, GetTransactions)
- **Responsibility**: Core business logic, independent of frameworks

### 3. **Data Layer** (`data/`)
- **Data Sources**: API calls, local database operations
- **Models**: Data transfer objects with JSON serialization
- **Repositories**: Concrete implementations of domain repositories
- **Responsibility**: Data fetching and persistence

## Dependencies

- **flutter_riverpod**: ^2.6.1 - State management solution
- **cupertino_icons**: ^1.0.8 - iOS style icons

## Getting Started

1. **Install dependencies**:
   ```bash
   flutter pub get
   ```

2. **Run the app**:
   ```bash
   flutter run
   ```

## State Management with Riverpod

The app is wrapped with `ProviderScope` in `main.dart`, enabling Riverpod throughout the app:

```dart
void main() {
  runApp(
    const ProviderScope(
      child: MyApp(),
    ),
  );
}
```

All pages use `ConsumerWidget` to access Riverpod providers via `WidgetRef`.

## Next Steps

1. **Core Setup**:
   - Define app constants (API URLs, colors, etc.) in `core/constants/`
   - Set up error handling classes in `core/errors/`
   - Configure HTTP client in `core/network/`
   - Implement app routing in `core/router/`
   - Define app theme in `core/theme/`

2. **Feature Development**:
   - Start with domain layer (entities, use cases)
   - Implement data layer (models, data sources, repositories)
   - Build presentation layer (providers, pages, widgets)

3. **Testing**:
   - Write unit tests for use cases
   - Test repositories with mock data sources
   - Widget tests for UI components

## Notes

- All empty directories contain `.gitkeep` files to ensure they're tracked by Git
- Follow the dependency rule: Domain → Data → Presentation
- Domain layer should have no dependencies on other layers
- Use dependency injection through Riverpod providers
