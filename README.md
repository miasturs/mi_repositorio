Stack de desarrollo — App móvil de gestión de citas médicas

Objetivo

Análisis técnico para seleccionar un stack multiplataforma para Android e iOS.

Stack recomendado

Framework: Flutter

Lenguaje: Dart

IDE: Android Studio Quail 4 2026.1.4 Patch 1

Estado: Riverpod (propuesto)

API: REST/JSON

Persistencia: SQLite/Drift o sqflite

Push: Firebase Cloud Messaging

QR/cámara: plugin de cámara/QR

Pruebas: flutter_test + integration_test

Comparativa

Se compararon Flutter, React Native con Expo y Kotlin Multiplatform considerando lenguaje, rendimiento, curva de aprendizaje, comunidad y ejemplos reales.

Flutter

Una base de código para Android/iOS, UI consistente y ecosistema maduro.

React Native + Expo

Alternativa especialmente conveniente para equipos con experiencia en React y TypeScript. Expo tiene soporte de primera clase para TypeScript.

Kotlin Multiplatform

Permite compartir lógica y, con Compose Multiplatform, también UI. Es apropiado cuando se busca conservar una integración cercana a lo nativo.

Hardware

Cámara: QR.

Notificaciones push: recordatorios y cambios.

Almacenamiento local: historial mínimo y sincronización offline.

Red: sincronización con el backend.

GPS/Bluetooth/NFC: no son necesarios para el alcance actual.

Entorno

Instalar Android Studio Quail 4 2026.1.4 Patch 1.

Configurar Android SDK, Platform Tools y Emulator.

Instalar Flutter SDK.

Instalar plugin Flutter (Dart como dependencia).

Ejecutar flutter doctor.

Crear un emulador Android.

Para iOS se requiere macOS + Xcode.

Estructura sugerida

lib/
  core/
  data/
  domain/
  presentation/
  features/
    auth/
    appointments/
    history/
    profile/

Fuentes

Flutter: https://docs.flutter.dev/reference/supported-platforms

Android Studio: https://developer.android.com/studio/releases

Android updates: https://developer.android.com/latest-updates/

Expo TypeScript: https://docs.expo.dev/guides/typescript/

Expo New Architecture: https://docs.expo.dev/guides/new-architecture/

Kotlin Multiplatform: https://kotlinlang.org/docs/multiplatform/kmp-overview.html

KMP examples: https://kotlinlang.org/docs/cross-platform-mobile-development.html
