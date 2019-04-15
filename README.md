# vkcoin
Враппер для платёжного API VK Coin. https://vk.com/@hs-marchant-api
# Установка
* Скачайте и установите [Python](https://www.python.org/downloads/) версии 3.6 и выше
* Введите следующую команду в командную строку:
```bash
pip install vkcoin
```
* Вы прекрасны!
# Начало работы
Для начала разработки, необходимо создать в своей папке исполняемый файл с расширением **.py**, например **test.py**. Вы не можете назвать файл vkcoin.py, так как это приведёт к конфликту. Теперь файл нужно открыть и импортировать библиотеку:
```python
import vkcoin

merchant = vkcoin.Merchant(user_id=123456789, key='xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx')
```
|Параметр|Тип|Описание|
|-|-|-|
|user_id|Integer|ID аккаунта ВКонтакте|
|key|String|Ключ для взаимодействия с API|
|_token_|String|Токен VK API, полученный по инструкции (необходим только для _on_payment_)|
|_on_payment_|Function|Callback функция, которая будет вызвана при получении перевода от других пользователей|
# Методы
Необязательные параметры при вызове функций выделены _курсивом_.

[`get_payment_url`](https://vk.com/@hs-marchant-api?anchor=ssylka-na-oplatu) - получет ссылку на оплату VK Coin
```python
result = merchant.get_payment_url(amount=10, payload=78922, free_amount=False)
print(result)
```
|Параметр|Тип|Описание|
|-|-|-|
|amount|Float|Количество VK Coin для перевода|
|_payload_|Integer|Число от -2000000000 до 2000000000, вернется в списке транзаций|
|_free_amount_|Boolean|True, что бы позволить пользователю изменять сумму перевода|
#
[`get_transactions`](https://vk.com/@hs-marchant-api?anchor=poluchenie-spiska-tranzaktsy) - получает список ваших транзакций
```python
result = merchant.get_transactions(tx=[1])
print(result)
```
|Параметр|Тип|Описание|
|-|-|-|
|tx|List|Массив ID переводов для получения или [1] - последние 1000 транзакций, [2] - 100|
|_last_tx_|Integer|Если указать номер последней транзакции то будут возвращены только транзакции после указанной|
#
[`send`](https://vk.com/@hs-marchant-api?anchor=perevod) - делает перевод другому пользователю
```python
result = merchant.send(amount=100, to_id=371576679)  # Если запустить этот код, вы переведёте мне 100 VK Coin :)
print(result)
```
|Параметр|Тип|Описание|
|-|-|-|
|amount|Float|Сумма перевода|
|to_id|Integer|ID аккаунта, на который будет совершён перевод|
#
`get_balance` - возвращает баланс аккаунта
```python
result = merchant.get_balance(user_ids=[123456789])
print(result)
```
|Параметр|Тип|Описание|
|-|-|-|
|user_ids|List|ID аккаунтов, баланс которых нужно получить|
# Callback
Описание параметров, которые будут переданы в callback функции.

`on_payment` - вызывается при получении перевода от других пользователей
```python
def on_payment_recieved(user_id, amount):
    print(user_id, amount)
```
|Параметр|Тип|Описание|
|-|-|-|
|user_id|Integer|ID аккаунта, с которого был совершён перевод|
|amount|Float|Сумма перевода|
# Примеры
### Callback
```python
import vkcoin

def on_payment_recieved(user_id, amount):
    print(user_id, amount)

merchant = vkcoin.Merchant(user_id=123456789, key='xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx', on_payment=on_payment_recieved)
```
# Благодарности
[Эдгар Горобчук](https://vk.com/edgar_gorobchuk) - за написание [SpootiFM/vkcoin](https://github.com/SpootiFM/vkcoin)

[Eвгений Чертков](https://vk.com/dgs00) - за PEP
# Где меня можно найти
Могу ответить на ваши вопросы
* [ВКонтакте](https://vk.com/crinny)
* [Telegram](https://t.me/truecrinny)
* [Чат ВКонтакте по VK Coin API (не мой)](https://vk.me/join/AJQ1d5eSUQ81wnwgfHSRktCi)