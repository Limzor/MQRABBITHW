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
# coding=utf-8
import pika

connection = pika.BlockingConnection(pika.ConnectionParameters('10.0.2.15'))
channel = connection.channel()
channel.queue_declare(queue='hello')


def callback(ch, method, properties, body):
    print(" [x] Received %r" % body)


channel.basic_consume(callback, queue='hello', no_ack=True)
channel.start_consuming()
### ERROR
### producer.py IP:10.0.2.15
#!/usr/bin/env python
# coding=utf-8
import pika

connection = pika.BlockingConnection(pika.ConnectionParameters('l0.0.2.5'))
channel = connection.channel()
channel.queue_declare(queue='hello')
channel.basic_publish(exchange='', routing_key='hello', body='Hello Netology!')
connection.close()
ERROR
