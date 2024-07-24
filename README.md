## Зміст

1. [Вступ-до-SQL](#Вступ-до-SQL)
2. [Створення БД](#Створення-БД)
3. [Перші запити](#Перші-запити)
4. [Типи даних](#Типи-даних)
5. [Підготовка DB `world` до практики](#Підготовка-DB-world-до-практики)
6. [Знайомство з запитом SELECT](#Знайомство-з-запитом-SELECT)
7. [DISTINCT, LIMIT, OFFSET](#DISTINCT,-LIMIT,-OFFSET)
8. [Сортування даних ORDER BY](#Сортування-даних-ORDER-BY)
9. [Фільтрування даних WHERE](#Фільтрування-даних-WHERE)
10. [Оператор LIKE](#Оператор-LIKEE)
11. [Обчислення полів та Аліаси](#Обчислення-полів-та-Аліаси)
12. [Функції в MySQL](#Функції-в-MySQL)
13. [Агрегатні функції в MySQL](#Агрегатні-функції-в-MySQL)

## Вступ до SQL

1. **База даних** — це організована колекція даних, яка зберігається та управляється за допомогою спеціального програмного забезпечення, відомого як система управління базами даних (СУБД). Основна ідея полягає в тому, щоб зберігати дані в структурованому форматі, який легко оновлювати, доступати та обробляти. В базі даних можуть зберігатися різноманітні типи інформації, від тексту до зображень і числових значень.

2. **СУБД (система управління базами даних)** — це програмне забезпечення, яке дозволяє створювати, управляти та використовувати бази даних. Основна функція СУБД полягає в забезпеченні ефективного доступу до даних, забезпеченні цілісності даних та можливості виконання різних операцій з ними, таких як додавання, видалення, модифікація та пошук. Деякі з найпопулярніших СУБД включають `MySQL, PostgreSQL, Microsoft SQL Server, Oracle Database та SQLite`.

> СУБД можна класифікувати за декількома категоріями залежно від різних критеріїв. Ось деякі основні категорії СУБД:

- **За моделлю даних**:

  - **Реляційні СУБД**: Дані організовані у вигляді таблиць з реляціями між ними. Приклади: MySQL, PostgreSQL, Microsoft SQL Server.
  - **Нереляційні (NoSQL) СУБД**: Вони використовують різні моделі даних, такі як ключ-значення, документи, колонкові сховища тощо. Приклади: MongoDB (документоорієнтована), Redis (ключ-значення), Cassandra (колонкова).

- **За типом доступу**:

  - **Онлайн-транзакційні СУБД (OLTP)**: Орієнтовані на швидкий інтерактивний доступ до даних для обробки транзакцій. Це типово для банківських систем, інтернет-магазинів тощо.
  - **Онлайн-аналітичні СУБД (OLAP)**: Призначені для обробки великих обсягів даних і підтримки аналітичних операцій, зазвичай здійснюються запити для звітності та аналізу.

- **За режимом розгортання**:

  - **Локальні СУБД**: Встановлені та запущені безпосередньо на одному комп'ютері чи сервері.
  - **Розподілені СУБД**: Системи, що працюють на різних вузлах мережі, дозволяють розподілену обробку даних та високу доступність.

3. **Первинний ключ (Primary Key)** — це унікальне значення у вигляді одного чи декількох полів (стовпців) в таблиці бази даних, яке однозначно ідентифікує кожен рядок цієї таблиці. Основна вимога до первинного ключа — він повинен бути унікальним для кожного запису в таблиці, тобто не може повторюватися для інших записів.
   Основні властивості первинного ключа:

- **Унікальність:** Кожне значення в полі первинного ключа повинно бути унікальним у межах таблиці.
- **Необхідність:** Кожен рядок таблиці повинен мати значення первинного ключа (це може бути одне або декілька полів, які утворюють складений первинний ключ).
- **Ідентифікація:** Використовується для однозначної ідентифікації кожного рядка в таблиці.

4. **SQL (Structured Query Language)** — це мова програмування, яка використовується для управління і маніпулювання реляційними базами даних. Основні функції SQL включають:

## Створення БД

1. Створити БД можна:

   - В ручну: [приклад](https://i.imgur.com/5QNcBst.png)
   - так і командою:

   ```sql
       CREATE DATBASE `<db_name>`;
   ```

2. Після створення БД, ми можемо створити таблицю. Таблицю, ми можемо так само створити в ручну, або командою

   - В ручну: [приклад](https://i.imgur.com/CM5OF6t.png)
   - Командою:

   ```sql
       CREATE TABLE test(
           `id` AUTO_INCREMENT PRIMARY KEY,
           `name` VARCHAR(50) NOT NULL,
           `age` TINYINT NOT NULL UNSIGNED,
           `phone` TINYINT(20) NOT NULL,
           `email` VARCHAR(50) NOT NULL UNIQUE
       );
   ```

   2.1. Іменування полів.

   - Ми можеме іменувати поля, зарезервованими назвами, проте наша СУДБ може нас про це попередити. Тому, краще так **не робити**

3. У SQL існує кілька основних типів даних, які можна використовувати для визначення структури таблиць і обробки даних. Ось деякі з них:

   - **Цілі числа (Integer)**: Використовується для зберігання цілих чисел без десяткової частини. Наприклад, `INT`, `INTEGER`, `SMALLINT`, `BIGINT`.

   - **Числа з плаваючою точкою (Floating Point)**: Використовується для зберігання чисел з десятковою частиною. Наприклад, `FLOAT`, `DOUBLE`, `REAL`, `DECIMAL`.

   - **Рядки (Strings)**: Використовуються для зберігання текстових даних. Наприклад, `CHAR`, `VARCHAR`, `TEXT`.

   - **Дата і час (Date and Time)**: Використовується для зберігання дати, часу або комбінацій їх. Наприклад, `DATE`, `TIME`, `DATETIME`, `TIMESTAMP`.

   - **Булевий тип (Boolean)**: Використовується для зберігання значень true або false. Наприклад, `BOOLEAN`, `BOOL`.

   - **Бінарні дані (Binary)**: Використовується для зберігання бінарних об'єктів, таких як зображення або документи. Наприклад, `BLOB`, `BYTEA`.

   - **Інші спеціалізовані типи**: Включають типи для зберігання IP-адрес, UUID (унікальні ідентифікатори) та інших специфічних даних.

4. Атрибут `UNSIGNED` в SQL використовується для числових типів даних і вказує на те, що колонка **_не може містити від'ємні значення_**. Він дозволяє використовувати всі доступні біти для зберігання значень не займаючи їх половину

   - Наприклад: TINYINT в MySQL:

     - Знаковий TINYINT: від -128 до 127.
     - Беззнаковий TINYINT: від 0 до 255.

5. Атрибут `UNIQUE` в SQL використовується для визначення унікальності значень в стовпці або групі стовпців у таблиці. Ось ключові моменти, які характеризують атрибут `UNIQUE`:

   - **Унікальність значень**: Коли на стовпець накладається обмеження `UNIQUE`, значення в цьому стовпці повинні бути унікальними для кожного рядка в таблиці. Це означає, що в таблиці не може бути двох рядків з однаковими значеннями в цьому стовпці (або групі стовпців, якщо обмеження `UNIQUE` застосоване до більше, ніж одного стовпця).

   - **Призначення**: Атрибут `UNIQUE` часто використовується для створення унікальних ключів або індексів у таблиці, що дозволяє ефективно шукати та обробляти дані за умови, що значення унікальні.

## Перші запити

1. Створення бази даних -
   ```mysql
        CREATE DATABASE [IF NOT EXISTS] `<db_name>`
   ```
   - `IF NOT EXISTS` - цей параметр є опціональним, тобто не обовязкововим, але він нам може допомогти створити базу якщо такої ще не існує
2. Створення таблиці -

   ```mysql
      CREATE DATABASE IF NOT EXISTS `mysql.go`;

      USE `mysql.go`;

      CREATE TABLE `users`(
         `id` INT UNSIGNED AUTO_INCREMENT PRIMARY KEY ,
         `name` VARCHAR(50) NOT NULL,
         `age` TINYINT(20) UNSIGNED NOT NULL ,
         `phone` VARCHAR(20) NOT NULL,
         `email` VARCHAR(20) NOT NULL
      );
   ```

   - В нас тут відбувається створення таблиці в базі. Але ми використовуємо ключове слово `USE` щоб показити, в які базі вона буде створен. А взагалі, це робиться заради того, щоб командою дати зрозуміти, до якої бази буде належати таблиця, бо може бути так, що ми попросту до неї доступу не будемо мати

   - Ну і потім базово наповнюємо таблицю

   - З наповненням наче все зрозуміло, тільки нагадаю що опція `UNSIGNED` - вказує на те, що значення поля, не можу бути відємним, там самим ми розширюємо кількість позитивних даних. Тобто:
     - Знаковий TINYINT: від -128 до 127.
     - Беззнаковий TINYINT: від 0 до 255.
   - ТУТ ЩЕ ПРИКОЛ З ТИМ, ДЕ САМЕ МАЄ РОЗТАШОВУВАТИСЬ КЛЮЧОВЕ СЛОВО `UNSIGNED`
   -

3. Перейменування таблиці:

   ```mysql
      RENAME TABLE `<old_name> TO `<new_name>`;
   ```

4. Очищення даних в таблиці:

   ```mysql
      TRUNCATE TABLE `<table_name>`;
   ```

5. Видалення таблиці:
   ```mysql
      DROP TABLE `<table_name>`;
   ```
6. Видалення бази даних:
   ```mysql
      DROP DATABASE `<table_name>`;
   ```

## Типи даних

В SQL існує кілька основних типів даних, які використовуються для зберігання різних видів інформації. Кожен тип даних має свій діапазон значень та займає певну кількість місця в пам'яті. Нижче наведені основні типи даних з їх діапазонами та розмірами в пам'яті.

### Числові типи даних

1. **TINYINT**

   - **Діапазон**:
     - Знакований: від -128 до 127
     - Беззнаковий: від 0 до 255
   - **Розмір в пам'яті**: 1 байт

2. **SMALLINT**

   - **Діапазон**:
     - Знакований: від -32,768 до 32,767
     - Беззнаковий: від 0 до 65,535
   - **Розмір в пам'яті**: 2 байти

3. **MEDIUMINT**

   - **Діапазон**:
     - Знакований: від -8,388,608 до 8,388,607
     - Беззнаковий: від 0 до 16,777,215
   - **Розмір в пам'яті**: 3 байти

4. **INT (INTEGER)**

   - **Діапазон**:
     - Знакований: від -2,147,483,648 до 2,147,483,647
     - Беззнаковий: від 0 до 4,294,967,295
   - **Розмір в пам'яті**: 4 байти

5. **BIGINT**

   - **Діапазон**:
     - Знакований: від -9,223,372,036,854,775,808 до 9,223,372,036,854,775,807
     - Беззнаковий: від 0 до 18,446,744,073,709,551,615
   - **Розмір в пам'яті**: 8 байтів

6. **FLOAT**

   - **Діапазон**: Приблизно від -3.4E+38 до 3.4E+38
   - **Розмір в пам'яті**: 4 байти

7. **DOUBLE**

   - **Діапазон**: Приблизно від -1.7E+308 до 1.7E+308
   - **Розмір в пам'яті**: 8 байтів

8. **DECIMAL (NUMERIC)**

   - **Діапазон**: Залежить від заданої точності і масштабу
   - **Розмір в пам'яті**: Залежить від точності (кількості цифр)

   - При створення поля з типом даних DECIMAL, слід передати два аргемента
     - Перший відповідає за те, скільки всього буде чисел, враховуючи і ті які після коми. Тобто, якщо це буде число `26000,55` - ми маємо вказати, що буде `7-цифр`
     - Другий за кількість знаків після
       [Приклад в PMA](https://i.imgur.com/BZQeZyY.png)
     ```mysql
       CREATE TABLE `users`(
        `id` INT UNSIGNED AUTO_INCREMENT PRIMARY KEY ,
        `name` VARCHAR(50) NOT NULL,
        `age` TINYINT(20) UNSIGNED NOT NULL ,
        `phone` VARCHAR(20) NOT NULL,
        `email` VARCHAR(20) NOT NULL,
        `salary` DECIMAL(5,2) UNSIGNED NOT NULL
     );
     ```

### Текстові типи даних

> В памяті буде завжди займати на 1-н байт більше, через те що, система його використовує на запис ДОВЖИНИ кількості даних в полі. Тобто, якщо поле буде песте, його місце в памяті, буде займати 1байт, а якщо в нас буде поле "привіт" - воно займе 7байтів

1. **CHAR(n)** - це тип фіксованої довжини. Тобто, якщо ми вкажемо, що його довжина 20-символів, то якщо ми запишемо навіть 1-н символ, буде все одно визначено 20байтів

   - **Діапазон**: До 255 символів
   - **Розмір в пам'яті**: Рівно n байтів

2. **VARCHAR(n)** - це тип, на відміну від `CHAR` гнучкий, буде використовувати стільки байтів, якільки символів буде записано

   - **Діапазон**: До 65,535 символів
   - **Розмір в пам'яті**: Розмір фактичних даних плюс 1 або 2 байти для зберігання довжини

3. **TEXT**

   - **Діапазон**: До 65,535 символів
   - **Розмір в пам'яті**: Розмір фактичних даних плюс 2 байти

4. **MEDIUMTEXT**

   - **Діапазон**: До 16,777,215 символів
   - **Розмір в пам'яті**: Розмір фактичних даних плюс 3 байти

5. **LONGTEXT**
   - **Діапазон**: До 4,294,967,295 символів
   - **Розмір в пам'яті**: Розмір фактичних даних плюс 4 байти

### Дата і час

1. **DATE**

   - **Діапазон**: Від '1000-01-01' до '9999-12-31'
   - **Розмір в пам'яті**: 3 байти

2. **TIME**

   - **Діапазон**: Від '-838:59:59' до '838:59:59'
   - **Розмір в пам'яті**: 3 байти

3. **DATETIME** - це повна дата у форматі `"0000-00-00 00:00:00"` - рік-місяць-день години-хвилини-секунди (займає `8-байт`, та дозволяє зберігати дану Від `'1000-01-01 00:00:00' до '9999-12-31 23:59:59'`)

   - **Діапазон**: Від '1000-01-01 00:00:00' до '9999-12-31 23:59:59'
   - **Розмір в пам'яті**: 8 байтів

4. **TIMESTAMP** - так само як і `DATETIME`, а у іншому форматі зберігання (займає `4-байт`, та дозволяє зберігати дану Від `'1970-01-01 00:00:01' до '2038-01-19 03:14:07'`)

   - **Діапазон**: Від '1970-01-01 00:00:01' до '2038-01-19 03:14:07'
   - **Розмір в пам'яті**: 4 байти

5. **YEAR**
   - **Діапазон**: Від 1901 до 2155
   - **Розмір в пам'яті**: 1 байт

#### Порівняємо DATETIME та TIMESTAMP

- Перша відмінність, це те, що TIMESTAMP, займає менше місця в памяті
- Для `TIMESTAMP`, можна обрати таку опцію як CURRENT_TIMESTAMP
  - `CURRENT_TIMESTAMP` - повертає поточну дату і час в момент виконання запиту `YYYY-MM-DD HH:MM:SS`
  - Для `TIMESTAMP` відразу можемо побачити, що буде додано поле, з датою створення запису [приклад](https://i.imgur.com/qT6ZYEF.png)

### Бінарні дані

> Бінарні дані — це дані, які зберігаються в тому вигляді, в якому вони представлені у комп'ютерній пам'яті, тобто у вигляді послідовності байтів. Вони можуть включати будь-які дані, які не є текстовими, наприклад, зображення, аудіо, відео, файли, шифровані дані, та інші форми неструктурованих або напівструктурованих даних.

1. **BINARY(n)**

   - **Діапазон**: До 255 байтів
   - **Розмір в пам'яті**: Рівно n байтів

2. **VARBINARY(n)**

   - **Діапазон**: До 65,535 байтів
   - **Розмір в пам'яті**: Розмір фактичних даних плюс 1 або 2 байти для зберігання довжини

3. **BLOB**

   - **Діапазон**: До 65,535 байтів
   - **Розмір в пам'яті**: Розмір фактичних даних плюс 2 байти

4. **MEDIUMBLOB**

   - **Діапазон**: До 16,777,215 байтів
   - **Розмір в пам'яті**: Розмір фактичних даних плюс 3 байти

5. **LONGBLOB**
   - **Діапазон**: До 4,294,967,295 байтів
   - **Розмір в пам'яті**: Розмір фактичних даних плюс 4 байти

### Використання `ENUM`

1. **Фіксовані списки варіантів**:

   - `ENUM` корисний, коли потрібно зберігати одне значення з фіксованого набору варіантів. Наприклад, для зберігання статі, стану замовлення, категорій продукції тощо.

   ```sql
   CREATE TABLE employees (
       employee_id INT AUTO_INCREMENT PRIMARY KEY,
       name VARCHAR(50) NOT NULL,
       gender ENUM('male', 'female', 'other') NOT NULL
   );
   ```

   У цьому прикладі стовпець `gender` може приймати тільки одне з трьох значень: 'male', 'female' або 'other'.

2. **Забезпечення цілісності даних**:

   - Використання `ENUM` забезпечує, що значення в стовпці будуть обмежені певним набором. Це запобігає введенню некоректних або неочікуваних значень.

   ```sql
   CREATE TABLE orders (
       order_id INT AUTO_INCREMENT PRIMARY KEY,
       order_status ENUM('pending', 'processing', 'shipped', 'delivered', 'cancelled') NOT NULL
   );
   ```

   У цьому прикладі стовпець `order_status` гарантує, що стан замовлення буде одним з визначених значень, що допомагає підтримувати цілісність даних.

3. **Оптимізація зберігання**:

   - `ENUM` зберігає значення як цілі числа, що може бути більш ефективним з точки зору зберігання та продуктивності, порівняно зі зберіганням значень як рядки.

   ```sql
   CREATE TABLE products (
       product_id INT AUTO_INCREMENT PRIMARY KEY,
       product_name VARCHAR(100) NOT NULL,
       product_category ENUM('electronics', 'furniture', 'clothing', 'food') NOT NULL
   );
   ```

   У цьому прикладі стовпець `product_category` зберігає значення як цілі числа, що представляють позиції у списку, зменшуючи обсяг пам'яті, необхідний для зберігання.

### Приклад використання

#### Створення таблиці з `ENUM`

```sql
CREATE TABLE user_roles (
    user_id INT AUTO_INCREMENT PRIMARY KEY,
    username VARCHAR(50) NOT NULL,
    role ENUM('admin', 'editor', 'viewer') NOT NULL
);
```

#### Вставка даних

```sql
INSERT INTO user_roles (username, role) VALUES ('john_doe', 'admin');
INSERT INTO user_roles (username, role) VALUES ('jane_smith', 'editor');
INSERT INTO user_roles (username, role) VALUES ('alice_jones', 'viewer');
```

#### Вибірка даних

```sql
SELECT * FROM user_roles WHERE role = 'admin';
```

### Переваги використання `ENUM`

- **Забезпечення цілісності даних**: Запобігає введенню некоректних значень.
- **Зручність читання**: Полегшує розуміння коду і структури бази даних завдяки явним значенням.
- **Ефективність зберігання**: Зберігає значення як цілі числа, що може бути більш ефективним.

### Недоліки використання `ENUM`

- **Обмеження гнучкості**: Додавання або зміна значень у `ENUM` потребує змін в структурі таблиці.
- **Складність у масштабуванні**: Не підходить для випадків, коли набір значень може часто змінюватися або розширюватися.

## Підготовка DB `world` до практики

1. Посилання на БД `world` можна знайти за [world database](https://dev.mysql.com/doc/index-other.html)
2. Ну і потім її [імпотртуємо](https://i.imgur.com/0fJ0ylD.png) в нашу СУБД

   - Але я зіштовхнувся з проблемою в PMA імпорт не спрацював, але зробив його з `HeidiSQL`. [Як імпортувати через `HeidiSQL`](https://www.heidisql.com/help.php) ну і пошуком знаходити, по щось ні пошука ні навігації

3. Коли ми імпортуємо базу `world`, ми побачимо три таблички - `country, city, countryLanguage`
4. Якщо піти в таблику `country` ми зможемо звернути увагу, що там є колока `code` яка являється `первинним ключем (primary key)` проте, слід зазначити, що цей ключ, може бути не тільки типу `INT`, ай типу `CHAR`, або буть яким іншим, як цей є в табличці `country. [LOOK](https://i.imgur.com/7ejYmx0.png)
   - Колонка `code` відповідає коду країни, по чому ми і будемо ідентифікувати таблички `city` та `countryLanguage`
5. ` Зовнішній ключ (foreign key)` — це обмеження в базах даних, яке забезпечує зв'язок між двома таблицями. Він використовується для забезпечення цілісності посилань, гарантуючи, що значення в одному стовпці (або наборі стовпців) збігається зі значенням у стовпці (або наборі стовпців) іншої таблиці.
   - У випадку з базою `world` зовнішніми клюбчами буде поле `CountryCode` - саме цей код і буде звязувати нас з табличкою `country`, для таких табличок як `city` та `countryLanguage`. [foreign key](https://i.imgur.com/F3tRmiY.png)
6. Є ще таке поняття, як `implicit foreign key`(неявно заданий зовнішній ключ) - у нашому випкадку це буде колонка `capital` для таблички `country`[приклад](https://i.imgur.com/ITu5lTF.png) - тут ми можемо побачити, що всі записи числові. Але, якщо ми підемо в табличку `city` - то ми побачимо що цифра в колонки `capital` таблиці `country` відповідатиме колонці `name` таблички `city`. Якщо не зрозуміло, глянь `відео 6 - 9 хв`

   > Може виникнути питання, навіщо це. У нашому випадку з країнами, ми можемо зіштовхнутись з тим, що назва столиці, міста, може змиінитись, але її номер лишиться не змінним. Тому, нам немає сенсу, привязуватись до назви міста, а краще до кода, щоб потім отримати його актуальну назву, навіть якщо місто змінить назву

## Знайомство з запитом SELECT

1. `SELECT` - Команда, яка допоможде нам шукати конкретні стовпчики, з обраної таблиці

   ```mysql
      SLECT <список_стовпчиків> FROM <імя_таблиці>;
   ```

2. `` SELECT * FROM `country`; `` - ця команда допоможе витягнути всі дані з таблиці `country`

3. Використання оператора зірочка `*` який вказує на те, щоб відобразити ВСІ дані, є поганою практикою. Через те, що бази даних можуть бути досить великі і тим самим, створювати досить потужні навантаження на сервери. Тому такі запити з використанням `SELECT` краще обмежувати, а саме вказувати на конкретні колонки, за якими хочемо отримати дані

`` SELECT `name`, `region` FROM `country`; `` - [example](https://i.imgur.com/RW8acNC.png)

4. Коментування

[Приклади коментарів](https://i.imgur.com/loa274b.png)

## DISTINCT, LIMIT, OFFSET

5. `DISTINCT` - Вибірка унікальних записів. За допомогою функції

`` SELECT DISTINCT `continent` FROM `country`; `` - [example](https://i.imgur.com/Cik1Xtq.png)

6. `LIMIT` - Вказання лімітів кількості відображених записів

`` SELECT `name`, `continent` FROM `country` LIMIT 5; `` - [example](https://i.imgur.com/1yvQ3iE.png)

7. `OFFSET` - команда яка допоможе нам, пропустити попередньо відображену кількість записів. Це може бути корисним для пагінації

- `SELECT `name`, `continent`FROM`country` LIMIT 5;` - Такий запис нам відобразить кількість записів у розмірі 5шт. А от при пагінації, нам потрібно обрати наступні 5шт, або більше штук. Тут і допоможе `OFFSET`

- `` SELECT `name`, `continent` FROM `country` LIMIT 5 OFFSET 5; `` - [example](https://i.imgur.com/s8Zistp.png)

- `OFFSET` - має короткий запис `` SELECT `name`, `continent` FROM `country` LIMIT 5,5; `` - цей запис ідентичний `` SELECT `name`, `continent` FROM `country` LIMIT 5 OFFSET 5; ``

## Сортування даних ORDER BY

1. `ORDER BY` - команда, для того, щоб вказати СУБД по якому полю будемо сортувати дані

- `` SELECT `name`, `population` FROM `country` ORDER BY `population`; `` - в цьому сортуванні, сортування буде відбуватись від меншого до більшого. [example](https://i.imgur.com/9CBzhss.png)

- Якщо нам потрібно сортувати від **більшего до меншого**, слід використати ключове слово `desc` - ``SELECT`name`, `population`FROM`country`ORDER BY`population`desc;`
- Якщо нам потрібно сортувати від **меншого до більшего**, слід використати ключове слово `asc` - ``SELECT`name`, `population`FROM`country`ORDER BY`population`asc;`

2. Якщо нам потрібно провести сортування по двум колонкам. То спочатку, сортування пройде в першій колонці, а потім, дані в другій колонці будуть сортуватись в першої колонки. `` SELECT `region`, `population` FROM `country` ORDER BY `region`, `population`; ``[Краще на прикладі](https://i.imgur.com/cMMuKo8.png) - тут на прикладі чітко видно, що сортування відбулось в межаї регіону і вже там, сортувало по популяції

3. Для команди `ORDER BY` - ми можемо вказувати не конкретні назви полів, в яких хочемо сортувтаи дані, а й просто порядкові номери цих полів `` SELECT `region`, `population`, `localname` FROM `country` ORDER BY 1, 2; ``

4. Також сортування, можна задавати не відразу для всіх колонок, а для потрібних нам - [example](https://i.imgur.com/OHIpA68.png)

## Фільтрування даних WHERE

1. `WHERE` - оператор використовується для фільтрації записів, щоб обрати тільки ті, які відповідають певній умові. Він дозволяє звузити результати запиту, повертаючи лише ті рядки, які відповідають заданим критеріям.

- `` SELECT `name`, `population` FROM `country` WHERE `population` > 1000000000; `` - [приклад](https://i.imgur.com/Hirwtwp.png), який нам покаже країни де населення більше 1-лярда

- `` SELECT `name`, `population` FROM `country` WHERE `population` > 100000000 ORDER BY `population` DESC LIMIT 5 ; `` - тепер, ми можемо робити запити на багато складніші, щоб отримувати потрібні нам результати. [example](https://i.imgur.com/JgqD6PQ.png)

- `` SELECT `name`, `region` FROM `country` WHERE `region` != 'Middle East' ORDER BY `name`; `` - цим запитом, ми відфільтрумо та покажемо всі регіони окрім 'Middle East', та сортуємо дані по полю `name` у алфавітному порядку

- `` SELECT `name`, `population` FROM `country` WHERE `population` BETWEEN 100000000 AND 200000000 ORDER BY `population`; `` - тут ми застосували опереатор [`BETWEEN`](#8-Оператори-роботи-з-діапазонами) - який допомже нам, зробити пошук в діапазоні, між країнами які знаходяться в діапазоні населення між 100 та 200 млн

- `` SELECT `name`, `headofstate` FROM `country` WHERE `headofstate` = '' OR `headofstate` IS NULL; `` - це запит, знайомити нас з оператором [IS NULL](#6-Оператори-роботи-з-NULL-значеннями) та з оператором [обєднання умов OR](#3.- Логічні-оператори) - та результат, буде таким, що нам виведе країни, де `headofstate` буде або пусте поле, або рівний `NULL`

- `` SELECT `name`, `indepyear` FROM `country` WHERE `indepyear` IS NOT NULL; `` - а ця команда, навпаки, покаже країни, де рік незалежності `indepyear` не є `NULL`

- `` SELECT `region`, `name`, `population` FROM `country` WHERE `population` > 50000000 AND (`region` = 'Southeast Asia' OR `region` = 'Southern Europe') ORDER BY `population`; `` - тут вже запит більш складний, та використовує в собі як логічні оператори [AND, OR](#3-Логічні-оператори) так і оператори порівняння. Також, ми можемо звернути увагу, що в нас є умови, які мі заключаємо в круглі дужки. Круглі дуєки, дозволдять нам, обмежити діапазон умови перевірки логічних операторів. Або ж розтавити приоріт їх виконання

- `` SELECT `region`, `name`, `code`  FROM `country` WHERE `region` IN ('Southern Europe', 'Middle East') ORDER BY `region`; `` - тут ми використовуємо оператор [`IN`](#5-Оператори-роботи-з-множинами) який дозволяє нам, перевірити, наявність чогось в обраній колонці

- `` SELECT `region`, `name`, `code`, `population` FROM `country` WHERE `region` NOT IN ('Southern Europe', 'Middle East', 'Western Africa'); `` - запит з використанням [`NOT IN`](#5-Оператори-роботи-з-множинами) ідентичний запису [`IN`](#5-Оператори-роботи-з-множинами) - але результат його виокнання буде протилежний `IN`, тобто буде обирати всі записи ЗА ВИНЯТКОМ тих, які вказані в переліку

## Оператори в SQL

### 1 Арифметичні оператори

Використовуються для виконання математичних операцій над числовими значеннями.

- `+` (додавання)
- `-` (віднімання)
- `*` (множення)
- `/` (ділення)
- `%` (модуль)

```sql
SELECT price, price * 0.1 AS discount FROM products;
```

### 2 Порівняльні оператори

Використовуються для порівняння двох значень.

- `=` (дорівнює)
- `!=` або `<>` (не дорівнює)
- `>` (більше)
- `<` (менше)
- `>=` (більше або дорівнює)
- `<=` (менше або дорівнює)

```sql
SELECT * FROM employees WHERE salary > 50000;
```

### 3 Логічні оператори

Використовуються для об'єднання декількох умов у запитах.

- `AND` (і)
- `OR` (або)
- `NOT` (не)

```sql
SELECT * FROM employees WHERE department = 'IT' AND salary > 50000;
```

### 4 Оператори роботи з рядками

Використовуються для роботи з рядковими значеннями.

- `LIKE` (для пошуку з шаблоном)
- `NOT LIKE` (для виключення з шаблону)
- `||` або `+` (конкатенація рядків, залежить від СУБД)

```sql
SELECT * FROM customers WHERE first_name LIKE 'J%';
```

### 5 Оператори роботи з множинами

Використовуються для перевірки значень в списках або підзапитах.

- `IN` (перевірка наявності в списку)
- `NOT IN` (перевірка відсутності в списку)
- `EXISTS` (перевірка наявності підзапиту)
- `NOT EXISTS` (перевірка відсутності підзапиту)

```sql
SELECT * FROM employees WHERE department IN ('IT', 'HR', 'Sales');
```

### 6 Оператори роботи з NULL значеннями

Використовуються для роботи зі значеннями NULL.

- `IS NULL` (перевірка на NULL)
- `IS NOT NULL` (перевірка на не NULL)

```sql
SELECT * FROM employees WHERE manager_id IS NULL;
```

### 7 Оператори присвоєння

Використовуються для присвоєння значень змінним або колонкам.

- `=` (присвоєння значення)

```sql
UPDATE employees SET salary = salary * 1.1 WHERE department = 'IT';
```

### 8 Оператори роботи з діапазонами

Використовуються для перевірки значень у певному діапазоні.

- `BETWEEN` (перевірка діапазону)
- `NOT BETWEEN` (перевірка відсутності в діапазоні)

```sql
SELECT * FROM products WHERE price BETWEEN 50 AND 150;
```

### Приклади використання операторів

#### Поєднання операторів у складному запиті

```sql
SELECT * FROM employees
WHERE (department = 'IT' OR department = 'HR')
AND salary > 50000
AND hire_date BETWEEN '2020-01-01' AND '2023-12-31'
AND first_name LIKE 'J%'
AND manager_id IS NOT NULL;
```

## Оператор LIKE

1. LIKE - оператор, який використовується для пошуку. Це оператор, менш продуктивний ніж оператори, для точного пошуку. Тому якщо можна обійтись без нього, то краще закривати потреби, без цього оператора

1. **`%`** (відсоток): Заміщає нуль або більше символів.
1. **`_`** (підкреслення): Заміщає один символ.

### Приклади використання метасимволів

#### Використання метасимволу `%`

- **Пошук рядків, що починаються з певного символу або послідовності символів**:

  ```sql
  SELECT * FROM customers WHERE name LIKE 'J%';
  ```

  Вибирає всі записи, де ім'я починається з літери 'J'.

- **Пошук рядків, що закінчуються на певний символ або послідовність символів**:

  ```sql
  SELECT * FROM customers WHERE name LIKE '%son';
  ```

  Вибирає всі записи, де ім'я закінчується на 'son'.

- **Пошук рядків, що містять певну послідовність символів будь-де в рядку**:

  ```sql
  SELECT * FROM customers WHERE name LIKE '%ann%';
  ```

  Вибирає всі записи, де ім'я містить 'ann' у будь-якій позиції.

#### Використання метасимволу `_`

- **Пошук рядків, що мають конкретну кількість символів і певний символ на певній позиції**:

  ```sql
  SELECT * FROM products WHERE code LIKE 'A_ _ _';
  ```

  Вибирає всі записи, де код продукту складається з чотирьох символів і починається з 'A'. Кожне підкреслення `_` заміщає один символ.

### Комбінування метасимволів

- **Поєднання `%` та `_` для складніших шаблонів пошуку**:

  ```sql
  SELECT * FROM employees WHERE phone_number LIKE '123%45_';
  ```

  Вибирає всі записи, де номер телефону починається з '123', далі може йти будь-яка кількість символів, потім '45', а на останньому місці один будь-який символ.

### Уникайте символів `%` та `_`

Щоб шукати рядки, що буквально містять символи `%` або `_`, можна використовувати екранування символів за допомогою `ESCAPE`:

- **Приклад використання `ESCAPE`**:

  ```sql
  SELECT * FROM file_names WHERE name LIKE '%!%%' ESCAPE '!';
  ```

  Вибирає всі записи, де ім'я файлу містить символ `%`.

- `` SELECT `region`, `name`, `population` FROM `country` WHERE `region` LIKE '%Western%'; `` - цей простенький запит, з використанням оператора `LIKE` який дозволить здійснити пошук, по всім записам, де буде в назві регіону запис "Western"

- `` SELECT `code`, `region`, `name`, `population` FROM `country` WHERE `code` LIKE 'A__'; `` - використання цього запису, дозволить здійснити пошук по полям, які починаються на **"A"** і мають ще наступні 2 символи. [Краще на прикладі](https://i.imgur.com/nghmbjz.png)

- `` SELECT `code`, `region`, `name`, `population` FROM `country` WHERE `region` LIKE '%Asia' ORDER BY `region `` - запит, який буде шукати за допомогою оператора LIKE всі включення до слова **"%Asia"** при пошуку за колонкою **region**. [example](https://i.imgur.com/UtCJf4G.png)

- `` SELECT `code`, `name`, `population` FROM `country` WHERE `name` LIKE 'A%a' ORDER BY `region`; `` - простенький, але корисний запит, який дозволить пошук назв країн по полю `name` в діапазоні від "А" великої до "а" маленької. [example](https://i.imgur.com/F8PKT94.png)

## Обчислення полів та Аліаси

1. **Обчислювані поля** - створюються шляхом виконання арифметичних операцій або функцій над існуючими полями в таблиці. Це дозволяє обчислити значення на основі наявних даних безпосередньо в запиті. Обчислювані поля дозволяють проводити необхідні обчислення безпосередньо в запитах, а псевдоніми спрощують читання та управління результатами запитів. Тобто ми відразу, можемо виконувати певні опереції в базі, та повернути результати нам на в проект, застосунок, тощо.

- `` SELECT `name`, CONCAT((`population` / `surfacearea`), ' км²') AS density FROM `country` ORDER BY `density`; `` - тут гарний спосіб, продемонструвати те, як вирахувати площу, на душу населення, з використанням **Обчислюваних полів**, **Псевдонімів (Aliases)** [example](https://i.imgur.com/oDrq2Y4.png)

2. **Псевдоніми (Aliases)** - Псевдоніми використовуються для надання тимчасових імен колонкам або таблицям у запитах SQL. Вони допомагають зробити результати запиту більш зрозумілими та зручними для використання.

`` SELECT CONCAT(`continent`, ', ', `region`, ', ', `name`) AS `adress` FROM `country` LIMIT 10; `` - цей запит в нас використовує як обчислення полів, так і використання аліасу. А саме, ми обєднуємо інформацію з трьох стовпчиків в один рядок, та повертаємо його під псевдонімом `adress` - [example](https://i.imgur.com/g2ElkrP.png)

- Також псевдоніми, можна використовувати і без ключового слова `AS` - SELECT CONCAT_WS(', ', `continent`, `region`, `name`) AS `adress` FROM `country` LIMIT 10;

## Функції в MySQL

1. За цим [посиланням](https://dev.mysql.com/doc/refman/8.4/en/built-in-function-reference.html) можна отриамти інфомрацію по всім існуючим функціям в MySQL
2. `CONCAT_WS` - функція, яка допоможе обєднати строки, по певному сепаратору - `` SELECT CONCAT_WS(', ', `continent`, `region`, `name`) AS `adress` FROM `country` LIMIT 10; `` [example](https://i.imgur.com/oLa4bgZ.png)
3. `FORMAT` - функція, яка приймає три аргументи (число, кількість цифр після коми, та локаль) `` SELECT `name`, `population`, CONCAT(FORMAT(`population` / `surfacearea`, 2), ' км²') AS density FROM `country` WHERE `population` > 10000000 ORDER BY `population` DESC LIMIT 10; `` [example](https://i.imgur.com/1ggq4sa.png)

4. `LCASE`, `LOWER` - ідентичні функції, яки приводять строку до нижнього регістру `` SELECT LCASE(CONCAT_WS(', ', `continent`, `region`, `name`)) AS `adress` FROM `country` LIMIT 10; `` [example](https://i.imgur.com/PbwyCk6.png)
5. `UCASE` - приводять строку до верхнього регістру `` SELECT UCASE(CONCAT_WS(', ', `continent`, `region`, `name`)) AS `adress` FROM `country` LIMIT 10; `` [example](https://i.imgur.com/Mopbmzn.png)
6. `TRIM`, `LTRIM`, `RTRIM` - обрізає пробільні символи **TRIM** з кожного з боків, **LTRIN, RTRIM** - з лівого, та правого `` SELECT TRIM(`name`) AS `name` FROM `country` LIMIT 1; ``
7. `CEIL` - округляє число в більше сторону `` SELECT `name`, `population`, CONCAT(FORMAT(`population` / `surfacearea`, 2), ' км²') AS density, CONCAT(CEIL(FORMAT(`population` / `surfacearea`, 2)), ' км²') AS density_ceil FROM `country` WHERE `population` > 10000000 ORDER BY `population` DESC LIMIT 10; `` - [example](https://i.imgur.com/W3i8bxh.png)
8. `FLOOR` - протилежна функція, функції **CEIL**, тобто округлює в меншу сторону
9. `ROUND` - робити округлення, за правилами математики [example](https://i.imgur.com/L5QBxCb.png)
10. `NOW` - Для отримання поточного дати і часу `` SELECT CONCAT('Зараз: ', NOW()) AS `date_now` FROM `country` LIMIT `` [example](https://i.imgur.com/VrU0z3N.png)
11. `DATE_FORMAT` - допоможе нам встановити потрібний форматат, дати та часу, в незалежності від локалі `` SELECT CONCAT('Зараз: ', DATE_FORMAT(NOW(), '%d-%m-%Y')) AS `date_now` FROM `country` LIMIT 1; `` [example](https://i.imgur.com/pKLJLUX.png)

> ЦЕ лише маленька части на функцій, їх на багато більше, тому все буде з досвідом...

## Агрегатні функції в MySQL

Агрегатні функції у SQL виконують різні задачі для обробки та аналізу даних. Вони застосовуються до набору значень **(колонки або рядків)** і повертають єдине значення. Агрегатні функції дуже корисні для обчислення підсумкових даних, таких як суми, середні значення, максимальні та мінімальні значення тощо.

Ось основні агрегатні функції і задачі, які вони виконують:

1. **COUNT()**

   - **Задача:** Підраховує кількість рядків у наборі результатів.
   - **Приклад використання:**
     ```sql
     SELECT COUNT(*) FROM employees;
     ```

   > Тут є певна різниця з використанням оператора "\*", та з указанням конкретного поля
   >
   > "\*" - порахує всі рядки і видасть результат
   > 'поле' - воно буде рахувати всі рядки, які не пусті, або НЕ NULL

   `` SELECT COUNT(*) AS `with_asterisk`, COUNT(`lifeexpectancy`) AS with_row FROM `country`; `` [example](https://i.imgur.com/vBLVFsE.png)

2. **SUM()**

   - **Задача:** Обчислює суму значень у колонці.
   - **Приклад використання:**

     ```sql
     SELECT SUM(salary) FROM employees;
     ```

     `` SELECT SUM(`population`) AS `sum_of_population` FROM `country` `` - [example](https://i.imgur.com/aX8DfOX.png)

     - Також на цьмоу прикладі, ми зможемо побачити, яку проблему вирішують агрегатні функції. [example](https://i.imgur.com/1MzUrcO.png) - тут якщо ми отримаємо через SQL запит інфомрацію, про замовелння з `order_id = 1`, ми побачимо замовлення, в якому є три товари і кожен товар, має свою вартість, у вигляді `` `(`quantity` * `price`) AS `products_total_amount` `` - і далі звісно в ручну, суму кожного товару рахувати буде не зручно
     - Вирішенням цієї проблеми, буде використання функції `SUM` - яка буде рахувати суму всіз значень в обраній колонці - [example](https://i.imgur.com/h3Y4doI.png)

3. **AVG()**

   - **Задача:** Обчислює середнє значення у колонці.
   - **Приклад використання:**
     ```sql
     SELECT AVG(salary) FROM employees;
     ```
   - Досить просто функція, яка дбуде виводити середнє значення по колонці: `` SELECT AVG(`population`) AS `AVG` FROM `country`; `` [example](https://i.imgur.com/9py51h2.png)

4. **MAX()**

   - **Задача:** Знаходить максимальне значення у колонці.
   - **Приклад використання:**
     ```sql
     SELECT MAX(salary) FROM employees;
     ```

5. **MIN()**

   - **Задача:** Знаходить мінімальне значення у колонці.
   - **Приклад використання:**

     ```sql
     SELECT MIN(salary) FROM employees;
     ```

     > слід враховувати такий нюанс, що немає сенсу, перед застосуванням агрегатної функції, використовувати вивід якихосб полів. Через те що, нам просто поверне перші значення з таблиці, ну і результат виконання самої агрегатної функції. Щоб нам отримати потрібний результат пошуку, от наприклад як у прикладі `` SELECT `name`, `price` FROM `oc_order_product` WHERE `price` = (SELECT MAX(`price`) FROM `oc_order_product`) LIMIT 1; `` - що дозволить нам отримати назву товару, який у таблиці має найбільше ціну. Тут виходить так, що ми робимо запит в якому будемо виводити потрібні нам поля. А там де буде перевірка WHERE ми робимо ще один запит, щоб отримати результат для агрегатної функції. [example](https://i.imgur.com/zwFGgdm.png)

     > Або ж такий, дуже очевидний та простий спосіб `` SELECT `name`, `price` FROM `oc_order_product` ORDER BY `price` DESC LIMIT 1; `` - [example](https://i.imgur.com/eJa0FRy.png)

     > Якщо говорити за застосування функцій MIN та MAX, для текстових значень, то дані будуть виводитись у алфавітному порядку

6. **GROUP_CONCAT()** (доступна в MySQL)

   - **Задача:** Об'єднує значення з кількох рядків у одну строку.
   - **Приклад використання:**
     ```sql
     SELECT GROUP_CONCAT(name) FROM employees;
     ```

   > Слід зазначити, що ці всі агрегатні функції, можна комбінувати без проблем, тобто, відразу всі їх вивести - `` SELECT MIN(`population`), MAX(`population`), AVG(`population`), SUM(`population`), COUNT(*) FROM `country`; `` - [example](https://i.imgur.com/vadf03x.png)
