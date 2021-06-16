---
title: Binance API и margin orders
tags: python binance api
---
По мотивам своих исследований написал бота, который торгует криптой на бинансе. Стратегия это [покупка на прорыве волатильности](https://zenoftrading.github.io/range-prev-day.html).

Пока бот тестируется в спотовом режиме, разбираюсь с маржинальной торговлей через API бинанса. Пишу этот пост скорее как напоминалка для себя.

Обычный режим называется spot. И есть два типа маржинальной торговли:
1. cross-margin Устанавливается общее плечо на весь аккаунт. В зависимости от крипты плечо может быть до 3.
2. isolated margin Устанавливается отдельное плечо для каждой торговой пары. Тут плечо может быть до 10.

Общий алгоритм работы с маржинальной торговлей:
1. Сделать маржинальный аккаунт
2. Перевести туда крипту со спотового аккаунта
3. Взять крипту в долг
4. Отторговать
5. Отдать долг
6. Перевести крипту назад на спотовый аккаунт

https://python-binance.readthedocs.io/en/latest/margin.html документация

Далее буду рассматривать isolated margin так как там плечо больше.

## Сделать маржинальный аккаунт 

	client.create_isolated_margin_account(base='BTC', quote='ETH')

## Перевести крипту со спотового аккаунта 

	client.transfer_spot_to_isolated_margin(asset='BTC',symbol='ETHBTC',amount='1.1')

## Взять крипту в долг 

	client.create_margin_loan(asset='BTC', amount='1.1', isIsolated='TRUE', symbol='ETHBTC')

	client.get_max_margin_loan(asset='BTC', isolatedSymbol='ETHBTC') - узнать сколько можно взять в долг по максимуму

## Торговля

Маркет ордер на покупку

	client.create_margin_order(
	    symbol='ETHBTC',
	    side=SIDE_BUY,
	    type=ORDER_TYPE_MARKET,
	    quantity=1.1,
	    isIsolated='TRUE')

Лимитный ордер на продажу

	client.create_margin_order(
	    symbol='ETHBTC',
	    side=SIDE_SELL,
	    type=ORDER_TYPE_LIMIT,
	    timeInForce=TIME_IN_FORCE_GTC,
	    quantity=1.1,
	    price=1490,
	    isIsolated='TRUE')

Проверить статус

	client.get_margin_order(
	    symbol='ETHBTC',
	    orderId=3175554719)

## Отдать долг

	client.repay_margin_loan(asset='BTC', amount='1.1')

## Перевести крипту на спотовый аккаунт

	client.transfer_isolated_margin_to_spot(asset='BTC', symbol='ETHBTC', amount='1.1')