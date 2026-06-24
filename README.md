# Домашнее задание к занятию "`Базы данных`" - `Тапилин Артём`

### Задание 1

Нужно создать 6 таблиц.

- таблица сотрудников(содержит ФИО, оклад, дату найма и ссылки на другие таблицы),
- таблица должности(содержит Наименования должностей)
- таблица тип подразделения(содержит информацию о типах подразделений Группа/Департамент/Отдел)
- таблица структурное подразделения(содержит информацию о структурах подразделений)
- таблица адреса филиалов(содержит Адреса)
- таблица проекты(содержит Наименования проектов)


### Задание 2

# Создание таблиц
CREATE TABLE IF NOT EXISTS employee (
id SERIAL PRIMARY KEY,
full_name VARCHAR(100) NOT NULL UNIQUE,
salary FLOAT NOT NULL,
position SMALLINT NOT NULL REFERENCES position(id),
department_type SMALLINT NOT NULL REFERENCES department(id),
department SMALLINT NOT NULL REFERENCES department_type(id),
hire_date DATE NOT NULL,
filial_address SMALLINT NOT NULL REFERENCES filial_addresses(id),
project_info SMALLINT NOT NULL REFERENCES projects(id)
);

ALTER TABLE employee (hire_date DATE)

CREATE TABLE IF NOT EXISTS position (
id SERIAL PRIMARY KEY,
name_pos VARCHAR(128) NOT NULL UNIQUE
);

CREATE TABLE IF NOT EXISTS department_type  (
id SERIAL PRIMARY KEY,
name_dep VARCHAR(100) NOT NULL UNIQUE
);

CREATE TABLE IF NOT EXISTS department (
id SERIAL PRIMARY KEY,
name_deps VARCHAR(100) NOT NULL UNIQUE
);

CREATE TABLE IF NOT EXISTS filial_addresses (
id SERIAL PRIMARY KEY,
address VARCHAR(255) NOT NULL UNIQUE
);

CREATE TABLE IF NOT EXISTS projects (
id SERIAL PRIMARY KEY,
name_of_project VARCHAR(255) NOT NULL UNIQUE
);

# Добавление данных

INSERT INTO position (name_pos)
VALUES
('ведущий QA инженер'),
('ведущий архитектор'),
('ведущий инженер'),
('ведущий разработчик'),
('инженер'),
('разработчик'),
('руководитель направления разработки'),
('руководитель проектов'),
('руководитель проектов по интеграции'),
('руководитель сервисных проектов'),
('специалист'),
('специалист по персоналу'),
('старший архитектор'),
('старший инженер'),
('старший разработчик');

INSERT INTO department_type (name_dep)
VALUES
('Отдел'),
('Группа'),
('Департамент');

INSERT INTO department (name_deps)
VALUES
('Центр компетенций QA Москва'),
('Группа сервисной поддержки'),
('Центр разработки продуктов для digital-маркетинга'),
('Департамент Техническая поддержка'),
('Группа CRM 2'),
('Группа первичной диагностики №2'),
('Группа Billing'),
('Группа DOC'),
('Группа ODS'),
('Группа Rating'),
('Центр управления сервисами'),
('Департамент FBF'),
('Центр анализа и архектуры Medio'),
('Центр разработки Medio'),
('Группа инфраструктуры'),
('Департамент Rating and Charging');

INSERT INTO filial_addresses (address)
VALUES
('Приморский край, г. Владивосток, ул Нижнепортовая, д. 1'),
('Краснодарский край, г. Краснодар, ул Путевая, д. 1'),
('Ростовская обл, г. Ростов-на-Дону, ул 2-я Краснодарская, д. 135/2');

INSERT INTO projects (name_of_project)
VALUES
('Итэлма Инженерный корпус'),
('Севастополь ТВ'),
('Кристалл Доп объем'),
('Ростелеком. Гончарная,ВТБ Башня PM'),
('Газпромбанк Бирюзова'),
('Гпб Оазис Кабинет З.'),
('Комплекс Pine Creek Доп работы'),
('Сбербанк Нижний Новгород'),
('Рособоронэкспорт _ PM'),
('Ростелеком Академик'),
('Оформление планировочных Итэлма'),
('ТМК. Сколково'),
('16120_1_TUL (ДС5)'),
('ИКСпФОН (РД)'),
('Европлан'),
('Газпромбанк Аквамарин АН,Гурзуф'),
('Департамент финансов и кадров'),
('Пансионат Дельфин (Крым)'),
('Ледовая Арена Кристалл РД АИ'),
('Сколково'),
('Билайн. Ставрополь,ТПУ Томск'),
('РТИ'),
('ИТЭЛМА'),
('Билайн. Нижний Новгород,Итэлма АМО ЗИЛ'),
('Общественное пространство Норильск'),
('17110_2_TMK'),
('Открытие Спартаковская'),
('ВТБ Башня PM');

INSERT INTO employee (
    full_name,
    salary,
    position,
    department_type,
    department,
    hire_date,
    filial_address,
    project_info
)
VALUES
(
    'Суханова Арина Руслановна',
    103333.00,
    (SELECT id FROM position WHERE name_pos = 'ведущий QA инженер'),
    (SELECT id FROM department_type WHERE name_dep = 'Отдел'),
    (SELECT id FROM department WHERE name_deps = 'Центр компетенций QA Москва'),
    TO_TIMESTAMP(LPAD('200113', 6, '0') || ' 00:00:00', 'DDMMYY HH24:MI:SS'),
    (SELECT id FROM filial_addresses WHERE address = 'Приморский край, г. Владивосток, ул Нижнепортовая, д. 1'),
    (SELECT id FROM projects WHERE name_of_project = 'Итэлма Инженерный корпус')
),
(
    'Баранов Георгий Александрович',
    12130.00,
    (SELECT id FROM position WHERE name_pos = 'специалист'),
    (SELECT id FROM department_type WHERE name_dep = 'Группа'),
    (SELECT id FROM department WHERE name_deps = 'Группа сервисной поддержки'),
    TO_TIMESTAMP(LPAD('31217', 6, '0') || ' 00:00:00', 'DDMMYY HH24:MI:SS'),
    (SELECT id FROM filial_addresses WHERE address = 'Краснодарский край, г. Краснодар, ул Путевая, д. 1'),
    (SELECT id FROM projects WHERE name_of_project = 'Севастополь ТВ')
),
(
    'Вишневская Виктория Матвеевна',
    12130.00,
    (SELECT id FROM position WHERE name_pos = 'специалист по персоналу'),
    (SELECT id FROM department_type WHERE name_dep = 'Группа'),
    (SELECT id FROM department WHERE name_deps = 'Группа сервисной поддержки'),
    TO_TIMESTAMP(LPAD('171117', 6, '0') || ' 00:00:00', 'DDMMYY HH24:MI:SS'),
    (SELECT id FROM filial_addresses WHERE address = 'Краснодарский край, г. Краснодар, ул Путевая, д. 1'),
    (SELECT id FROM projects WHERE name_of_project = 'Кристалл Доп объем')
),
(
    'Алексеев Константин Николаевич',
    12366.00,
    (SELECT id FROM position WHERE name_pos = 'специалист по персоналу'),
    (SELECT id FROM department_type WHERE name_dep = 'Группа'),
    (SELECT id FROM department WHERE name_deps = 'Группа сервисной поддержки'),
    TO_TIMESTAMP(LPAD('230620', 6, '0') || ' 00:00:00', 'DDMMYY HH24:MI:SS'),
    (SELECT id FROM filial_addresses WHERE address = 'Ростовская обл, г. Ростов-на-Дону, ул 2-я Краснодарская, д. 135/2'),
    (SELECT id FROM projects WHERE name_of_project = 'Ростелеком. Гончарная,ВТБ Башня PM')
),
(
    'Лаптев Владислав Даниилович',
    71000.00,
    (SELECT id FROM position WHERE name_pos = 'ведущий разработчик'),
    (SELECT id FROM department_type WHERE name_dep = 'Отдел'),
    (SELECT id FROM department WHERE name_deps = 'Центр разработки продуктов для digital-маркетинга'),
    TO_TIMESTAMP(LPAD('220616', 6, '0') || ' 00:00:00', 'DDMMYY HH24:MI:SS'),
    (SELECT id FROM filial_addresses WHERE address = 'Ростовская обл, г. Ростов-на-Дону, ул 2-я Краснодарская, д. 135/2'),
    (SELECT id FROM projects WHERE name_of_project = 'Газпромбанк Бирюзова')
),
(
    'Коновалов Даниил Матвеевич',
    62000.00,
    (SELECT id FROM position WHERE name_pos = 'ведущий разработчик'),
    (SELECT id FROM department_type WHERE name_dep = 'Отдел'),
    (SELECT id FROM department WHERE name_deps = 'Центр разработки продуктов для digital-маркетинга'),
    TO_TIMESTAMP(LPAD('261113', 6, '0') || ' 00:00:00', 'DDMMYY HH24:MI:SS'),
    (SELECT id FROM filial_addresses WHERE address = 'Краснодарский край, г. Краснодар, ул Путевая, д. 1'),
    (SELECT id FROM projects WHERE name_of_project = 'Гпб Оазис Кабинет З.')
);

![Диаграмма](https://github.com/tapilin34/12-01-hw/blob/main/img/diagram.jpg)