# Quantity Suffix Layer - dynamic suffix only

Suffix Layer нужен, когда в строке уже есть основа слова, а RU MorphLib должен подставить только окончание.

## Поддерживаемая модель

Только route-first dynamic sources:

```text
$ruln_suf_mem_<realMemoryKey>_<pattern>
$ruln_suf_player_<resourceId>_<pattern>
RuMorphQuantity.suffix(amount, pattern)
```

## Что не поддерживается как workflow

```text
$ruln_suf_num_*
previous-number guessing
автоматическое угадывание числа слева от слова
```

## Когда использовать

Хорошо:

```text
$coff_bribeprice_text полновесн$ruln_suf_mem_coff_bribeprice_yi__ih__ih кредит$ruln_suf_mem_coff_bribeprice__blank__a__ov
```

Смысл: число берётся из `$coff_bribeprice`, а красиво отформатированная цена берётся из `$coff_bribeprice_text`.

## Same-source multi-pattern

Один источник может управлять разными окончаниями в одной строке:

```text
$coff_bribeprice_text кредит$ruln_suf_mem_coff_bribeprice__blank__a__ov
$coff_bribeprice_text полновесн$ruln_suf_mem_coff_bribeprice_yi__ih__ih кредит$ruln_suf_mem_coff_bribeprice__blank__a__ov
```

## Как читать pattern

Pattern хранит варианты через `__`.

```text
_blank__a__ov
```

Обычно это значит:

```text
one -> пусто
few -> а
many -> ов
```

Точные паттерны лучше документировать рядом с конкретным модом, потому что суффиксы зависят от слова и фразы.
