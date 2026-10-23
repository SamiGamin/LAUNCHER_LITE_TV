# LAUNCHER_LITE_TV

# Lite TV (TVliteHome) 📺

<p align="center">
  <img src="tv/src/main/res/drawable-xhdpi/banner.png" alt="Lite TV Banner" width="380"/>
</p>

<p align="center">
  <strong>Un launcher minimalista, ultraligero y fluido para Android TV y Google TV, optimizado para dispositivos de bajos recursos (1GB - 2GB RAM).</strong>
</p>

<p align="center">
  <a href="https://github.com/SamiGamin/TV_lite_Home/releases/latest">
    <img src="https://img.shields.io/github/v/release/SamiGamin/TV_lite_Home?color=blue&label=Versi%C3%B3n" alt="Última versión"/>
  </a>
  <img src="https://img.shields.io/badge/Plataforma-Android%20TV-3DDC84?logo=android" alt="Plataforma Android TV"/>
  <img src="https://img.shields.io/badge/Kotlin-100%25-7F52FF?logo=kotlin" alt="Kotlin 100%"/>
  <img src="https://img.shields.io/badge/Min%20SDK-26%20(Android%208.0%2B)-orange" alt="Min SDK 26"/>
  <img src="https://img.shields.io/badge/Licencia-MIT-green" alt="Licencia MIT"/>
</p>

---

## ✨ Características Principales

* ⚡ **Diseñado para TV Boxes de Bajos Recursos (1GB - 2GB RAM):**
  * Sin shaders de desenfoque en tiempo real (*blur*), capas translúcidas redundantes ni saturación de CPU.
  * Consumo mínimo de memoria RAM (< 40 MB) y arranque instantáneo.
* 🕒 **Barra HUD Superior Fija (Siempre Visible):**
  * Reloj digital inteligente que respeta de forma nativa la configuración de hora de tu televisor (**12h con indicador AM/PM** o **24h**) con **0 bytes de consumo de RAM adicional**.
  * Encabezado permanente: al desplazarte hacia abajo por las filas de aplicaciones, la barra con la hora, fecha y accesos rápidos permanece visible en todo momento.
* 🎮 **Modo Reorganizar con D-Pad:**
  * Reordena tus aplicaciones favoritas directamente con las flechas del control remoto (**⬅️ Izquierda, ➡️ Derecha, ⬆️ Arriba, ⬇️ Abajo**).
  * Fija la posición presionando **OK** o **Atrás**, guardando tus preferencias de forma persistente.
* 👁️ **Ocultar y Restaurar Aplicaciones:**
  * Mantén tu pantalla despejada ocultando las aplicaciones del sistema o de poco uso.
  * Botón dinámico en la barra superior para ver y restaurar tus aplicaciones ocultas con un solo clic.
* 🛡️ **Blindaje Direct Boot & Cold Boot:**
  * Declarado con `directBootAware` y almacenamiento protegido por dispositivo (`Device Protected Storage`).
  * Inicia en el segundo 0 tras un apagado completo sin caer en pantallas negras ni bucles de recuperación.
* 🚀 **Apertura de Aplicaciones Nativa (Leanback & Estándar):**
  * Soporte completo para aplicaciones nativas de TV (Leanback) y apps móviles estándar (sideloaded) sin cierres forzados ni errores de tarea descartada.

---

## 📥 Descarga e Instalación

### Opción 1: Descargar el APK
Descarga la versión más reciente lista para instalar desde la sección de [Releases de GitHub](https://github.com/SamiGamin/TV_lite_Home/releases/latest).

### Opción 2: Instalación por ADB
Conecta tu televisor por depuración de red o USB y ejecuta:
```bash
adb install -r "Lite TV-v1.0.0-release.apk"
```

---

## ⚙️ Fijar como Launcher Principal (Procedimiento Seguro)

Basado en el estándar de seguridad de *Home Guard* (CleanYourTV):

```bash
# 1. Abrir la interfaz de Lite TV en la pantalla
adb shell am start -n com.launcher.samidev/.presentation.MainActivity

# 2. Fijar Lite TV como el launcher predeterminado del sistema
adb shell cmd package set-home-activity "com.launcher.samidev/.presentation.MainActivity"

# 3. En Google TV, inhabilitar de forma segura el launcher de fábrica y el asistente inicial:
adb shell pm disable-user --user 0 com.google.android.apps.tv.launcherx
adb shell pm disable-user --user 0 com.google.android.tungsten.setupwraith

# 4. Verificar que el sistema resuelva directamente a Lite TV
adb shell cmd package resolve-activity --brief -a android.intent.action.MAIN -c android.intent.category.HOME
```

> [!TIP]
> **Rollback de Emergencia (para volver al launcher de Google TV en cualquier momento):**
> ```bash
> adb shell pm enable com.google.android.apps.tv.launcherx
> adb shell pm enable com.google.android.tungsten.setupwraith
> adb shell cmd package set-home-activity "com.google.android.apps.tv.launcherx/.home.HomeActivity"
> ```

---

## 🛠️ Stack Tecnológico

* **Lenguaje:** Kotlin 100%
* **UI:** Jetpack Compose for TV (`androidx.tv.material3`)
* **Arquitectura:** Clean Architecture + MVVM
* **Asincronía & Estado:** Coroutines + StateFlow (`@Immutable` UI States)
* **Almacenamiento Local:** DataStore en `DeviceProtectedStorage`
* **Imágenes & Banners:** Coil Compose optimizado a resolución exacta de pantalla



## 📄 Licencia

Este proyecto está bajo la licencia [MIT](LICENSE).
