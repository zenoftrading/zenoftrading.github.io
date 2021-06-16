---
title: Как скачать исторические котировки c yahoo finance и финама с помощью python
tags: python
---

В одной из [прошлых заметок](https://zenoftrading.github.io/buyonclose-650.html) мне нужно было скачать исторические котировки по 650 активам. Часть из них на российском рынке, часть крипта и большая часть на рынке США. Всё, что касается крипты, валют и американского рынка качал с yahoo finance. Российский рынок качал с финама. Естественно качал с помощью питона. Дальше расскажу как это можно повторить.

## Yahoo finance и python

Пакет `yfinance`. Гитахб https://github.com/ranaroussi/yfinance Установка командой: `pip install yfinance`

Можно качать не только дневные данные. Интервалы из документации: 1m,2m,5m,15m,30m,60m,90m,1h,1d,5d,1wk,1mo,3mo На практике данные меньше дневных сильно ограничены. Например, часовые доступны за 60 последних дней.

Перейдём к делу, как качать котировки:

```
import yfinance as yf

data = yf.download("TSLA", start="2017-01-01", end="2017-04-30")
```

Как добавить интервал:

```
data = yf.download("TSLA", start="2017-01-01", end="2017-04-30", interval='1h')
```

Данные скачиваются в датафрейм. Датафрейм можно сохранить в csv:

```
data.to_csv('tsla.csv')
```

Для тикеров с московской биржи нужно добавить постфикс .ME. То есть SBER и GAZP превращаются в SBER.ME и GAZP.ME Для валют тикеры выглядят вот так RUBUSD=X Для криптовалют BTC-USD

## Finam и python

Нашёл замечательный пакет `finam-export`. Гитхаб https://github.com/ffeast/finam-export Установить можно командой: `pip install finam-export`

В отличии от яху финанс можно качать даже тиковые данные за любой срок! Правда где-то читал, что за слишком большой срок данные могут качаться несколько дней. Я пока не придумал как использовать тиковые данные.

Сам пакет не так хорошо продуман, как предыдущий. Иногда приходится поломать голову.

Как тут качать? Минимальный набор:

```
from finam import Exporter, Market, Timeframe

exporter = Exporter()
ticker = 'SBER'
asset = exporter.lookup(name=ticker, market=Market.SHARES)
asset_id = asset[asset['name'] == ticker].index[0]
data = exporter.download(asset_id, market=Market.SHARES)
```

Ищем айдишник тикера в финаме и по нему скачиваем котировки.

Вот так можно задавать другие параметры:

```
data = exporter.download(asset_id, market=Market.SHARES, start_date=datetime.date(2017, 1, 1), end_date=datetime.date(2018, 1, 1), timeframe=Timeframe.DAILY)
```

### Особенности finam-export

Тикер нужно искать в том рынке, где он есть. Фьючерсы во фьючерсах, акции в акциях. Если искать без рынка, то у одного тикера может найтись несколько айдишников. Константы по рынкам и таймфреймам можно посмотреть в файле: https://github.com/ffeast/finam-export/blob/master/finam/const.py

Иногда в строчке `asset = exporter.lookup(name=ticker, market=Market.SHARES)` нужно name заменить на code, будет вот так `asset = exporter.lookup(code=ticker, market=Market.SHARES)` Хрен его знает что от этого меняется, но иногда работает так иногда так.

В константах может не быть рынка, который вам нужен. Например для биткоина айдишник рынка 520. Его нет в константах. Я пробовал его добавлять руками, но котировки всё равно не качались. Если знаете как скачать, напишите.

Если качать много тикеров, то нужно задавать задержку между заросами в одном тикере и между тикерами, инче будет 403 ошибка. Я прописывал через рандом в запросе: `data = exporter.download(asset_id, market=Market.SHARES, start_date=datetime.date(2017, 1, 1), end_date=datetime.date(2018, 1, 1), timeframe=Timeframe.DAILY, delay=random.randint(3,5))` И в цикле: `time.sleep(random.randint(3,5))`

## Как скорость?

Да в целом норм. Дневные данные по 650 тикерам с января 2007 года вчера скачались примерно за час.
