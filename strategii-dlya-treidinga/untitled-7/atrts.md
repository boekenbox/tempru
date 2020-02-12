# ATRTS

На этой странице описано, как маржинальная торговля на Bitmex работает со стратегией ATRTS. Триггеры для сделок немного отличаются от той же стратегии для обычной торговли.

## Как работать с этой стратегией <a id="how-to-work-with-this-strategy"></a>

**Ожидаемое поведение для маржинальной торговли**

Gunbot откроет одну позицию, длинную или короткую, и закроет эту позицию, когда цель будет достигнута. Когда срабатывает стоп до прибыльного закрытия сделки, Gunbot выставит стоп-ордер на убыток. После закрытия позиции Gunbot снова попытается открыть новую длинную или короткую позицию. Gunbot не добавит к существующим открытым позициям.

Пожалуйста, не добавляйте и не уменьшайте позиции, открытые Gunbot вручную, если только вы не прекратите запуск Gunbot на этой торговой паре, пока не закроете эту позицию.

​

### Long / Buy <a id="long-buy"></a>

Длинная позиция открывается, когда цена Ask пересекает длинное значение ATR предыдущего раунда.

### Short / Sell <a id="short-sell"></a>

Короткая позиция открывается, когда цена предложения пересекает значение ATR по сравнению с предыдущим раундом.

### Close <a id="close"></a>

Позиция закрывается при достижении желаемой `ROE`.

### Stop <a id="stop"></a>

Позиция закрывается с убытком при достижении `STOP_BUY`или `STOP_SELL`.

## Параметры Стратегий <a id="strategy-parameters"></a>

Эти настройки являются глобальными и применяются ко всем парам, использующим эту стратегию. Если вы хотите, чтобы определенный параметр отличался для одной или нескольких пар, используйте [переопределение ](../../kak-rabotat-s-gunbot/untitled-1/trading-pairs.md#override-settings-pereopredelenie-nastroiki)на уровне пары.

Используя параметры `BUY_METHOD`и `SELL_METHOD`, вы можете комбинировать различные методы покупки и продажи. На этой странице стратегии предполагается, что для `BUY_METHOD`и `SELL_METHOD`установлены значения `ATRTS`. Допустимые значения - это имена стратегий, перечисленные [здесь](../../#yarlyki-k-opisaniyam-strategii).

## Margin settings <a id="margin-settings"></a>

Margin settings control settings like leverage and the target for ROE. These parameters are relevant when using `ATRTS` as buy and/or sell method.

### ROE <a id="roe"></a>

This sets the target for closing a position.

ROE is the Return On Equity for a position, the percentage profit and loss on your invested margin. This value is calculated in a similar way to how Bitmex calculates it, it does include leverage and does not include fees.

**Examples:** Long position, 1x leverage. When price moves 1% above the average entry price, 1% ROE is reached.

Long position, 100x leverage \(or cross leverage\). When price moves 1% above the average entry price, 100% ROE is reached.

Short position, 20x leverage When price moves 1% below the average entry price, 20% ROE is reached.

**Values:** numerical – represent a percentage.

**Default value:** 1

Parameter name in `config.js`: `ROE`

### Leverage <a id="leverage"></a>

Sets the leverage for opening any position. Setting 0 places the order with cross margin.

**Values:** numerical

**Default value:** 0

Parameter name in `config.js`: `LEVERAGE`

### Stop Buy <a id="stop-buy"></a>

Places a market stop order for a long position, at the same time as the position is opened.

When set to 1 and a long order is opened at a price of 100, a stop market order will be placed at 99.

**Values:** numerical - represents a percentage.

**Default value:** 0

Parameter name in `config.js`: `STOP_BUY`

### Stop Sell <a id="stop-sell"></a>

Places a market stop order for a short position, at the same time as the position is opened.

When set to 1 and a short order is opened at a price of 100, a stop market order will be placed at 101.

**Values:** numerical - represents a percentage.

**Default value:** 0

Parameter name in `config.js`: `STOP_SELL`

### ROE Trailing <a id="roe-trailing"></a>

Use this to enable tssl-style trailing for ROE.

**Values:** true or false

**Default value:** false

Parameter name in `config.js`: `ROE_TRAILING`

### ROE Limit <a id="roe-limit"></a>

This sets the range for ROE trailing.

Setting a range of 5% at a ROE target of 1 would set an initial range between 0.95 and 1.05.

As long as ROE keeps increasing, the range moves along with ROE. As soon as ROE start decreasing, the lower range gets frozen. A close order is placed when ROE crosses the lower limit.

**Values:** numerical – represent a percentage of ROE.

**Default value:** 1

Parameter name in `config.js`: `ROE_LIMIT`

### Pre Order <a id="pre-order"></a>

When set to true, limit orders will placed at a configurable rate beyond the best bid/ask price to get ahead of the order book.

**Values:** true or false

**Default value:** false

Parameter name in `config.js`: `PRE_ORDER`

### Pre Order Gap <a id="pre-order-gap"></a>

Sets the gap between the best bid/ask price in the orderbook and the rate at which a limit order gets placed. Long orders are placed at ask + gap. Short orders are placed at bid - gap.

It is possible to use negative values, this will increase the chance of receiving maker fees.

Example when set to 1 and a buy signal occurs at an ask price of 100: a limit order gets placed at a rate of 101. When set to -1 and a buy signal occurs at an ask price of 100: a limit order gets placed at a rate of 99.

Don't use a negative gap together with `STOP_BUY` and/or `STOP_SELL`, as these stops do not combine well with position that do not always fill. Instead use `STOP_LIMIT`.

**Values:** numerical - represents a percentage.

**Default value:** 0

Parameter name in `config.js`: `PRE_ORDER_GAP`

## Buy settings <a id="buy-settings"></a>

Buy settings are the primary trigger for opening long positions. These parameters control the execution of buy orders when using `ATRTS` as buy method.

### Buy enabled <a id="buy-enabled"></a>

Set this to false to prevent Gunbot from placing buy orders.

**Values:** true or false

**Default value:** true

Parameter name in `config.js`: `BUY_ENABLED`

### NBA <a id="nba"></a>

"Never Buy Above". Use this to only allow buy orders below the last sell rate.

This sets the minimum percentage difference between the last sell order and the next buy. The default setting of 0 disables this option.

When set to 1, Gunbot will only place a buy order when the strategy buy criteria meet and price is at least 1% below the last sell price.

**Values:** numerical, represents a percentage.

**Default value:** 0

Parameter name in `config.js`: `NBA`

## Sell settings <a id="sell-settings"></a>

Sell settings are the primary trigger for opening short positions. These parameters control the execution of sell orders when using `ATRTS` as sell method.

### Sell enabled <a id="sell-enabled"></a>

Set this to false to prevent Gunbot from placing sell orders.

**Values:** true or false

**Default value:** true

Parameter name in `config.js`: `SELL_ENABLED`

## Indicator settings <a id="indicator-settings"></a>

Relevant indicators for trading with ATRTS.

These settings have a direct effect on trading with `ATRTS`.

### Period <a id="period"></a>

This sets the candlestick period used for trading, this affects all indicators within the strategy.

Only use [supported values](https://wiki.gunthy.org/how-to-work-with-gunbot/basic-workings/period#supported-period-values).

Setting a short period allows you to trade on shorter trends, but be aware that these will be noisier than longer periods.

**Values:** numerical– represents candlestick size in minutes.

**Default value:** 15

Parameter name in `config.js`: `PERIOD`

### ATRx <a id="atrx"></a>

This value defines the multiplier used for calculation of the lower and upper limits for trading with `ATRTS`

When set to 5, ATR gets multiplied by 5 and the result gets subtracted from next rounds bid & added to next rounds ask to set the limits.

**Values:** numerical - represents a multiplier for ATR.

**Default value:** 0.5

Parameter name in `config.js`: `ATRX`

### ATR Period <a id="atr-period"></a>

The number of periods used for calculating ATR.

**Values:** numerical, represents a number of periods.

**Default value:** 14

Parameter name in `config.js`: `ATR_PERIOD`

## Balance settings <a id="balance-settings"></a>

## **Confirming indicators + advanced indicator settings** <a id="confirming-indicators-advanced-indicator-settings"></a>

## **Misc settings** <a id="misc-settings"></a>

## Dollar cost avg settings <a id="dollar-cost-avg-settings"></a>

DCA is not intented to be used for margin trading.

## Reversal trading settings <a id="reversal-trading-settings"></a>

RT is not intented to be used for margin trading.

## TrailMe settings <a id="trailme-settings"></a>

TrailMe is not intended to be used with this strategy.

## Placeholders <a id="placeholders"></a>

The following parameters in `config.js` have no function for this strategy and act as placeholder.

