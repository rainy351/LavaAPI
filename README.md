# LavaAPI
A Python API for Lava Payment System - 2024

Forked from `https://github.com/Banjirome/NewLavaAPI`

Добавлена функция для вывода и исправлены некоторые опечатки.
# LavaAPI documentation
## Начало
Добавьте файл `LavaAPI.py` в проект

Для использования библиотеки вам необходимо создать экземпеляр LavaAPI с указанием api_key и shop_id вашего магазина.
```
api_key = '****************************************'
shopid = "********-****-****-****-************"
api = LavaAPI(api_key, shopid)
```
## Использование
В созданном вами экземпляре имеются следующие функции:
1. `create_invoice()` - Принимает в себя айди счета, сумму и комментарий к вашему чеку. Важно: айди счета существующих чеков должны быть уникальными
2. `balance()` - Возвращает баланс вашего магазина в валюте, указанной в личном кабинете
3. `create_payoff()` - Принимает в себя айди счета, сумму, название сервиса, номер кошелька и переменную, отвечающую за способ оплаты комиссии - с магазина или с суммы. Важно: айди счета существующих чеков должны быть уникальными

## Статусы платежей
Функция `create_invoice()` возвращает класс типа Payment(). Он содержит в себе информацию о выставленном счете (orderID, paymentID, payment_url)

В нем есть функция проверки платежа `check_invoice_status()` возвращающая True или False в зависимости от статуса платежа

## Пример
```
from LavaAPI import LavaAPI
import random

api_key = '****************************************'
shopid = "********-****-****-****-************"
api = LavaAPI(api_key, shopid) # Вызываем класс LavaAPI

print(f"Ваш баланс: {api.balance()}")
orderid = random.randint(11111111, 99999999) # Лучше всего генерировать orderID случайно
print(f"Создаем платеж с номером: {orderid}")
payment = api.create_invoice(orderid, float(amount), comment)
print(f"URL счета: {payment.url}")
print(f"Айди счета: {payment.paymentID}")
payment_status = payment.check_invoice_status()
if payment_status:
  print(f"Счет оплачен")
else:
  print(f"Счет не оплачен")

valid_status = api.auth_test() # проверяем валидность наших данных. Можно использовать для установки статуса в вашем проекте и уведомлениях
if valid_status:
  print("Данные валидны")

```
