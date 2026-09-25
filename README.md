# App de Gestión de Citas Médicas — Análisis de Stack Tecnológico

## Resumen de la decisión

| Capa | Tecnología seleccionada |
|---|---|
| Framework / lenguaje | Flutter 3.44+ / Dart 3.12+ |
| Gestión de estado | Riverpod |
| Backend y notificaciones | Firebase (Authentication y Cloud Messaging) o API REST propia |
| Almacenamiento offline | Drift (SQLite) cifrado con SQLCipher |
| Escaneo QR | `mobile_scanner` |
| Biometría | `local_auth` |
| Calendario del dispositivo | `device_calendar` (opcional) |
| Entorno de desarrollo | VS Code (extensiones Flutter y Dart) + Android Studio (SDK/emulador) + Xcode (build iOS) |
| Integración continua | Codemagic o GitHub Actions + Fastlane |

**¿Por qué Flutter?** Para una app de salud, la consistencia visual entre Android e iOS y un único
equipo/base de código pesan más que la ganancia marginal de rendimiento de Kotlin Multiplatform o la
familiaridad JS de React Native. Flutter ofrece rendimiento cercano al nativo, paquetes maduros para
cámara/push/almacenamiento cifrado/biometría, y precedentes en sectores regulados (Google Pay, Nubank).
Detalles y alternativas según contexto de equipo en el PDF.

## Arquitectura por capas

```
lib/
├── presentation/   # Pantallas y widgets (agenda, detalle de cita, historial, perfil)
├── application/    # Providers Riverpod: sesión, agenda, sincronización offline/online
├── data/           # Drift (SQLite local cifrado) + cliente Firebase/API REST remota
└── services/       # Envoltorios de cámara (QR), notificaciones push y biometría
```

## Hardware y permisos requeridos

| Función | Paquete | Permiso |
|---|---|---|
| Escaneo de QR (check-in, receta, identificador de paciente) | `mobile_scanner` | Cámara |
| Recordatorios y cambios de cita | `firebase_messaging` + `flutter_local_notifications` | Notificaciones |
| Historial offline | `drift` + `sqlcipher_flutter_libs` | Almacenamiento cifrado |
| Acceso seguro a datos médicos | `local_auth` | Biometría (huella / Face ID), con respaldo de PIN |

## Configuración del entorno de desarrollo

1. Instalar el Flutter SDK 3.44+ y agregar `flutter/bin` al `PATH`.
2. Ejecutar `flutter doctor` y resolver cualquier dependencia faltante.
3. Instalar Android Studio (última versión estable, serie 2026.1.x) para el SDK de Android, Platform
   Tools y el AVD Manager.
4. En macOS, instalar Xcode para compilar y firmar la app iOS (Flutter 3.44+ usa Swift Package Manager
   por defecto).
5. Instalar VS Code con las extensiones **Flutter** y **Dart**.
6. Configurar un emulador Android y, en macOS, un simulador iOS.
7. Verificar `flutter doctor -v` sin errores antes de comenzar.

## Seguridad y cumplimiento

- Cifrado en reposo (SQLCipher) y en tránsito (TLS) para todo dato clínico.
- Autenticación biométrica con respaldo de PIN y cierre de sesión por inactividad.
- Minimización de datos offline: solo el historial necesario, no el expediente clínico completo.
- Validar el marco regulatorio de datos de salud del país de despliegue (equivalentes locales a
  HIPAA/GDPR) antes de definir la política de retención.
