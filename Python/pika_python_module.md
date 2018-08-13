# Pika
- pure-Python implementation of the AMQP 0-9-1 protocol that tries to stay fairly independent of the underlying network support library

## install Pika
```python
pip install pika
```

## Sending
```python
import pika

connection = pika.BlockingConnection(pika.ConnectionParameters(hostname))
channel = connection.channel()
channel.queue_declare(queue=queuename)
```

---
## 참고문헌
- [rabbitMQ - tutorial one python](https://www.rabbitmq.com/tutorials/tutorial-one-python.html)
- [Pika - pure-Python implementation of the AMQP](https://pika.readthedocs.io/en/stable/)