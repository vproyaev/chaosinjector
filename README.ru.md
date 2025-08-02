# ChaosInjector 🚀

🇺🇸 [English](README.md) | 🇷🇺 [Русский](README.ru.md)

### Community and Support

📢 Присоединяйтесь к авторскому
Telegram-каналу [@almost_it](https://t.me/almost_it) для insights по
разработке на Python, обсуждений chaos engineering, обновлений библиотеки и
закулисных мыслей об инновационных практиках кодирования.

[![PyPI version](https://badge.fury.io/py/chaosinjector.svg)](https://badge.fury.io/py/chaosinjector)

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

[![Downloads](https://pepy.tech/badge/chaosinjector)](https://pepy.tech/project/chaosinjector)

**Внедряйте хаос, контролируйте неопределённость – революционизируйте свой код
на Python с помощью вероятностных прокси!**

Представьте, что любой объект Python превращается в вероятностный центр силы:
методы, которые "сбоят" случайно, логи, которые выборочно записываются, тесты,
имитирующие реальные сбои без единой строки мокинга. **ChaosInjector** – это
ultimate-инструмент для разработчиков, стремящихся к динамичному, устойчивому и
инновационному коду. Независимо от того, укрепляете ли вы приложение против
нестабильности, оптимизируете производительность через семплинг или добавляете
случайность в симуляции и игры – ChaosInjector делает это простым и элегантным.

Зачем довольствоваться статичным кодом, когда можно принять контролируемый хаос?
Присоединяйтесь к рядам дальновидных разработчиков, использующих ChaosInjector
для усиления тестирования, логирования, поведения ИИ и многого другого. *
*Установите сейчас и раскройте силу вероятности!**

## Почему ChaosInjector? 🔥

В мире непредсказуемых систем ChaosInjector даёт вам преимущество:

- **Инъекция сбоев на стероидах**: Симулируйте нестабильные сети, базы данных
  или API одной строкой – идеально для надёжных unit- и интеграционных тестов.
- **Магия семплинга производительности**: Снижайте нагрузку на логирование,
  трассировку или аналитику, выполняя операции только в X% случаев.
- **Стохастические симуляции**: Добавляйте реалистичную случайность в игры,
  модели машинного обучения или методы Монте-Карло без переписывания логики.
- **Упрощённое A/B-тестирование**: Внедряйте функции вероятностно, без сложной
  инфраструктуры.
- **Усиление приватности и безопасности**: Анонимизируйте доступы к
  чувствительным данным случайно для соответствия нормам и создания honeypot.

Построенный на динамической магии Python (проксирование классов в runtime
через `__getattribute__`), ChaosInjector лёгкий, без зависимостей и тщательно
протестирован с полным покрытием. Это не просто библиотека – это ваш секретный
инструмент для более умного и адаптивного кода.

## Быстрый старт ⚡

### Установка

Начните за секунды:

```bash
pip install chaosinjector
```

### Базовое использование

Подавление логов вероятностно? Легко!

```python
import logging
from chaosinjector import ChaosInjector


logger = logging.getLogger("my_app")
ChaosInjector.inject(
    logger, probability=0.1
)  # Только 10% шанс на выполнение логов

logger.info("Этот лог может не записаться!")  # Неустойчиво по дизайну!
```

Нужен больший контроль? Используйте decider или вероятности по методам:

```python
ChaosInjector.inject(
    logger, method_probs={"info": 0.0, "error": 1.0}
)  # Info всегда пропускается, ошибки всегда логируются
```

Или кастомную логику:

```python
ChaosInjector.inject(
    logger, decider=lambda name: "debug" not in name
)  # Пропускать все методы с 'debug'
```

### Создание прокси без мутации оригинала

Для случаев, когда нужно сохранить оригинальный объект нетронутым,
используйте `create_proxy`, который возвращает новый объект с хаосом, сохраняя
типизацию:

```python
import logging
from chaosinjector import ChaosInjector


original_logger = logging.getLogger("my_app")
chaos_logger = ChaosInjector.create_proxy(original_logger, probability=0.1)

chaos_logger.info("Этот лог flaky в прокси!")  # 10% шанс в прокси
original_logger.info("Этот лог всегда работает!")  # Оригинал нетронут
```

## Функции вкратце 🌟

- **Вероятностный доступ к атрибутам**: Возврат реальных атрибутов/методов с
  настраиваемой вероятностью (0.0-1.0).
- **Кастомные decider**: Передавайте callable для решения по атрибуту (например,
  на основе имени, переменных окружения или времени).
- **Гранулярность по методам**: Словарь вероятностей для конкретных методов для
  точного контроля.
- **Безопасная обработка no-op**: Вызываемые объекты становятся тихими lambda;
  не вызываемые возвращают None – без крашей!
- **Встроенная валидация**: Обеспечивает валидность вероятностей (0-1),
  предотвращая silent-ошибки.
- **Сохранение типизации**: Прокси сохраняют isinstance-совместимость с
  оригинальным типом, включая generics и type hints.
- **Два режима работы**: In-place мутация через `inject` или недеструктивный
  прокси через `create_proxy`.
- **Лёгкий и чистый Python**: Без зависимостей, совместим с Python 3.8+.
- **Тщательно протестировано**: 100% покрытие с pytest, включая мокинг
  случайности для детерминизма.

## Примеры из реального мира 💡

### 1. Инъекция сбоев в тестах

Симулируйте ненадёжные сервисы:

```python
import requests
from chaosinjector import ChaosInjector


session = requests.Session()
ChaosInjector.inject(session, probability=0.3)  # 70% шанс сбоя

response = session.get(
    "https://api.example.com"
)  # Часто None – тестируйте ретраи!
```

Или без мутации:

```python
chaos_session = ChaosInjector.create_proxy(session, probability=0.3)
response = chaos_session.get("https://api.example.com")  # Flaky только в прокси
```

### 2. Семплинг дорогих операций

Оптимизируйте трассировку:

```python
from opentelemetry import trace
from chaosinjector import ChaosInjector


tracer = trace.get_tracer(__name__)
ChaosInjector.inject(
    tracer, probability=0.1
)  # Трассировка только в 10% случаев

with tracer.start_as_current_span("operation"):  # Иногда no-op
    pass
```

С прокси:

```python
chaos_tracer = ChaosInjector.create_proxy(tracer, probability=0.1)
with chaos_tracer.start_as_current_span(
    "operation"
):  # Flaky в прокси, оригинал intact
    pass
```

### 3. Вероятностный ИИ в играх

Добавьте непредсказуемость:

```python
class NPC:
    def attack(self):
        print("Boom!")


npc = NPC()
ChaosInjector.inject(
    npc, method_probs={"attack": 0.7}
)  # Атака в 70% случаев

npc.attack()  # Может быть... может нет!
```

С прокси:

```python
chaos_npc = ChaosInjector.create_proxy(npc, method_probs={"attack": 0.7})
chaos_npc.attack()  # Flaky в прокси, оригинальный npc стабилен
```

### 4. Маскировка приватных данных

Анонимизируйте чувствительные поля:

```python
class UserData:
    user_id = "sensitive123"


data = UserData()
ChaosInjector.inject(
    data, decider=lambda name: name != "user_id"
)  # user_id всегда None

print(data.user_id)  # None – защищено!
```

С прокси:

```python
chaos_data = ChaosInjector.create_proxy(
    data, decider=lambda name: name != "user_id"
)
print(chaos_data.user_id)  # None в прокси, оригинал нетронут
```

Изучите больше в нашей [документации](https://chaosinjector.readthedocs.io) (
скоро)!

## Вклад 🤝

Любите ChaosInjector? Помогите улучшить! Форкните репозиторий, добавьте
функции/тесты и отправьте pull request.

- Сообщайте об
  ошибках: [GitHub Issues](https://github.com/vproyaev/chaosinjector/issues)
- Поставьте звезду репозиторию: ⭐️
- Расскажите о нас: Поделитесь в X или Reddit!

## Лицензия 📄

Выпущено под [MIT License](LICENSE). Свободно используйте, модифицируйте и
распространяйте.

---

**Готовы внедрить хаос в свой код?** Установите ChaosInjector сегодня и
превратите неопределённость в суперсилу. Вопросы? Обращайтесь в issues – мы
поможем! 🚀