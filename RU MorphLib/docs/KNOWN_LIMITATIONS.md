# Known Limitations

## Не автоматический переводчик

RU MorphLib не переводит английские строки на русский. Он только помогает уже переведённой строке правильно согласоваться по роду, падежу и числу.

## Static numbers manual

Статичные числа переводятся руками:

```text
5 кредитов
20 морпехов
3 дня
```

Не используйте dynamic suffix для обычного статичного текста.

## Unknown dynamic numbers need audit

Если чужой мод хранит число в неизвестной переменной, RU MorphLib не угадает её сам. Нужно найти реальный source:

```text
memory key
player resource
Java/Kotlin amount
```

После этого можно выбрать `$ruln_mem_*`, `$ruln_player*` или Public API.

## No previous-number guessing

Мод не смотрит на число слева в готовом тексте и не пытается угадать форму следующего слова.

## No raw float formatting

RU MorphLib не превращает `9375.0` в `9,375¢`. Используйте готовые formatted values мода или игры, например `$coff_bribeprice_text`, если они есть.

## Active person зависит от контекста

`$rulm_*` берёт текущего NPC/activePerson. Для TNP-like prisoner dialogs добавлен fallback, но в других модах всё равно нужен тест конкретной сцены.

## UI-fit остаётся задачей переводчика

Даже грамматически правильная строка может быть слишком длинной для кнопки, вкладки или tooltip.
