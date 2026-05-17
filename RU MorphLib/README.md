# RU MorphLib 0.6.14b

RU MorphLib - библиотека русской морфологии для переводов Starsector.

Автор: Lasplagas.

Мод нужен переводчикам и авторам русификаций. Он не переводит текст сам, а даёт безопасные токены и API, чтобы в `rules.csv`, диалогах и JAR/UI-коде нормально работали русский род, падежи, обращения к игроку и формы чисел.

## Что нового в 0.6.14b

- Добавлены отдельные н-формы местоимений после уже написанного предлога: `него`, `неё`, `нему`, `ней`, `ним`, `нём`.
- Главная новая группа: `$rulm_himAfterPrep*`.
- Это нужно для фраз вроде `для $rulm_himAfterPrepGen`, `к $rulm_himAfterPrepDat`, `с $rulm_himAfterPrepIns`, `о $rulm_himAfterPrepPrep`.
- Готовые формы с частыми предлогами вроде `$rulm_forHim`, `$rulm_withHim`, `$rulm_aboutHim` остаются и часто удобнее.
- Runtime JAR не менялся относительно подтверждённой ветки `0.6.13 FINAL`; обновлены таблица токенов и документация.

## Что мод умеет сейчас

| Задача переводчика | Слой | Пример |
|---|---|---|
| Текущий NPC, пленник, офицер, контакт, собеседник | `$rulm_*` | `$rulm_thisNom $rulm_prisonerNom` |
| Игрок и выбранное обращение `Сэр/Мэм/Капитан` | `$rulp_*` | `$rulp_Address, $rulp_youNom $rulp_arrivedDirect` |
| Полное слово после числа прямо в токене | `$ruln_num_*` | `$ruln_num_5_credit` -> `кредитов` |
| Полное слово для ресурса игрока | `$ruln_player*` | `$ruln_playerCreditsValue $ruln_playerCredits_credit` |
| Полное слово для числа из memory/dialogue variable | `$ruln_mem_*` | `$coff_ransomprice_text $ruln_mem_coff_ransomprice_credit` |
| Только окончание/хвост слова для динамического числа | `$ruln_suf_mem_*`, `$ruln_suf_player_*` | `$price_text кредит$ruln_suf_mem_price__blank__a__ov` |
| Java/Kotlin/JAR/UI-код | `RuMorphQuantity` | `RuMorphQuantity.word(amount, "credit")` |

## Быстрый пример

```text
$rulm_GuyOrGirlNom молча смотрит в пол. Конвой ведёт $rulm_himAcc к шаттлу.
Никто сегодня не вступится за $rulm_himAfterPrepAcc.
```

В игре это может стать:

```text
Парень молча смотрит в пол. Конвой ведёт его к шаттлу.
Никто сегодня не вступится за него.

Девушка молча смотрит в пол. Конвой ведёт её к шаттлу.
Никто сегодня не вступится за неё.
```

## Новые токены 0.6.14b

| Токен | Мужская форма | Женская форма | Когда использовать |
|---|---|---|---|
| `$rulm_himAfterPrepGen` | него | неё | после предлогов с родительным: `для`, `без`, `от`, `у`, `ради` |
| `$rulm_himAfterPrepAcc` | него | неё | после предлогов с винительным: `в`, `на`, `за`, `через` |
| `$rulm_himAfterPrepDat` | нему | ней | после `к`, иногда `по` |
| `$rulm_himAfterPrepIns` | ним | ней | после `с`, `перед`, `над`, `за` |
| `$rulm_himAfterPrepPrep` | нём | ней | после `о`, `в`, `на`, `при` |

## Токены 0.6.14a

| Назначение | Нижний регистр | Верхний регистр | Мужская форма | Женская форма |
|---|---|---|---|---|
| парень/девушка, им. | `$rulm_guyOrGirlNom` | `$rulm_GuyOrGirlNom` | парень | девушка |
| парень/девушка, род. | `$rulm_guyOrGirlGen` | `$rulm_GuyOrGirlGen` | парня | девушки |
| парень/девушка, дат. | `$rulm_guyOrGirlDat` | `$rulm_GuyOrGirlDat` | парню | девушке |
| парень/девушка, вин. | `$rulm_guyOrGirlAcc` | `$rulm_GuyOrGirlAcc` | парня | девушку |
| парень/девушка, твор. | `$rulm_guyOrGirlIns` | `$rulm_GuyOrGirlIns` | парнем | девушкой |
| парень/девушка, предл. | `$rulm_guyOrGirlPrep` | `$rulm_GuyOrGirlPrep` | парне | девушке |
| мужчина/женщина, им. | `$rulm_manOrWomanNom` | `$rulm_ManOrWomanNom` | мужчина | женщина |
| мужчина/женщина, род. | `$rulm_manOrWomanGen` | `$rulm_ManOrWomanGen` | мужчины | женщины |
| мужчина/женщина, дат. | `$rulm_manOrWomanDat` | `$rulm_ManOrWomanDat` | мужчине | женщине |
| мужчина/женщина, вин. | `$rulm_manOrWomanAcc` | `$rulm_ManOrWomanAcc` | мужчину | женщину |
| мужчина/женщина, твор. | `$rulm_manOrWomanIns` | `$rulm_ManOrWomanIns` | мужчиной | женщиной |
| мужчина/женщина, предл. | `$rulm_manOrWomanPrep` | `$rulm_ManOrWomanPrep` | мужчине | женщине |

## С чего начать переводчику

1. Откройте `docs/START_HERE_FOR_TRANSLATORS.md`.
2. Затем откройте `docs/TOKEN_LAYERS_CHEATSHEET.md`.
3. Для полного списка токенов используйте `docs/TOKENS_REFERENCE.md` и `docs/TOKENS_FULL_TABLE.md`.
4. Для чисел и ресурсов используйте `docs/QUANTITY_LAYER.md`.
5. Для динамических окончаний используйте `docs/QUANTITY_SUFFIX_LAYER.md`.

## Установка

Скопируйте папку `RU_MorphLib` в папку `mods` Starsector и включите мод в лаунчере.

Другой мод может указать зависимость:

```json
{
  "id": "your_mod_id",
  "name": "Your Mod",
  "dependencies": [
    { "id": "ru_morphlib", "name": "RU MorphLib" }
  ]
}
```

## Ограничения

- Мод не заменяет ручной перевод.
- Мод не угадывает неизвестные числа из чужих модов без аудита.
- Мод не форматирует сырые числа вроде `9375.0` в `9,375¢`.
- Статичные числа переводятся руками.
- Для редких UI-сцен всё равно нужна проверка в игре.

Полный список ограничений: `docs/KNOWN_LIMITATIONS.md`.
