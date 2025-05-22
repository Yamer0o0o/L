# Домашнее задание к занятию "`11.2. Кеширование Redis/memcached`" - `Леонов Александр`
## Задание 1. Кеширование 

Приведите примеры проблем, которые может решить кеширование. 

*Приведите ответ в свободной форме.*

### Кеширование повышает производительность системы
Кеширование оптимизирует работу системы за счет:
- расположения в быстром кеше данных, к которым выполняются запросы чаще всего;
- экономии ресурсов (обращаемся не к БД а к кешу);
- сглаживания бустов трафика во время пиковых нагрузок обращений к БД.

---

## Задание 2. Memcached

Установите и запустите memcached.

*Приведите скриншот systemctl status memcached, где будет видно, что memcached запущен.*

### Установка memcached
```
sudo apt update && sudo apt install memcached
memcached -V
sudo netstat -tap | grep memcached
sudo systemctl status memcached
```
### Скриншот состояния memcached
![Скриншот состояния memcached](https://github.com/StanislavBaranovskii/11-2-hw/blob/main/img/11-2-2.png "Скриншот состояния memcached")
---

## Задание 3. Удаление по TTL в Memcached

Запишите в memcached несколько ключей с любыми именами и значениями, для которых выставлен TTL 5. 

*Приведите скриншот, на котором видно, что спустя 5 секунд ключи удалились из базы.*

### Листинг команд (ключ k3 задан с TTL=5)
```
telnet localhost 11211
version
get k1
get k2
get k3
set k1 1 120 10
JournalDev
set k2 0 120 8
testword
set k3 2 5 10
JournalDev
get k3
get k2
get k1
flush_all
quit
```

### Скриншот выполнения команд
![Скриншот3](https://github.com/StanislavBaranovskii/11-2-hw/blob/main/img/11-2-3.png "Скриншот3")
---

## Задание 4. Запись данных в Redis

Запишите в Redis несколько ключей с любыми именами и значениями. 

*Через redis-cli достаньте все записанные ключи и значения из базы, приведите скриншот этой операции.*

### Установка и проверка redis
```
sudo apt install -y redis
sudo systemctl status redis

```
### Листинг команд
```
redis-cli

scan 0
set k1 test
set k2 100
scan 0
get k1
get k2
flushall
exit
```
### Скриншот выполнения команд
![Скриншот4](https://github.com/StanislavBaranovskii/11-2-hw/blob/main/img/11-2-4.png "Скриншот4")

---

## Задание 5*. Работа с числами 

Запишите в Redis ключ key5 со значением типа "int" равным числу 5. Увеличьте его на 5, чтобы в итоге в значении лежало число 10.  

*Приведите скриншот, где будут проделаны все операции и будет видно, что значение key5 стало равно 10.*

### Листинг команд
```
redis-cli

scan 0
set key5 5
exists key5
get key5
ttl key5
type key5
incrby key5 5
get key5
type key5
flushall
exit
```
### Скриншот выполнения команд
![Скриншот5](https://github.com/StanislavBaranovskii/11-2-hw/blob/main/img/11-2-5.png "Скриншот5")

---
