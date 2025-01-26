
#### **3.1 Что такое события?**

События в Telethon — это действия, которые происходят в Telegram, например:

- Новое сообщение.
    
- Редактирование сообщения.
    
- Добавление в чат.
    
- Удаление сообщения.
    

Telethon позволяет подписываться на эти события и выполнять определенные действия при их возникновении.

---

#### **3.2 Подписка на события**

Для подписки на события используется декоратор `@client.on()`. Например, чтобы обрабатывать новые сообщения, нужно подписаться на событие `events.NewMessage`.

---

#### **3.3 Пример: Обработка новых сообщений**

Вот пример кода, который обрабатывает новые сообщения и отвечает на них:

```python
from telethon import TelegramClient, events

api_id = 123456
api_hash = 'your_api_hash'
phone_number = '+1234567890'

client = TelegramClient('my_session', api_id, api_hash)
```

# Обработчик новых сообщений

```python
@client.on(events.NewMessage)
async def new_message_handler(event):
    # Получаем текст сообщения
    message_text = event.message.text

    # Отвечаем на сообщение
    await event.reply(f"Вы написали: {message_text}")

async def main():
    await client.start(phone_number)
    print("Клиент запущен и готов к работе!")
    await client.run_until_disconnected()

with client:
    client.loop.run_until_complete(main())
```

---

#### **Что делает этот код:**

1. Создается обработчик `new_message_handler`, который срабатывает при получении нового сообщения.
    
2. Внутри обработчика:
    
    - Получается текст сообщения с помощью `event.message.text`.
        
    - Отправляется ответ с текстом `"Вы написали: {message_text}"`.
        
3. Клиент запускается и работает до тех пор, пока не будет отключен.
    

---

#### **3.4 Фильтрация событий**

Иногда нужно обрабатывать только определенные сообщения. Например, только те, которые начинаются с конкретного слова. Для этого используются фильтры.

---

#### **Пример: Фильтрация сообщений**

Вот пример, который отвечает только на сообщения, начинающиеся с "Привет":

```python
from telethon import TelegramClient, events

api_id = 123456
api_hash = 'your_api_hash'
phone_number = '+1234567890'

client = TelegramClient('my_session', api_id, api_hash)
```

# Обработчик сообщений, начинающихся с "Привет"

```python
@client.on(events.NewMessage(pattern='Привет'))
async def hello_handler(event):
    await event.reply("Привет! Как дела?")

async def main():
    await client.start(phone_number)
    print("Клиент запущен и готов к работе!")
    await client.run_until_disconnected()

with client:
    client.loop.run_until_complete(main())
```

---

#### **Что делает этот код:**

1. Обработчик `hello_handler` срабатывает только на сообщения, которые начинаются с "Привет".
    
2. На такие сообщения отправляется ответ: `"Привет! Как дела?"`.
    

---

#### **3.5 Обработка других событий**

Telethon поддерживает множество событий. Вот несколько примеров:

1. **Редактирование сообщений**:

```python
    @client.on(events.MessageEdited)
    async def edited_message_handler(event):
        await event.reply("Вы отредактировали сообщение!")
```
    
2. **Добавление в чат**:
    
```python
    @client.on(events.ChatAction)
    async def chat_action_handler(event):
        if event.user_joined:
            await event.reply("Добро пожаловать в чат!")
```
    
3. **Удаление сообщений**:
    
```python
    @client.on(events.MessageDeleted)
    async def deleted_message_handler(event):
        await event.reply("Сообщение было удалено!")
```
    

---

#### **3.6 Важность перевода ошибок и поиска их в Google**

При работе с событиями могут возникать ошибки, например:

- `telethon.errors.rpcerrorlist.FloodWaitError`: Ошибка, связанная с ограничением Telegram (например, слишком много запросов).
    
- `telethon.errors.rpcerrorlist.ChatAdminRequiredError`: Ошибка, связанная с отсутствием прав администратора.
    

---

#### **Как действовать:**

1. **Переведите ошибку**: Например, `FloodWaitError` — "Необходимо подождать перед следующим действием".
    
2. **Проверьте причину**: Убедитесь, что вы не нарушаете ограничения Telegram.
    
3. **Поищите решение в Google**: Введите текст ошибки, чтобы найти похожие случаи и решения.
    

---

#### **3.7 Практическое задание**

1. Создайте обработчик, который отвечает на сообщения, содержащие слово "котик".
    
2. Добавьте обработчик для события "добавление в чат", который отправляет приветственное сообщение новым участникам.
    
3. Попробуйте вызвать ошибку (например, отправьте слишком много сообщений) и найдите решение в Google.