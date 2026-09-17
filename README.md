## Description EN / [RU](#oniks-ru)

# Oniks

<p align="center">
  <img src="https://img.shields.io/badge/Android-3DDC84?style=plastic&logo=android&logoColor=white" alt="Android">
  <img src="https://img.shields.io/badge/Kotlin-7F52FF?style=plastic&logo=kotlin&logoColor=white" alt="Kotlin">
  <img src="https://img.shields.io/badge/minSdk-26-1976D2?style=plastic" alt="minSdk 26">
  <img src="https://img.shields.io/badge/targetSdk-34-1976D2?style=plastic" alt="targetSdk 34">
  <img src="https://img.shields.io/badge/Material_3-757575?style=plastic" alt="Material 3">
</p>

<p align="center">
  <img src="https://img.shields.io/badge/License-MIT-2EA043?style=plastic" alt="MIT License">
  <img src="https://img.shields.io/badge/Version-1.24-F57C00?style=plastic" alt="Version 1.24">
  <img src="https://img.shields.io/badge/Status-Active-2EA043?style=plastic" alt="Active">
  <img src="https://img.shields.io/badge/Local--First-100%25-9C27B0?style=plastic" alt="Local-First">
</p>

**Voice notes with local storage, Markdown rendering, a knowledge graph, and a plugin system.**

Oniks is an Android note-taking app inspired by Obsidian. Everything is stored locally on your device — no cloud, no internet. It supports voice and keyboard input, extended Markdown, automatic links between notes, collections, a knowledge graph, and plugins written in JavaScript.

---

## Features

### Notes

- **Markdown** — extended renderer, close to Obsidian:
  - ATX headings (`# H1` … `###### H6`) and Setext headings (`===`, `---`)
  - bold, italic, strikethrough, inline code
  - highlight `==text==` — works around any content
  - underline via `<u>text</u>`
  - superscript `x^2^`
  - links: regular `[text](url)`, auto-links, wiki-links `[[Title]]`, reference links `[text][ref]`
  - images — shown as `🖼 alt (url)` (no network loading)
  - bulleted, numbered, and nested lists
  - checklists `- [ ]` / `- [x]` — interactive, clickable, with nesting
  - blockquotes, including multi-paragraph
  - HR — three dots `• • •`
  - code blocks with 10 languages of syntax highlighting
  - GFM tables
  - definition lists
  - collapsible blocks `<details><summary>`
  - **Obsidian Callouts** — `> [!note]`, `> [!tip]`, `> [!warning]`, `> [!important]`, `> [!caution]` + aliases
- **Code blocks** — language label, line numbers, syntax highlighting, copy button. Kotlin, Java, JSON, SQL, Bash, Python, JavaScript, XML, Markdown, Excel.
- **Wiki-links** — clickable, navigate to another note or create it.
- **Autocomplete** for wiki-links and tags.
- **Wiki-link highlighting in the editor**.
- **Collections** — manual note groups.
- **Multi-select** — long-press to select multiple notes.
- **Undo delete** — countdown Snackbar with circular progress.
- **Search** — by title, body, tags. Match highlighting and smart preview.
- **Sorting** — by date, alphabet, or link count.
- **Link counter** on each card.
- **Markdown guide** — built-in screen with all elements.

### Plugins

**Extending functionality via JavaScript.**

- **Install from `.zip`** — manifest + code + optional icon.
- **Runtime** — Rhino JS (ES5), isolated thread per plugin.
- **`oniks` API — 15 namespaces, 60 methods:**
  - `oniks.log` — logging
  - `oniks.storage` — local JSON storage
  - `oniks.commands` — commands in the editor menu
  - `oniks.editor` — work with the active editor (including `getNoteId`)
  - `oniks.notes` — notes (read / write / search), including `getAllWithBody`, `getRecent`, `getPinned`
  - `oniks.dialog` — `alert` / `confirm`
  - `oniks.renderer` — Markdown preprocessor
  - `oniks.graph` — graph styling (`nodeStyler`, `edgeStyler`, `labelStyler`)
  - `oniks.settings` — read app settings
  - `oniks.clipboard` — system clipboard
  - `oniks.share` — system "Share" dialog
  - `oniks.markdown` — Markdown parsing (no rendering)
  - `oniks.events` — subscribe to app events
  - `oniks.collections` — collections (create / rename / delete)
  - `oniks.ui` — UI navigation (`openNote`)
- **Permissions** — 12 in total. Confirmation dialog for `write_notes`, management screen with revocation.
- **Icons** from `icon.png` in the archive — in the list, install overlay, and details overlay.
- **Built-in guide** — all manifest fields, API, permissions, limitations, example.
- **Full API reference** — see [PLUGIN_API.md](PLUGIN_API.md).

### Voice

- **Speech recognition** via `SpeechRecognizer`
- **Live transcript** — text appears as you speak
- **Insert at cursor position** — voice doesn't overwrite existing text
- **11 languages** to choose from + system default
- **Auto-start** — from the FAB, App Shortcut, or Quick Settings Tile, voice input starts immediately

### Knowledge graph

- **Custom force-directed algorithm** — separates disconnected components, regions proportional to size
- **Obsidian-style visuals**:
  - edges — thin Bezier curves with smooth bend
  - nodes — semi-transparent fill + background-colored outline
  - labels hidden on zoom-out (declutter)
  - tap on a node — highlights the node and its neighbors, the selected node's edges become colored, everything else fades
  - second tap — open the note
- **Filters** — by title and tags
- **Zoom, pan, double-tap** to reset scale
- **Cascade animation** — nodes appear by BFS levels from the focus
- **Node color** — based on the first tag

### Library

- **Automatic clustering** — by tags and keywords
- **Expandable sections** — with renaming and merging of topics
- **Detach** — remove a note from a topic without deleting its tag

### Home and quick scenarios

- **Collections section** — horizontal row of folder icons. Tap → notes in that collection.
- **Recent notes** — up to N latest (N configurable: 3 / 5 / 10).
- **FAB "quick mode"** — overlay with "Voice" / "Text" choice.
- **App Shortcuts** — long-press the icon: "New voice note" / "New note".
- **Home screen widget** — two buttons: voice and text.
- **Quick Settings Tile** — "Voice note" in the quick settings panel.
- **Search** — from Home in one tap, with autofocus.

### Settings

- **Theme** — system / light / dark
- **App language** — system / Russian / English
- **Speech recognition language**
- **Autosave** — with an "Exit without saving?" dialog
- **Notes on Home** — 3 / 5 / 10
- **Collections** — management screen
- **Plugins** — management screen, permissions, guide
- **Export** — all notes and collections to ZIP
- **Import** — from `.md` or `.zip` (with collection restoration and link normalization)
- **About** — version (dynamically from the manifest), author, license, privacy policy

### Appearance

- **Material 3** — `Theme.Material3.DayNight`, all dialogs with 28dp corner radius
- **Dynamic Colors** on Android 12+ — colors adapt to wallpapers
- **Dark theme** — all screens, including code blocks (adaptive syntax highlighting), graph, callouts
- **Edge-to-edge** — content respects system bars
- **Splash Screen** — via `core-splashscreen`
- **Card animations** — cascade appearance when the list loads
- **Bold colored toolbar titles** in icon color
- **Countdown Snackbar** for Undo with circular progress

---

## Screenshots

| Home | Notes | Viewer |
|---|---|---|
|![Home](https://github.com/KsandrSkif/OniksNote/releases/download/V1/1.jpg)|![Notes](https://github.com/KsandrSkif/OniksNote/releases/download/V1/3.jpg)|![Viewer](https://github.com/KsandrSkif/OniksNote/releases/download/V1/8.jpg)|

| Graph | Library | Settings |
|---|---|---|
|![Graph](https://github.com/KsandrSkif/OniksNote/releases/download/V1/6.jpg)|![Library](https://github.com/KsandrSkif/OniksNote/releases/download/V1/7.jpg)|![Settings](https://github.com/KsandrSkif/OniksNote/releases/download/V1/5.jpg)|

---

## Technologies

| Component | Technology |
|---|---|
| Language | Kotlin |
| UI | XML + View system (no Compose) |
| Architecture | MVVM + Clean (`data/`, `domain/`, `ui/`) |
| Storage | `.md` files with YAML frontmatter + `collections.json` + `installed_plugins.json` |
| Async | Coroutines + Flow |
| Navigation | Single-Activity + Navigation Component |
| UI components | Material Components 3 |
| Markdown | CommonMark + GFM extensions + custom renderer |
| Voice | `SpeechRecognizer` |
| Plugins | Rhino JavaScript Engine (ES5) |
| DI | Manual `AppContainer` (no Hilt/Dagger) |

### Library stack

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

## Requirements

- Android 8.0+ (API 26)
- `RECORD_AUDIO` permission — for voice input
- Device with `SpeechRecognizer` — for voice (usually Google services)

---

## Project structure

```
app/src/main/
├── java/com/oniksnotes/
│   ├── OniksApp.kt
│   ├── MainActivity.kt
│   ├── data/
│   │   ├── model/               # Note, NoteMeta, Collection, PluginManifest, InstalledPlugin
│   │   ├── markdown/            # NoteSerializer, YamlFrontMatter
│   │   ├── repository/          # NoteRepository, CollectionRepository, PluginRepository
│   │   ├── settings/            # SettingsRepository, ThemeMode, LanguageMode, AppLanguage
│   │   └── speech/              # SpeechRecognitionManager, SpeechState
│   ├── domain/
│   │   ├── links/               # LinksCalculator, KeywordExtractor, LinksCache
│   │   ├── export/              # ExportManager, ImportManager
│   │   ├── deletion/            # DeletionManager
│   │   └── plugins/             # PluginInstaller, PluginManager, PluginRuntime,
│   │                            # PluginApi, PluginStorage, PluginPermissionStore,
│   │                            # EditorBridge, PluginDialogBridge,
│   │                            # PermissionRequestBridge, UIBridge, PluginCommand
│   ├── di/
│   │   └── AppContainer.kt
│   └── ui/
│       ├── home/                # HomeFragment, QuickCreateDialogFragment
│       ├── notes/               # NotesFragment, NoteAdapter, SwipeActionsCallback
│       ├── editor/              # EditNoteFragment, WikiAutocompleteController, TagAutocompleteController
│       ├── viewer/              # ViewNoteFragment
│       ├── voice/               # VoiceInputFragment
│       ├── graph/               # GraphView, ForceDirectedLayout, GraphStyles, GraphFragment
│       ├── library/             # LibraryClustering, LibraryFragment
│       ├── collections/         # CollectionsFragment, CollectionsViewModel
│       ├── plugins/             # PluginsFragment, PluginsAdapter, PluginPermissionsFragment,
│       │                        # PluginDetailsDialogFragment, PluginInstallDialogFragment,
│       │                        # PluginDialogFragment, PermissionRequestDialogFragment
│       ├── guide/               # MarkdownGuideFragment, PluginGuideFragment
│       ├── settings/            # SettingsFragment, AboutFragment, PrivacyPolicyDialogFragment
│       ├── tile/                # QuickVoiceNoteTileService
│       ├── widget/              # QuickNoteWidgetProvider
│       └── common/              # AudioPermissionHelper, UndoSnackbarHelper
├── res/
│   ├── anim/, drawable/, layout/, menu/, mipmap-*/, navigation/
│   ├── values/, values-night/, values-en/, xml/
└── AndroidManifest.xml
```

---

## Storage format

Each note is a `<uuid>.md` file in `filesDir/notes/` with YAML frontmatter:

```yaml
title: Note title
tags: [work, ideas]
created: 1700000000000
updated: 1700000000000
pinned: false
collection: 550e8400-e29b-41d4-a716-446655440000
```

---

Note body in Markdown

☐ Checklist item
☑ Completed item

[!tip] Tip
Callouts are supported too.

```kotlin
fun main() = println("Hello, Oniks")
```

### Collections

`filesDir/collections.json`, TSV:

```
<uuid>\t<name>\t<order>\t<created>
```

### Plugins

- Registry: `filesDir/installed_plugins.json`
- Content: `filesDir/plugins/<id>/`
- Permissions: `filesDir/plugins/<id>/data/permissions.json`
- Local storage: `filesDir/plugins/<id>/data/storage.json`

---

## Plugins

### Format

`.zip` archive with a flat structure:

```
my-plugin.zip
├── manifest.json     (required)
├── main.js           (required)
├── icon.png          (optional)
└── ...               (any additional files)
```

### Manifest

```json
{
  "id": "com.example.myplugin",
  "name": "My plugin",
  "version": "1.0.0",
  "author": "John Doe",
  "description": "Short description.",
  "apiVersion": 1,
  "entry": "main.js",
  "icon": "icon.png",
  "permissions": ["commands", "read_notes"]
}
```

### Plugin example

**manifest.json:**

```json
{
  "id": "com.example.date",
  "name": "Insert date",
  "version": "1.0.0",
  "author": "John Doe",
  "apiVersion": 1,
  "entry": "main.js",
  "permissions": ["commands"]
}
```

**main.js:**

```javascript
oniks.commands.register({
    id: "insert-date",
    title: "Insert date",
    handler: function () {
        var d = new Date();
        var day = ("0" + d.getDate()).slice(-2);
        var month = ("0" + (d.getMonth() + 1)).slice(-2);
        oniks.editor.insertText(day + "." + month + "." + d.getFullYear());
    }
});
```

### Permissions

| Permission | What it grants |
|---|---|
| `commands` | Register commands in the editor menu |
| `read_notes` | Read notes (11 methods: `getAll`, `getAllWithBody`, `getRecent`, `getPinned`, `getNote`, `getMeta`, `search`, `getByTag`, `getByCollection`, `getBacklinks`, `getAllTitles`) + `oniks.ui.openNote` |
| `write_notes` | Modify notes (`create`, `update`, `delete`) and collections (`create`, `rename`, `delete`). Confirmation dialog on first use. |
| `read_settings` | Read app settings |
| `ui_dialog` | Show dialogs (`alert`, `confirm`) |
| `render_custom` | Markdown preprocessor |
| `graph_style` | Graph styling |
| `clipboard` | System clipboard |
| `share` | System "Share" dialog |
| `events` | Subscribe to app events |
| `collections` | Read collections (`getAll`, `getNotesCount`) |
| `ui_panel` | Reserved for future use |

### Limitations

- **JavaScript ES5.** Not supported: `let`, `const`, arrow functions, template literals, `class`, `import`/`export`, spread, destructuring.
- **No `try/catch`** — Rhino on Android crashes on catch-scope (`javax.lang.model.SourceVersion`). Check types via `typeof` and explicit conditions.
- **No `.call()`, `.apply()`, `.bind()`** on `oniks.*` methods — they are Java wrappers. Call directly: `oniks.notes.getAll()`.
- **Emoji outside BMP** (`✅`, `❌`) may not render in dialogs. Use ASCII markers: `[OK]`, `[FAIL]`.
- No access to Java classes, file system, or network.
- One thread per plugin.

### What a plugin can do

- Add commands to the editor menu.
- Insert or modify text in the editor (including the current note's `id` via `editor.getNoteId()`).
- Create, read, update, delete notes.
- Manage collections.
- Show dialogs (`alert`, `confirm`).
- Preprocess note text before rendering.
- Change color, size, and outline of graph nodes and edges, and labels.
- Read app settings.
- Work with the system clipboard.
- Open the system "Share" dialog.
- Parse Markdown (plain text, structure, wiki-links, tags, headings).
- Subscribe to app events (note created / updated / deleted / opened, collection created / deleted, plugin startup / shutdown).
- Open a note in the viewer via `oniks.ui.openNote(id)`.

---

## License

MIT License. Full text in the [LICENSE](LICENSE) file.

---

### Author
**Mikihisa**

### Contact: 
phreakO7@mail.ru

---

## Описание RU / [EN](#oniks)

# Oniks-ru

<p align="center">
  <img src="https://img.shields.io/badge/Android-3DDC84?style=plastic&logo=android&logoColor=white" alt="Android">
  <img src="https://img.shields.io/badge/Kotlin-7F52FF?style=plastic&logo=kotlin&logoColor=white" alt="Kotlin">
  <img src="https://img.shields.io/badge/minSdk-26-1976D2?style=plastic" alt="minSdk 26">
  <img src="https://img.shields.io/badge/targetSdk-34-1976D2?style=plastic" alt="targetSdk 34">
  <img src="https://img.shields.io/badge/Material_3-757575?style=plastic" alt="Material 3">
</p>

<p align="center">
  <img src="https://img.shields.io/badge/License-MIT-2EA043?style=plastic" alt="MIT License">
  <img src="https://img.shields.io/badge/Version-1.24-F57C00?style=plastic" alt="Version 1.24">
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
  - подсветка `==text==` — работает вокруг любого контента
  - подчёркнутый через `<u>text</u>`
  - верхний индекс `x^2^`
  - ссылки: обычные `[text](url)`, автоссылки, wiki-ссылки `[[Заголовок]]`, определения `[text][ref]`
  - изображения — как `🖼 alt (url)` (без загрузки из сети)
  - маркированные, нумерованные и вложенные списки
  - чек-листы `- [ ]` / `- [x]` — интерактивные, кликабельные, с вложенностью
  - цитаты, включая многострочные
  - HR — три точки `• • •`
  - блоки кода с 10 языками подсветки
  - таблицы GFM
  - определения терминов
  - сворачиваемые блоки `<details><summary>`
  - **Callouts Obsidian** — `> [!note]`, `> [!tip]`, `> [!warning]`, `> [!important]`, `> [!caution]` + алиасы
- **Блоки кода** — язык, номера строк, подсветка, кнопка копирования. Kotlin, Java, JSON, SQL, Bash, Python, JavaScript, XML, Markdown, Excel.
- **Wiki-ссылки** — кликабельные, ведут на другую заметку или создают её.
- **Автодополнение** wiki-ссылок и тегов.
- **Подсветка wiki-ссылок в редакторе**.
- **Коллекции** — ручные группы заметок.
- **Мультивыбор** — долгий тап для выбора нескольких заметок.
- **Undo удаления** — countdown-Snackbar с круговым прогрессом.
- **Поиск** — по заголовку, телу, тегам. Подсветка совпадений и «умное» превью.
- **Сортировка** — по дате, алфавиту, числу связей.
- **Счётчик связей** на карточке.
- **Справка по Markdown** — встроенный экран со всеми элементами.

### Плагины

**Расширение функциональности через JavaScript.**

- **Установка из `.zip`** — манифест + код + опциональная иконка.
- **Runtime** — Rhino JS (ES5), изолированный поток на плагин.
- **API `oniks` — 15 namespace, 60 методов:**
  - `oniks.log` — логирование
  - `oniks.storage` — локальное JSON-хранилище
  - `oniks.commands` — команды в меню редактора
  - `oniks.editor` — работа с активным редактором (включая `getNoteId`)
  - `oniks.notes` — заметки (чтение / запись / поиск), включая `getAllWithBody`, `getRecent`, `getPinned`
  - `oniks.dialog` — `alert` / `confirm`
  - `oniks.renderer` — препроцессор Markdown
  - `oniks.graph` — стилизация графа (`nodeStyler`, `edgeStyler`, `labelStyler`)
  - `oniks.settings` — чтение настроек приложения
  - `oniks.clipboard` — системный буфер обмена
  - `oniks.share` — системный диалог «Поделиться»
  - `oniks.markdown` — парсинг Markdown (без рендеринга)
  - `oniks.events` — подписка на события приложения
  - `oniks.collections` — коллекции (создание / переименование / удаление)
  - `oniks.ui` — UI-навигация (`openNote`)
- **Разрешения** — 12. Диалог подтверждения для `write_notes`, экран управления с отзывом.
- **Иконки** из `icon.png` в архиве — в списке, оверлее установки и оверлее деталей.
- **Встроенная инструкция** — все поля манифеста, API, разрешения, ограничения, пример.
- **Полный справочник API** — см. [PLUGIN_API.md](PLUGIN_API.md).

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
│   ├── OniksApp.kt
│   ├── MainActivity.kt
│   ├── data/
│   │   ├── model/               # Note, NoteMeta, Collection, PluginManifest, InstalledPlugin
│   │   ├── markdown/            # NoteSerializer, YamlFrontMatter
│   │   ├── repository/          # NoteRepository, CollectionRepository, PluginRepository
│   │   ├── settings/            # SettingsRepository, ThemeMode, LanguageMode, AppLanguage
│   │   └── speech/              # SpeechRecognitionManager, SpeechState
│   ├── domain/
│   │   ├── links/               # LinksCalculator, KeywordExtractor, LinksCache
│   │   ├── export/              # ExportManager, ImportManager
│   │   ├── deletion/            # DeletionManager
│   │   └── plugins/             # PluginInstaller, PluginManager, PluginRuntime,
│   │                            # PluginApi, PluginStorage, PluginPermissionStore,
│   │                            # EditorBridge, PluginDialogBridge,
│   │                            # PermissionRequestBridge, UIBridge, PluginCommand
│   ├── di/
│   │   └── AppContainer.kt
│   └── ui/
│       ├── home/                # HomeFragment, QuickCreateDialogFragment
│       ├── notes/               # NotesFragment, NoteAdapter, SwipeActionsCallback
│       ├── editor/              # EditNoteFragment, WikiAutocompleteController, TagAutocompleteController
│       ├── viewer/              # ViewNoteFragment
│       ├── voice/               # VoiceInputFragment
│       ├── graph/               # GraphView, ForceDirectedLayout, GraphStyles, GraphFragment
│       ├── library/             # LibraryClustering, LibraryFragment
│       ├── collections/         # CollectionsFragment, CollectionsViewModel
│       ├── plugins/             # PluginsFragment, PluginsAdapter, PluginPermissionsFragment,
│       │                        # PluginDetailsDialogFragment, PluginInstallDialogFragment,
│       │                        # PluginDialogFragment, PermissionRequestDialogFragment
│       ├── guide/               # MarkdownGuideFragment, PluginGuideFragment
│       ├── settings/            # SettingsFragment, AboutFragment, PrivacyPolicyDialogFragment
│       ├── tile/                # QuickVoiceNoteTileService
│       ├── widget/              # QuickNoteWidgetProvider
│       └── common/              # AudioPermissionHelper, UndoSnackbarHelper
├── res/
│   ├── anim/, drawable/, layout/, menu/, mipmap-*/, navigation/
│   ├── values/, values-night/, values-en/, xml/
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

### Коллекции

`filesDir/collections.json`, TSV:

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
| `commands` | Регистрация команд в меню редактора |
| `read_notes` | Чтение заметок (11 методов: `getAll`, `getAllWithBody`, `getRecent`, `getPinned`, `getNote`, `getMeta`, `search`, `getByTag`, `getByCollection`, `getBacklinks`, `getAllTitles`) + `oniks.ui.openNote` |
| `write_notes` | Изменение заметок (`create`, `update`, `delete`) и коллекций (`create`, `rename`, `delete`). Диалог подтверждения при первом использовании. |
| `read_settings` | Чтение настроек приложения |
| `ui_dialog` | Показ диалогов (`alert`, `confirm`) |
| `render_custom` | Препроцессор Markdown |
| `graph_style` | Стилизация графа |
| `clipboard` | Системный буфер обмена |
| `share` | Системный диалог «Поделиться» |
| `events` | Подписка на события приложения |
| `collections` | Чтение коллекций (`getAll`, `getNotesCount`) |
| `ui_panel` | Зарезервировано |

### Ограничения

- **JavaScript ES5.** Не поддерживаются: `let`, `const`, стрелочные функции, template literals, `class`, `import`/`export`, spread, destructuring.
- **Нет `try/catch`** — Rhino на Android падает при создании catch-scope (`javax.lang.model.SourceVersion`). Проверяйте типы через `typeof` и явные условия.
- **Нет `.call()`, `.apply()`, `.bind()`** на методах `oniks.*` — это Java-обёртки. Вызывайте напрямую: `oniks.notes.getAll()`.
- **Эмодзи вне BMP** (`✅`, `❌`) могут не отрисоваться в диалогах. Используйте ASCII: `[OK]`, `[FAIL]`.
- Нет доступа к Java-классам, файловой системе, сети.
- Один поток на плагин.

### Что может плагин

- Добавлять команды в меню редактора.
- Вставлять и изменять текст в редакторе (включая `id` текущей заметки через `editor.getNoteId()`).
- Создавать, читать, изменять, удалять заметки.
- Управлять коллекциями.
- Показывать диалоги (`alert`, `confirm`).
- Препроцессить текст заметки перед рендером.
- Менять цвет, размер и обводку узлов и рёбер графа, а также подписи.
- Читать настройки приложения.
- Работать с системным буфером обмена.
- Открывать системный диалог «Поделиться».
- Парсить Markdown (плоский текст, структура, wiki-ссылки, теги, заголовки).
- Подписываться на события приложения (заметка создана / изменена / удалена / открыта, коллекция создана / удалена, запуск / остановка плагина).
- Открывать заметку в просмотрщике через `oniks.ui.openNote(id)`.

---

## Лицензия

MIT License. Полный текст — в файле [LICENSE](LICENSE).

---

### Автор
**Mikihisa**

### По вопросам: 
phreakO7@mail.ru