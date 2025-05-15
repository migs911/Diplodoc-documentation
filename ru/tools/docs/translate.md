---
metadata:
  - name: generator
    content: Diplodoc Platform v4.57.23
meta:
  tags:
    - translate
    - xliff
    - cat
    - i18n
    - l10n
    - localization
    - internationalization
---
# Локализация

Для перевода документации на разные языки используется команда `yfm translate`, которая обеспечивает быстрые [автоматические переводы](#auto).

Подкоманды `extract` и `compose` этой команды позволяют работать с системами [машинного перевода](#cat) (Computer Assisted Translation, или CAT), обмениваясь с ними `*.xliff` файлами.

Поддерживается перевод как `*.md` файлов, так и `*.json` (в том числе `*.yaml`) файлов по [описанным схемам](#json-schemas).

## Параметры вызова подкоманды extract

#|
|| Параметр             | Path
|| --schema {{optional}}| 
Путь до одного или нескольких файлов, содержащих кастомные схемы для перевода.
\
`yfm translate extract --schema ./some/path/to/file.yaml ./some/path/toAnother/file.yaml`
|#

## Автоматический перевод {#auto}

```bash
yfm translate --source ru-RU --target en-US
```

Автоматический перевод может быть выполнен с использованием таких сервисов, как [Yandex Translate](https://cloud.yandex.ru/docs/translate/).

У этих систем есть [ограничения](https://cloud.yandex.ru/ru/docs/translate/concepts/limits) по объему переводимых документов и качеству перевода. Однако они значительно выигрывают с точки зрения скорости.

Для уменьшения объема текста для перевода документ разбивается на более короткие сегменты, например, предложения или заголовки. Повторяющиеся сегменты затем удаляются.

Также для уменьшения объема переводов поддерживаются `include` и `exclude` фильтры.

Параметр запуска `--dry-run` может быть использован для определения объема текста, готового к переводу.

Если лимиты превышены, команда завершится с ошибкой `TRANSLATE_LIMIT_EXCEED`.

### Использование

* Перевести проект в текущей директории с `ru` на `{{translate.target-lang}}`:

  ```
  yfm translate --source ru --target {{translate.target-lang}}
  ```

* Не переводить скрытые файлы в проекте:

  ```
  yfm translate --exclude ru/**/_*.* --source ru --target {{translate.target-lang}}
  ```

### Параметры вызова

##### Основные

#|
|| Параметр             | Формат    | Описание ||
|| --source <b style="color:red" title="Обязательный">*</b>| [Locale](https://en.wikipedia.org/wiki/ISO_639-1) |
Код языка оригинального документа в формате ISO 639-1
\
`yfm translate --source ru-RU`
||
|| --target <b style="color:red" title="Обязательный">*</b>| [Locale](https://en.wikipedia.org/wiki/ISO_639-1) |
Код языка переведенного документа в формате ISO 639-1
\
`yfm translate --target en-US`
||
|| --input              | Path      | 
Путь до **корня** переводимого проекта или конкретного файла в проекте. Если не указан, используется директория запуска команды.
\
Директорию языка в пути указывать не надо — она добавляется автоматически. 
\
`yfm translate -i ./docs`
\
`yfm translate -i ./docs/index.md`
\
Также в качестве пути можно указать [файл фильтр](#filter).
\
`yfm translate -i translate.list` 
||
|| --output             | Path      |
Путь до **корня** проекта, в который нужно сохранить перевод. Если не указан, используется `input` директория.
||
|| --include            | [Glob](https://en.wikipedia.org/wiki/Glob_(programming)) |
Набор правил для фильтрации отправляемых на перевод файлов. По умолчанию `{lang}/**/*.@(md\|yaml\|json)`.
\
Может быть передан несколько раз.
\
Игнорируется, если используется [файл фильтр](#filter).
\
`yfm translate --include ru/**/*.md`
||
|| --exclude            | [Glob](https://en.wikipedia.org/wiki/Glob_(programming)) |
Набор правил, запрещающих отправлять файлы на перевод. Применяется после `include`.
\
Может быть передан несколько раз.
\
`yfm translate --exclude ru/_no-translate/**/*.md`
||
|#

##### Система переводов

{% list tabs %}

- Yandex Translation

  #|
  || Параметр             | Формат         | Описание ||
  || --auth <b style="color:red" title="Обязательный">*</b>  | Path<br/>[IAM‑токен](https://cloud.yandex.ru/ru/docs/translate/api-ref/authentication)<br/>[API‑ключ](https://cloud.yandex.ru/ru/docs/iam/operations/api-key/create) |
  Токен авторизации. Может быть передан несколькими способами:
  \
  [IAM‑токен](https://cloud.yandex.ru/ru/docs/translate/api-ref/authentication) как параметр командной строки
  \
    `yfm translate --auth <token>`
  \
  Путь до файла, в котором хранится [IAM‑токен](https://cloud.yandex.ru/ru/docs/translate/api-ref/authentication)
  \
  `yfm translate --auth path/to/.auth`
  \
  Путь до файла, в котором хранится [API‑ключ](https://cloud.yandex.ru/ru/docs/iam/operations/api-key/create) сервисного аккаунта.
  \
  `yfm translate --auth path/to/.api-key`

  ||
  || --folder <b style="color:red" title="Обязательный">*</b>  | Id |
  [Идентификатор каталога](https://cloud.yandex.ru/ru/docs/resource-manager/operations/folder/get-id), для которого у вашего аккаунта есть роль `ai.translate.user` или выше.
  ||
  |#
  
{% endlist %}

### Файл фильтр

Если необходимо ограничить переводимые тексты фиксированным набором файлов, механизм гибких фильтров `include/exclude` может не подойти.
В таком случае можно сформировать файл с расширением `*.list`. Например `translate.list`.

```
# Файл поддерживает комментарии и пустые строки

# Пути до файлов должны быть сформированы относительно самого файла translate.list.
./some/path/to/translated/file-1.md
./some/path/to/translated/file-2.md

# Пути до файлов не должны находиться выше, чем translate.list.
# Пример неправильного пути:
../some/path/to/translated/file.md
```

Пример вызова команды с файлом фильтром

```bash
yfm translate --input ./translate.list --source ru --target {{translate.target-lang}}
```