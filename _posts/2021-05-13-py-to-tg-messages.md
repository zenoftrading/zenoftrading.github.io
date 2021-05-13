---
title: Как слать сообщения в телеграм из питона в три строчки
tags: python
---

Удобно когда бот шлёт сообщения в телеграм, а не в лог файл. Как это можно сделать в python? Очень просто.

- Шаг 1. Устанавливаем либу [loguru](https://github.com/Delgan/loguru). Вам же нужно логирование в боте? Через `loguru` настраивается парой строчек.
- Шаг 2. Устанавливаем либу [notifiers](https://github.com/liiight/notifiers) которая шлёт сообщения куда угодно тоже парой строчек.
- Шаг 3. Настраиваем.
```
# подключаем либы
from loguru import logger
from notifiers.logging import NotificationHandler

# прописываем параметры телеграм бота, от чьего имени и куда слать, где их взять думаю сами разберетесь
params = {
    'token': 'dfdfsfasdfljsahdfkljhasdfklj',
    'chat_id': 'dfkdsflksdjfls;kfjas;ldkf'
}
tg_handler = NotificationHandler("telegram", defaults=params)

# добавляем в logger правило, что все логи уровня info и выше отсылаются в телегу
logger.add(tg_handler, level="INFO")
```

Я у себя настроил уровень info. Использую его как раз для сообщений в телегу. А вот debug сообщения в телегу уже не приходят. Нечего эфир засорять. Подробнее про уровни логов [можно почитать в справке](https://docs.python.org/3/library/logging.html#logging-levels)

- Шаг 4. Отправляем сообщение
```
logger.info("Слава роботам! Убить всех человеков!")
```

Если не нужны логи, можно слать просто через `notifiers`.