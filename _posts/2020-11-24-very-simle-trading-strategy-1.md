---
title: Самая простая стратегия для трейдинга
tags: проверкаидеи
---

Когда читал книгу Ларри Вильямса «Долгосрочные секреты краткосрочной торговли», думал, что хорошо бы проверить о чём он там пишет. Итак, вот его первая идея. Цитата из книги:

> Фьючерс на фондовый индекс DAX за период с 1998 по 2011 годы. При покупке после каждого закрытия вниз с последующим выходом из рынка по цене закрытия того же самого дня мы совершим 1591 сделок, 52 процента которых будут выигрышными, но зато общая сумма убытка составит внушительные 60558$! При двух медвежьих закрытиях подряд реализуются 724 сделки, 52,2 процента которых будут закрыты с прибылью, причем общие потери оказываются значительно ниже – 1568$. Если вам хватит терпения каждый раз дожидаться подряд трёх закрытий вниз, вы будете вознаграждены 334 сделками, 55 процентов из которых принесут серьёзную прибыль 25295$.

Проверять буду на сбербанке, на чём же ещё. Взял историю за последние 10 лет. Вот его график.

![Купи и держи](/assets/images/2020/11/buyhold.png)

График цены сбербанка за последние 10 лет.

Написал на питоне простенький бектестер. Итак, смотрим график.

![Покупки](/assets/images/2020/11/equity_buy_1_3_days.png)

Покупки после 1, 2 и 3 закрытий вниз подряд. Получилось 1290, 626 и 294 сделок соответственно.

Что тут видим:
1. Сложно понять работает идея или нет, графики ходят туда сюда около 0
2. Чем больше закрытий вниз подряд, тем меньше просадка. В первом случае до 30%, во втором до 20%, в третьем до 10%
3. На дистанции в 10 лет есть небольшое увеличение доходности с увеличением количества дней закрытий подряд

Ларри пишет только про покупки, но посмотрим что будет если перевернуть сделки и продавать после закрытия вверх.

![Продажи](/assets/images/2020/11/equity_sell_1_3_days.png)

Продажи после 1, 2 и 3 закрытий вверх подряд. Получилось 1212, 547 и 238 сделок соответственно.

Что видно при продажах? В целом примерно тоже, что и при покупках:
1. При продажах после трёх закрытий вверх подряд идея скорее работает, чем нет. Но прибыль 60% за 10 лет.
2. Просадка так же уменьшается с количеством дней.
3. Чем больше ждём закрытий подряд, тем выше доходность.

А теперь посмотрим что будет при покупках и продажах одновременно.

![Покупки и продажи вместе](/assets/images/2020/11/equity_buysell_1_3_days.png)

Покупки и продажи после 1, 2 и 3 закрытий подряд. Сделок 2502, 1173 и 532 штук.

Что видим:
1. На последней кривой идея работает. Доходность около 70% за 10 лет.
2. У последней кривой почти нет просадки.
3. Чем больше ждём закрытий подряд, тем выше доходность.

## Выводы
1. Хоть доходность маленькая, но идея скорее работает чем нет, даже на сбербанке.
2. Идея очень простая, легко повторить.
3. Тест без учёта комиссий. Вероятно, что они съедят и без того маленькую доходность.

Думаю что даже такую простую идею можно доработать. Что проверю ещё и о чём напишу:
- Посмотрю как на доходность влияет комиссия.
- Проверю как эта идея ведёт себя на разных классах активов на разных рынках.
- Что будет если ждать 4, 5, а может 6 закрытий подряд?
- Что тут ещё можно улучшить?

P.S. Код бектестера на питоне можно взять в телеграме [https://t.me/zenoftrading](https://t.me/zenoftrading)