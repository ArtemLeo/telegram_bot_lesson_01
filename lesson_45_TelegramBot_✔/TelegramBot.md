# ✅ Урок 41: Основи Telegram-бота. Бібліотека `aiogram 3`

---
<img src="main_image.png" alt="pygame" width="1500">

## Зміст уроку:

1. [Сьогодні на уроці](#1-сьогодні-на-уроці)
2. [Що таке **Telegram-Bot**?](#2-що-таке-telegram-bot)
3. [Створення проєкту **MyTelegramBot**](#3-створення-проєкту-my_telegram_bot)
4. [Налаштування **Telegram-Bot**](#4-налаштування-telegram-bot)
5. [Реалізація команди `/start`](#5-реалізація-команди-start)
6. [Підсумки уроку](#6-підсумки-уроку)

> 🔗 Useful Links:

- [Aiogram3](https://docs.aiogram.dev/en/latest/)
- [BotFather](https://t.me/BotFather)

---

## 1. Сьогодні на уроці

> 💡 На цьому уроці ми розглянемо наступні теми:

- Створимо директорію для проекту **Telegram-Bot**.
- Ініціалізуємо віртуальне середовище, щоб усі залежності та бібліотеки були організовані та легко керовані.
- Установимо необхідні залежності для роботи з ботом, зокрема бібліотеку `aiogram`, яка допоможе керувати ботом в
  `Telegram`.
- Отримаємо токен для бота за допомогою `BotFather` у `Telegram`, що дозволить програмі взаємодіяти з `Telegram`.
- Створимо файл `config.py` де зберігатиметься токен бота. Це необхідно для захищеного зберігання налаштувань.
- Створимо головний файл бота (`bot.py`), де будемо писати код, що керуватиме всіма функціями бота.
- Реалізуємо першу команду бота - `/start`
- Використаємо клас `Command` для створення команди `/start`, яка буде вітати кожного користувача.
- Бот привітає користувача або коротко розкаже про себе та свою функціональність.
- Додамо меню з доступними командами, щоб користувачі могли легко зрозуміти, які функції доступні в боті.
- Після цього уроку в нас буде готовий базовий **Telegram-Bot** з початковими налаштуваннями та першою командою для
  взаємодії з користувачами.

### 🧩 Функціонал бота:

- Вітання користувача та опис бота
- Перегляд списку фільмів
- Перегляд інформації про фільм
- Додавання фільму до списку
- Робота з медіафайлами (зображення)

### 🛠 Інструменти та корисні посилання:

- [aiogram](https://docs.aiogram.dev/en/latest/): Асинхронний фреймворк для Telegram Bot API
- [BotFather](https://t.me/BotFather): Телеграм бот для керування ботами
- [Keyboard builder](https://docs.aiogram.dev/en/latest/#keyboard-builder): Утиліта для створення клавіатур
- [Command](https://docs.aiogram.dev/en/latest/): Фільтр для обробки команд
- [Magic filters](https://docs.aiogram.dev/en/latest/#magic-filters): Утиліта для створення custom фільтрів
- [Finite State Machine](https://docs.aiogram.dev/en/latest/#finite-state-machine): Утиліта для керування сесіями
  користувачів

[Повернутися до змісту](#зміст-уроку)

---

## 2. Що таке Telegram-Bot?

> 💡 **Telegram-Bot** - це спеціальний акаунт, який може відповідати на команди користувачів, надавати різну інформацію,
> виконувати дії та навіть автоматизувати складні завдання.

У багатьох застосунках **Telegram-Bots** стають незамінними, оскільки здатні полегшити роботу для людей та надавати
зручний інтерфейс для взаємодії.

### 💡 Функції Telegram-Bots:

- **Відповіді на команди користувачів**: Боти можуть реагувати на команди, наприклад, такі як `/start`, `/help`,
  `/add_movie` та виконувати відповідні дії.
- **Надання інформації та інтерактивний досвід**: За допомогою бота можна отримувати різну інформацію, наприклад,
  погоду, новини, курси валют або дані з бібліотеки фільмів.
- **Обробка тексту та медіа**: Боти можуть працювати з текстовими повідомленнями, фото, відео та іншими файлами, що
  робить процес обміну інформацією зручнішим.
- **Інтеграція з іншими сервісами**: Боти можуть підключатися до баз даних, інших **API** або сторонніх сервісів, щоб
  надавати актуальну інформацію.

### 💡 Як працюють телеграм-боти?

**Telegram-Bots** працюють за допомогою **API**, через яке розробники можуть взаємодіяти з платформою **Telegram**.

- Це означає, що ми пишемо код, який взаємодіє з **Telegram** через спеціальні запити (наприклад, надіслати повідомлення
  чи отримати нове).
- Боти працюють за принципом очікування команд від користувачів і виконання відповідних дій, залежно від команд та
  заданого програмного коду.

### Бібліотека `aiogram 3`:

> 💡 Бібліотека `aiogram 3` використовується для асинхронного програмування **telegram-bots**, що робить бібліотеку дуже
> ефективною та швидкою під час роботи з **Telegram Bot API**.

- **Асинхронність**: дозволяє ботам обробляти багато запитів одночасно, що важливо для швидкості та ефективності.
- **Простота використання**: `aiogram` має зрозумілу документацію та зручний інтерфейс для написання коду.
- **Гнучкість і підтримка нових функцій**: `aiogram` постійно оновлюється та підтримує останні функції **Telegram Bot
  API**, тому з бібліотекою легко створювати сучасні та функціональні боти.

Розширена документація `aiogram 3` українською мовою за [посиланням.](https://docs.aiogram.dev/uk-ua/dev-3.x/)

В наступному блоку ми налаштуємо базову структуру нашого бота та почнемо розбиратись з його основними командами.

[Повернутися до змісту](#зміст-уроку)

---

## 3. Створення проєкту `my_telegram_bot`

> 💡 Відкриваємо редактор коду **PyCharm**.

- В головному меню вибираємо пункт **Create New Project**.
- Вказуємо шлях до папки, де буде зберігатися проєкт.
- Вибираємо віртуальне оточення на базі `pip`.
- **PyCharm** автоматично створює віртуальне оточення при створенні нового проєкту.
- Якщо віртуальне оточення потрібно створити вручну, можна скористатися терміналом у PyCharm.

```bash
python -m venv venv

# Активація віртуального оточення для Windows:
.\venv\Scripts\activate

# Активація віртуального оточення для MacOS/Linux
source venv/bin/activate
```

- [Встановлюємо](https://packaging.python.org/en/latest/tutorials/installing-packages/#installing-from-pypi)
  бібліотеку [aiogram](https://docs.aiogram.dev/en/latest/install.html).

```bash
pip install -U aiogram
```

- Необхідно виконати наступну команду для створення файлу `requirements.txt`, який буде містити список інстальованих
  бібліотек.

```bash
pip freeze > requirements.txt
```

[Повернутися до змісту](#зміст-уроку)

---

## 4. Налаштування Telegram-Bot

> 💡 Необхідно отримати **токен** бота з **@BotFather**.

- Відкрити чат з [BotFather](https://t.me/BotFather) в Telegram.
- Відкрити меню (**Menu**) та надіслати команду `/newbot`, слідуючи інструкціям **BotFather**.
- Якщо ви раніше вже створювали бота, то його можна знайти за командою `/mybots`
- Створити назву (наприклад, `EducationalTelegramBot`) та унікальний `username` для бота (наприклад,
  `educational_telegram_bot`).
- Обов'язково `username` повинно бути унікальним та використовувати закінчення `_bot` наприкінці.
- Після створення бота, **BotFather** надішле **токен**, який необхідно зберегти та використати для підключення бота до
  нашої програми, та посилання, яке використовується вашим ботом.

> ⚠️ **Важливо**! Нікому не передавайте та не демонструйте цей токен.

💡 Оновити поточний токен на інший (за будь яких причин) можна за допомогою наступних кроків:

- Відкрити чат з [BotFather](https://t.me/BotFather) в Telegram.
- Відкрити меню (**Menu**) та натиснути команду `/mybots`
- Обирати необхідного бота
- Натиснути **API Token**
- Натиснути **Revoke current token**

### Створення файлу `config.py` з токеном бота:

> 💡 Об’єкти, які є **константами** та які **заборонено змінювати**, у товаристві розробників Python, принято називати в
> стилі **UPPER_CASE**.

Таким чином інші розробники зрозуміють, що це налаштування і важливо його тримати без змін протягом усього життєвого
циклу програми.

```python
# config.py
BOT_TOKEN = "6743572452:AAFRAMqF3hr7H2NionAn7vGNShOelB0MYnc"
```

### Створення головного файлу програми `bot.py`:

- Необхідно створити файл `bot.py` в директорії проєкту.
- Відкрити приклад [QuickStart](https://docs.aiogram.dev/en/latest/#simple-usage) на сторінці офіційної документації
  бібліотеки `aiogram`.
- Скопіювати приклад коду в файл `bot.py`

```python
import asyncio
import logging
import sys
from os import getenv

from aiogram import Bot, Dispatcher, html
from aiogram.client.default import DefaultBotProperties
from aiogram.enums import ParseMode
from aiogram.filters import CommandStart
from aiogram.types import Message

# Bot token can be obtained via https://t.me/BotFather
TOKEN = getenv("BOT_TOKEN")

# All handlers should be attached to the Router (or Dispatcher)

dp = Dispatcher()


@dp.message(CommandStart())
async def command_start_handler(message: Message) -> None:
    """
    This handler receives messages with `/start` command
    """
    # Most event objects have aliases for API methods that can be called in events' context
    # For example if you want to answer to incoming message you can use `message.answer(...)` alias
    # and the target chat will be passed to :ref:`aiogram.methods.send_message.SendMessage`
    # method automatically or call API method directly via
    # Bot instance: `bot.send_message(chat_id=message.chat.id, ...)`
    await message.answer(f"Hello, {html.bold(message.from_user.full_name)}!")


@dp.message()
async def echo_handler(message: Message) -> None:
    """
    Handler will forward receive a message back to the sender

    By default, message handler will handle all message types (like a text, photo, sticker etc.)
    """
    try:
        # Send a copy of the received message
        await message.send_copy(chat_id=message.chat.id)
    except TypeError:
        # But not all the types is supported to be copied so need to handle it
        await message.answer("Nice try!")


async def main() -> None:
    # Initialize Bot instance with default bot properties which will be passed to all API calls
    bot = Bot(token=TOKEN, default=DefaultBotProperties(parse_mode=ParseMode.HTML))

    # And the run events dispatching
    await dp.start_polling(bot)


if __name__ == "__main__":
    logging.basicConfig(level=logging.INFO, stream=sys.stdout)
    asyncio.run(main())
```

Необхідно змінити код, щоб імпортувати **токен** з файлу `config.py` в файл `bot.py`, а рядок з використанням бібліотеки
`python-dotenv` закоментуємо.

```python
# from os import getenv
from config import BOT_TOKEN as TOKEN

# TOKEN = getenv("BOT_TOKEN")
```

Необхідно імпортувати токен з файлу `config.py`, а рядки `from os import getenv` та `TOKEN = getenv("BOT_TOKEN")`
закоментувати.

```python
import asyncio
import logging
import sys
# from os import getenv
from config import BOT_TOKEN as TOKEN

from aiogram import Bot, Dispatcher, html
from aiogram.client.default import DefaultBotProperties
from aiogram.enums import ParseMode
from aiogram.filters import CommandStart
from aiogram.types import Message

# Bot token can be obtained via https://t.me/BotFather
# TOKEN = getenv("BOT_TOKEN")

# All handlers should be attached to the Router (or Dispatcher)

dp = Dispatcher()


@dp.message(CommandStart())
async def command_start_handler(message: Message) -> None:
    """
    This handler receives messages with `/start` command
    """
    # Most event objects have aliases for API methods that can be called in events' context
    # For example if you want to answer to incoming message you can use `message.answer(...)` alias
    # and the target chat will be passed to :ref:`aiogram.methods.send_message.SendMessage`
    # method automatically or call API method directly via
    # Bot instance: `bot.send_message(chat_id=message.chat.id, ...)`
    await message.answer(f"Hello, {html.bold(message.from_user.full_name)}!")


@dp.message()
async def echo_handler(message: Message) -> None:
    """
    Handler will forward receive a message back to the sender

    By default, message handler will handle all message types (like a text, photo, sticker etc.)
    """
    try:
        # Send a copy of the received message
        await message.send_copy(chat_id=message.chat.id)
    except TypeError:
        # But not all the types is supported to be copied so need to handle it
        await message.answer("Nice try!")


async def main() -> None:
    # Initialize Bot instance with default bot properties which will be passed to all API calls
    bot = Bot(token=TOKEN, default=DefaultBotProperties(parse_mode=ParseMode.HTML))

    # And the run events dispatching
    await dp.start_polling(bot)


if __name__ == "__main__":
    logging.basicConfig(level=logging.INFO, stream=sys.stdout)
    asyncio.run(main())
```

[Повернутися до змісту](#зміст-уроку)

---

## 5. Реалізація команди `/start`

У прикладі [QuickStart](https://docs.aiogram.dev/en/latest/#simple-usage), який ми скопіювали зі сторінки офіційної
документації бібліотеки `aiogram`, вже є реалізація обробника для команди `/start`.

```python
@dp.message(CommandStart())
async def command_start_handler(message: Message) -> None:
    """
    This handler receives messages with `/start` command
    """
    # Most event objects have aliases for API methods that can be called in events' context
    # For example if you want to answer to incoming message you can use `message.answer(...)` alias
    # and the target chat will be passed to :ref:`aiogram.methods.send_message.SendMessage`
    # method automatically or call API method directly via
    # Bot instance: `bot.send_message(chat_id=message.chat.id, ...)`
    await message.answer(f"Hello, {html.bold(message.from_user.full_name)}!")
```

Детально ознайомитись з класом **Command** можна за
цим [посиланням](https://docs.aiogram.dev/en/latest/dispatcher/filters/command.html#usage).

### Розглянемо кожну частину коду детальніше:

```text
@dp.message(CommandStart())
```

- Рядок `@dp.message(CommandStart())` вказує диспетчеру, що функція, яка оголошується нижче, буде викликатися при
  отриманні повідомлення із текстом `/start`.
- **CommandStart** - це заготовлений клас, екземпляр якого є фільтром для специфічного повідомлення.
- В цьому випадку використовується метод диспетчера `message`, який реалізує шаблон проєктування **Decorator** над
  функцією `command_start_handler`, а саме `TelegramEventObserver`, тобто він викликає функцію коли подія настає.
- Також цей метод приймає в якості аргументів різноманітні фільтри для обробки специфічних даних, **CommandStart** якраз
  є таким прикладом.

```python
async def command_start_handler(message: Message) -> None:
```

Ключове слово `async` використовується для роботи функції або метода
в [асинхронному](https://docs.python.org/3/library/asyncio.html) режимі і являється частиною `async`/`await`
конструкції.

Всі функції з декоратором `message` отримують першим позиційним параметром екземпляр `Message`, який являється класом
для представлення повідомлення та містить є все необхідне для роботи з користувачем, що його надіслав, та контентом
самого повідомлення.

Далі в коді знаходиться [docstring](https://docs.python.org/3/glossary.html#term-docstring) та **usage** (пояснення) до
використання функції.

- **Docstring** містить інформацію про роботу функції, а саме: "**Цей обробник отримує повідомлення із командою**
  `/start`".
- **Usage** пояснює в коментарях, яким чином обробник отримує повідомлення.

```python
"""
This handler receives messages with `/start` command
"""
# Most event objects have aliases for API methods that can be called in events' context
# For example if you want to answer to incoming message you can use `message.answer(...)` alias
# and the target chat will be passed to :ref:`aiogram.methods.send_message.SendMessage`
# method automatically or call API method directly via
# Bot instance: `bot.send_message(chat_id=message.chat.id, ...)`
```

Наступний рядок, що починається з ключового слова `await`, створює запит до відповідного ендпоінту **Telegram Bot API**.

- Процес потребує очікування відповіді від сервера телеграму, про результат виконання запиту.
- Ключове слово `await` надає можливість процесора нашого комп'ютера не очікувати відповіді, виконувати інші задачі та
  повернувся до цього рядка коли буде готовий результат.

```python
await message.answer(f"Hello, {html.bold(message.from_user.full_name)}!")
```

Наступний код містить реалізацію обробника всіх повідомлень **без фільтра**.

```python
@dp.message()
async def echo_handler(message: Message) -> None:
    """
    Handler will forward receive a message back to the sender

    By default, message handler will handle all message types (like a text, photo, sticker etc.)
    """
    try:
        # Send a copy of the received message
        await message.send_copy(chat_id=message.chat.id)
    except TypeError:
        # But not all the types is supported to be copied so need to handle it
        await message.answer("Nice try!")
```

Створимо власний обробник з фільтром для команди `/start`, для цього змінимо наступний рядок в секції імпортів.

### Необхідно змінити обробник `command_start_handler` для наших потреб.

```python
# Old string
from aiogram.filters import CommandStart
```

```python
# New string
from aiogram.filters import CommandStart, Command
```

Новий `import` дозволить використовувати кастомні (користувацькі) фільтри в обробниках.

### Необхідно змінити наступний код обробника.

```python
# Old code
@dp.message(CommandStart())
async def command_start_handler(message: Message) -> None:
    """
    This handler receives messages with `/start` command
    """
    # Most event objects have aliases for API methods that can be called in events' context
    # For example if you want to answer to incoming message you can use `message.answer(...)` alias
    # and the target chat will be passed to :ref:`aiogram.methods.send_message.SendMessage`
    # method automatically or call API method directly via
    # Bot instance: `bot.send_message(chat_id=message.chat.id, ...)`
    await message.answer(f"Hello, {html.bold(message.from_user.full_name)}!")
```

```python
# New code
@dp.message(Command("start"))
async def start(message: Message) -> None:
    await message.answer(
        f"Hello🖐, {html.bold(message.from_user.full_name)}!\n"
        "I'm your first Telegram Bot 🥳"
    )
```

### Перевіримо зміни, запустивши модуль `bot.py`:

- Необхідно перейти в **Telegram Bot** за посиланням, яке ми отримали від **BotFather**.
- Натиснути кнопку `start` або вручну написати повідомлення з текстом `/start`

[Повернутися до змісту](#зміст-уроку)

---

## 6. Підведення підсумків 🚀

> На цьому уроці ми вивчили наступні теми:

- Створили окрему директорію для проєкту та ініціалізували віртуальне середовище, що дозволяє ефективно організувати
  залежності проєкту та зробити код більш незалежним від системних налаштувань.
- Встановили бібліотеку `aiogram`, яка є основним інструментом для розробки асинхронних телеграм-ботів.
- `Aiogram` дозволить легко обробляти команди та повідомлення користувачів.
- Зареєстрували **Telegram Bot** за допомогою **BotFather** та отримали унікальний токен.
- Токен - це ключ, який дозволяє нашій програмі взаємодіяти з платформою **Telegram**.
- Створили файл `config.py` для збереження токена, що робить проєкт більш захищеним та зручним у налаштуванні.
- У головному файлі `bot.py` написали перший код для нашого **Telegram Bot**.
- Створили першу команду `/start`, яка вітає користувача і коротко пояснює функціональність бота, що допоможе
  користувачам зрозуміти, що бот вміє робити та як ним користуватися.
- Після цього уроку у нас вже є основи **Telegram Bot**, який відповідає на перші команди.

> 💡 На наступному занятті ми будемо додавати нові функції та поступово наближатися до завершення проєкту.

[Повернутися до змісту](#зміст-уроку)

---
