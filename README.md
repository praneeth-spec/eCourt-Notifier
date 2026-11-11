# eCourt Notify

**eCourt Notify** is a premium, local-first Flutter mobile application for tracking court cases, managing hearing reminders, receiving judiciary notifications, reading court announcements, locating courts, and discovering advocates.

Built as a final-year project and portfolio-ready demonstration, it pairs a polished judiciary-focused interface with SQLite storage, Provider state management, and Android local notifications.

## Features

- Local registration, login, logout, and persisted sessions
- Guided onboarding and a polished dashboard
- Searchable case tracking with judge, court hall, status, next hearing, timeline, and history
- Live in-app notifications with unread badges and animated cards
- Android instant and scheduled hearing notifications
- Notification tap handling that opens the notifications screen
- Court announcements with expandable details
- Searchable advocate directory with specialization, court, contact details, and rating
- Google Maps court locator with seeded court markers
- Editable user profile, notification preferences, and dark mode
- One-tap app reset that clears local data and restores seeded sample data
- Responsive layouts designed for Android emulators and physical devices

## Screens

- Splash and onboarding
- Login, registration, and password recovery UI
- Home dashboard
- Case tracking and case details
- Notifications
- Court announcements
- Advocate directory
- Court locator
- Profile and settings

## Tech Stack

| Area | Technology |
| --- | --- |
| Mobile framework | Flutter and Dart |
| Local database | SQLite with `sqflite` |
| State management | Provider |
| Local storage | SharedPreferences |
| Android alerts | flutter_local_notifications |
| Maps | google_maps_flutter |
| UI | Material 3 and flutter_animate |

## Architecture

```text
Presentation Layer
  Screens + Reusable Widgets
          |
Provider State Layer
  Auth / Case / Notification / Profile / Theme
          |
Service Layer
  SQLite / SharedPreferences / Local Notifications
          |
Local Device Storage and Android Notification Center
```

The project follows a clean, feature-oriented structure:

```text
lib/
├── constants/       # Colors and application constants
├── core/            # Theme configuration
├── models/          # Typed SQLite models
├── providers/       # Reactive application state
├── routes/          # Named navigation routes
├── screens/         # Application screens
├── services/        # Database, auth, preferences, notifications
├── utils/           # Formatting and SnackBar helpers
├── widgets/         # Reusable UI components
└── main.dart        # Application bootstrap
```

## Database Design

SQLite is created automatically on first launch. The app seeds meaningful local data for demonstration and testing.

| Table | Purpose |
| --- | --- |
| `users` | Local user accounts and notification preferences |
| `cases` | Case IDs, status, hearings, timeline, and history |
| `notifications` | In-app alerts with read state and linked case IDs |
| `announcements` | Court and registry announcements |
| `advocates` | Advocate profiles and contact details |
| `courts` | Court names, addresses, phone numbers, and coordinates |

## Notification Flow

```text
Court event / user action
          |
SQLite notification insert
          |
Provider + StreamController update
          |
In-app list and unread badge refresh
          |
Android local notification
          |
Tap notification -> Notifications screen
```

## Getting Started

### Prerequisites

- Flutter SDK compatible with Dart `^3.10.0`
- Android Studio, Cursor, or VS Code with Flutter support
- Android emulator or physical Android device
- Java 17 for Android builds

### Installation

```powershell
git clone <your-repository-url>
cd eCourt_Notifier
flutter pub get
flutter run
```

### Demo Account

The initial seeded account is:

```text
Email:    demo@ecourt.in
Password: Password@123
```

You may also register a new local account from the app.

## Google Maps Setup

The Court Locator requires a Google Maps Android API key.

1. Create a project in Google Cloud Console.
2. Enable **Maps SDK for Android**.
3. Create and restrict an Android API key for your package.
4. Replace `YOUR_GOOGLE_MAPS_API_KEY` in:

```text
android/app/src/main/AndroidManifest.xml
```

```xml
<meta-data
    android:name="com.google.android.geo.API_KEY"
    android:value="YOUR_GOOGLE_MAPS_API_KEY" />
```

Do not commit a production key to a public GitHub repository. Use a restricted key or local configuration before publishing.

## Android Notifications

On Android 13 and above, allow notification permission when prompted.

To test notifications:

1. Sign in using the demo account.
2. Open **Notifications** and tap **Test alert**, or use **Live demo** on Home.
3. Confirm the in-app list and Android notification tray update.
4. Open a case and select **Schedule hearing reminder**.
5. Tap a delivered notification to open the Notifications screen.

If scheduled alerts do not appear, check Android notification channel settings, exact alarm access, and battery optimization settings for the app.

## Resetting the Demo

Tap the reset icon in the top-right corner of the Home dashboard. After confirmation, the app clears its local session, preferences, SQLite data, and notifications, then restores the original sample records and opens onboarding.

## Quality Checks

```powershell
flutter analyze
flutter test
flutter build apk --debug
```

The debug APK is generated at:

```text
build/app/outputs/flutter-apk/app-debug.apk
```

## Key Dependencies

- [sqflite](https://pub.dev/packages/sqflite)
- [provider](https://pub.dev/packages/provider)
- [shared_preferences](https://pub.dev/packages/shared_preferences)
- [flutter_local_notifications](https://pub.dev/packages/flutter_local_notifications)
- [google_maps_flutter](https://pub.dev/packages/google_maps_flutter)
- [flutter_animate](https://pub.dev/packages/flutter_animate)

## Documentation

For implementation-level SQLite and notification setup, see [SQLite and notification setup](docs/sqlite_notifications_setup.md).

## License

This project is intended for educational, portfolio, and demonstration use. Add your preferred license before public distribution.
