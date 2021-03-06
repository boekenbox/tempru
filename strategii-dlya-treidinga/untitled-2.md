---
description: Трейлинг цены для различных типов заказов.
---

# TrailMe

TrailMe - это группа функций, которая позволяет вам отслеживать различные типы сделок, чтобы достичь лучших точек входа или выхода. На этой странице описаны все доступные параметры конфигурации. 

Трейлинг работает так же, как и для стратегии TSSL, различие является отправной точкой трейлинга. 

Ордера, полученные в результате трейлинга, размещаются только при выполнении основных критериев стратегии, и подтверждающие индикаторы \(если таковые имеются\) разрешают ордер. Все эти условия должны происходить в одном и том же цикле.

## Настройки параметров TrailMe <a id="trailme-settings-parameters"></a>

### Trail Me Buy - Покупка при Trail Me <a id="trail-me-buy"></a>

Используйте это для включения трейлинга в стиле tssl для стратегических ордеров на покупку.

**Values:** true or false

**Default value:** false

Parameter name in `config.js`: `TRAIL_ME_BUY`

### Trail Me Sell - Продажа при Trail Me <a id="trail-me-sell"></a>

Используйте это для включения трейлинга в стиле tssl для стратегий на продажу.

**Values:** true or false

**Default value:** false

Parameter name in `config.js`: `TRAIL_ME_SELL`

### Trail Me DU <a id="trail-me-du"></a>

Используйте это для включения трейлинга в стиле tssl для ордеров DU.

**Values:** true or false

**Default value:** false

Parameter name in `config.js`: `TRAIL_ME_DU`

### Trail Me RT Buy - Покупка при разворотной торговле <a id="trail-me-rt"></a>

Используйте это для включения трейлинга в стиле tssl для ордеров на покупку при разворотной торговле RT\_BUY.

**Values:** true or false

**Default value:** false

Parameter name in `config.js`: `TRAIL_ME_RT`

### Trail Me RT Sell - Продажа при РТ <a id="trail-me-rt-sell"></a>

Используйте это для включения трейлинга в стиле tssl для ордеров RT\_SELL выше последней ставки RT\_BUY.

**Values:** true or false

**Default value:** false

Parameter name in `config.js`: `TM_RT_SELL`

### Trail Me Buy Range - Покупка в диапазоне <a id="trail-me-buy-range"></a>

Это устанавливает диапазон покупки для TrailMe. 

Установка диапазона 0,5% при начальной цене 0,1 установит диапазон от 0,0995 до 0,1005. Пока цены продолжают двигаться вниз, диапазон движется вниз вместе с ценой. 

Как только цены начинают повышаться, диапазон замораживается, и ордер на покупку размещается, когда цена пересекает верхнюю границу диапазона.

**Values:** числовой - представляет процент.

**Default value:** 0.5

Parameter name in `config.js`: `TRAIL_ME_BUY_RANGE`

### Trail Me Sell Range - Продажа в диапазоне <a id="trail-me-sell-range"></a>

Это устанавливает диапазон продаж для TrailMe. 

Установка диапазона 0,5% при текущей цене 0,1 установит диапазон от 0,0995 до 0,1005. Пока цены продолжают двигаться вверх, диапазон движется вместе с ценой. 

Как только цены начинают снижаться, диапазон замораживается и выставляется ордер на продажу, когда цены пересекают нижнюю границу диапазона.

**Values:** числовой - представляет процент.

**Default value:** 0.5

Parameter name in `config.js`: `TRAIL_ME_SELL_RANGE`

### Trail Me RT Sell Range <a id="trail-me-rt-sell-range"></a>

Это устанавливает диапазон продаж для TrailMe. 

Установка диапазона 0,5% при текущей цене 0,1 установит диапазон от 0,0995 до 0,1005. Пока цены продолжают двигаться вверх, диапазон движется вместе с ценой. 

Как только цены начинают снижаться, диапазон замораживается и выставляется ордер на продажу, когда цены пересекают нижнюю границу диапазона.

**Values:** числовой, представляет процент.

**Default value:** 0.5

Parameter name in `config.js`: `TRAIL_ME_RT_SELL_RANGE`





