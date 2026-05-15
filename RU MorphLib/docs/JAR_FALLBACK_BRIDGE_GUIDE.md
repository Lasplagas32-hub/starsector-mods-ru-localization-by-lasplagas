# RU MorphLib - fallback-интеграция для JAR

## 1. Когда это нужно

Обычным `rules.csv`-диалогам JAR-bridge не нужен. RU MorphLib уже работает через штатную систему token replacement Starsector.

Fallback-интеграция нужна только если мод выводит текст напрямую из JAR и не прогоняет строку через стандартную подстановку токенов.

Примеры рискованных зон:

```text
custom shop UI
custom intel UI
custom tooltip panel
самописные диалоговые панели
hardcoded addPara/addOption без token replacement
```

Если на экране видно сырой `$rulm_*`, значит эта строка, вероятно, не прошла через стандартный token replacement.

## 2. Предпочтительный способ

Лучший fallback - не читать `tokens.csv` вручную, а заставить JAR мода прогонять строку через штатный token replacement Starsector перед выводом.

Смысл:

```text
сырой текст с $rulm_*
-> стандартный token replacement Starsector
-> RU MorphLib отдаёт замены
-> готовый русский текст выводится на экран
```

Псевдокод:

```java
String raw = "$rulm_He поднял$rulm_past взгляд.";
String resolved = rules.performTokenReplacement(ruleId, raw, dialog, memoryMap);
dialog.getTextPanel().addPara(resolved);
```

Точную сигнатуру `performTokenReplacement` нужно сверять по версии Starsector API. Для 0.98a-RC8 подтверждён сам механизм `RuleTokenReplacementGeneratorPlugin`.

## 3. Запасной data bridge

Если стандартный token replacement использовать нельзя, можно сделать ручной data bridge.

Идея:

```text
1. JAR переводимого мода читает RU_MorphLib/data/config/rulm/tokens.csv.
2. Берёт gender нужного PersonAPI.
3. Выбирает колонку masc или fem.
4. Заменяет $rulm_* в строке перед выводом.
```

Псевдокод:

```java
String csv = Global.getSettings().loadText(
    "data/config/rulm/tokens.csv",
    "ru_morphlib"
);

boolean female = person != null && person.getGender() == Gender.FEMALE;

Map<String, String> forms = loadForms(csv, female ? "fem" : "masc");

String resolved = raw;
for (Map.Entry<String, String> entry : forms.entrySet()) {
    resolved = resolved.replace(entry.getKey(), entry.getValue());
}

dialog.getTextPanel().addPara(resolved);
```

Это именно fallback. Для обычных `rules.csv`-диалогов так делать не нужно.

## 4. Чего не делать

Не копируй всю таблицу токенов внутрь JAR каждого переводимого мода.

Плохо:

```text
каждый мод хранит свою копию tokens.csv
обновления RU MorphLib не доходят до старых JAR
сложнее поддержка
```

Лучше:

```text
RU MorphLib хранит tokens.csv
переводимый мод зависит от RU MorphLib
JAR только вызывает token replacement или читает tokens.csv при необходимости
```

## 5. Что писать в инструкции к переводу

Если перевод использует только `rules.csv`-токены:

```text
Требуется RU MorphLib. Дополнительная JAR-интеграция не нужна.
```

Если перевод патчит custom JAR UI:

```text
В этом переводе есть JAR-интеграция RU MorphLib для custom UI. Она нужна только для строк, которые не проходят через стандартную token replacement систему Starsector.
```
