---
metadata:
  - name: generator
    content: Diplodoc Platform v4.57.23
---
# Быстрый старт

Платформа diplodoc разрабатывается на основе набора независимых модулей, расположенных в GitHub организации [diplodoc-platform](https://github.com/diplodoc-platform).

Каждый модуль можно разрабатывать как по отдельности, так и в составе [метапакета](./metapackage.md).

Самый простой способ начать разрабатку любого модуля в системе - запустить преднастроенный GitHub Codespace в соответствующем репозитории.

{% note info "" %}

Подробнее про работу с GitHub Codespaces можно почитать в [официальной документации](https://docs.github.com/en/codespaces/getting-started/quickstart).

{% endnote %}

## Подготовка модуля

После создания codespace дождитесь выполнения postCreateCommand (~3мин). 

На этом этапе проходит несколько подготовительных действий:
- установка необходимых модулю NodeJS пакетов
- предварительная сборка модуля (`npm run build`)
- основные проверки качества кода (`npm run lint`)
- основные тесты (`npm run test`)

Когда подготовка успешно завершена, т.е. модуль собирается и проходит основные проверки - он готов к [внесению изменений](#add-changes). 

## Подготовка метапакета

Разработка в рамках метапакета упрощает одновременное внесение изменений сразу в несколько модулей.

После создания codespace дождитесь выполнения postCreateCommand (~3мин).

На этом этапе проходит несколько подготовительных действий:
- связывание git субмодулей
- установка необходимых NodeJS пакетов в режиме npm workspaces
- предварительная сборка графа модулей для проекта CLI (`npx nx build @diplodoc/cli`)

По умолчанию при инициализации метапакета не запускаются проверки качества кода и тесты.
Их можно запустить самостоятельно выполнив в корневой директории `npm run lint` и `npm run test` соответственно.
При этом выполнятся соответствующие проверки во всех зависимых модулях.

Когда подготовка успешно завершена, т.е. модуль собирается и проходит основные проверки - он готов к [внесению изменений](#add-changes). 

## Внесение изменений {add-changes}

В процессе внесения изменений необходимо убедиться, что проверки качества кода (`npm run lint` и `npm run test`) в измененном модуле все еще проходят без ошибок.

После этого можно приступить к [оформлению коммитов и пулл реквеста](./contribution.md).