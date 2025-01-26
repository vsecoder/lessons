
## **1.1 Что такое Telethon?**

Telethon — это библиотека для Python, которая позволяет взаимодействовать с Telegram API. Она предоставляет возможность создавать как пользовательских ботов, так и клиентов для автоматизации задач в Telegram.

### **Основные возможности Telethon:**

- Отправка и получение сообщений.
- Работа с медиа (фото, видео, документы).
- Управление чатами и каналами.
- Обработка событий (новые сообщения, редактирование сообщений и т.д.).

### **Зачем использовать Telethon?**

- Гибкость: Telethon поддерживает как MTProto, так и Bot API.
- Асинхронность: Telethon полностью асинхронный, что позволяет эффективно работать с большим количеством запросов.
- Поддержка прокси: Telethon может работать через прокси (SOCKS, HTTP).

---

## **1.2 Установка Telethon**

Для начала работы с Telethon его нужно установить. Это можно сделать с помощью pip:

```bash
pip install telethon
```
https://docs.telethon.dev/en/stable/basic/installation.html
### **Проверка установки:**

После установки можно проверить, что Telethon установлен корректно, запустив Python и выполнив:

```python
import telethon
print(telethon.__version__)
```


Если версия Telethon выводится без ошибок, значит, установка прошла успешно.

---

## **1.3 Создание первого клиента**

Для работы с Telethon нужно создать клиент. Клиент — это объект, который управляет соединением с Telegram API.
https://docs.telethon.dev/en/stable/basic/quick-start.html
### **Шаги для создания клиента:**

1. Получить API ID и API Hash:
    
    - Перейдите на [my.telegram.org](https://my.telegram.org/).
        
    - Создайте новое приложение и получите API ID и API Hash.
        
2. Создать клиент:
    
    - Используйте `TelegramClient` для создания клиента.
        

### **Пример кода:**

```python
from telethon import TelegramClient
```

# Замените на свои значения

```python
api_id = 123456  # Ваш API ID
api_hash = 'your_api_hash'  # Ваш API Hash
phone_number = '+1234567890'  # Ваш номер телефона
```

# Создаем клиент

```python
client = TelegramClient('session_name', api_id, api_hash)

async def main():
    # Подключаемся к Telegram
    await client.start(phone_number)
    print("Клиент успешно запущен!")
```

# Запускаем клиент

```python
with client:
    client.loop.run_until_complete(main())
```

### **Что происходит в этом коде:**

- `TelegramClient('session_name', api_id, api_hash)` — создает клиент с именем сессии `session_name`.
    
- `client.start(phone_number)` — авторизует клиент по номеру телефона.
    
- `client.loop.run_until_complete(main())` — запускает асинхронную функцию `main()`.
    

---

## **1.4 Работа с сессиями**

Telethon использует сессии для сохранения состояния клиента. Сессии позволяют не авторизовываться каждый раз при запуске клиента.
https://docs.telethon.dev/en/stable/basic/signing-in.html
### **Как работают сессии:**

- При первом запуске клиент запрашивает код подтверждения и сохраняет сессию.
    
- При последующих запусках клиент использует сохраненную сессию для авторизации.
    

### **Пример сохранения и загрузки сессии:**

```python
from telethon import TelegramClient

api_id = 123456
api_hash = 'your_api_hash'
phone_number = '+1234567890'
```

# Создаем клиент с именем сессии 'my_session'

```python
client = TelegramClient('my_session', api_id, api_hash)

async def main():
    # Подключаемся к Telegram
    await client.start(phone_number)
    print("Клиент успешно запущен!")
```

# Запускаем клиент

```python
with client:
    client.loop.run_until_complete(main())
```

### **Где хранится сессия:**

- Сессия сохраняется в файле `my_session.session` в текущей директории.
    

---

## **1.5 Получение информации о себе**

После авторизации можно получить информацию о своем аккаунте с помощью метода `get_me()`.
https://docs.telethon.dev/en/stable/modules/client.html#telethon.client.users.UserMethods.get_me
### **Пример кода:**

```python
from telethon import TelegramClient

api_id = 123456
api_hash = 'your_api_hash'
phone_number = '+1234567890'

client = TelegramClient('my_session', api_id, api_hash)

async def main():
    await client.start(phone_number)
    me = await client.get_me()
    print(f"Имя: {me.first_name}")
    print(f"Фамилия: {me.last_name}")
    print(f"Username: {me.username}")
    print(f"ID: {me.id}")

with client:
    client.loop.run_until_complete(main())
```

### **Что выводит этот код:**

- Имя, фамилия, username и ID вашего аккаунта.
    

---

## **1.6 Важность перевода ошибок и поиска их в Google**

При работе с Telethon (и любым другим API) могут возникать ошибки. Важно уметь их переводить и искать решения в Google.

### **Пример ошибки:**

```
telethon.errors.rpcerrorlist.PhoneNumberInvalidError: The phone number is invalid
```
https://docs.telethon.dev/en/stable/concepts/errors.html
### **Как действовать:**

1. **Переведите ошибку**: "Номер телефона недействителен".
    
2. **Проверьте номер телефона**: Убедитесь, что номер введен правильно.
    
3. **Поищите решение в Google**: Введите текст ошибки в Google, чтобы найти похожие случаи и решения.
    

---

## **1.7 Практическое задание**

1. Установите Telethon и создайте клиент.
    
2. Авторизуйтесь с помощью номера телефона и получите информацию о своем аккаунте. (но рекомендуется использовать твинк, или аккаунт с физическим номером)
    
3. Попробуйте вызвать ошибку (например, введите неверный номер телефона) и найдите решение в Google.
    

---

## **1.8 Дополнительные материалы**

- [Официальная документация Telethon](https://docs.telethon.dev/)
    
- [Примеры использования Telethon](https://docs.telethon.dev/en/stable/concepts/full-api.html)
    

---
