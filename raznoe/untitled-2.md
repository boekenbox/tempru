# Logs

Журналы Gunbot содержат большую часть информации, с которой он работает. Эта статья содержит обзор различных разделов в этих журналах и объясняет, как их читать. ‌ 

Эта статья относится ко всем стратегиям, кроме Emotionless, который намеренно ограничил вывод журнала. ‌ 

Файлы журналов для каждой торговой пары автоматически сохраняются в папке / gunbot\_logs и автоматически превращаются в архивные копии после достижения размера файла 25 МБ. На каждую торговую пару хранится до трех резервных лог-файлов.

## Trailing <a id="trailing"></a>

Когда вы используете стратегию, которая содержит трейлинг, несколько разделов цикла журнала содержат всю информацию, связанную с трейлингом.

_Записи в журнале для TrailMe Trailing и TSSL выглядят практически одинаково и следуют той же логике, отличаются только начальные точки для трейлинга._

![](https://user-images.githubusercontent.com/2372008/41924015-3d28d2e6-7969-11e8-8cab-4637c23f70fb.png)

### **Buy trailing** <a id="buy-trailing"></a>

| Значение | Описание |
| :--- | :--- |
| `TrailingBuy limit` | Нижний предел для трейлинга, как определено установленным диапазоном покупки. Это значение обновляется каждый цикл, после движения цены `Last price`. |
| `Last price` | Текущая минимальная цена предложения. |
| `Target to buy` | Начальная точка для покупки трейлинга, процент от самой низкой EMA, как определено с `BUY_LEVEL`. |
| `Stop limit` | Верхний предел для трейлинга, как определено установленным диапазоном покупки. Это значение обновляется каждый цикл, после движения цены`Last price`. |

Ордер на покупку возникает, когда `Last price` пересекает `Stop limit` и находится ниже самой низкой EMA. 

Когда в журналах указывается, что цена находится в диапазоне, это означает, что текущая цена находится между `Stop limit` и `TrailingBuy limit`.

### **Sell trailing** <a id="sell-trailing"></a>

| **Значение** | Описание |
| :--- | :--- |
| `TrailingStop limit` | Верхний предел для трейлинга, определяемый установленным диапазоном продаж. Это значение обновляется каждый цикл, после движения цены `Last price`. |
| `Last price` | Текущая максимальная цена. |
| `Target to sell` | Начальная точка для трейлинга на продажу, процент от средней цены покупки, как определеноwith `GAIN`. |
| `StopLoss limit` | Нижний предел для трейлинга, как определено установленным диапазоном продаж. Это значение обновляется каждый цикл, после движения цены `Last price`. |

Ордер на продажу будет иметь место, когда `Last price`пересечет `StopLoss limit` после того, как он окажется в диапазоне и будет соответствовать `GAIN`. 

Когда в журналах указывается, что цена находится в диапазоне, это означает, что текущая цена находится между `StopLoss limit` и `TrailingStop limit`. 

Если вы установили `TSSL_TARGET_ONLY`в false, ордера на продажу также будут размещены без учета `GAIN`. Это можно использовать только для TSSL, но не для TrailMe

## The "grid" <a id="the-grid"></a>

Так называемая область сетки содержит всю информацию об основных проверках, индикаторах и торговых проверках. Этот раздел должен всегда отображаться для правильно обработанных циклов \(кроме `emotionless`, для этой стратегии не отображается сетка\).

![](https://user-images.githubusercontent.com/2372008/41924087-5e62f810-7969-11e8-9967-6b6299c1bba3.png)

### **Core checks** <a id="core-checks"></a>

| Значение | Описание |
| :--- | :--- |
| `Stop limit hit` | Указывает, достигли ли текущие цены или превысили установленный `STOP_LIMIT`. |
| `Can we buy` | Показывает ДА, если вы не владеете валютой котировки, и рыночные условия соответствуют одному или нескольким критериям стратегии покупки. |
| `Can we sell` | Показывает ДА, когда ваша собственная валюта котировки и рыночные условия соответствуют одному или нескольким критериям стратегии продажи. |
| `Panic sell` | Указывает, включен ли `PANIC_SELL` или нет. |
| `Can average` | Когда `DOUBLE_UP`включен, это показывает ДА, когда удвоение возможно в соответствии с `DU_METHOD`и `DU_CAP_COUNT`. |
| `REVERSAL TRADE` | Указывается, если пара находится в разворотной торговле. Показывает YES, когда `REVERSAL_TRADING`включен, `RT_BUY`выполнен, и пока нет ордера на выкуп. |

### **Indicators** <a id="indicators"></a>

В разделе индикаторов отображаются все индикаторы, рассчитанные Gunbot.

### **Trading checks** <a id="trading-checks"></a>

| Значение | Описание |
| :--- | :--- |
| `Ask` | Текущая минимальная цена предложения. |
| `Bid` | Текущая максимальная цена. |
| `Base Balance` | Общий доступный баланс базовой валюты. |
| `Quote Balance` | Общий доступный баланс валюты котировки. |
| `Quote On Orders` | Количество валюты котировки в настоящее время в открытых ордерах. |
| `BreakEven point` | Точка безубыточности, включая торговые сборы. |
| `ENTRY POINT` | Цена для покупки, в соответствии с настройками вашей стратегии. Например, с чистой стратегией полос Боллинджера вы бы увидели цену х% выше нижней полосы Боллинджера. Для стратегий без четкой точки входа, например, когда используются дополнительные подтверждающие индикаторы, здесь указывается цена для покупки в соответствии с `BUY_LEVEL`. |
| `EXIT POINT` | Цена для продажи, в соответствии с настройками вашей стратегии. Например, с чистой стратегией полос Боллинджера вы увидите цену на% ниже верхней полосы Боллинджера. Для стратегий без четкой точки выхода, например, когда используются дополнительные подтверждающие индикаторы, здесь указывается цена продажи в соответствии с `GAIN`. |
| `RT BUY` | Цена для покупки на следующий RT\_BUY. Когда трейлинг включен, эта цена является отправной точкой для трейлинга. |
| `RT SELL` | Цена для покупки на следующий RT\_SELL. Когда трейлинг включен, эта цена является отправной точкой для трейлинга. |
| `BUYBACK` | Точка безубыточности, где разворотная торговля выкупит сумку, чтобы продолжить обычную торговлю. |
| `STOP LIMIT` | Стоп-лимит рассчитывается как средняя покупная цена минус`STOP_LIMIT`. |
| `XTREND` | Показывает тренд, измеренный XTREND. Используется только для Stepgain. |
| `BAG VALUE IN BASE` | Показывает стоимость вашей «сумки» в базовой валюте. Может случиться, что это значение не исчезнет после ордера на продажу, это не имеет значения и будет обновлено после следующего ордера на покупку. |
| `LAST TRADE P/L` | Процент прибыли или убытка последнего ордера на продажу стратегии. |
| `BASE LAST TRADE P/L` | Абсолютная прибыль или убыток последней стратегии на продажу. |

### **Profit/Loss - Прибыль и убытки** <a id="profit-loss"></a>

Этот раздел показывает точную статистику прибылей и убытков по каждой торговой паре. Сборы уже вычтены.

Все сделки, полученные с биржи, анализируются, использование `IGNORE_TRADES_BEFORE`может привести к тому, что только сделки с определенной даты и времени будут выбраны и проанализированы

| Значение | Описание |
| :--- | :--- |
| `Pair P/L` | Сумма всех поступлений за пару \(заявки на покупку имеют отрицательную выручку\). Только понятные прибыль и убытки. |
| `Normal Trading` | Прибыль / убыток по всем сделкам, кроме сделок, совершенных во время торговли с разворотом. Заказы на покупку без последующих заявок на продажу учитываются как нереализованная прибыль, полная сумма заказа на покупку считается убытком. |
| `Reversal Trading` | Profiti / Loss для сделок, совершенных только во время разворотной торговли. Заявки на покупку без последующей заявки на продажу учитываются как нереализованная прибыль, полная сумма заявки на покупку считается убытком. |
| `Last 24h` | То же, что и для `Pair P/L`, но фильтруется для сделок, совершенных за последние 24 часа. Обратите внимание, что это может быть неправильно, если перед продажей произошло несколько ордеров на покупку, и один или несколько из них выходят за пределы отфильтрованного периода времени. |
| `Last week` | То же, что и для `Pair P/L`, но фильтруется для сделок, совершенных за последние 7 дней. Обратите внимание, что это может быть неправильно, если перед продажей произошло несколько ордеров на покупку, и один или несколько из них выходят за пределы отфильтрованного периода времени. |
| `Last month` | То же, что и для `Pair P/L`, но фильтруется для сделок, совершенных за последние 30 дней. Обратите внимание, что это может быть неправильно, если перед продажей произошло несколько ордеров на покупку, и один или несколько из них выходят за пределы отфильтрованного периода времени. |

