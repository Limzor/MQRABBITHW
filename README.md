# Домашнее задание к занятию "`Очереди RabbitMQ`" - `Фёдоров Илья`

### Задание 1
![alt text](https://github.com/Limzor/mqrabbithw/blob/main/Screenshot_1.png)

### Задание 2
![alt text](https://github.com/Limzor/mqrabbithw/blob/main/Screenshot_2.png)
![alt text](https://github.com/Limzor/mqrabbithw/blob/main/Screenshot_3.png)
![alt text](https://github.com/Limzor/mqrabbithw/blob/main/Screenshot_4.png)
![alt text](https://github.com/Limzor/mqrabbithw/blob/main/Screenshot_5.png)
![alt text](https://github.com/Limzor/mqrabbithw/blob/main/Screenshot_6.png)
![alt text](https://github.com/Limzor/mqrabbithw/blob/main/Screenshot_7.png)
![alt text](https://github.com/Limzor/mqrabbithw/blob/main/Screenshot_8.png)
![alt text](https://github.com/Limzor/mqrabbithw/blob/main/Screenshot_9.png)

### Задание 3
![alt text](https://github.com/Limzor/mqrabbithw/blob/main/Screenshot_10.png)


P.S я пытался выполнить задание №2 используя виртуальные машины но каждый раз выходила ошибка. Решения в интернете я не смог найти, буду очень благодарен если подскажете. (обе машины находились в одной сети и пинговались)
вот
### consumer.py IP:10.0.2.5
#!/usr/bin/env python
#coding=utf-8
import pika

connection = pika.BlockingConnection(pika.ConnectionParameters('10.0.2.15'))
channel = connection.channel()
channel.queue_declare(queue='hello')


def callback(ch, method, properties, body):
    print(" [x] Received %r" % body)


channel.basic_consume(callback, queue='hello', no_ack=True)
channel.start_consuming()
### ERROR
limzor@limzor:~/pip$ /home/limzor/pip/myenv/bin/python /home/limzor/pip/consumer.py
Traceback (most recent call last):
  File "/home/limzor/pip/consumer.py", line 5, in <module>
    connection = pika.BlockingConnection(pika.ConnectionParameters('10.0.2.15'))
                 ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
  File "/home/limzor/pip/myenv/lib/python3.11/site-packages/pika/adapters/blocking_connection.py", line 360, in __init__
    self._impl = self._create_connection(parameters, _impl_class)
                 ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
  File "/home/limzor/pip/myenv/lib/python3.11/site-packages/pika/adapters/blocking_connection.py", line 451, in _create_connection
    raise self._reap_last_connection_workflow_error(error)
pika.exceptions.AMQPConnectionError
### producer.py IP:10.0.2.15
#!/usr/bin/env python
#coding=utf-8
import pika

connection = pika.BlockingConnection(pika.ConnectionParameters('l0.0.2.5'))
channel = connection.channel()
channel.queue_declare(queue='hello')
channel.basic_publish(exchange='', routing_key='hello', body='Hello Netology!')
connection.close()
### ERROR
(myenv) limzor@limzor:~/pip$ /home/limzor/pip/myenv/bin/python /home/limzor/pip/producer.py
Traceback (most recent call last):
  File "/home/limzor/pip/producer.py", line 5, in <module>
    connection = pika.BlockingConnection(pika.ConnectionParameters('10.0.2.15'))
                 ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
  File "/home/limzor/pip/myenv/lib/python3.11/site-packages/pika/adapters/blocking_connection.py", line 360, in __init__
    self._impl = self._create_connection(parameters, _impl_class)
                 ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
  File "/home/limzor/pip/myenv/lib/python3.11/site-packages/pika/adapters/blocking_connection.py", line 451, in _create_connection
    raise self._reap_last_connection_workflow_error(error)
pika.exceptions.AMQPConnectionError

P.S 2.0
Я нашёл решение проблемы. Полез в оф документацию и там код для consumer/producer немного отличается. Для верности удалил MQ и установил как следуюет, после чего всё заработало.

![alt text](https://github.com/Limzor/mqrabbithw/blob/main/mq1.png)
![alt text](https://github.com/Limzor/mqrabbithw/blob/main/mq2.png)
![alt text](https://github.com/Limzor/mqrabbithw/blob/main/mq3.png)
![alt text](https://github.com/Limzor/mqrabbithw/blob/main/mq4.png)
