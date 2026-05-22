# Сборка и установка без Android Studio

## Способ 1 — GitHub (рекомендуется, всё в облаке)

Нужны только браузер и бесплатный аккаунт GitHub.

### 1. Загрузите проект на GitHub

1. Зарегистрируйтесь на [github.com](https://github.com), если ещё нет аккаунта.
2. Создайте новый репозиторий (например `ssm-apk`), **без** README.
3. На компьютере откройте PowerShell в папке проекта:

```powershell
cd c:\Users\xio\Desktop\apk
git init
git add .
git commit -m "WebView app"
git branch -M main
git remote add origin https://github.com/ВАШ_ЛОГИН/ssm-apk.git
git push -u origin main
```

(При первом push GitHub попросит войти в аккаунт.)

### 2. Соберите APK в облаке

1. На GitHub откройте ваш репозиторий → вкладка **Actions**.
2. Слева выберите workflow **Build APK** → **Run workflow** → **Run workflow**.
3. Подождите 5–10 минут (зелёная галочка).
4. Внизу страницы запуска в блоке **Artifacts** скачайте **SSM-debug-apk** (внутри файл `app-debug.apk`).

При каждом изменении кода и `git push` APK пересоберётся автоматически.

### 3. Установите на телефон

1. Перешлите `app-debug.apk` себе (Telegram, WhatsApp, USB в папку «Загрузки»).
2. Откройте файл на телефоне → **Установить**.
3. Если просит — разрешите установку из этого источника (Файлы / Telegram и т.д.).

**Важно:** сайт `http://192.168.0.179:9664` откроется только если телефон в **той же Wi‑Fi сети**, что и компьютер с сервером. Иначе укажите публичный адрес сайта в `strings.xml`.

---

## Способ 2 — только командная строка на Windows

Без Android Studio, но нужно один раз поставить SDK и Java.

### 1. Java 17

Скачайте и установите [Eclipse Temurin JDK 17](https://adoptium.net/temurin/releases/?version=17&os=windows&arch=x64).

Проверка:

```powershell
java -version
```

Должно быть `17`, не `1.8`.

### 2. Android SDK (командные инструменты)

1. Скачайте [Command line tools for Windows](https://developer.android.com/studio#command-line-tools-only) (zip).
2. Распакуйте, например в `C:\Android\cmdline-tools\latest\` (внутри должна быть папка `bin` с `sdkmanager.bat`).
3. В PowerShell:

```powershell
$env:ANDROID_HOME = "C:\Android\Sdk"
New-Item -ItemType Directory -Force -Path $env:ANDROID_HOME

& "C:\Android\cmdline-tools\latest\bin\sdkmanager.bat" --sdk_root=$env:ANDROID_HOME "platform-tools" "platforms;android-35" "build-tools;35.0.0"
```

Ответьте `y` на лицензии.

### 3. Сборка APK

```powershell
cd c:\Users\xio\Desktop\apk

@"
sdk.dir=C\:\\Android\\Sdk
"@ | Set-Content -Encoding UTF8 local.properties

.\gradlew.bat assembleDebug
```

APK: `app\build\outputs\apk\debug\app-debug.apk`

---

## Установка на телефон (кратко)

| Действие | Как |
|----------|-----|
| Перенести APK | Telegram «Избранное», USB, облако |
| Установить | Открыть файл → Установить |
| Ошибка «не установлено» | Удалите старую версию приложения SSM |

Отладка по USB и `adb` **не обязательны** — достаточно скопировать APK на телефон.
