---
title: Как убыточную стратегию сделать прибыльной
tags: проверкаидеи
---

Продолжаю серию заметок с самой простой стратегией для трейдинга. 

1. [Рассмотрел очень простую стратегию: покупай после закрытия вниз и продавай после закрытия вверх](https://zenoftrading.github.io/very-simle-trading-strategy-1.html)
2. [Посмотрел сколько может быть закрытий подряд и на что это влияет](https://zenoftrading.github.io/very-simle-trading-strategy-2.html)
3. [Посмотрел как влияют комиссии ](https://zenoftrading.github.io/very-simle-trading-strategy-3.html)
4. [Рассмотрел стратегию на 15 активах за 10 лет](https://zenoftrading.github.io/very-simle-trading-strategy-4.html)

Сегодня буду пробовать улучшаять эквити.

Итак, среди эквити есть те, которые стремятся к 0. А что если покупки заменить продажами, а продажи покупками? Возможно кривая изменит свой характер на противоположный. Отзеркалится. Примерно вот так:

![](/assets/images/2020/12/waiting.png)\
Примерно так я себе представлял изменения, если поменять покупки на продажи и продажи на покупки

Посмотрим как будет на самом деле.

![](/assets/images/2020/12/buy_vs_reverse.png)\
Покупки с разным количеством одинаковых закрытий подряд

![](/assets/images/2020/12/sell_vs_reverse.png)\
Продажи с разным количеством одинаковых закрытий подряд

![](/assets/images/2020/12/buysell_vs_reverse.png)\
Покупки и продажи вместе с разным количеством одинаковых закрытий подряд

Еще посмотрим под другим углом:
![](/assets/images/2020/12/buy_vs_reverse_days.png)\
Сравнение прямых сделок с реверсом по дням

Ну всё, можно открывать шампанское. Работает. Есть универсальная стратегия, как превратить любую убыточную стратегию в прибыльную. Достаточно просто сделать реверс. Там где покупали продавать и там где продавали покупать... Что-то забыл? Ах да, комиссии. Посмотрим как это всё выглядит с комиссиями:

![](/assets/images/2020/12/buy_vs_reverse_days_commiss.png)\
Сравнение прямых сделок с реверсом по дням с комиссиями

Реальность оказалась немного иначе. Опять комиссии всё портят. И я всё больше понимаю, что биржи и брокеры это отличный бизнес.

Что это всё нам даёт:
1. Смена местами покупки и продажи может сделать убыточную статегию прибыльной, при условии, что нет комиссий.
2. Если есть комиссии, то такая процедура сделает даже прибыльные сстратегии убыточными. В общем так делать не надо.

Как обычно, код для бектестера можно найти в телеграме [https://t.me/zenoftrading](https://t.me/zenoftrading)

Что ещё рассмотрю в ближайшее время:
1. Что если совершать сделки не в один день (покупать на открытии и продавать на закрытии), а покупать на предыдущем закртытии? Когда уже понятно, что день закрывается вниз. Часто гэпы возникают между днями. Посмотрю как они улучшат или ухудшат статегию.
2. Как на прибыльные стратегии влияет плечо. На сколько увеличится прибыль и увеличится ли вообще.