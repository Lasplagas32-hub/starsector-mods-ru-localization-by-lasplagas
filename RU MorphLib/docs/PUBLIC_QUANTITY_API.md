# Public Quantity API

Public API нужен авторам JAR/UI-кода, когда токены в `rules.csv` неудобны.

Класс:

```text
rulm.api.RuMorphQuantity
```

## Типовые вызовы

```java
RuMorphQuantity.word(1, "credit");   // кредит
RuMorphQuantity.word(2, "credit");   // кредита
RuMorphQuantity.word(5, "credit");   // кредитов

RuMorphQuantity.wordAcc(1, "relic"); // реликвию
RuMorphQuantity.wordGen(5, "beacon"); // маяков

RuMorphQuantity.suffix(amount, "__blank__a__ov");
```

## Проверка слова

```java
RuMorphQuantity.hasWord("credit");
```

## Когда использовать API

- UI строится в Java/Kotlin.
- Строка не проходит через `rules.csv` token replacement.
- Нужно получить форму слова внутри custom tooltip, intel, market UI или plugin-кода.

## Ограничения

API не форматирует число и не переводит строку. Он возвращает только форму слова или суффикс.
