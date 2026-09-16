# Оникс

<p align="center">
  <img src="https://img.shields.io/badge/Android-3DDC84?style=plastic&logo=android&logoColor=white" alt="Android">
  <img src="https://img.shields.io/badge/Kotlin-7F52FF?style=plastic&logo=kotlin&logoColor=white" alt="Kotlin">
  <img src="https://img.shields.io/badge/minSdk-26-1976D2?style=plastic" alt="minSdk 26">
  <img src="https://img.shields.io/badge/targetSdk-34-1976D2?style=plastic" alt="targetSdk 34">
  <img src="https://img.shields.io/badge/Material_3-757575?style=plastic" alt="Material 3">
</p>

<p align="center">
  <img src="https://img.shields.io/badge/License-MIT-2EA043?style=plastic" alt="MIT License">
  <img src="https://img.shields.io/badge/Version-1.19-F57C00?style=plastic" alt="Version 1.19">
  <img src="https://img.shields.io/badge/Status-Active-2EA043?style=plastic" alt="Active">
  <img src="https://img.shields.io/badge/Local--First-100%25-9C27B0?style=plastic" alt="Local-First">
</p>

**Голосовые заметки с локальным хранением, Markdown-рендером, графом связей и системой плагинов.**

Оникс — Android-приложение для ведения заметок, вдохновлённое Obsidian. Всё хранится локально на устройстве, без облака и без интернета. Поддерживает ввод голосом и с клавиатуры, расширенный Markdown, автоматические связи между заметками, коллекции, граф знаний и плагины на JavaScript.

---

## Возможности

### Заметки

- **Markdown** — расширенный рендер, близкий к Obsidian:
  - заголовки ATX (`# H1` … `###### H6`) и Setext (`===`, `---`)
  - жирный, курсив, зачёркнутый, инлайн-код
  - подсветка `==text==` — работает вокруг любого контента, включая код и ссылки
  - подчёркнутый через `<u>text</u>`
  - верхний индекс `x^2^`
  - ссылки: обычные `[text](url)`, автоссылки `https://...`, wiki-ссылки `[[Заголовок]]`, определения `[text][ref]`
  - изображения — как `🖼 alt (url)` (без загрузки из сети)
  - маркированные, нумерованные и вложенные списки
  - чек-листы `- [ ]` / `- [x]` — интерактивные, кликабельные, с вложенностью
  - цитаты, включая многострочные
  - HR — три точки `• • •`
  - блоки кода с 10 языками подсветки
  - таблицы GFM
  - определения терминов (`Термин` + `: Определение`)
  - сворачиваемые блоки `<details><summary>`
  - **Callouts Obsidian** — `> [!note]`, `> [!tip]`, `> [!warning]`, `> [!important]`, `> [!caution]` + алиасы (`info`, `danger`, `success`)
- **Блоки кода** — с подписью языка, номерами строк, подсветкой синтаксиса и кнопкой копирования. Поддерживаются Kotlin, Java, JSON, SQL, Bash, Python, JavaScript, XML, Markdown, Excel.
- **Wiki-ссылки** `[[Заголовок]]` — кликабельные, ведут на другую заметку или создают её.
- **Автодополнение wiki-ссылок** и **автодополнение тегов** — по мере ввода.
- **Подсветка wiki-ссылок в редакторе** — существующие цветом `colorPrimary`, несуществующие серым.
- **Коллекции** — ручные группы заметок. Заметка в одной коллекции или ни в одной.
- **Мультивыбор** — долгий тап для выбора нескольких заметок и удаления пачкой.
- **Undo удаления** — снэкбар с обратным отсчётом и круговым прогрессом. Свайп, мультивыбор, меню просмотра — все защищены.
- **Поиск** — по заголовку, телу и тегам. Подсветка совпадений в карточках, «умное» превью вокруг найденного фрагмента.
- **Сортировка** — по дате, алфавиту или числу связей.
- **Счётчик связей** на карточке — видно «узловые» заметки.
- **Справка по Markdown** — встроенный экран со всеми элементами и примерами.

### Плагины

**Расширение функциональности через JavaScript.**

- **Установка из `.zip`** — манифест + код + опционально иконка.
- **Runtime** — Rhino JS (ES5), изолированный поток на плагин.
- **API `oniks`**:
  - `oniks.log` — логирование
  - `oniks.storage` — локальное JSON-хранилище плагина
  - `oniks.commands` — регистрация команд в меню редактора
  - `oniks.editor` — работа с активным редактором (вставка, обёртка выделения)
  - `oniks.notes` — доступ к заметкам (чтение, создание, изменение, удаление, поиск)
  - `oniks.dialog` — показ диалогов `alert` / `confirm`
  - `oniks.renderer` — препроцессор Markdown перед рендером
- **Разрешения** — 7 штук: `read_notes`, `write_notes`, `read_settings`, `ui_panel`, `ui_dialog`, `render_custom`, `commands`. Диалог подтверждения при первом использовании чувствительных разрешений. Отдельный экран управления с возможностью отзыва.
- **Иконки** — из файла `icon.png` в архиве.
- **Встроенная инструкция** — экран со всеми полями манифеста, API, разрешениями, ограничениями и примером.

### Голос

- **Распознавание речи** через `SpeechRecognizer`
- **Live-транскрипт** — текст появляется по мере речи
- **Вставка в позицию курсора** — голос не затирает существующий текст
- **11 языков** на выбор + системный
- **Автозапуск** — из FAB, App Shortcut или Quick Settings Tile голосовой ввод стартует сразу

### Граф знаний

- **Свой алгоритм force-directed** — разделение несвязных компонент, регионы пропорционально размеру
- **Визуальный стиль Obsidian**:
  - рёбра — тонкие кривые Безье с плавным изгибом
  - узлы — полупрозрачная заливка + обводка цвета фона
  - подписи скрываются при zoom-out (declutter)
  - тап по узлу — подсветка узла и соседей, рёбра выделенного становятся цветными, остальное тускнеет
  - повторный тап — открыть заметку
- **Фильтры** — по заголовку и тегам
- **Zoom, pan, double-tap** для сброса масштаба
- **Каскадная анимация** — узлы появляются по BFS-уровням от фокуса
- **Цвет узла** — по первому тегу

### Библиотека

- **Автоматическая кластеризация** — по тегам и ключевым словам
- **Раскрывающиеся секции** — с переименованием и объединением тем
- **Открепление** — убрать заметку из темы, не удаляя тег

### Home и быстрые сценарии

- **Секция «Коллекции»** — горизонтальный ряд иконок папок. Тап → заметки этой коллекции.
- **Последние заметки** — до N свежих (N настраивается: 3 / 5 / 10).
- **FAB «скоростной режим»** — оверлей с выбором «Голос» / «Текст».
- **App Shortcuts** — долгий тап по иконке: «Новая голосовая заметка» / «Новая заметка».
- **Виджет на домашнем экране Android** — две кнопки: голос и текст.
- **Quick Settings Tile** — «Голосовая заметка» в шторке быстрых настроек.
- **Поиск** — из Home в один тап, с автофокусом.

### Настройки

- **Тема** — системная / светлая / тёмная
- **Язык распознавания речи**
- **Автосохранение** — с диалогом «Выйти без сохранения?»
- **Заметок на Главной** — 3 / 5 / 10
- **Коллекции** — экран управления
- **Плагины** — экран управления, разрешения, инструкция
- **Экспорт** — все заметки и коллекции в ZIP
- **Импорт** — из `.md` или `.zip` (с восстановлением коллекций и нормализацией ссылок)
- **О приложении** — версия (динамически из манифеста), автор, лицензия, политика конфиденциальности

### Внешний вид

- **Material 3** — тема `Theme.Material3.DayNight`, все диалоги со скруглением 28dp
- **Dynamic Colors** на Android 12+ — цвета подстраиваются под обои
- **Тёмная тема** — все экраны, включая блоки кода (адаптивная подсветка синтаксиса), граф, callouts
- **Edge-to-edge** — контент учитывает системные бары
- **Splash Screen** — через `core-splashscreen`
- **Анимации карточек** — каскадное появление при загрузке списка
- **Жирные цветные заголовки** тулбаров в цвет иконок
- **Countdown-Snackbar** для Undo с круговым прогрессом

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
| Хранение | Файлы `.md` с YAML frontmatter + `collections.json` + `installed_plugins.json` |
| Асинхронность | Coroutines + Flow |
| Навигация | Single-Activity + Navigation Component |
| UI-компоненты | Material Components 3 |
| Markdown | CommonMark + GFM extensions + кастомный рендер |
| Голос | `SpeechRecognizer` |
| Плагины | Rhino JavaScript Engine (ES5) |
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
org.mozilla:rhino:1.7.14
```

---

## Требования

- Android 8.0+ (API 26)
- Разрешение `RECORD_AUDIO` — для голосового ввода
- Устройство с `SpeechRecognizer` — для голоса (обычно Google-сервисы)

---


## Структура проекта

```
app/src/main/
├── java/com/oniksnotes/
│   ├── OniksApp.kt              # Application, создаёт AppContainer
│   ├── MainActivity.kt          # Единственная Activity
│   ├── data/
│   │   ├── model/               # Note, NoteMeta, Collection, PluginManifest, InstalledPlugin
│   │   ├── markdown/            # NoteSerializer, YamlFrontMatter
│   │   ├── repository/          # NoteRepository, CollectionRepository, PluginRepository
│   │   ├── settings/            # SettingsRepository, ThemeMode, LanguageMode
│   │   └── speech/              # SpeechRecognitionManager, SpeechState
│   ├── domain/
│   │   ├── links/               # LinksCalculator, KeywordExtractor, LinksCache
│   │   ├── export/              # ExportManager, ImportManager
│   │   ├── deletion/            # DeletionManager (Undo удаления)
│   │   └── plugins/             # PluginInstaller, PluginManager, PluginRuntime,
│   │                            # PluginApi, PluginStorage, PluginPermissionStore,
│   │                            # EditorBridge, PluginDialogBridge,
│   │                            # PermissionRequestBridge, PluginCommand
│   ├── di/
│   │   └── AppContainer.kt      # Ручной DI
│   └── ui/
│       ├── home/                # HomeFragment, QuickCreateDialogFragment, HomeCollectionsAdapter
│       ├── notes/               # NotesFragment, NoteAdapter, SwipeActionsCallback
│       ├── editor/              # EditNoteFragment, WikiAutocompleteController, TagAutocompleteController
│       ├── viewer/              # ViewNoteFragment
│       ├── voice/               # VoiceInputFragment
│       ├── graph/               # GraphView, ForceDirectedLayout, GraphFragment
│       ├── library/             # LibraryClustering, LibraryFragment
│       ├── collections/         # CollectionsFragment, CollectionsViewModel, CollectionsAdapter
│       ├── plugins/             # PluginsFragment, PluginsAdapter, PluginsViewModel,
│       │                        # PluginDetailsDialogFragment, PluginInstallDialogFragment,
│       │                        # PluginPermissionsFragment, PluginDialogFragment,
│       │                        # PermissionRequestDialogFragment
│       ├── guide/               # MarkdownGuideFragment, PluginGuideFragment
│       ├── settings/            # SettingsFragment, AboutFragment, PrivacyPolicyDialogFragment
│       ├── tile/                # QuickVoiceNoteTileService
│       ├── widget/              # QuickNoteWidgetProvider
│       └── common/              # AudioPermissionHelper, UndoSnackbarHelper
├── res/
│   ├── anim/                    # Анимации
│   ├── drawable/                # Векторные иконки
│   ├── layout/                  # XML-вёрстка
│   ├── menu/                    # Меню тулбара и BottomNavigation
│   ├── mipmap-*/                # Иконка приложения
│   ├── navigation/              # nav_graph.xml
│   ├── values/                  # colors, strings, themes, styles, arrays
│   ├── values-night/            # Тёмная тема
│   └── xml/                     # settings.xml, shortcuts.xml, widget info
└── AndroidManifest.xml
```

---

## Формат хранения

Каждая заметка — файл `<uuid>.md` в `filesDir/notes/` с YAML frontmatter:


```yaml
title: Заголовок заметки
tags: [работа, идеи]
created: 1700000000000
updated: 1700000000000
pinned: false
collection: 550e8400-e29b-41d4-a716-446655440000
```

---

Тело заметки в Markdown

☐ Чек-лист
☑ Выполненный пункт

[!tip] Совет
Callouts тоже поддерживаются.

```kotlin
fun main() = println("Hello, Oniks")
```

```

### Коллекции

```filesDir/collections.json```, TSV:

```
<uuid>\t<имя>\t<порядок>\t<создано>
```

### Плагины

- Реестр: `filesDir/installed_plugins.json`
- Содержимое: `filesDir/plugins/<id>/`
- Разрешения: `filesDir/plugins/<id>/data/permissions.json`
- Локальное хранилище: `filesDir/plugins/<id>/data/storage.json`

---

## Плагины

### Формат

`.zip`-архив с плоской структурой:

```
my-plugin.zip
├── manifest.json     (обязательно)
├── main.js           (обязательно)
├── icon.png          (опционально)
└── ...               (любые дополнительные файлы)
```

### Манифест

```json
{
  "id": "com.example.myplugin",
  "name": "Мой плагин",
  "version": "1.0.0",
  "author": "Иван",
  "description": "Краткое описание.",
  "apiVersion": 1,
  "entry": "main.js",
  "icon": "icon.png",
  "permissions": ["commands", "read_notes"]
}
```

### Пример плагина

**manifest.json:**

```json
{
  "id": "com.example.date",
  "name": "Вставить дату",
  "version": "1.0.0",
  "author": "Иван",
  "apiVersion": 1,
  "entry": "main.js",
  "permissions": ["commands"]
}
```

**main.js:**
```javascript
oniks.commands.register({
    id: "insert-date",
    title: "Вставить дату",
    handler: function () {
        var d = new Date();
        var day = ("0" + d.getDate()).slice(-2);
        var month = ("0" + (d.getMonth() + 1)).slice(-2);
        oniks.editor.insertText(day + "." + month + "." + d.getFullYear());
    }
});
```

### Разрешения

| Разрешение | Что даёт |
|---|---|
| `read_notes` | Чтение заметок |
| `write_notes` | Изменение заметок (диалог подтверждения) |
| `read_settings` | Чтение настроек (зарезервировано) |
| `ui_panel` | Дополнительные панели (зарезервировано) |
| `ui_dialog` | Показ диалогов |
| `render_custom` | Препроцессор Markdown |
| `commands` | Регистрация команд |
| `graph_style` | Стилизация графа |

### Ограничения

- **JavaScript ES5.** Не поддерживаются: `let`, `const`, стрелочные функции, template literals, `class`, `import`/`export`, spread, destructuring.
- Нет доступа к Java-классам, файловой системе, сети.
- Один поток на плагин.

### Что может плагин

- Добавлять команды в меню редактора.
- Вставлять/менять текст в редакторе.
- Создавать, читать, обновлять, удалять заметки.
- Показывать диалоги.
- Преобразовывать текст заметки перед рендером.
- Менять цвет, размер, обводку узлов и рёбер графа, подписи.

---

### Автор
**Mikihisa**

### По вопросам: 
phreakO7@mail.ru
