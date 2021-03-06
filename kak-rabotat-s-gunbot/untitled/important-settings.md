---
description: >-
  Поймите самые важные настройки: настройки баланса, которые определяют, сколько
  может потратить Gunbot.
---

# Важные настройки

{% hint style="info" %}
Каждая торговая стратегия содержит несколько настроек баланса, это одни из самых важных настроек, и вы должны понимать, что они делают.
{% endhint %}

## Торговый лимит

С помощью этой настройки вы указываете Gunbot, сколько потратить на заказ на покупку. 

Торговый лимит обычно определяется в «базовой валюте» пары. Это означает, что если вы хотите купить LTC с BTC, торговый лимит должен быть установлен в биткойнах. Если вы хотите купить BTC за доллары США, вам необходимо установить торговый лимит в виде суммы в долларах США. 

Поскольку в криптографии есть много разных базовых валют, очень важно, чтобы вы установили это правильно. Неправильная установка может привести к торгам на нежелательные суммы или к торгам вообще. 

Важно установить торговый предел, по крайней мере, немного выше, чем минимальный размер сделки вашей биржи. 

Причина этого заключается в том, что из-за округления и / или сборов торговля в основном приводит к сумме, немного превышающей торговый лимит. Если эта сумма меньше минимального размера сделки вашей биржи, она не может быть продана без покупки дополнительных единиц.

## Минимальный объем для продажи

Этот параметр определяет минимальный размер сделки для пары, которой вы торгуете, это касается как пары, так и биржи. При правильной настройке Gunbot будет игнорировать низкие балансы, которые не могут быть проданы. 

Найдите минимальный размер сделки для вашей пары и установите его именно так. 

**Пример использования:**

* Торговая пара: USDT-BTC 
* Биржа определила минимальный размер сделки: 10 USDT 
* Текущее значение баланса: 8 USDT

Когда минимальный объем для продажи правильно установлен на 10, Gunbot проигнорирует текущий баланс и продолжит поиск возможности покупки. 

Когда минимальный объем продажи установлен неправильно, например, 3, Gunbot попытается продать текущий баланс стоимостью всего 8 USDT. Это не удастся, потому что биржа не разрешает торговлю.

## Минимальный объем для продажи

Этот параметр очень похож на минимальный объем для продажи, он определяет минимальную сумму, на которую Gunbot может разместить ордер на покупку. 

Найдите минимальный размер сделки для вашей пары и установите его именно так. Обычно этот параметр устанавливается точно так же, как минимальный объем для продажи. 

В некоторых случаях Gunbot будет размещать ордер на покупку несколькими частями, настройка минимального объема на покупку сообщает боту, какой может быть абсолютная минимальная сумма для частичного ордера. Если вы установите его слишком низким, такие сделки не удастся.

{% hint style="danger" %}
**Примечание редактора:**

В боте по умолчанию прописаны настройки минимального объема в BTC? если вы создаете торговлю пары например USDT-BTC то вам придется в стратегии прописывать минимальный объем в USDT. Если вы захотите сменить стратегию на этой паре, то вам придется снова прописывать минимальный объем в новой стратегии. И соответственно другие пары работающие с основной валютой BTC на этой же стратегии уже работать не будут, потому что им требуется запись минимального объема в BTC.

Выход из этой ситуации один, создавать копии стратегий, которые будут работать с другой основной валютой и уже их использовать в торговле с ней. 

При создании копии стратегии нужно будет менять все настройки из BTC \(по умолчанию\) в USDT или другую основную валюту, которую вы выберете.
{% endhint %}



