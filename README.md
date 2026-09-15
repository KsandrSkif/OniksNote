# Оникс

![Platform](https://img.shields.io/badge/platform-Android-3DDC84?logo=android&logoColor=white&style=flat-square)
![Min SDK](https://img.shields.io/badge/minSdk-26-blue?style=flat-square)
![Target SDK](https://img.shields.io/badge/targetSdk-34-blue?style=flat-square)
![Kotlin](https://img.shields.io/badge/Kotlin-1.9-7F52FF?logo=kotlin&logoColor=white&style=flat-square)
![License](https://img.shields.io/badge/license-MIT-green?style=flat-square)
![Version](https://img.shields.io/badge/version-1.0-orange?style=flat-square)
![Status](https://img.shields.io/badge/status-active-brightgreen?style=flat-square)

**Голосовые заметки с локальным хранением, Markdown-рендером и графом связей.**

Оникс — Android-приложение для ведения заметок, вдохновлённое Obsidian. Всё хранится локально на устройстве, без облака и без интернета. Поддерживает ввод голосом и с клавиатуры, Markdown с подсветкой кода, автоматические связи между заметками и граф знаний.

---

## Возможности

### Заметки
- **Markdown** — заголовки, списки, чек-листы, цитаты, ссылки, таблицы, блоки кода
- **Блоки кода** — с подписью языка, номерами строк, подсветкой синтаксиса и кнопкой копирования (Kotlin, Java, JSON, SQL, Bash, Python, JavaScript, XML, Markdown, Excel)
- **Чек-листы** — интерактивные, кликабельные прямо в просмотре
- **Wiki-ссылки** `[[Заголовок]]` — кликабельные, ведут на другую заметку или создают её
- **Теги** — группировка, фильтрация, переименование, объединение тем
- **Закрепление** — важные заметки всегда сверху
- **Свайпы** — влево удалить, вправо закрепить/открепить
- **Мультивыбор** — долгий тап для выбора нескольких заметок и удаления пачкой

### Голос
- **Распознавание речи** через `SpeechRecognizer`
- **Live-транскрипт** — текст появляется по мере речи
- **Вставка в позицию курсора** — голос не затирает существующий текст
- **11 языков** на выбор + системный
- **Автозапуск** — из FAB или App Shortcut голосовой ввод стартует сразу

### Граф знаний
- **Force-directed раскладка** — свой алгоритм, без сторонних библиотек
- **Связи** — по общим тегам, ключевым словам и wiki-ссылкам
- **Фильтры** — по заголовку и тегам
- **Zoom, pan, тап** — открыть заметку из графа
- **Каскадная анимация** — узлы появляются по BFS-уровням от фокуса
- **Цвет узла** — по первому тегу (детерминированный маппинг)

### Библиотека
- **Автоматическая кластеризация** — по тегам и ключевым словам
- **Раскрывающиеся секции** — с переименованием и объединением тем
- **Открепление** — убрать заметку из темы, не удаляя тег

### Home и быстрые сценарии
- **Последние заметки** — до 5 свежих на главном экране
- **FAB «скоростной режим»** — оверлей с выбором «Голос» / «Текст»
- **App Shortcuts** — долгий тап по иконке: «Новая голосовая заметка» / «Новая заметка»
- **Поиск** — из Home в один тап, с автофокусом

### Настройки
- **Тема** — системная / светлая / тёмная
- **Язык распознавания речи**
- **Автосохранение** — с диалогом «Выйти без сохранения?»
- **Экспорт** — все заметки в ZIP (Markdown + YAML frontmatter)
- **Импорт** — из `.md` или `.zip`

### Внешний вид
- **Material 3** — тема `Theme.Material3.DayNight`
- **Dynamic Colors** на Android 12+ — цвета подстраиваются под обои
- **Edge-to-edge** — контент учитывает системные бары
- **Тёмная тема** — все экраны, включая блоки кода и граф
- **Splash Screen** — через `core-splashscreen`

---

## Скриншоты

| Home | Заметки | Просмотр |
|---|---|---|
|![Home](https://github.com/KsandrSkif/OniksNote/releases/download/V1/1.jpg)|![Заметки](https://github.com/KsandrSkif/OniksNote/releases/download/V1/3.jpg)|![Просмотр](https://github.com/KsandrSkif/OniksNote/releases/download/V1/8.jpg)|

| Граф | Библиотека | Настройки |
|---|---|---|
|![Граф](https://github.com/KsandrSkif/OniksNote/releases/download/V1/6.jpg)|![Библиотека](https://github.com/KsandrSkif/OniksNote/releases/download/V1/7.jpg)|![Настройки](https://github.com/KsandrSkif/OniksNote/releases/download/V1/5.jpg)|

---

## Технологии

| Компонент | Технология |
|---|---|
| Язык | Kotlin |
| UI | XML + View-система (без Compose) |
| Архитектура | MVVM + Clean (`data/`, `domain/`, `ui/`) |
| Хранение | Файлы `.md` с YAML frontmatter в `filesDir/notes/` |
| Асинхронность | Coroutines + Flow |
| Навигация | Single-Activity + Navigation Component |
| UI-компоненты | Material Components 3 |
| Markdown | CommonMark + GFM extensions |
| Голос | `SpeechRecognizer` |
| DI | Ручной `AppContainer` (без Hilt/Dagger) |

### Стек библиотек

```
androidx.core:core-ktx:1.13.1
androidx.appcompat:appcompat:1.7.0
com.google.android.material:material:1.12.0
androidx.constraintlayout:constraintlayout:2.1.4
androidx.activity:activity-ktx:1.9.3
androidx.fragment:fragment-ktx:1.8.5
androidx.lifecycle:lifecycle-viewmodel-ktx:2.8.7
androidx.lifecycle:lifecycle-runtime-ktx:2.8.7
androidx.lifecycle:lifecycle-viewmodel-savedstate:2.8.7
androidx.navigation:navigation-fragment-ktx:2.8.4
androidx.navigation:navigation-ui-ktx:2.8.4
org.jetbrains.kotlinx:kotlinx-coroutines-core:1.9.0
org.jetbrains.kotlinx:kotlinx-coroutines-android:1.9.0
androidx.recyclerview:recyclerview:1.3.2
androidx.preference:preference-ktx:1.2.1
androidx.core:core-splashscreen:1.0.1
org.commonmark:commonmark:0.22.0
org.commonmark:commonmark-ext-gfm-strikethrough:0.22.0
org.commonmark:commonmark-ext-gfm-tables:0.22.0
```

---

## Требования

- Android 8.0+ (API 26)
- Разрешение `RECORD_AUDIO` — для голосового ввода
- Устройство с `SpeechRecognizer` — для голоса (обычно Google-сервисы)

---

## Сборка

Проект собирается в **CodeAssist** (мобильная IDE) — без Gradle.

1. Открой проект в CodeAssist.
2. Добавь зависимости через раздел **Модуль app → Зависимости → «+»** (список выше, по одной).
3. Включи **View Binding** в настройках модуля.
4. Собери APK кнопкой сборки.

Если собираешь в Android Studio — создай `build.gradle.kts` с теми же зависимостями, `namespace = "com.oniksnotes"`, `minSdk = 26`, `targetSdk = 34`, `viewBinding = true`.

---

## Структура проекта

```
app/src/main/
├── java/com/oniksnotes/
│   ├── OniksApp.kt              # Application, создаёт AppContainer
│   ├── MainActivity.kt          # Единственная Activity
│   ├── data/
│   │   ├── model/               # Note, NoteMeta
│   │   ├── markdown/            # NoteSerializer, YamlFrontMatter
│   │   ├── repository/          # NoteRepository, FileNoteRepository
│   │   ├── settings/            # SettingsRepository, ThemeMode, LanguageMode
│   │   └── speech/              # SpeechRecognitionManager, SpeechState
│   ├── domain/
│   │   ├── links/               # LinksCalculator, KeywordExtractor, LinksCache
│   │   └── export/              # ExportManager, ImportManager
│   ├── di/
│   │   └── AppContainer.kt      # Ручной DI
│   └── ui/
│       ├── home/                # HomeFragment, QuickCreateDialogFragment
│       ├── notes/               # NotesFragment, NoteAdapter
│       ├── editor/              # EditNoteFragment, WikiAutocomplete
│       ├── viewer/              # ViewNoteFragment, MarkdownRenderer
│       ├── voice/               # VoiceInputFragment
│       ├── graph/               # GraphView, ForceDirectedLayout
│       ├── library/             # LibraryClustering, LibraryFragment
│       ├── settings/            # SettingsFragment, AboutFragment
│       └── common/              # AudioPermissionHelper
├── res/
│   ├── anim/                    # Анимации (появление карточек)
│   ├── drawable/                # Свои векторные иконки
│   ├── layout/                  # XML-вёрстка экранов и элементов
│   ├── menu/                    # Меню тулбара и BottomNavigation
│   ├── mipmap-*/                # Иконка приложения
│   ├── navigation/              # nav_graph.xml
│   ├── values/                  # colors, strings, themes, styles, arrays
│   └── xml/                     # settings.xml, shortcuts.xml, backup_rules
└── AndroidManifest.xml
```

---

## Формат хранения

Каждая заметка — файл `<uuid>.md` в `filesDir/notes/` с YAML frontmatter:

---

- title: Заголовок заметки
- tags: [работа, идеи]
- created: 1700000000000
- updated: 1700000000000
- pinned: false

---

## Тело заметки в Markdown

- [ ] Чек-лист
- [x] Выполненный пункт

```kotlin
fun main() = println("Hello, Oniks")
```

Заголовок хранится внутри YAML, а не в имени файла. Это гарантирует отсутствие коллизий и корректный экспорт/импорт.

---

Лицензия

MIT License. См. LICENSE.

---

### Автор
**Mikihisa**

### По вопросам: 
phreakO7@mail.ru


---

**LICENSE**:


MIT License

Copyright (c) 2026 Mikihisa

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.