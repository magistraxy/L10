# 📱 Инструкция по сборке APK для Android

## Способ 1: Облачная сборка (САМЫЙ ПРОСТОЙ - БЕЗ УСТАНОВКИ)

### Через Adobe PhoneGap Build (РЕКОМЕНДУЕТСЯ)

**Шаг 1: Подготовьте файлы**
1. Скачайте ваше веб-приложение (index.html)
2. Скачайте файл `config.xml` (конфигурация для Cordova)
3. Создайте на компьютере папку:
   ```
   sign-language-app/
   ├── index.html
   └── config.xml
   ```

**Шаг 2: Загрузите на PhoneGap Build**
1. Перейдите на https://build.phonegap.com/
2. Нажмите "Sign up" (зарегистрируйтесь через GitHub или Adobe ID)
3. Нажмите "+ New App"
4. Выберите "Upload a .zip file"
5. Создайте архив из папки `sign-language-app` (ZIP):
   - В Windows: правый клик на папку → "Отправить" → "Сжатая папка"
   - На Mac: правый клик на папку → "Сжать"
   - На Linux: `zip -r sign-language-app.zip sign-language-app/`
6. Загрузите этот ZIP на PhoneGap Build
7. Выберите платформу **Android**
8. Нажмите **"Build"**
9. Дождитесь завершения (2-5 минут)
10. Скачайте готовый APK файл

**Шаг 3: Установите на телефон**
1. Скачайте APK на Android-смартфон
2. Откройте файловый менеджер
3. Нажмите на APK файл
4. Разрешите установку из неизвестных источников (если спросит)
5. Приложение установится ✓

---

## Способ 2: Локальная сборка (С УСТАНОВКОЙ Node.js И Android Studio)

### Предварительные требования:
- Node.js (https://nodejs.org/)
- Java JDK 8+ (https://www.oracle.com/java/technologies/downloads/)
- Android SDK (встроен в Android Studio)

### Шаг 1: Установите Cordova

```bash
npm install -g cordova
```

### Шаг 2: Создайте проект

```bash
cordova create sign-language-app com.signlanguage.translator "Sign Language Translator"
cd sign-language-app
```

### Шаг 3: Добавьте платформу Android

```bash
cordova platform add android
```

### Шаг 4: Замените файлы

1. Скопируйте ваш `index.html` в папку `www/`
   ```
   sign-language-app/
   └── www/
       └── index.html
   ```

2. Замените `config.xml` на загруженный файл

### Шаг 5: Сройте APK

```bash
cordova build android
```

Готовый APK будет в:
```
sign-language-app/platforms/android/app/build/outputs/apk/debug/app-debug.apk
```

### Шаг 6: Установите на устройство

Подключите Android-смартфон по USB и выполните:
```bash
cordova run android
```

Или установите вручную, скопировав APK файл на телефон.

---

## Способ 3: Через Android Studio (ПРОФЕССИОНАЛЬНЫЙ)

### Шаг 1: Откройте проект в Android Studio

1. Откройте Android Studio
2. File → Open → выберите папку `sign-language-app/platforms/android`

### Шаг 2: Подождите синхронизацию Gradle

Android Studio автоматически загрузит все зависимости (2-5 минут)

### Шаг 3: Соберите приложение

1. Build → Build Bundle(s) / APK(s) → Build APK(s)
2. Дождитесь завершения

### Шаг 4: Найдите APK

```
app/build/outputs/apk/debug/app-debug.apk
```

---

## 📲 Установка APK на телефон

### Способ 1: По USB кабелю
1. Подключите телефон к ПК кабелем USB
2. Включите режим разработчика (Settings → About Phone → Version → нажмите 7 раз на Build Number)
3. Откройте командную строку в папке с APK
4. Выполните: `adb install app-debug.apk`
5. Приложение установится автоматически

### Способ 2: По Bluetooth/облаку
1. Отправьте APK по email или Telegram себе
2. Скачайте на телефон
3. Откройте файловый менеджер и нажмите на APK
4. Подтвердите установку

### Способ 3: Через Google Play (если публикуете)
1. Создайте аккаунт разработчика Google Play ($25)
2. Загрузите подписанный APK
3. Опубликуйте приложение
4. Установите из Google Play Store

---

## 🔑 Подписание APK для продажи

Для публикации в Google Play нужен подписанный APK:

```bash
jarsigner -verbose -sigalg MD5withRSA -digestalg SHA1 \
  -keystore my-key.keystore app-debug.apk alias_name
```

Затем оптимизируйте:
```bash
zipalign -v 4 app-debug.apk app-release.apk
```

---

## ⚙️ Решение проблем

### Ошибка: "Android SDK not found"
- Установите Android Studio с встроенным SDK
- Установите Java JDK

### Ошибка: "cordova is not recognized"
- Переустановите Node.js
- Запустите `npm install -g cordova` заново

### Микрофон не работает в приложении
- В AndroidManifest.xml добавьте разрешение:
  ```xml
  <uses-permission android:name="android.permission.RECORD_AUDIO" />
  <uses-permission android:name="android.permission.INTERNET" />
  ```

### Приложение медленно запускается
- Это нормально для первого запуска
- Кэширование улучшает скорость

---

## 📊 Сравнение способов

| Способ | Сложность | Время | Требования | Результат |
|--------|-----------|-------|-----------|----------|
| PhoneGap Build | ⭐ Низкая | 5 мин | Браузер | APK готов |
| Локальная Cordova | ⭐⭐ Средняя | 20 мин | Node.js | APK готов |
| Android Studio | ⭐⭐⭐ Высокая | 1 час | Studio + SDK | APK + исходники |

**Рекомендуем: Способ 1 (PhoneGap Build)** - самый быстрый и не требует установок!

---

## 💾 Скачивание готовых файлов

Используйте эти файлы:
1. `index.html` - ваше веб-приложение
2. `config.xml` - конфигурация Cordova
3. Архивируйте оба в ZIP
4. Загрузите на PhoneGap Build

Готово! 🎉
