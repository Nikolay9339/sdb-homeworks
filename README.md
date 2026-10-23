# Домашнее задание: Базы данных MySQL и SQL-запросы
**Студент:** Захарян Николай Артурович

---

## Задание 1. Настройка пользователя и восстановление базы Sakila
*(Сюда вставьте скриншоты из Задания 1.3, 1.5 и 1.8, как показано ниже)*

**Скриншот списка пользователей (1.3):**
![Список пользователей](screenshots/1-3-users.png)

**Скриншот прав пользователя sys_temp (1.5):**
![Права sys_temp](screenshots/1-5-grants.png)

**Скриншот списка таблиц базы sakila (1.8):**
![Таблицы sakila](screenshots/1-8-tables.png)

---

## Задание 2. Таблица первичных ключей
| Название таблицы | Название первичного ключа |
|------------------|---------------------------|
| actor            | actor_id                  |
| address          | address_id                |
| category         | category_id               |
| city             | city_id                   |
| country          | country_id                |
| customer         | customer_id               |
| film             | film_id                   |
| film_actor       | actor_id, film_id         |
| film_category    | film_id, category_id      |
| film_text        | film_id                   |
| inventory        | inventory_id              |
| language         | language_id               |
| payment          | payment_id                |
| rental           | rental_id                 |
| staff            | staff_id                  |
| store            | store_id                  |

---

## Задание 3. Базовые SQL-запросы

### 1. Уникальные районы (начинаются на K, заканчиваются на a, без пробелов)
```sql
SELECT DISTINCT district
FROM address
WHERE district LIKE 'K%a' 
  AND district NOT LIKE '% %';
---

<img width="809" height="618" alt="2026-10-23_13-57-49" src="https://github.com/user-attachments/assets/7c0f2c00-c750-4710-8766-ecb04a03e874" />
<img width="525" height="382" alt="2026-10-23_14-05-13" src="https://github.com/user-attachments/assets/36ec0ce5-0d44-4133-8f9f-41f799dab7b8" />
<img width="803" height="449" alt="2026-10-23_14-18-17" src="https://github.com/user-attachments/assets/9361f5fc-eae2-46d9-b7ac-b9e32064a171" />
<img width="806" height="622" alt="2026-10-23_14-19-53" src="https://github.com/user-attachments/assets/6562a7c4-19c2-4739-aba0-11bc59a32062" />
<img width="803" height="250" alt="2026-10-23_14-19-05" src="https://github.com/user-attachments/assets/dc7bf987-cb99-4675-8ce2-e968818b4ebc" />
