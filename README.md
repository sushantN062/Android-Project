# NIT3213 Final Assignment — Android Application

An Android application for the NIT3213 unit that demonstrates API integration, clean architecture, dependency injection with Hilt, and unit testing.

---

## Features

- **Login Screen** — Authenticates against the VU NIT3213 API using your Student ID and First Name
- **Dashboard Screen** — Displays a list of topic entities in a RecyclerView, fetched using the keypass returned from login
- **Details Screen** — Shows full information for a selected entity, including its description
- **Dependency Injection** — Full Hilt setup across ViewModels, Repositories, and Network layer
- **Unit Tests** — Tests for ViewModels, Repository, and Entity model

---

## Prerequisites

| Tool | Version |
|------|---------|
| Android Studio | Hedgehog (2023.1.1) or later |
| JDK | 17 |
| Android SDK | API 34 (compileSdk), API 24 (minSdk) |
| Gradle | 8.2+ |

---

## Setup & Build Instructions

### 1. Clone the repository

```bash
git clone https://github.com/YOUR_USERNAME/NIT3213App.git
cd NIT3213App
```

### 2. Open in Android Studio

- Launch Android Studio
- Select **File → Open** and navigate to the project folder
- Wait for Gradle sync to complete (this may take a few minutes on first run)

### 3. Build the project

```bash
./gradlew assembleDebug
```

Or use **Build → Make Project** in Android Studio.

### 4. Run on device or emulator

- Connect a physical device (USB debugging enabled) **or** launch an AVD
- Click **Run → Run 'app'** or press `Shift+F10`

### 5. Run unit tests

```bash
./gradlew test
```

Or in Android Studio: right-click on `app/src/test` → **Run Tests**

---

## How to Use the App

1. **Login Screen**
   - Enter your **Student ID** in the format `s12345678` (lowercase `s` + 8 digits)
   - Enter your **First Name** as the password
   - Tap **Sign In**

2. **Dashboard Screen**
   - After successful login, a list of entities for your topic is displayed
   - Tap any card to view full details

3. **Details Screen**
   - All entity properties are shown in a clean card layout
   - The full description is displayed in a dedicated section
   - Use the back arrow to return to the Dashboard

---

## Project Structure

```
app/src/main/java/com/example/nit3213app/
├── NIT3213Application.kt          # Hilt application class
├── data/
│   ├── model/
│   │   └── Models.kt              # LoginRequest, LoginResponse, Entity, DashboardResponse
│   ├── network/
│   │   ├── ApiService.kt          # Retrofit interface
│   │   └── DashboardDeserializer.kt # Custom Gson deserializer for dynamic entity fields
│   └── repository/
│       └── Repository.kt          # AuthRepository, DashboardRepository + implementations
├── di/
│   └── AppModule.kt               # Hilt NetworkModule + RepositoryModule
└── ui/
    ├── login/
    │   ├── LoginActivity.kt
    │   └── LoginViewModel.kt
    ├── dashboard/
    │   ├── DashboardActivity.kt
    │   ├── DashboardViewModel.kt
    │   └── EntityAdapter.kt
    └── details/
        └── DetailsActivity.kt
```

---

## Architecture

This project follows **MVVM (Model-View-ViewModel)** clean architecture:

- **View** (Activities) — observes LiveData, delegates actions to ViewModel
- **ViewModel** — holds UI state, calls repository, survives configuration changes
- **Repository** — single source of truth, abstracts data source
- **Network** — Retrofit + OkHttp for API communication

---

## API Configuration

The app targets the **Sydney** endpoint:

```
POST https://nit3213api.onrender.com/sydney/auth
GET  https://nit3213api.onrender.com/dashboard/{keypass}
```

To switch to a different campus endpoint (e.g. `footscray` or `ort`), update the `@POST` annotation in `ApiService.kt`.

---

## Dependencies

| Library | Purpose |
|---------|---------|
| Hilt 2.48 | Dependency Injection |
| Retrofit 2.9 | HTTP client |
| OkHttp 4.12 | Network layer + logging |
| Gson | JSON serialisation |
| Coroutines 1.7 | Async operations |
| LiveData / ViewModel | Lifecycle-aware state |
| Material Components | UI components |
| Mockito + Mockito-Kotlin | Unit test mocking |
| Coroutines Test | ViewModel coroutine testing |
| AndroidX Arch Core | `InstantTaskExecutorRule` for LiveData |

---

## Git Commit Convention

Commits follow the pattern:

```
<type>: <short description>

feat:     new feature
fix:      bug fix
test:     adding or updating tests
refactor: code restructure without behaviour change
docs:     documentation only
chore:    build/config changes
```

---

## Author

- **Student ID:** s8150049 *
- **Name:** Sushant Nepal
- **Unit:** NIT3213 — Android Development
- **Campus:** Sydney
