## Зміст

1. [Вступ-до-SQL](#Вступ-до-SQL)
2. [Створення БД](#Створення-БД)
3. [Перші запити](#Перші-запити)
4. [Типи даних](#Типи-даних)
5. [Підготовка DB `world` до практики](#Підготовка-DB-`world`-до-практики)

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

123
