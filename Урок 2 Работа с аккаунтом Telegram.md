
## **2.1 Получение информации о чатах и пользователях**

Telethon позволяет получать информацию о чатах, каналах и пользователях. Это полезно для автоматизации задач, таких как управление группами или анализ активности.

### **Основные методы:**

- `client.get_entity()` — получение информации о чате или пользователе по username, ID или ссылке.
- `client.get_participants()` — получение списка участников чата.
- `client.get_messages()` — получение сообщений из чата.

### **Пример: Получение информации о чате**

```python
from telethon import TelegramClient

api_id = 123456
api_hash = 'your_api_hash'
phone_number = '+1234567890'

client = TelegramClient('my_session', api_id, api_hash)

async def main():
    await client.start(phone_number)

    # Получаем информацию о чате по username
    chat = await client.get_entity('username_or_chat_link')
    print(f"Название чата: {chat.title}")
    print(f"ID чата: {chat.id}")
    print(f"Участников: {chat.participants_count}")

with client:
    client.loop.run_until_complete(main())
```

### **Что делает этот код:**

- Получает информацию о чате по его username или ссылке.
- Выводит название чата, его ID и количество участников.

---

## **2.2 Получение списка участников чата**

Для получения списка участников чата используется метод `get_participants()`.

### **Пример: Получение списка участников**

```python
from telethon import TelegramClient

api_id = 123456
api_hash = 'your_api_hash'
phone_number = '+1234567890'

client = TelegramClient('my_session', api_id, api_hash)

async def main():
    await client.start(phone_number)

    # Получаем информацию о чате
    chat = await client.get_entity('username_or_chat_link')

    # Получаем список участников
    participants = await client.get_participants(chat)
    for user in participants:
        print(f"Имя: {user.first_name}, Username: {user.username}, ID: {user.id}")

with client:
    client.loop.run_until_complete(main())
```

### **Что делает этот код:**

- Получает список участников чата.
    
- Выводит имя, username и ID каждого участника.
    

---

## **2.3 Отправка сообщений**

Telethon позволяет отправлять текстовые сообщения, медиафайлы и даже стикеры.

### **Основные методы:**

- `client.send_message()` — отправка текстового сообщения.
    
- `client.send_file()` — отправка медиафайла.
    
- `client.send_sticker()` — отправка стикера.
    

### **Пример: Отправка текстового сообщения**

```python
from telethon import TelegramClient

api_id = 123456
api_hash = 'your_api_hash'
phone_number = '+1234567890'

client = TelegramClient('my_session', api_id, api_hash)

async def main():
    await client.start(phone_number)

    # Отправляем сообщение в чат
    await client.send_message('username_or_chat_link', 'Привет, это тестовое сообщение!')

with client:
    client.loop.run_until_complete(main())
```

### **Что делает этот код:**

- Отправляет текстовое сообщение в указанный чат.
    

---

## **2.4 Отправка медиафайлов**

Для отправки медиафайлов используется метод `send_file()`.

### **Пример: Отправка фото**

```python
from telethon import TelegramClient

api_id = 123456
api_hash = 'your_api_hash'
phone_number = '+1234567890'

client = TelegramClient('my_session', api_id, api_hash)

async def main():
    await client.start(phone_number)

    # Отправляем фото в чат
    await client.send_file('username_or_chat_link', 'path/to/photo.jpg')

with client:
    client.loop.run_until_complete(main())
```

### **Что делает этот код:**

- Отправляет фото в указанный чат.
    

---

## **2.5 Получение сообщений**

Telethon позволяет получать сообщения из чата с помощью метода `get_messages()`.

### **Пример: Получение последних 10 сообщений**


```python
from telethon import TelegramClient

api_id = 123456
api_hash = 'your_api_hash'
phone_number = '+1234567890'

client = TelegramClient('my_session', api_id, api_hash)

async def main():
    await client.start(phone_number)

    # Получаем последние 10 сообщений из чата
    messages = await client.get_messages('username_or_chat_link', limit=10)
    for message in messages:
        print(f"Сообщение от {message.sender_id}: {message.text}")

with client:
    client.loop.run_until_complete(main())
```

### **Что делает этот код:**

- Получает последние 10 сообщений из чата.
    
- Выводит текст сообщения и ID отправителя.
    

---

## **2.6 Важность перевода ошибок и поиска их в Google**

При работе с Telethon могут возникать ошибки, связанные с ограничениями Telegram API или неправильным использованием методов.

### **Пример ошибки:**

```
telethon.errors.rpcerrorlist.ChatWriteForbiddenError: You can't write in this chat
```

### **Как действовать:**

1. **Переведите ошибку**: "Вы не можете писать в этом чате".
    
2. **Проверьте права**: Убедитесь, что у вас есть права на отправку сообщений в этом чате.
    
3. **Поищите решение в Google**: Введите текст ошибки в Google, чтобы найти похожие случаи и решения.
    

---

## **2.7 Практическое задание**

1. Получите информацию о чате и выведите его название и количество участников.
    
2. Отправьте текстовое сообщение и фото в чат.
    
3. Получите последние 10 сообщений из чата и выведите их текст.