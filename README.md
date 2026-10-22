# Домашнее задание: Установка и настройка кластера RabbitMQ

**Выполнил:** Захарян Николай  
  
**Дата:** 22 октября 2026 г.

---

## Задание 1. Установка RabbitMQ

**Выполненные действия:**
1. Создана виртуальная машина в VirtualBox (ОС: Ubuntu 22.04/24.04).
2. Установлен пакет `rabbitmq-server`.
3. Включен плагин управления: `sudo rabbitmq-plugins enable rabbitmq_management`.
4. Создан пользователь `admin` с правами администратора для доступа к веб-интерфейсу по IP-адресу.

**Результат:**
Веб-интерфейс RabbitMQ успешно запущен и доступен по адресу `http://<IP_адрес_VM>:15672`.

![Веб-интерфейс RabbitMQ Overview](screenshots/task1_overview.png)  
<img width="1920" height="792" alt="2026-10-02_13-49-31" src="https://github.com/user-attachments/assets/5c9cb16a-072b-4d7f-b9eb-bbc2fdddef64" />


<img width="463" height="89" alt="2026-10-02_14-02-42" src="https://github.com/user-attachments/assets/af798461-e9eb-49cb-905b-6e8f991ca6e5" />

<img width="1273" height="799" alt="2026-10-21_15-01-56" src="https://github.com/user-attachments/assets/b1ee21f6-c502-4ce2-948a-9ebe4e5cc734" />

<img width="1275" height="723" alt="2026-10-21_16-41-25" src="https://github.com/user-attachments/assets/a87f4d37-49a3-485c-bf53-cba7e7054897" />

<img width="598" height="109" alt="2026-10-21_16-44-07" src="https://github.com/user-attachments/assets/267ff950-bda8-432b-90e3-cb33ab4e2e3b" />

<img width="800" height="535" alt="2026-10-22_17-14-23" src="https://github.com/user-attachments/assets/3e0ca000-10b8-4af1-923e-17cbc85d4c6d" />

<img width="813" height="578" alt="2026-10-22_17-15-06" src="https://github.com/user-attachments/assets/553f67e7-ba91-450c-beb6-9b12ec6d92db" />

<img width="1053" height="180" alt="2026-10-22_17-23-59" src="https://github.com/user-attachments/assets/eda456f0-ff44-4e6b-869f-bfdfc6f08209" />

## Задание 2. Отправка и получение сообщений

producer.py
```python
import pika

credentials = pika.PlainCredentials('admin', 'admin')
connection = pika.BlockingConnection(pika.ConnectionParameters(
    host='192.168.56.10', # Заменен localhost на IP виртуальной машины
    credentials=credentials
))
channel = connection.channel()
channel.queue_declare(queue='hello')
channel.basic_publish(exchange='', routing_key='hello', body='Hello RabbitMQ!')
print(" [x] Sent 'Hello RabbitMQ!'")
connection.close()


`consumer.py`:
```python
import pika

credentials = pika.PlainCredentials('admin', 'admin')
connection = pika.BlockingConnection(pika.ConnectionParameters(
    host='192.168.56.10', 
    credentials=credentials
))
channel = connection.channel()
channel.queue_declare(queue='hello')

def callback(ch, method, properties, body):
    print(f" [x] Received {body.decode()}")

channel.basic_consume(queue='hello', on_message_callback=callback, auto_ack=True)
print(' [*] Waiting for messages. To exit press CTRL+C')
channel.start_consuming():

---

## Задание 3. Подготовка HA кластера

Выполненные действия:
Созданы две ВМ: rmq01 (192.168.56.10) и rmq02 (192.168.56.11).
В /etc/hosts на обеих машинах добавлены записи для разрешения имен.
Синхронизирован файл .erlang.cookie.
Нода rmq02 присоединена к кластеру rmq01.
Создана политика высокой доступности:
sudo rabbitmqctl set_policy ha-all "^" '{"ha-mode":"all"}'

<img width="1199" height="716" alt="2026-10-22_17-21-48" src="https://github.com/user-attachments/assets/cf8fa87e-af8d-49ae-9537-4d3433bba12d" />

<img width="806" height="532" alt="2026-10-22_17-33-41" src="https://github.com/user-attachments/assets/ecfceae5-3cc1-4d5f-8896-6feb77d76d26" />
