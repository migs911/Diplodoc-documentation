---
metadata:
  - name: generator
    content: Diplodoc Platform v4.57.23
---
# Плагины

Кроме базового синтаксиса [CommonMark Spec](https://spec.commonmark.org/), YFM предоставляет набор плагинов с дополнительными возможностями и уникальными элементами разметки.

{% note warning %}

Порядок добавления плагинов важен. При добавлении плагинов необходимо указывать полный набор плагинов.

{% endnote %}

{% include [plugins.md](../_includes/plugins.md) %}

Выше перечислены плагины, включенные в пакет YFM. Но вы можете [подключить дополнительные](import.md) или написать свой плагин, используя [руководство от markdown-it](https://github.com/markdown-it/markdown-it/tree/master/docs). 
