
#### **5.1 Основные компоненты модуля**

Каждый модуль для Hikka состоит из нескольких ключевых компонентов:

1. **Декораторы**: Управляют поведением методов (например, команды, watchers, inline-запросы).
    
2. **База данных (DB)**: Хранит данные между перезапусками модуля.
    
3. **Конфигурация**: Позволяет настраивать параметры модуля.
    
4. **Строки (strings)**: Используются для локализации и перевода текстов.
    
5. **Логирование**: Помогает отслеживать ошибки и отлаживать код.
    

---

#### **5.2 Декораторы**

Декораторы — это специальные функции, которые изменяют поведение методов. В Hikka используются следующие декораторы:

1. **`@loader.command`**:
    
    - Превращает метод в команду. Например, метод `examplecmd` будет доступен как команда `.example`.
        
    - Пример:
        
```python
        @loader.command
        async def examplecmd(self, message):
            """Пример команды"""
            await utils.answer(message, "Это пример команды!")
```
        
2. **`@loader.watcher`**:
    
    - Превращает метод в watcher, который отслеживает события (например, новые сообщения).
        
    - Пример:
        
```python
        @loader.watcher
        async def watcher(self, message):
            """Отслеживает новые сообщения"""
            if "привет" in message.text.lower():
                await message.reply("Привет!")
```
        
3. **`@loader.inline_handler`**:
    
    - Превращает метод в обработчик inline-запросов.
        
    - Пример:
        
```python
        @loader.inline_handler
        async def inline_handler(self, query):
            """Обрабатывает inline-запросы"""
            await query.answer([{"title": "Пример", "message": "Это inline-ответ!"}])
```
        
4. **`@loader.tds`**:
    
    - Используется для поддержки динамического перевода строк.
        
    - Пример:
        
```python
        @loader.tds
        class ExampleMod(loader.Module):
            strings = {"name": "ExampleMod"}
```
        

---

#### **5.3 База данных (DB)**

База данных позволяет сохранять данные между перезапусками модуля. Для работы с базой данных используются методы `self.get` и `self.set`.

1. **`self.get(key, default=None)`**:
    
    - Получает значение из базы данных по ключу. Если ключ отсутствует, возвращает значение по умолчанию.
        
    - Пример:
        
        `value = self.get("my_key", "default_value")`
        
2. **`self.set(key, value)`**:
    
    - Сохраняет значение в базе данных по ключу.
        
    - Пример:
        
        `self.set("my_key", "my_value")`
        

---

#### **5.4 Конфигурация**

Конфигурация позволяет настраивать параметры модуля. Для работы с конфигурацией используется `loader.ModuleConfig`.

1. **Создание конфигурации**:
    
    - Конфигурация создается в методе `__init__`.
        
    - Пример:
        
```python
        def __init__(self):
            self.config = loader.ModuleConfig(
                "param1", "default_value", "Описание параметра"
            )
```
        
2. **Использование конфигурации**:
    
    - Значения конфигурации доступны через `self.config`.
        
    - Пример:
        
```python
        async def examplecmd(self, message):
            value = self.config["param1"]
            await utils.answer(message, f"Значение параметра: {value}")
        
```

---

#### **5.5 Строки (strings)**

Строки используются для локализации и перевода текстов. Они объявляются в словаре `strings` и могут быть переведены на другие языки.

1. **Объявление строк**:
    
    - Пример:
        
```python
        strings = {
            "name": "ExampleMod",
            "hello": "Привет, {}!",
        }
```
        
2. **Использование строк**:
    
    - Строки доступны через `self.strings`.
        
    - Пример:
        
```python
        async def examplecmd(self, message):
            name = utils.get_args_raw(message)
            await utils.answer(message, self.strings["hello"].format(name))
```
        
3. **Перевод строк**:
    
    - Для перевода строк на другие языки создаются словари `strings_<язык>`.
        
    - Пример:
        
```python
        strings_ru = {
            "hello": "Привет, {}!",
        }
        strings_en = {
            "hello": "Hello, {}!",
        }
```
        

---

#### **5.6 Логирование**

Логирование помогает отслеживать ошибки и отлаживать код. Для логирования используется модуль `logging`.

1. **Создание логгера**:
    
    - Пример:
        
```python
        import logging
        logger = logging.getLogger(__name__)
```
        
2. **Использование логгера**:
    
    - Пример:
        
```python
        async def examplecmd(self, message):
            try:
                # Код, который может вызвать ошибку
            except Exception as e:
                logger.error(f"Ошибка: {e}")
                await utils.answer(message, "Произошла ошибка.")
```
        

---

#### **5.7 Пример модуля**

Соберем все компоненты в одном модуле:

```python
from .. import loader, utils
import logging

logger = logging.getLogger(__name__)

@loader.tds
class ExampleMod(loader.Module):
    """Пример модуля"""

    strings = {
        "name": "ExampleMod",
        "hello": "Привет, {}!",
    }

    def __init__(self):
        self.config = loader.ModuleConfig(
            "param1", "default_value", "Описание параметра"
        )

    async def client_ready(self, client, db):
        self._client = client
        self._db = db

    @loader.command
    async def examplecmd(self, message):
        """Пример команды"""
        try:
            name = utils.get_args_raw(message)
            await utils.answer(message, self.strings["hello"].format(name))
        except Exception as e:
            logger.error(f"Ошибка: {e}")
            await utils.answer(message, "Произошла ошибка.")

    @loader.watcher
    async def watcher(self, message):
        """Отслеживает новые сообщения"""
        if "привет" in message.text.lower():
            await message.reply("Привет!")
```

---

#### **5.8 Практическое задание**

1. Создайте модуль, который:
    
    - Хранит значение в базе данных.
        
    - Использует конфигурацию для настройки параметра.
        
    - Выводит локализованное сообщение.
        
    - Логирует ошибки.
        
2. Протестируйте модуль, установив его в Hikka.
    

---

#### **5.9 Дополнительные материалы**

- [Официальная документация Telethon](https://docs.telethon.dev/)
    
- [Примеры модулей для Hikka](https://github.com/hikariatama/Hikka)