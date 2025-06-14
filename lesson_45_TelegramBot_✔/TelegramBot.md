# ✅ Урок 41: Основи Telegram-бота. Бібліотека `aiogram 3`

---
<img src="/Documentations/Images/main_image.png" alt="pygame" width="1500">

## Зміст уроку:

1. [Сьогодні на уроці](#1-сьогодні-на-уроці)
2. [Що таке **Telegram-Bot**?](#2-що-таке-telegram-bot)
3. [Створення проєкту **MyTelegramBot**](#3-створення-проєкту-my_telegram_bot)
4. [Налаштування **Telegram-Bot**](#4-налаштування-telegram-bot)
5. [Реалізація команди `/start`](#5-реалізація-команди-start)
6. [Підсумки уроку 🚀](#6-підсумки-уроку)

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
- Отримаємо токен для бота за допомогою `BotFather`, що дозволить програмі взаємодіяти з `Telegram`.
- Створимо файл `config.py` де зберігатиметься токен бота. Це необхідно для захищеного зберігання налаштувань.
- Створимо головний файл `bot.py`, в якому будемо писати код, що керуватиме всіма функціями бота.
- Використаємо клас `Command` для створення команди `/start`.
- За допомогою команди `/start`, бот привітає користувача або коротко розкаже про себе та свою функціональність.
- Додамо **меню** з доступними командами, щоб користувачі могли легко зрозуміти, які функції доступні в боті.
- Після цього уроку в нас буде готовий базовий **Telegram-Bot** з початковими налаштуваннями та першою командою для
  взаємодії з користувачами.

### 🧩 Функціонал бота:

- Вітання користувача та опис бота.
- Перегляд списку фільмів.
- Перегляд інформації про фільм.
- **Додавання, пошук, редагування та видалення** фільму зі списку.
- Робота із зображеннями (постер фільму).

[Повернутися до змісту](#зміст-уроку)

---

## 2. Що таке Telegram-Bot?

> 💡 **Telegram-Bot** - це спеціальний акаунт, який може відповідати на команди користувачів, надавати різну інформацію,
> виконувати дії та навіть автоматизувати складні завдання.

У багатьох застосунках **Telegram-Bots** стають незамінними, оскільки здатні полегшити роботу для людей та надавати
зручний інтерфейс для взаємодії.

### 💡 Функції Telegram-Bots:

- **Відповіді на команди користувачів**: Боти можуть реагувати на команди (наприклад, `/start`, `/help`, `/add_movie`)
  та виконувати відповідні дії.
- **Отримання інформації**: За допомогою бота можна отримувати різну інформацію (наприклад, **погоду, новини, курси
  валют** або дані з **бібліотеки фільмів**).
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

Розширена документація `aiogram` за [посиланням.](https://docs.aiogram.dev/uk-ua/dev-3.x/)

В наступному блоку ми налаштуємо базову структуру нашого бота та почнемо розбиратись з його основними командами.

[Повернутися до змісту](#зміст-уроку)

---

## 3. Створення проєкту `my_telegram_bot`

> 💡 Відкриваємо редактор коду **PyCharm**.

- В головному меню вибираємо пункт **Create New Project**.
- Вказуємо шлях до папки, де буде зберігатися проєкт.
- Вибираємо віртуальне оточення на базі `pip`
- **PyCharm** автоматично активує віртуальне оточення при створенні нового проєкту.
- Якщо віртуальне оточення потрібно створити вручну, можна скористатися терміналом у PyCharm.

```bash
# Створення віртуального оточення
python -m venv venv

# Активація віртуального оточення для Windows:
.\venv\Scripts\activate

# Активація віртуального оточення для MacOS/Linux
source venv/bin/activate
```

[Встановлюємо](https://packaging.python.org/en/latest/tutorials/installing-packages/#installing-from-pypi)
бібліотеку [aiogram](https://docs.aiogram.dev/en/latest/install.html):

```bash
pip install -U aiogram
```

Наступну команду необхідно виконати для створення файлу `requirements.txt`, який буде містити список інстальованих
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
- Обов'язково `username` повинно бути унікальним та використовувати в назві закінчення `_bot`.
- Після створення бота, **BotFather** надішле **ТОКЕН**, який необхідно зберегти і використати для підключення бота до
  нашої програми, та **ПОСИЛАННЯ** - це **адреса** яка використовується нашим ботом.

> ⚠️ **Важливо**! Нікому не передавайте та не демонструйте цей токен.

💡 Оновити поточний токен на інший (за будь яких причин) можна за допомогою наступних кроків:

- Відкрити чат з [BotFather](https://t.me/BotFather) в Telegram.
- Відкрити меню (**Menu**) та натиснути команду `/mybots`
- Обрати необхідного бота.
- Натиснути **API Token**.
- Натиснути **Revoke current token**.

### Створення файлу `config.py` з токеном бота:

> 💡 Об’єкти, які є **константами** та які **заборонено змінювати**, у товаристві розробників Python, принято називати в
> стилі **UPPER_CASE**.

Таким чином інші розробники зрозуміють, що це налаштування і важливо його тримати без змін протягом усього життєвого
циклу програми.

```python
# config.py
BOT_TOKEN = "6743572452:AAFRAMqF3hr7H2NionAn7vGNShOelB0MYnc"
```

## 5. Створення головного файлу програми `bot.py`

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

Необхідно імпортувати токен з файлу `config.py`, а рядки `from os import getenv` та `TOKEN = getenv("BOT_TOKEN")`
закоментувати.

```python
# from os import getenv
from config import BOT_TOKEN as TOKEN

# TOKEN = getenv("BOT_TOKEN")
```

### Code ✅

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

## 6. Реалізація команди `/start`

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

### 💡 Розглянемо кожен рядок цього коду, щоб зрозуміти, що відбувається:

### Декоратор:

```python
@dp.message(CommandStart())
```

- `@dp.message` - це декоратор, який використовується для обробки повідомлень у бібліотеці `aiogram`. Він вказує, що
  функція, яка йде після нього, буде обробляти певний тип повідомлень.
- `CommandStart()` - це фільтр, який вказує, що функція буде викликана тільки тоді, коли користувач надсилає команду
  `/start`.

### Оголошення функції:

```python
async def command_start_handler(message: Message) -> None:
```

- `async def` - це оголошення асинхронної функції. Асинхронні функції дозволяють виконувати операції, які можуть
  виконуватись певний час (наприклад, мережеві запити), не блокуючи виконання інших частин програми.
- `command_start_handler` - це ім'я функції, яка буде обробляти команду `/start`.
- `message: Message` - це параметр функції, який представляє об'єкт повідомлення, отриманого від користувача.
- `Message` - це клас з бібліотеки `aiogram`, який містить інформацію про повідомлення.
- `-> None` - це вказує, що функція не повертає жодного значення.

### Docstring:

```python
""" 
This handler receives messages with /start command
"""
```

- Це рядок документації, який описує, що робить функція.
- У цьому випадку рядок говорить, що ця функція обробляє повідомлення з командою `/start`.

### Коментар:

```python
# Most event objects have aliases for API methods that can be called in events' context
# For example if you want to answer to incoming message you can use `message.answer(...)` alias
# and the target chat will be passed to :ref:`aiogram.methods.send_message.SendMessage`
# method automatically or call API method directly via
# Bot instance: `bot.send_message(chat_id=message.chat.id, ...)`
```

- Це коментар, який пояснює, що більшість об'єктів подій мають псевдоніми для методів API, які можна викликати в
  контексті подій.
- Наприклад, якщо ви хочете відповісти на вхідне повідомлення, ви можете використовувати `message.answer(...)`, і
  цільовий чат буде автоматично переданий до методу `SendMessage`.

### Відправлення повідомлення:

```python
await message.answer(f"Hello, {html.bold(message.from_user.full_name)}!")
```

- `await` - це ключове слово, яке використовується для очікування завершення асинхронної операції.
- `message.answer(...)` - це метод, який використовується для відправлення відповіді на отримане повідомлення.
- `f"Hello, {html.bold(message.from_user.full_name)}!"` - це рядок, який містить вітання.
- `html.bold(...)` - це метод, який робить текст жирним.
- `message.from_user.full_name` - це ім'я користувача, який надіслав повідомлення.

Отже, цей код обробляє команду `/start`, і коли користувач надсилає цю команду, бот відповідає вітальним повідомленням з
ім'ям користувача.

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

### 💡 Розглянемо кожен рядок цього коду, щоб зрозуміти, що відбувається:

### Декоратор:

```python
@dp.message()
```

- `@dp.message` - це декоратор, який вказує, що функція, яка йде після нього, буде обробляти всі типи повідомлень.
- Декоратор не містить фільтрів, тому оброблятиме всі повідомлення, незалежно від їх типу (текст, фото, стикер тощо).

### Оголошення функції:

```python
async def echo_handler(message: Message) -> None:
```

- `async def` - це оголошення асинхронної функції. Асинхронні функції дозволяють виконувати операції, які можуть
  виконуватись певний час (наприклад, мережеві запити), не блокуючи виконання інших частин програми.
- `echo_handler` - це ім'я функції, яка буде обробляти повідомлення.
- `message: Message` - це параметр функції, який представляє об'єкт повідомлення, отриманого від користувача.
- `Message` - це клас з бібліотеки `aiogram`, який містить інформацію про повідомлення.
- `-> None` - це вказує, що функція не повертає жодного значення.

### Docstring:

```python
"""
Handler will forward receive a message back to the sender
By default, message handler will handle all message types (like a text, photo, sticker etc.)
"""
```

- Це рядок документації, який описує, що робить функція.
- У цьому випадку рядок говорить, що цей обробник буде пересилати отримане повідомлення назад відправнику і за
  замовчуванням оброблятиме всі типи повідомлень.

### Блок `try-except`:

```python
try:
    # Send a copy of the received message
    await message.send_copy(chat_id=message.chat.id)
except TypeError:
    # But not all the types is supported to be copied so need to handle it
    await message.answer("Nice try!")
```

- `try:` - це спроба виконати код всередині блоку. У цьому випадку, це спроба надіслати копію отриманого повідомлення
  назад у чат.
- `await message.send_copy(chat_id=message.chat.id)` - цей рядок коду намагається надіслати копію отриманого
  повідомлення назад у чат, з якого воно було отримано.
- `except TypeError:` - якщо виникає помилка типу `TypeError`, це означає, що тип повідомлення не підтримується для
  копіювання. У цьому випадку бот відповідає текстом `"Nice try!"`.

Отже, цей код просто повторює будь-яке отримане повідомлення назад відправнику. Якщо повідомлення не може бути
скопійоване, бот відповідає текстом `"Nice try!"`.

### Створимо власний обробник з фільтром для команди `/start`

Необхідно змінити наступний рядок в секції імпортів.

```python
# Old string
from aiogram.filters import CommandStart

# New string
from aiogram.filters import CommandStart, Command
```

Новий `import` дозволить використовувати кастомні (користувацькі) фільтри в обробниках.

Також, необхідно змінити функцію `command_start_handler`.

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


# New code
@dp.message(Command("start"))
async def start(message: Message) -> None:
    await message.answer(
        f"Hello🖐, {html.bold(message.from_user.full_name)}!\n"
        "I'm your first Telegram Bot 🥳"
    )
```

### Перевіримо зміни, запустивши модуль `bot.py`

- Необхідно перейти в **Telegram Bot** за посиланням, яке ми отримали від **BotFather**.
- Натиснути кнопку `start` або вручну написати повідомлення з текстом `/start`

### Виконаємо рефакторинг нашого коду

Видалимо рядки, які ми більше не будемо використовувати.

```python
# from os import getenv

# Bot token can be obtained via https://t.me/BotFather
# TOKEN = getenv("BOT_TOKEN")

# All handlers should be attached to the Router (or Dispatcher)

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

### ✅ Фінальний code  після сьогоднішнього заняття:

```python
# Імпортуємо необхідні модулі
import asyncio  # Для асинхронного програмування
import logging  # Для логування подій
import sys  # Для доступу до деяких змінних та функцій, пов'язаних з інтерпретатором Python

# Імпортуємо токен бота з конфігураційного файлу
from config import BOT_TOKEN as TOKEN

# Імпортуємо необхідні класи та функції з бібліотеки aiogram
from aiogram import Bot, Dispatcher, html
from aiogram.client.default import DefaultBotProperties
from aiogram.enums import ParseMode
from aiogram.filters import CommandStart, Command
from aiogram.types import Message

# Ініціалізуємо диспетчер для обробки оновлень
dp = Dispatcher()


# Обробник для команди /start
@dp.message(Command("start"))
async def start(message: Message) -> None:
    # Відповідаємо на команду /start, вітаючи користувача
    await message.answer(
        f"Hello🖐, {html.bold(message.from_user.full_name)}!\n"
        "I'm your first Telegram Bot 🥳"
    )


# Головна асинхронна функція для запуску бота
async def main() -> None:
    # Ініціалізуємо екземпляр бота з токеном та властивостями за замовчуванням
    bot = Bot(token=TOKEN, default=DefaultBotProperties(parse_mode=ParseMode.HTML))

    # Запускаємо цикл опитування для отримання оновлень
    await dp.start_polling(bot)


# Перевіряємо, чи скрипт запускається напряму
if __name__ == "__main__":
    # Налаштовуємо базове логування для виведення інформаційних повідомлень у стандартний потік виведення
    logging.basicConfig(level=logging.INFO, stream=sys.stdout)
    # Запускаємо головну асинхронну функцію
    asyncio.run(main())
```

[Повернутися до змісту](#зміст-уроку)

---

## 6. Підведення підсумків 🚀

> На цьому уроці ми вивчили наступні теми:

- Створили окрему директорію для проєкту та ініціалізували віртуальне середовище.
- Встановили бібліотеку `aiogram` - основний інструмент для розробки асинхронних **Telegram Bot**.
- Бібліотека `aiogram` дозволить легко обробляти команди та повідомлення користувачів.
- Зареєстрували **Telegram Bot** за допомогою **BotFather** та отримали унікальний **токен**.
- **Токен** - це ключ, який дозволяє нашій програмі взаємодіяти з платформою **Telegram**.
- Створили файл `config.py` для збереження токена, що робить проєкт більш захищеним та зручним у налаштуванні.
- У головному файлі `bot.py` написали перший код для нашого **Telegram Bot**.
- Створили першу команду `/start`, яка вітає користувача і коротко пояснює функціональність бота, що допоможе
  користувачам зрозуміти, що бот вміє робити та як ним користуватися.
- Після цього уроку у нас вже є основи **Telegram Bot**, який відповідає на перші команди.

> На наступному занятті ми створимо нові функції, що значно розширить функціональність нашого **Telegram Bot**.

[Повернутися до змісту](#зміст-уроку)

---
