# Plugin API Reference

Полная таблица API для разработки плагинов Оникса.

**Версия API:** 1
**Всего:** 60 методов, 15 namespace, 12 разрешений.

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
15. [oniks.ui](#15-oniksui--ui-навигация)
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
| 8 | `oniks.commands.register` | `{id, title, handler}` | — | `commands` |

Команды появляются в меню редактора (три точки в тулбаре).

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

Вызовы **блокируют** поток плагина до ответа пользователя. Не используйте в цикле.

---

## 7. `oniks.renderer` — препроцессор Markdown

| # | Метод | Аргументы | Возвращает | Разрешение |
|---|---|---|---|---|
| 36 | `oniks.renderer.register` | `{id, process}` | — | `render_custom` |

`process(text)` получает весь текст заметки перед рендером и возвращает изменённый текст. Порядок препроцессоров — порядок регистрации.

---

## 8. `oniks.graph` — стилизация графа

| # | Метод | Аргументы | Возвращает | Разрешение |
|---|---|---|---|---|
| 37 | `oniks.graph.register` | `{id, nodeStyler?, edgeStyler?, labelStyler?}` | — | `graph_style` |

**Поля NodeStyle:** `color` (hex), `radiusMultiplier` (float), `borderColor` (hex).

**Поля EdgeStyle:** `color` (hex), `widthMultiplier` (float).

Возврат `null` — не менять стандартный вид.

**Нюанс:** степень узла (`node.degree`) зависит от размера графа. На маленьких базах (10–20 заметок) `degree >= 3` может никогда не сработать. Начинайте с `degree >= 1`, повышайте порог по мере роста базы.

---

## 9. `oniks.settings` — чтение настроек

| # | Метод | Аргументы | Возвращает | Разрешение |
|---|---|---|---|---|
| 38 | `oniks.settings.getTheme` | — | `"system"` / `"light"` / `"dark"` | `read_settings` |
| 39 | `oniks.settings.getLanguage` | — | `"system"` / `"ru"` / `"en"` и т.д. | `read_settings` |
| 40 | `oniks.settings.getAppLanguage` | — | `"system"` / `"ru"` / `"en"` | `read_settings` |
| 41 | `oniks.settings.getSpeechLanguage` | — | BCP-47 тег или `""` | `read_settings` |
| 42 | `oniks.settings.isAutoSaveEnabled` | — | `true` / `false` | `read_settings` |
| 43 | `oniks.settings.getHomeRecentLimit` | — | `3` / `5` / `10` | `read_settings` |

---

## 10. `oniks.clipboard` — буфер обмена

| # | Метод | Аргументы | Возвращает | Разрешение |
|---|---|---|---|---|
| 44 | `oniks.clipboard.copy` | `text` | `true` / `false` | `clipboard` |
| 45 | `oniks.clipboard.paste` | — | `string` | `clipboard` |
| 46 | `oniks.clipboard.hasText` | — | `true` / `false` | `clipboard` |

---

## 11. `oniks.share` — системный диалог «Поделиться»

| # | Метод | Аргументы | Возвращает | Разрешение |
|---|---|---|---|---|
| 47 | `oniks.share.send` | `text, [title]` | `true` / `false` | `share` |

Открывает системный диалог «Поделиться» с указанным текстом.

---

## 12. `oniks.markdown` — парсинг Markdown

| # | Метод | Аргументы | Возвращает | Разрешение |
|---|---|---|---|---|
| 48 | `oniks.markdown.toPlainText` | `markdown` | `string` | — |
| 49 | `oniks.markdown.render` | `markdown` | `string` (со структурой) | — |
| 50 | `oniks.markdown.parseWikiLinks` | `text` | массив строк | — |
| 51 | `oniks.markdown.parseTags` | `text` | массив строк | — |
| 52 | `oniks.markdown.parseHeadings` | `text` | массив `{level, text}` | — |

**`toPlainText`** — полностью убирает Markdown-разметку.

**`render`** — сохраняет структуру (`#`, `-`, `- [ ]`, `>`), нормализует пробелы.

---

## 13. `oniks.events` — подписка на события

| # | Метод | Аргументы | Возвращает | Разрешение |
|---|---|---|---|---|
| 53 | `oniks.events.on` | `eventName, handler` | — | `events` |
| 54 | `oniks.events.off` | `eventName, [handler]` | `int` (снято) | `events` |

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
| 55 | `oniks.collections.getAll` | — | массив коллекций | `collections` |
| 56 | `oniks.collections.getNotesCount` | `id` | `int` | `collections` |
| 57 | `oniks.collections.create` | `name` | `id` | `collections` + `write_notes` |
| 58 | `oniks.collections.rename` | `id, newName` | `true` / `false` | `collections` + `write_notes` |
| 59 | `oniks.collections.delete` | `id` | `true` / `false` | `collections` + `write_notes` |

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

## 15. `oniks.ui` — UI-навигация

| # | Метод | Аргументы | Возвращает | Разрешение |
|---|---|---|---|---|
| 60 | `oniks.ui.openNote` | `id` | `true` / `false` | `read_notes` |

Открывает заметку в просмотрщике. Работает только когда приложение активно (Activity в `onResume`). Возвращает `true`, если навигация запущена.

**Не открывайте заметку внутри обработчика `noteOpened`** — получится бесконечный цикл.

---

## Разрешения

| # | Разрешение | Что покрывает |
|---|---|---|
| 1 | `commands` | `oniks.commands.register` |
| 2 | `read_notes` | 11 методов `oniks.notes` (чтение) + `oniks.ui.openNote` |
| 3 | `write_notes` | 3 метода `oniks.notes` (запись) + `oniks.collections.create/rename/delete` (совместно с `collections`). Требует диалога подтверждения. |
| 4 | `read_settings` | 6 методов `oniks.settings` |
| 5 | `ui_dialog` | 2 метода `oniks.dialog` |
| 6 | `render_custom` | `oniks.renderer.register` |
| 7 | `graph_style` | `oniks.graph.register` |
| 8 | `clipboard` | 3 метода `oniks.clipboard` |
| 9 | `share` | `oniks.share.send` |
| 10 | `events` | 2 метода `oniks.events` + 8 событий |
| 11 | `collections` | 5 методов `oniks.collections` |
| 12 | `ui_panel` | Зарезервировано |

---

## Итого

| Namespace | Методов | Разрешение |
|---|---|---|
| `oniks.log` | 3 | — |
| `oniks.storage` | 4 | — |
| `oniks.commands` | 1 | `commands` |
| `oniks.editor` | 11 | — |
| `oniks.notes` | 14 | `read_notes` / `write_notes` |
| `oniks.dialog` | 2 | `ui_dialog` |
| `oniks.renderer` | 1 | `render_custom` |
| `oniks.graph` | 1 | `graph_style` |
| `oniks.settings` | 6 | `read_settings` |
| `oniks.clipboard` | 3 | `clipboard` |
| `oniks.share` | 1 | `share` |
| `oniks.markdown` | 5 | — |
| `oniks.events` | 2 | `events` |
| `oniks.collections` | 5 | `collections` + `write_notes` |
| `oniks.ui` | 1 | `read_notes` |
| **Всего** | **60** | **12 разрешений** |

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