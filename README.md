# AI Конструктор

Android-приложение (Kotlin), которое превращает описание на русском языке в готовое веб-приложение: вы пишете «сделай калькулятор» — ИИ присылает полный HTML-файл, и он сразу открывается во встроенном предпросмотре.

## Как это работает

- Одна Activity с WebView на весь экран; интерфейс — чистый HTML/JS из `app/src/main/assets/index.html`.
- Страницы раздаются из assets через [WebViewAssetLoader](https://developer.android.com/reference/androidx/webkit/WebViewAssetLoader) (`androidx.webkit`), включены JavaScript и DOM storage (настройки, чат и текущий проект хранятся в localStorage).
- Слева — чат с ИИ, справа — iframe-предпросмотр. Можно просить правки: текущий HTML передаётся модели, и она возвращает файл целиком.
- Поддерживаемые провайдеры (ключ хранится только на устройстве):
  - **Claude** — `https://api.anthropic.com/v1/messages`, заголовки `x-api-key`, `anthropic-version: 2023-06-01`, `anthropic-dangerous-direct-browser-access: true`;
  - **OpenAI** и **любой OpenAI-совместимый** (другой) — формат `chat/completions`, настраиваемый Base URL.

## Сборка

Требуется JDK 17 и Android SDK (compileSdk 34, minSdk 24).

```bash
gradle assembleDebug
```

APK: `app/build/outputs/apk/debug/app-debug.apk`.

## Сборка на GitHub Actions

Workflow [.github/workflows/build.yml](.github/workflows/build.yml) собирает debug APK на каждый push и выкладывает его как артефакт `ai-builder-debug-apk`.

## Скачать APK

1. Откройте вкладку **Actions** в репозитории.
2. Выберите последний успешный запуск **Build APK**.
3. В разделе **Artifacts** скачайте **ai-builder-debug-apk**, распакуйте архив и установите `app-debug.apk` на устройство (разрешите установку из неизвестных источников).
