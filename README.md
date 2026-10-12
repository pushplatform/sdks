<div align="center">

<a href="https://pushpilot.ru">
  <img src="https://raw.githubusercontent.com/pushplatform/.github/HEAD/assets/pushpilot-banner.png" alt="PushPilot — push-уведомления для приложений и сайтов" width="100%">
</a>
<br/><br/>

[Быстрый старт](https://pushpilot.ru/docs/quick-start) &nbsp; • &nbsp; [Сайт](https://pushpilot.ru) &nbsp; • &nbsp; [Документация](https://pushpilot.ru/docs) &nbsp; • &nbsp; [Примеры](https://pushpilot.ru/docs/examples)

</div>

---

Официальный каталог SDK **PushPilot** для мобильных приложений и сайтов. Все SDK опубликованы: выберите платформу вашего проекта, установите пакет и завершите настройку по инструкции.

Для нативного приложения выберите **iOS** или **Android**, для проекта на **React Native / Expo** или **Flutter** — соответствующий SDK, для сайта — **Web SDK**. Ниже указаны опубликованные версии, сверенные 12 октября 2026 года.

## 📱 Мобильные SDK

SDK для нативных приложений iOS и Android.

| Платформа | Версия и установка | Репозиторий |
| :--- | :--- | :--- |
| **iOS · Swift** | **1.0.0** · SPM или [CocoaPods](https://cocoapods.org/pods/PushPlatformSDK) | [pushpilot-sdk-ios](https://github.com/pushplatform/pushpilot-sdk-ios) |
| **Android · Kotlin** | **1.0.0** · [публичный Maven-репозиторий GitHub](https://github.com/pushplatform/pushpilot-sdk-android/tree/maven) | [pushpilot-sdk-android](https://github.com/pushplatform/pushpilot-sdk-android) |

### iOS — Swift Package Manager или CocoaPods

**SPM:** в Xcode откройте **File → Add Package Dependencies**, укажите URL и выберите версию **1.0.0**. Добавьте продукт **PushPlatformSDK** в target приложения.

```text
https://github.com/pushplatform/pushpilot-sdk-ios.git
```

Для проекта с `Package.swift` добавьте в `dependencies`:

```swift
.package(url: "https://github.com/pushplatform/pushpilot-sdk-ios.git", from: "1.0.0")
```

**CocoaPods:** добавьте в target приложения в `Podfile`:

```ruby
pod 'PushPlatformSDK', '1.0.0'
```

```sh
pod install
```

Откройте `.xcworkspace`. Используйте один способ подключения SDK в target. Требуется **iOS 13+**; настройка APNs, capabilities и callbacks описана в [README iOS SDK](https://github.com/pushplatform/pushpilot-sdk-ios#readme).

### Android — публичный Maven-репозиторий GitHub

В `settings.gradle.kts` добавьте репозиторий SDK в `dependencyResolutionManagement.repositories`, сохранив `google()` и `mavenCentral()`:

```kotlin
dependencyResolutionManagement {
    repositories {
        google()
        mavenCentral()
        maven {
            url = uri("https://raw.githubusercontent.com/pushplatform/pushpilot-sdk-android/maven/")
            content { includeModule("com.pushplatform", "sdk-android") }
        }
    }
}
```

В `build.gradle.kts` модуля приложения:

```kotlin
dependencies {
    implementation("com.pushplatform:sdk-android:1.0.0")
}
```

SDK опубликован в ветке `maven` на GitHub, а не в Maven Central; GitHub-токен и Maven Local не нужны. Требуется **Android API 21+**. Настройку Firebase Cloud Messaging и разрешений смотрите в [README Android SDK](https://github.com/pushplatform/pushpilot-sdk-android#readme).

## 🌐 Web SDK

SDK для push-уведомлений в браузерах.

| Платформа | Версия и установка | Репозиторий |
| :--- | :--- | :--- |
| **Web · JavaScript / TypeScript** | **0.1.1** · [npm](https://www.npmjs.com/package/@pushplatform/web-sdk) | [pushpilot-sdk-web](https://github.com/pushplatform/pushpilot-sdk-web) |

```sh
npm install @pushplatform/web-sdk@0.1.1
```

Разместите service worker на своём сайте. Для проекта с директорией `public`:

```sh
mkdir -p public
cp node_modules/@pushplatform/web-sdk/dist/service-worker.js public/pushpilot-sw.js
```

Для Web Push нужны HTTPS, поддерживаемый браузер, публичный browser key и VAPID public key. Файл worker должен открываться по `/pushpilot-sw.js`. Настройка подписки, подключение через обычный `<script>` и интеграция с существующим worker — в [README Web SDK](https://github.com/pushplatform/pushpilot-sdk-web#readme).

## ⚛️ Кроссплатформенные SDK

Интеграция для приложений на React Native / Expo и Flutter под iOS и Android.

| Платформа | Версия и установка | Репозиторий |
| :--- | :--- | :--- |
| **React Native / Expo · JavaScript / TypeScript** | **1.0.1** · [npm](https://www.npmjs.com/package/@pushplatform/react-native) | [pushpilot-sdk-react-native](https://github.com/pushplatform/pushpilot-sdk-react-native) |
| **Flutter · Dart** | **1.0.0** · [pub.dev](https://pub.dev/packages/push_platform_flutter) | [pushpilot-sdk-flutter](https://github.com/pushplatform/pushpilot-sdk-flutter) |

### React Native и Expo

```sh
npm install @pushplatform/react-native@1.0.1
```

Для **Expo** дополнительно установите development client:

```sh
npx expo install expo-dev-client
```

Добавьте plugin `@pushplatform/react-native` в `app.json` или `app.config.ts` и настройте UUID приложения, Firebase и APNs по [инструкции установки Expo и bare React Native](https://github.com/pushplatform/pushpilot-sdk-react-native/blob/main/docs/INSTALLATION.md).

Используйте **development build или EAS build**: Expo Go не поддерживается. Документированная Expo-связка — **SDK 54 / React Native 0.81.4**. Для bare React Native требуется **0.77+ с New Architecture**, а также настройка нативных проектов по той же инструкции. Нативные SDK входят в npm-пакет.

### Flutter

```sh
flutter pub add push_platform_flutter:^1.0.0
```

Пакет опубликован на [pub.dev](https://pub.dev/packages/push_platform_flutter) и подключает Android и iOS SDK **1.0.0**. Требуются **Flutter 3.24+ / Dart 3.5+**, **Android API 21+** или **iOS 13+**. Настройка Firebase, APNs и CocoaPods — в [README Flutter SDK](https://github.com/pushplatform/pushpilot-sdk-flutter#readme). Flutter Web и desktop не поддерживаются.

<a name="quickstart"></a>

## 🚀 Быстрый старт

1. Создайте аккаунт на [pushpilot.ru](https://pushpilot.ru/register).
2. Добавьте проект и приложение.
3. Настройте данные выбранного push-провайдера на сервере.
4. Установите SDK командой или способом выше и завершите настройку по его README.
5. Настройте параметры подключения, разрешения и регистрацию устройств или браузерных подписок. Ключи отправки и приватные ключи провайдеров храните на сервере.
6. Подключите отправку уведомлений через REST API с вашего сервера по [документации](https://pushpilot.ru/docs).

Доставка и фоновая обработка зависят от APNs / FCM, браузера, разрешений и ограничений ОС. Установленный SDK сам по себе не подтверждает доставку; особенности silent push и VoIP смотрите в документации выбранной платформы.

<a name="documentation"></a>

## 📚 Документация

| Что подключаете | Где искать инструкцию | Пример |
| :--- | :--- | :--- |
| Нативное приложение для iOS | [iOS SDK README](https://github.com/pushplatform/pushpilot-sdk-ios#readme) | [Приложение iOS](https://github.com/pushplatform/pushpilot-sdk-ios/tree/main/Example) |
| Нативное приложение для Android | [Android SDK README](https://github.com/pushplatform/pushpilot-sdk-android#readme) | [Приложение Android](https://github.com/pushplatform/pushpilot-sdk-android/tree/main/example) |
| Приложение на React Native / Expo | [Установка Expo и bare React Native](https://github.com/pushplatform/pushpilot-sdk-react-native/blob/main/docs/INSTALLATION.md) | [Приложение Expo](https://github.com/pushplatform/pushpilot-sdk-react-native/tree/main/example/expo-app) |
| Приложение на Flutter | [Flutter SDK README](https://github.com/pushplatform/pushpilot-sdk-flutter#readme) | [Приложение Flutter](https://github.com/pushplatform/pushpilot-sdk-flutter/tree/main/example) |
| Сайт или веб-приложение | [Web SDK README](https://github.com/pushplatform/pushpilot-sdk-web#readme) | [npm и script tag](https://github.com/pushplatform/pushpilot-sdk-web/tree/main/example) |

Актуальные требования, параметры подключения и ограничения смотрите в документации конкретного SDK.

## 💬 Обратная связь

Нашли ошибку или хотите предложить улучшение? Создайте **Issue в репозитории соответствующего SDK**.

Укажите платформу, версию SDK, ожидаемый результат и шаги воспроизведения. Не прикладывайте API-ключи, provider credentials или токены устройств.

---

<div align="center">

[PushPilot](https://pushpilot.ru) &nbsp; • &nbsp; [GitHub](https://github.com/pushplatform) &nbsp; • &nbsp; [Все SDK](https://github.com/pushplatform/sdks)

</div>
