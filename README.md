# Домашнее задание: SQL. Часть 2
**Студент:** Захарян Николай Артурович

---

## Задание 1. Настройка пользователя и восстановление базы Sakila


**Скриншоты:**
<img width="809" height="618" alt="2026-10-23_13-57-49" src="https://github.com/user-attachments/assets/a59d5e74-8e27-4796-93ee-96ec65f53c22" />
<img width="525" height="382" alt="2026-10-23_14-05-13" src="https://github.com/user-attachments/assets/de39f9b1-5196-4efb-b15b-f95b05327f6f" />
<img width="803" height="449" alt="2026-10-23_14-18-17" src="https://github.com/user-attachments/assets/37411da4-a609-4a05-aaf0-00cabc05a5b4" />
<img width="806" height="622" alt="2026-10-23_14-19-53" src="https://github.com/user-attachments/assets/6b65a34e-15a1-46b0-84ef-83fad219f023" />
<img width="803" height="250" alt="2026-10-23_14-19-05" src="https://github.com/user-attachments/assets/52f1d7d5-307f-442b-8439-c021fd45d190" />

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

