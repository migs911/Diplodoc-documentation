---
metadata:
  - name: generator
    content: Diplodoc Platform v4.57.23
---
# Файл конфигурации

В файле конфигурации можно задать:

* [стандартные настройки YFM](../settings.md);
* [настройки трансформации YFM в HTML](../tools/transform/settings.md);
* [настройки сборки](../tools/docs/settings.md).

По умолчанию используется файл `.yfm` в корне документа. При сборке можно указать путь до другого файла с помощью [ключа запуска](../tools/docs/settings.md) `--config`. 

## Структура

Файл конфигурации `.yfm` содержит список всех параметров в формате YAML:

```yaml
parameter: value
parameter: value
```
* `parameter` — имя задаваемой настройки;
* `value` — значение настройки.
