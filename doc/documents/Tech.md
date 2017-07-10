#Техническое описание 

# BASE SERVICE   
## API сервис    
 Draft 
	Введение  
	Запуск сервиса с начала  
	Заполнение историческими данными  
	Описание общей структуры сервиса  
	Управление  
	Особенности эксплуатации  
	Технические аспекты 


Автор :  
**Savage **  
Киев - 2015  
26-02-2015  




**Создание новой точки**  
Для создания новой точки необходимо произвести ряд операций в результате которых будет сделано :

    http://10.0.3.24:5555/api/system/newpoint/2*1*1*newpoint

1. Добавлена новая точка в справочник “Company” и получен новый ИД
2. Создана новая таблица  для аккумулирования данных поступающих от точках о продажах.
3. Имя таблицы - “А_” + ID (Например A_XXXXXX) 
4. Созданы индексы 
5. Преобразованы данные в INTEGER  ChangeTypeFields [1577]
6. Созданы записи в таблице Matrix      SysCreateMatrix() [3533]
7. Созданы записи в таблице Contributors.KOEF
8. Перенесены данные из исторических

**2. Backup Restore**  
Backup
Back up your data as follows:
**Dump the data from a RethinkDB cluster (placed in a file rethinkdb_dump_DATE_TIME.tar.gz by default)**

		$ rethinkdb dump -c HOST:PORT
		rethinkdb dump -c localhost:28015 -f backdb -e HO.A_3565506
		rethinkdb dump -c 127.0.0.1:28015 -f backdb -e HO.A_3565506
		rethinkdb dump -c localhost:28015 -f backdb -e HO.A_3565506


Since the backup process is using client drivers, it automatically takes advantage of the MVCC functionality built into RethinkDB. It will use some cluster resources, but will not lock out any of the clients, so you can safely run it on a live cluster.

**3. Restore**  
You can reimport the backup into a running cluster as follows:
# Reimport an earlier dump
$ rethinkdb restore -c HOST:PORT rethinkdb_dump_DATE_TIME.tar.gz

Таблицы

|Таблица|Назначение |Primary|Indexes|
|------|------|------|----|
|A_000000|Данные по точке хранится каждая в отдельной таб|ID|DOC_DATE_TIME,ID_DRUG 
|Aliance|Справочник альянсов|id||
|ssplan|Справочник ассортиментного плана|id
|Contractors|Справочник аптек|ID
|Docs|Документы|id
|Drugs|Справочник медикаментов|ID
|Error|Справочник ошибок|id
|Holders|Справочник держателей лицензий|id
|Linedirect|Справочник|id
|Log|Лог файл|id
|Matrix|Справочник матриц для расчета анализа АВС|id
|System|Системные значения и прочие вспомогательные|id
|Task|Задачи по развитию системы|id
|Templates|Справочник заготовок и шаблонов|id
|Unified|Справочник связной|id
|Wrk|Расчетный промежуточная таблица|ID|ID_STRUCTURE

##Открытие новой точки :

- Создание записи в справочнике Contractors
- Создание таблицы по формату А_идточки (см . ID.Contractors)
- Создание данных для матрицы в справочнике Matrix
- Cоздание коєфициентов в справочнике Contractors

**Добавление движения по аптеке в базу хранилище**

Путь для загрузки документа из файла

    curl -X POST http://0.0.0.00:5555/add/doc/xxxxxx   -T "docs.json" 
    -H "Content-Type: application/json; charset=utf-8;" 
Каждая запись должна иметь IDSTRUCTURE
