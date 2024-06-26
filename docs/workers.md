# Рабочие
Рабочие - важная часть игры, ведь именно они работают над проектами компании.
У каждого рабочего есть свой уровень, который напрямую влияет на его производительность и зарплату.
Зарплата указана в кредитах и взимается каждые сутки
****
## Рабочие компании

Данный метод используется для получения информации о рабочих компании

**URL запроса** - `https://sep.fdu.su/api/my_employees`

**Метод:** `POST`

**Параметры:**

    token - токен пользователя

_Пример ответа:_ 

    {
        "result": "ok", 
        "data": [
                    {
                        "worker_id": 1,
                        "lvl": 2,
                        "salary": 550,
                        "worked_by": 2
                    },
                    {
                        "worker_id": 2,
                        "lvl": 1,
                        "salary": 150,
                        "worked_by": 2
                    },
    }

`worker_id - порядковый номер работника в игре`

`lvl - уровень работника`

`salary - зарплата работника (взимается каждые сутки)`

`worked_by - project_id, над которым закреплен работник (см. Проекты)`
****
## Увольнение работника

Данный метод используется для увольнения работника из компании

**URL запроса** - `https://sep.fdu.su/api/bench_worker`

**Метод:** `POST`

**Параметры:**

    token - токен пользователя
    worker_id - ID работника, который можно получить из my_employees

_Пример ответа:_ 
    
    {"result": "ok", "text": "Success bench"}

****
## Биржа работников

Данный метод используется для получения информации о всех работниках, доступных для найма. 
Количество работников ограничено и обновляется спустя некоторое время, если их мало. 
Так же сюда попадают уволенные из других компаний работники

**URL запроса** - `https://sep.fdu.su/api/employees_market`

**Метод:** `POST`

**Параметры:**

    token - токен пользователя

_Пример ответа:_ 
    
    {
        "result": "ok", 
        "data": [
                    {
                        "lvl": 1,
                        "salary": 150,
                        "worker_id": 3
                    },
                    {
                        "lvl": 2,
                        "salary": 450,
                        "worker_id": 4
                    },
                ]
    }

****
## Найм работника

Данный метод используется для найма работника в компанию. 
Для трудоустройства работника в свою компанию, необходимо оплатить сумму его зарплаты при найме

**URL запроса** - `https://sep.fdu.su/api/hire_employee`

**Метод:** `POST`

**Параметры:**

    token - токен пользователя
    employee_id - ID работника, который можно получить из worker_market

_Пример ответа:_ 
    
    {"result": "ok", "text": "Success"}

**Внутриигровые ошибки:**
    
    "Employee lvl > your lvl" - уровень рабочего выше вашего уровня (нанимать можно только рабочих, уровень который ниже или равен вашему)

    "You've reach a limit of employees. Boost your lvl" - вы достигли лимита по количество работников в вашей компании. Повысьте свой уровень или увольте ненужных работников

    "Not enough credits" - у вас не хватает средств на балансе

