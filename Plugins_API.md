# Plugin API Reference

Полная таблица API для разработки плагинов Оникса.

**Версия API:** 1
**Всего:** 70 методов, 15 namespace, 14 разрешений.

---

## Содержание

1. [oniks.log](#1-onikslog--логирование)
2. [oniks.storage](#2-oniksstorage--локальное-хранилище)
3. [oniks.commands](#3-onikscommands--команды-в-редакторе)
4. [oniks.editor](#4-onikseditor--работа-с-активным-редактором)
5. [oniks.notes](#5-oniksnotes--работа-с-заметками)
6. [oniks.dialog](#6-oniksdialog--модальные-диалоги)
7. [oniks.renderer](#7-oniksrenderer--препроцессор-markdown)
8. [oniks.graph](#8-oniksgraph--стилизация-графа)
9. [oniks.settings](#9-onikssettings--чтение-настроек)
10. [oniks.clipboard](#10-oniksclipboard--буфер-обмена)
11. [oniks.share](#11-oniksshare--системный-диалог-поделиться)
12. [oniks.markdown](#12-oniksmarkdown--парсинг-markdown)
13. [oniks.events](#13-oniksevents--подписка-на-события)
14. [oniks.collections](#14-onikscollections--работа-с-коллекциями)
15. [oniks.ui](#15-oniksui--ui-навигация-и-кастомизация)
16. [Разрешения](#разрешения)
17. [Итого](#итого)

---

## 1. `oniks.log` — логирование

| # | Метод | Аргументы | Возвращает | Разрешение |
|---|---|---|---|---|
| 1 | `oniks.log.info` | `message` | — | — |
| 2 | `oniks.log.warn` | `message` | — | — |
| 3 | `oniks.log.error` | `message` | — | — |

Тег для фильтрации в logcat: `Oniks.Plugin.<id>`, где `<id>` — идентификатор плагина.

---

## 2. `oniks.storage` — локальное хранилище

| # | Метод | Аргументы | Возвращает | Разрешение |
|---|---|---|---|---|
| 4 | `oniks.storage.get` | `key` | `string` или `undefined` | — |
| 5 | `oniks.storage.set` | `key, value` | — | — |
| 6 | `oniks.storage.remove` | `key` | — | — |
| 7 | `oniks.storage.keys` | — | массив строк | — |

Значения — только строки. Для объектов используйте `JSON.stringify` / `JSON.parse`.

---

## 3. `oniks.commands` — команды в редакторе

| # | Метод | Аргументы | Возвращает | Разрешение |
|---|---|---|---|---|
| 8 | `oniks.commands.register` | `{id, title, handler, icon?}` | — | `commands` |

Команды появляются в меню редактора (три точки в тулбаре).

**Поля объекта:**

| Поле | Обязательное | Описание |
|---|---|---|
| `id` | Да | Уникален в рамках плагина. |
| `title` | Да | Отображается в меню. |
| `handler` | Да | Функция без аргументов. |
| `icon` | Нет | Имя иконки из белого списка Оникса. Если не указано или не найдено — команда показывается без иконки. |

**Доступные имена иконок (25):**

```yaml
add, check, close, copy, delete, edit, export, folder, graph,
import, info, library, link, markdown, mic, note, pin, save,
search, settings, share, sort, star, undo, warning

```

Пример с иконкой:

```javascript
oniks.commands.register({
    id: "improve-note",
    title: "Улучшить текст",
    icon: "star",
    handler: function () {
        // ...
    }
});
```

---

## 4. `oniks.editor` — работа с активным редактором

| # | Метод | Аргументы | Возвращает | Разрешение |
|---|---|---|---|---|
| 9 | `oniks.editor.insertText` | `text` | — | — |
| 10 | `oniks.editor.wrapSelection` | `prefix, suffix` | — | — |
| 11 | `oniks.editor.getSelection` | — | `string` | — |
| 12 | `oniks.editor.getFullText` | — | `string` | — |
| 13 | `oniks.editor.setFullText` | `text` | — | — |
| 14 | `oniks.editor.getTitle` | — | `string` | — |
| 15 | `oniks.editor.setTitle` | `text` | — | — |
| 16 | `oniks.editor.getNoteId` | — | `string` (id или `""`) | — |
| 17 | `oniks.editor.getCursorPosition` | — | `int` или `-1` | — |
| 18 | `oniks.editor.setCursorPosition` | `position` | — | — |
| 19 | `oniks.editor.selectRange` | `start, end` | — | — |

Если редактор не открыт — методы возвращают пустое значение или игнорируются.

`getNoteId` возвращает id заметки, открытой в редакторе, или пустую строку, если редактор закрыт. Полезно для плагинов, которые хотят обновить текущую заметку через `oniks.notes.update(id, ...)`.

---

## 5. `oniks.notes` — работа с заметками

| # | Метод | Аргументы | Возвращает | Разрешение |
|---|---|---|---|---|
| 20 | `oniks.notes.getAll` | — | массив заметок (без `body`) | `read_notes` |
| 21 | `oniks.notes.getAllWithBody` | — | массив заметок с `body` | `read_notes` |
| 22 | `oniks.notes.getRecent` | `limit` | массив заметок | `read_notes` |
| 23 | `oniks.notes.getPinned` | — | массив заметок | `read_notes` |
| 24 | `oniks.notes.getNote` | `id` | заметка с `body` или `undefined` | `read_notes` |
| 25 | `oniks.notes.getMeta` | `id` | метаданные или `undefined` | `read_notes` |
| 26 | `oniks.notes.search` | `query` | массив заметок | `read_notes` |
| 27 | `oniks.notes.getByTag` | `tag` | массив заметок | `read_notes` |
| 28 | `oniks.notes.getByCollection` | `collectionId` | массив заметок | `read_notes` |
| 29 | `oniks.notes.getBacklinks` | `id` | массив заметок | `read_notes` |
| 30 | `oniks.notes.getAllTitles` | — | массив строк | `read_notes` |
| 31 | `oniks.notes.create` | `title, body` | `id` | `write_notes` |
| 32 | `oniks.notes.update` | `id, {title?, body?, tags?, collectionId?}` | `true` / `false` | `write_notes` |
| 33 | `oniks.notes.delete` | `id` | `true` / `false` | `write_notes` |

**Структура заметки в `getAll` / `getRecent` / `getPinned` / `search` / `getByTag` / `getByCollection` / `getBacklinks`:**

```yaml
{
id: string,
title: string,
preview: string,
tags: array,
pinned: boolean,
created: number,
updated: number
}
```

Структура заметки в getNote / getAllWithBody:

```yaml
{
id, title, preview, tags, pinned, created, updated,
body: string,
collectionId: string
}
```

При первом использовании write_notes пользователю показывается диалог подтверждения. Без согласия операции возвращают false / undefined.

---

## 6. `oniks.dialog` — модальные диалоги

| # | Метод | Аргументы | Возвращает | Разрешение |
|---|---|---|---|---|
| 34 | `oniks.dialog.alert` | `message, [title]` | — | `ui_dialog` |
| 35 | `oniks.dialog.confirm` | `message, [title]` | `true` / `false` | `ui_dialog` |
| 36 | `oniks.dialog.prompt` | `message, [default], [title]` | `string` или `undefined` | `ui_dialog` |
| 37 | `oniks.dialog.choose` | `message, items, [title]` | `int` (индекс) или `-1` | `ui_dialog` |

**`prompt`** — диалог ввода текста. Аргументы:
- `message` — вопрос.
- `[default]` — предзаполненный текст (опционально).
- `[title]` — заголовок диалога (опционально).

Возвращает введённую строку или `undefined`, если пользователь отменил.

**`choose`** — диалог выбора из списка. Аргументы:
- `message` — вопрос.
- `items` — массив строк.
- `[title]` — заголовок диалога (опционально).

Возвращает индекс выбранного варианта (`0..N-1`) или `-1`, если пользователь отменил.

**Примеры:**

```javascript
// prompt
var name = oniks.dialog.prompt("Как вас зовут?");
if (name !== undefined) {
    oniks.log.info("Привет, " + name);
}

// prompt с дефолтом и заголовком
var city = oniks.dialog.prompt("Ваш город?", "Москва", "Знакомство");

// choose
var colors = ["Красный", "Зелёный", "Синий"];
var idx = oniks.dialog.choose("Какой цвет?", colors);
if (idx >= 0) {
    oniks.log.info("Выбрано: " + colors[idx]);
}

// choose с заголовком
var picked = oniks.dialog.choose("Любимая еда", ["Пицца", "Суши", "Паста"], "Опрос");
```

Все четыре метода **блокируют** поток плагина до ответа пользователя. Не используйте в цикле.

---

## 7. `oniks.renderer` — препроцессор Markdown

| # | Метод | Аргументы | Возвращает | Разрешение |
|---|---|---|---|---|
| 38 | `oniks.renderer.register` | `{id, process}` | — | `render_custom` |

`process(text)` получает весь текст заметки перед рендером и возвращает изменённый текст. Порядок препроцессоров — порядок регистрации.

---

## 8. `oniks.graph` — стилизация графа

| # | Метод | Аргументы | Возвращает | Разрешение |
|---|---|---|---|---|
| 39 | `oniks.graph.register` | `{id, nodeStyler?, edgeStyler?, labelStyler?}` | — | `graph_style` |

**Поля NodeStyle:** `color` (hex), `radiusMultiplier` (float), `borderColor` (hex).

**Поля EdgeStyle:** `color` (hex), `widthMultiplier` (float).

Возврат `null` — не менять стандартный вид.

**Нюанс:** степень узла (`node.degree`) зависит от размера графа. На маленьких базах (10–20 заметок) `degree >= 3` может никогда не сработать. Начинайте с `degree >= 1`, повышайте порог по мере роста базы.

---

## 9. `oniks.settings` — чтение настроек

| # | Метод | Аргументы | Возвращает | Разрешение |
|---|---|---|---|---|
| 40 | `oniks.settings.getTheme` | — | `"system"` / `"light"` / `"dark"` | `read_settings` |
| 41 | `oniks.settings.getLanguage` | — | `"system"` / `"ru"` / `"en"` и т.д. | `read_settings` |
| 42 | `oniks.settings.getAppLanguage` | — | `"system"` / `"ru"` / `"en"` | `read_settings` |
| 43 | `oniks.settings.getSpeechLanguage` | — | BCP-47 тег или `""` | `read_settings` |
| 44 | `oniks.settings.isAutoSaveEnabled` | — | `true` / `false` | `read_settings` |
| 45 | `oniks.settings.getHomeRecentLimit` | — | `3` / `5` / `10` | `read_settings` |

---

## 10. `oniks.clipboard` — буфер обмена

| # | Метод | Аргументы | Возвращает | Разрешение |
|---|---|---|---|---|
| 46 | `oniks.clipboard.copy` | `text` | `true` / `false` | `clipboard` |
| 47 | `oniks.clipboard.paste` | — | `string` | `clipboard` |
| 48 | `oniks.clipboard.hasText` | — | `true` / `false` | `clipboard` |

---

## 11. `oniks.share` — системный диалог «Поделиться»

| # | Метод | Аргументы | Возвращает | Разрешение |
|---|---|---|---|---|
| 49 | `oniks.share.send` | `text, [title]` | `true` / `false` | `share` |

Открывает системный диалог «Поделиться» с указанным текстом.

---

## 12. `oniks.markdown` — парсинг Markdown

| # | Метод | Аргументы | Возвращает | Разрешение |
|---|---|---|---|---|
| 50 | `oniks.markdown.toPlainText` | `markdown` | `string` | — |
| 51 | `oniks.markdown.render` | `markdown` | `string` (со структурой) | — |
| 52 | `oniks.markdown.parseWikiLinks` | `text` | массив строк | — |
| 53 | `oniks.markdown.parseTags` | `text` | массив строк | — |
| 54 | `oniks.markdown.parseHeadings` | `text` | массив `{level, text}` | — |

**`toPlainText`** — полностью убирает Markdown-разметку.

**`render`** — сохраняет структуру (`#`, `-`, `- [ ]`, `>`), нормализует пробелы.

---

## 13. `oniks.events` — подписка на события

| # | Метод | Аргументы | Возвращает | Разрешение |
|---|---|---|---|---|
| 55 | `oniks.events.on` | `eventName, handler` | — | `events` |
| 56 | `oniks.events.off` | `eventName, [handler]` | `int` (снято) | `events` |

Дедупликация: один и тот же обработчик не регистрируется дважды.

off("eventName") — снимает все обработчики события.

off("eventName", handler) — снимает конкретный обработчик.

### Доступные события

| Событие | Когда срабатывает | Поля `data` |
|---|---|---|
| `startup` | Плагин загружен и активен | — |
| `shutdown` | Плагин выключается | — |
| `noteCreated` | Создана заметка | `id, title, body, tags, collectionId` |
| `noteUpdated` | Заметка сохранена | `id, title, body, tags, collectionId` |
| `noteDeleted` | Заметка удалена | `id` |
| `noteOpened` | Открыт редактор заметки | `id` |
| `collectionCreated` | Создана коллекция | `id, name` |
| `collectionDeleted` | Коллекция удалена | `id` |

Обработчики вызываются асинхронно. Если обработчик бросает исключение — оно логируется, остальные обработчики всё равно вызываются.

Осторожно с write_notes внутри noteCreated — можно создать бесконечный цикл.

---

## 14. `oniks.collections` — работа с коллекциями

| # | Метод | Аргументы | Возвращает | Разрешение |
|---|---|---|---|---|
| 57 | `oniks.collections.getAll` | — | массив коллекций | `collections` |
| 58 | `oniks.collections.getNotesCount` | `id` | `int` | `collections` |
| 59 | `oniks.collections.create` | `name` | `id` | `collections` + `write_notes` |
| 60 | `oniks.collections.rename` | `id, newName` | `true` / `false` | `collections` + `write_notes` |
| 61 | `oniks.collections.delete` | `id` | `true` / `false` | `collections` + `write_notes` |

**Структура коллекции:**

```yaml
{
id: string,
name: string,
order: number,
created: number
}
```

Заметки в коллекции получаются через oniks.notes.getByCollection(id).

---

## 15. `oniks.ui` — UI-навигация и кастомизация

### 15.1 Навигация (требует `read_notes`)

| # | Метод | Аргументы | Возвращает | Разрешение |
|---|---|---|---|---|
| 62 | `oniks.ui.openNote` | `id` | `true` / `false` | `read_notes` |

Открывает заметку в просмотрщике. Работает только когда приложение активно (Activity в `onResume`). Возвращает `true`, если навигация запущена.

**Не открывайте заметку внутри обработчика `noteOpened`** — получится бесконечный цикл.

### 15.2 Темы приложения (требует `ui_theme`)

| # | Метод | Аргументы | Возвращает | Разрешение |
|---|---|---|---|---|
| 63 | `oniks.ui.setTheme` | `id` | `true` / `false` | `ui_theme` |
| 64 | `oniks.ui.setThemeColorsHex` | `{colorPrimary}` | `id` темы или `""` | `ui_theme` |
| 65 | `oniks.ui.resetTheme` | — | `true` / `false` | `ui_theme` |
| 66 | `oniks.ui.getTheme` | — | `id` темы или `""` | `ui_theme` |
| 67 | `oniks.ui.getAvailableThemes` | — | массив строк | `ui_theme` |

**Доступные id тем (8):**

```yaml
red, blue, green, purple, amber, pink, teal, monochrome
```

**Пример:**

```javascript
var themes = oniks.ui.getAvailableThemes();
if (themes.indexOf("red") >= 0) {
    oniks.ui.setTheme("red");
}
```

**Про `setThemeColorsHex`:** экспериментальный метод. Принимает hex основного цвета (`colorPrimary`), подбирает **ближайшую** из 8 предустановленных тем по HSV-расстоянию. Точный hex **не гарантируется**. Для точного контроля используйте `setTheme` с конкретным id.

Тема применяется через пересоздание Activity — небольшой визуальный переход. Это норма.

При удалении плагина тема снимается автоматически.

### 15.3 Стиль карточек заметок (требует `ui_note_card`)

| # | Метод | Аргументы | Возвращает | Разрешение |
|---|---|---|---|---|
| 68 | `oniks.ui.setNoteCardStyle` | `{...}` | `int` (применено полей) | `ui_note_card` |
| 69 | `oniks.ui.resetNoteCardStyle` | — | `true` / `false` | `ui_note_card` |
| 70 | `oniks.ui.getNoteCardStyle` | — | объект стиля | `ui_note_card` |

**Полная свобода hex** — цвета применяются напрямую к карточкам, минуя тему. Все поля опциональны.

| Поле | Тип | Что делает |
|---|---|---|
| `showPreview` | boolean | Показывать превью заметки. |
| `showDate` | boolean | Показывать дату. |
| `showTags` | boolean | Показывать теги. |
| `showLinks` | boolean | Показывать счётчик связей. |
| `showPin` | boolean | Показывать иконку закрепления. |
| `cardBackground` | hex | Цвет фона карточки. |
| `titleColor` | hex | Цвет заголовка. |
| `previewColor` | hex | Цвет превью. |
| `dateColor` | hex | Цвет даты. |
| `tagBackground` | hex | Цвет фона тегов. |
| `tagTextColor` | hex | Цвет текста тегов. |
| `pinColor` | hex | Цвет иконки закрепления. |
| `linksColor` | hex | Цвет счётчика связей. |
| `titleSize` | число (SP) | Размер заголовка. |
| `previewSize` | число (SP) | Размер превью. |
| `dateSize` | число (SP) | Размер даты. |
| `tagTextSize` | число (SP) | Размер текста тегов. |
| `cornerRadius` | число (dp) | Радиус углов карточки. |
| `cardPaddingH` | число (dp) | Горизонтальные отступы. |
| `cardPaddingV` | число (dp) | Вертикальные отступы. |

**Пример:**

```javascript
oniks.ui.setNoteCardStyle({
    showPreview: false,
    showDate: false,
    cardBackground: "#2A2A2A",
    titleColor: "#FFFFFF",
    titleSize: 17,
    cornerRadius: 12
});
```

**Важно:** стиль применяется к карточкам **при следующем возврате в список заметок**. Пока список открыт, изменения не перерисуются мгновенно — нужно уйти и вернуться.

Стиль снимается автоматически при удалении плагина.

---

## Разрешения

| # | Разрешение | Что покрывает |
|---|---|---|
| 1 | `commands` | `oniks.commands.register` |
| 2 | `read_notes` | 11 методов `oniks.notes` (чтение) + `oniks.ui.openNote` |
| 3 | `write_notes` | 3 метода `oniks.notes` (запись) + `oniks.collections.create/rename/delete` (совместно с `collections`). Требует диалога подтверждения. |
| 4 | `read_settings` | 6 методов `oniks.settings` |
| 5 | `ui_dialog` | 4 метода `oniks.dialog` |
| 6 | `ui_theme` | 5 методов `oniks.ui` (темы) |
| 7 | `ui_note_card` | 3 метода `oniks.ui` (карточки) |
| 8 | `render_custom` | `oniks.renderer.register` |
| 9 | `graph_style` | `oniks.graph.register` |
| 10 | `clipboard` | 3 метода `oniks.clipboard` |
| 11 | `share` | `oniks.share.send` |
| 12 | `events` | 2 метода `oniks.events` + 8 событий |
| 13 | `collections` | 5 методов `oniks.collections` |
| 14 | `ui_panel` | Зарезервировано |

---

## Итого

| Namespace | Методов | Разрешение |
|---|---|---|
| `oniks.log` | 3 | — |
| `oniks.storage` | 4 | — |
| `oniks.commands` | 1 | `commands` |
| `oniks.editor` | 11 | — |
| `oniks.notes` | 14 | `read_notes` / `write_notes` |
| `oniks.dialog` | 4 | `ui_dialog` |
| `oniks.renderer` | 1 | `render_custom` |
| `oniks.graph` | 1 | `graph_style` |
| `oniks.settings` | 6 | `read_settings` |
| `oniks.clipboard` | 3 | `clipboard` |
| `oniks.share` | 1 | `share` |
| `oniks.markdown` | 5 | — |
| `oniks.events` | 2 | `events` |
| `oniks.collections` | 5 | `collections` + `write_notes` |
| `oniks.ui` | 9 | `read_notes`, `ui_theme`, `ui_note_card` |
| **Всего** | **70** | **14 разрешений** |

---

## Ограничения

**JavaScript — только ES5.** Не поддерживаются:

- `let`, `const` — используйте `var`.
- Стрелочные функции — используйте `function() {}`.
- Template literals — используйте конкатенацию `"text " + x`.
- `class`, `import`, `export`.
- Spread `...` и destructuring `{a, b} = obj`.
- Lookbehind в регулярках: `(?<=...)`, `(?<!...)`.
- `Array.prototype.includes` — используйте `indexOf() >= 0`.
- `Array.prototype.flat`, `flatMap`.
- `String.prototype.padStart`, `padEnd`.
- `Object.entries`, `Object.values`.
- `String.prototype.matchAll`.
- `Promise`, `async`, `await`.
- `Symbol`.

---

Критические особенности Rhino на Android

Движок Rhino 1.7.14 на Android имеет три фундаментальных отличия от обычного JavaScript. Их обязательно учитывать — иначе плагин будет падать или тихо не работать.

1. try/catch не работает

При входе в блок try Rhino пытается создать catch-scope и падает с:

```yaml
java.lang.NoClassDefFoundError: Ljavax/lang/model/SourceVersion;
```

Приложение не крашится — ошибка ловится на стороне Оникса. Но команда плагина прерывается и до конца не выполняется.

Не используйте try/catch в плагинах. Проверяйте типы через typeof и явные условия.

```javascript
// НЕПРАВИЛЬНО — команда прервётся:
try {
    var all = oniks.notes.getAll();
} catch (e) {
    oniks.log.error("failed");
}

// ПРАВИЛЬНО:
if (typeof oniks.notes.getAll !== "function") {
    oniks.log.error("getAll недоступен");
    return;
}
var all = oniks.notes.getAll();
```

2. .call(), .apply(), .bind() не работают на методах oniks.*

Методы oniks.* — это Java-обёртки, а не обычные JS-функции. Если вынести метод в переменную и вызвать через .call() — Rhino падает с ошибкой:

```yaml
TypeError: Cannot find default value for object
```

Вызывайте методы напрямую:

```javascript
// НЕПРАВИЛЬНО:
var fn = oniks.notes.getAll;
var all = fn.call(oniks.notes);

// ПРАВИЛЬНО:
var all = oniks.notes.getAll();
```

Это касается всех методов oniks.*, включая oniks.notes.getAll, oniks.notes.getRecent, oniks.ui.openNote и т.д.

3. Эмодзи вне BMP могут не отрисоваться

Символы вида ✅, ❌, 🖼 — это пары surrogate в UTF-16. Rhino на Android может передать их в диалог некорректно, и они не отобразятся.

Используйте ASCII-маркеры: [OK], [FAIL], [!], *.

```javascript
// НЕПРАВИЛЬНО:
oniks.dialog.alert("✅ Проверка пройдена");

// ПРАВИЛЬНО:
oniks.dialog.alert("[OK] Проверка пройдена");
```

---

Нет доступа к:

· Java-классам Android.
· Файловой системе.
· Сети.
· Системным API.
· Другим плагинам.

---

Лимиты

· Размер архива: до 50 МБ распакованного.
· Файл manifest.json: до 64 КБ.
· Один поток на плагин.