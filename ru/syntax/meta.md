---
metadata:
  - name: generator
    content: Diplodoc Platform v4.57.23
---
# Комментарии и метаданные

Комментарии и метаданные — это элементы разметки, которые не отображаются в собранном файле. Они используются, чтобы хранить в исходном тексте информацию для SEO или авторов документа.

## Комментарии {#comments}

Чтобы добавить комментарий, используйте следующую разметку. Убедитесь, что до комментария есть пустая строка.

```markdown
[//]: # (Комментарий)
```

## Метаданные {#meta}

Метаданные можно добавить в формате YAML в начало файла. После преобразования они вернутся вместе с полученным HTML. 

```yaml
---
title: Заголовок
description: Описание
---
```
