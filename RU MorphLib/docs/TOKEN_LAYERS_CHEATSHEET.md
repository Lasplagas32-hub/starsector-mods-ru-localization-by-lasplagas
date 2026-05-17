# Token Layers Cheatsheet

| Задача переводчика | Слой | Пример |
|---|---|---|
| Текущий NPC, пленник, офицер, контакт, собеседник | `$rulm_*` | `$rulm_thisNom $rulm_prisonerNom` |
| Игрок и выбранное обращение `Сэр/Мэм/Капитан` | `$rulp_*` | `$rulp_Address, $rulp_youNom $rulp_arrivedDirect` |
| Полное слово после числа прямо в токене | `$ruln_num_*` | `$ruln_num_5_credit` -> `кредитов` |
| Полное слово для ресурса игрока | `$ruln_player*` | `$ruln_playerCreditsValue $ruln_playerCredits_credit` |
| Полное слово для числа из memory/dialogue variable | `$ruln_mem_*` | `$coff_ransomprice_text $ruln_mem_coff_ransomprice_credit` |
| Только окончание/хвост слова для динамического числа | `$ruln_suf_mem_*`, `$ruln_suf_player_*` | `$price_text кредит$ruln_suf_mem_price__blank__a__ov` |
| Java/Kotlin/JAR/UI-код | `RuMorphQuantity` | `RuMorphQuantity.word(amount, "credit")` |


## Слои коротко

### `$rulm_*` - NPC Layer

Для текущего NPC или `activePerson`: пленник, офицер, контакт, собеседник.

| Токен | Мужская форма | Женская форма | Когда использовать |
|---|---|---|---|
| `$rulm_he` | он | она | простое местоимение |
| `$rulm_He` | Он | Она | начало предложения |
| `$rulm_himAcc` | его | её | винительный: вижу кого |
| `$rulm_himDat` | ему | ей | дательный: дать кому |
| `$rulm_himGen` | его | её | родительный или притяжательная форма |
| `$rulm_himAfterPrepGen` | него | неё | если предлог уже написан: `для $rulm_himAfterPrepGen` |
| `$rulm_withHim` | с ним | с ней | готовая форма с предлогом |
| `$rulm_aboutHim` | о нём | о ней | готовая форма с предлогом |
| `$rulm_thisNom` | этот | эта | этот пленник / эта пленница |
| `$rulm_thisAccAnim` | этого | эту | вести этого / эту |
| `$rulm_prisonerNom` | пленник | пленница | нейтральное слово для TNP-like сцен |
| `$rulm_prisonerAcc` | пленника | пленницу | действие над пленником |
| `$rulm_speakerNom` | собеседник | собеседница | когда слово пленник не подходит |
| `$rulm_capturedState` | захвачен | захвачена | готовое состояние |
| `$rulm_hiredState` | нанят | нанята | готовое состояние |
| `$rulm_freedState` | освобождён | освобождена | готовое состояние |

Если предлог уже есть в строке, используйте н-формы `$rulm_himAfterPrep*`: `для $rulm_himAfterPrepGen`, `к $rulm_himAfterPrepDat`, `с $rulm_himAfterPrepIns`, `о $rulm_himAfterPrepPrep`.


### `$rulp_*` - Player Address Layer

Для игрока и выбранного обращения.

| Токен | Вывод для `Сэр` | Вывод для `Мэм` | Вывод для `Капитан` |
|---|---|---|---|
| `$rulp_Address` | Сэр | Мэм | Капитан |
| `$rulp_address` | сэр | мэм | капитан |
| `$rulp_LuddicAddress` | Брат | Сестра | Путник |
| `$rulp_he` | он | она | вы |
| `$rulp_himAcc` | его | её | вас |
| `$rulp_withHim` | с ним | с ней | с вами |
| `$rulp_aboutHim` | о нём | о ней | о вас |
| `$rulp_heArrived` | он прибыл | она прибыла | вы прибыли |
| `$rulp_heKnown` | он известен | она известна | вы известны |
| `$rulp_youNom` | вы | вы | вы |
| `$rulp_arrivedDirect` | прибыли | прибыли | прибыли |
| `$rulp_readyDirect` | готовы | готовы | готовы |


### `$ruln_*` - Quantity Layer

Для чисел и слов после чисел.

| Маршрут | Когда нужен | Пример |
|---|---|---|
| `$ruln_num_<N>_<wordId>` | число известно прямо в строке | `$ruln_num_22_credit` -> `кредита` |
| `$ruln_player<resource>` | ресурс игрока | кредиты, топливо, припасы, морпехи |
| `$ruln_mem_<key>_<wordId>` | число лежит в memory/dialogue variable | `$ruln_mem_coff_ransomprice_credit` |
| `$ruln_suf_mem_*` | нужен только хвост слова после dynamic числа | `кредит` + `ов` |

## Падежи

| Суффикс | Падеж | Когда нужен |
|---|---|---|
| `Nom` | именительный | кто? что? |
| `Gen` | родительный | кого? чего? нет кого? |
| `Dat` | дательный | кому? чему? |
| `Acc` | винительный | кого? что? |
| `AccAnim` | винительный одушевлённый | видеть пленника, этого офицера |
| `AccInan` | винительный неодушевлённый | видеть этот объект |
| `Ins` | творительный | кем? чем? |
| `Prep` | предложный | о ком? о чём? |

