# Quantity Layer - `$ruln_*`

Quantity Layer нужен для правильных русских форм после чисел.

## Что он решает

```text
1 кредит
2 кредита
5 кредитов
21 кредит
22 кредита
25 кредитов
```

## Основные маршруты

| Маршрут | Когда использовать | Пример |
|---|---|---|
| `$ruln_num_<N>_<wordId>` | число заранее известно и прямо записано в токене | `$ruln_num_5_credit` -> `кредитов` |
| `$ruln_player<resource>` | число берётся из ресурсов игрока | кредиты, топливо, припасы, морпехи |
| `$ruln_mem_<memoryKey>_<wordId>` | число берётся из memory/dialogue variable | `$ruln_mem_coff_ransomprice_credit` |
| `RuMorphQuantity.word(amount, wordId)` | Java/Kotlin/JAR/UI-код | `word(22, "credit")` -> `кредита` |

## Важное правило

Статичные числа можно и нужно переводить руками:

```text
5 кредитов
20 морпехов
3 дня
```

RU MorphLib нужен там, где число приходит из игры, memory, ресурса игрока или кода.

## Форматированные деньги

Если мод уже даёт красивое число вроде `$coff_bribeprice_text`, используйте его для числа:

```text
Заплатить $coff_bribeprice_text $ruln_mem_coff_bribeprice_credit.
```

RU MorphLib здесь отвечает только за слово `кредит/кредита/кредитов`, а не за формат цены.

## Словарь

Слова для Quantity Layer лежат в:

```text
data/config/rulm/plurals.csv
```

Полная таблица: `docs/PLURALS_DICTIONARY.md`.
