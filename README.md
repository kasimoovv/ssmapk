# APK с вашим сайтом

Простое Android-приложение: открывает ваш сайт во встроенном браузере (WebView).

## 1. Укажите адрес сайта

Откройте файл `app/src/main/res/values/strings.xml` и замените URL:

```xml
<string name="site_url">https://ваш-сайт.ru</string>
```

При желании измените название приложения:

```xml
<string name="app_name">Название</string>
```

## 2. Сборка APK

### Без Android Studio

См. подробную инструкцию: **[СБОРКА_БЕЗ_STUDIO.md](СБОРКА_БЕЗ_STUDIO.md)**

- **GitHub Actions** — загрузить проект на GitHub, вкладка Actions → Run workflow → скачать APK (ничего не ставить на ПК).
- **Командная строка** — JDK 17 + Android SDK command-line tools + `gradlew.bat assembleDebug`.

### С Android Studio

1. Установите [Android Studio](https://developer.android.com/studio).
2. **File → Open** → папка `apk`.
3. **Build → Build APK(s)** → `app/build/outputs/apk/debug/app-debug.apk`.

## 3. Установка на телефон

- Скопируйте APK на телефон и откройте файл, или
- Подключите USB, включите «Отладка по USB», выполните: `adb install app-debug.apk`

## Возможности

- Полноэкранный сайт без адресной строки
- Кнопка «Назад» листает историю внутри сайта
- Поддержка http и https
- JavaScript и localStorage включены
