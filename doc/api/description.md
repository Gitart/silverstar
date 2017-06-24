# Описание API
## Все методы деляться на три категории :   

1. Информационные - получение справочников и состояние заказа   
2. Рабочие - управление системой и размещение информации  
3. Логирование - получение информации по логу действий   


## Error Codes
Если вызов API вызывает ошибку, в ответе задается наиболее подходящий код состояния HTTP, и объект JSON возвращается с подробностями об ошибке. Коды состояния HTTP в 200-х годах означают успешный вызов API, коды статуса в 400-х годах означают, что проблема с параметрами в кодах API и кодах статуса в значении 500 означает, что проблема была с серверами Streak. В любом случае объект JSON возвращается в ответ. Ниже приведена таблица возможных кодов состояния:

|Status Code|	Description|
|------|---|
|200|	Success
|400|	Bad Request. This usually occurs when trying to access the API over http instead of https.
|401|	Unauthorized. Either the api key provided does not have access to the resource or the provided API key is invalid.
|404|	Not Found. The resource requested was not found.

## Описание сущьностей в системе
|Сущьность|	Описание|
|------|---|
|Справочник |Получение информации о свободном месте в размещении	
|400|	
|401|	
|404|	



## Используется класический метод аутонтификации
[Basic Method](https://en.wikipedia.org/wiki/Basic_access_authentication)

## Примеры и пояснения
[Пример описания API](https://www.streak.com/api/#pipeline)  

