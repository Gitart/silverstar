# Описание API
## Все методы деляться на три категории :   

1. Информационные - получение справочников и состояние заказа   
2. Рабочие - управление системой и размещение информации  
3. Логирование - получение информации по логу действий   


## Error Codes

If a call to the Streak API causes an error, the most appropriate HTTP status code is set in the response and a JSON object is returned with details about the error. HTTP status codes in the 200's mean a successful call to the API, status codes in the 400's mean there was a problem with the the parameters in the API call and status codes in the 500's mean there was an issue with Streak servers. In any case, a JSON object is returned in the response. Below is a table of possible status codes:

|Status Code|	Description|
|----|---|
|200|	Success
|400|	Bad Request. This usually occurs when trying to access the API over http instead of https.
|401|	Unauthorized. Either the api key provided does not have access to the resource or the provided API key is invalid.
|404|	Not Found. The resource requested was not found.


[Пример описания API](https://www.streak.com/api/#pipeline)
