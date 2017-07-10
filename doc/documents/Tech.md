#Техническое описание 

#HEAD OFFICE

##API сервис

“Cофтинформ”   
 Draft 


	Введение  
	Запуск сервиса с начала  
	Заполнение историческими данными  
	Описание общей структуры сервиса  
	Управление  
	Особенности эксплуатации  
	Технические аспекты 


Автор :  
**Савченко Артур**  
Киев - 2015  
26-02-2015  




**Создание новой аптеки**  
Для создания новой аптеки необходимо произвести ряд операций в результате которых будет сделано :

    http://10.0.3.24:5555/api/system/addapteka/3565506*1*1*tablename

1. Добавлена новая аптека в справочник “Contributors” и получен новый ИД
2. Создана новая таблица  для аккумулирования данных поступающих от аптек о продажах.
3. Имя таблицы - “А_” + ID (Например A_5645775) Addapteka (4060)
4. Созданы индексы 
5. Преобразованы данные в INTEGER  ChangeTypeFields [1577]
6. Созданы записи в таблице Matrix      Sys_CreateMatrix() [3533]
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

Таблица
Назначение 
Primary
Indexes
A_000000
Данные по аптеки хранится каждая в отдельной таб
ID
DOC_DATE_TIME,ID_DRUG 
Aliance
Справочник альянсов
id


Assplan
Справочник ассортиментного плана
id


Contractors
Справочник аптек
ID


Docs
Документы
id


Drugs
Справочник медикаментов
ID


Error
Справочник ошибок
id


Holders
Справочник держателей лицензий
id


Linedirect
Справочник 
id


Log
Лог файл
id


Matrix
Справочник матриц для расчета анализа АВС
id
ABCC
ABCF 
BCQ 
ID_STRUCTURE
STRUCTURE 
XYZ
Need
Расчет потребностей
id
ABCC
ABCF 
BCQ 
ID_STRUCTURE
STRUCTURE 
XYZ
Setting
Справочник настройки
id


System
Системные значения и прочие вспомогательные
id


Task
Задачи по развитию системы
id


Templates
Справочник заготовок и шаблонов
id


Unified
Справочник связной
id

  Wrk
Расчетный промежуточная таблица
ID
ID_STRUCTURE


##Открытие новой аптеки :

- Создание записи в справочнике Contractors
- Создание таблицы по формату А_идаптеки (см . ID.Contractors)
- Создание данных для матрицы в справочнике Matrix
- Cоздание коєфициентов в справочнике Contractors

**Добавление движения по аптеке в базу хранилище**

Путь для загрузки документа из файла

    curl -X POST http://10.0.3.24:5555/need/adddoc/3565506   -T "docs.json" 
    -H "Content-Type: application/json; charset=utf-8;" 

Каждая запись аптеки должна иметь ID_STRUCTURE

Функция Need_AddNewDoc [4279]

