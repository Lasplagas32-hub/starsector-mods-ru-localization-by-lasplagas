# Integration Guide

## Для переводчика rules.csv

Добавьте зависимость на `RU MorphLib` в мод, который использует токены:

```json
"dependencies": [
  { "id": "ru_morphlib", "name": "RU MorphLib" }
]
```

В `rules.csv` используйте токены прямо в видимом `text` или видимой части `options`.

Пример:

```text
$rulm_GuyOrGirlNom молчит. Освободить $rulm_himAcc?
```

## Для JAR/UI-кода

Используйте Public Quantity API:

```java
import rulm.api.RuMorphQuantity;

String word = RuMorphQuantity.word(amount, "credit");
```

## Для новых слов Quantity Layer

Добавьте строку в:

```text
data/config/rulm/plurals.csv
```

Проверьте формы `one/few/many`, а также `Acc` и `Gen`, если они нужны.

## Для чужого мода

Не подключайте dynamic suffix без аудита. Сначала найдите, откуда реально берётся число:

```text
memory key
player resource
Java/Kotlin variable
```

Шаблон аудита: `docs/PER_MOD_DYNAMIC_NUMBER_AUDIT.md`.
