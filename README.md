# SQLDojo

> # `Relational Database`
> คือ database แบบที่มีความสัมพันธ์
>
> __คุณสมบัติ__
> - แต่ละ Table จะมีหรือไม่มี Primary Key(Unique key)ก็ได้ ถ้ามี Primary Key ข้อมูลจะไม่มีทางซ้ำกัน (`Primary Key จะไม่ซ้ำกัน`)
> - field ใน Table เรียกว่า column
>


> # `SQLite`
> คือ Relational Database ที่อยู่บนเครื่องเรา (Local Database)

> # `SQL`
> คือ programming language ที่ใช้ในการจัดการกับ Relational Database เช่น
> - insert
> - delete
> - update
> - query
>
> ## *`SELECT`*
> => เป็น command ที่เอาไว้เรียกแสดงผล data
> ```
> SELECT "ชื่อfield(column)" FROM "ชื่อTable";
>
> SELECT * FROM customers;
>
> SELECT FirstName,LastName FROM customers;
>```
> `Note :` `* `  คือทุก field (column)
>
> `Note :` ชื่อ field (column) lower case, upper case ไม่มีผลใส่ได้หมด
> ## *`AS`*
> => เป็น command ที่เอาไว้กำหนดชื่อ field (column) ที่เราอยากให้แสดงออกมาโดยไม่ได้ใช้ชื่อ field เดิม
> ```
> SELECT 
>	FirstName AS customer_firstName,
>	LastName AS customer_lastName
>FROM customers;
> ```
> `Note : ` 
> - ต้องการให้ field FirstName แสดงออกมาเป็น customer_firstName
> - ต้องการให้ field LastName แสดงออกมาเป็น customer_lastName
> ## *`WHERE`*
> => เป็น command เอาไว้ query โดยใส่เงื่อนไขของการ query ที่เราต้องการลงไป เพื่อดึง data เฉพาะที่เราต้องการ
> ```
> SELECT * FROM customers
> WHERE CustomerId = 8;
>
> SELECT * FROM customers
> WHERE Country = 'Canada'
> AND State = 'ON';
>
> SELECT * FROM customers
> WHERE Country = 'Canada'
> OR Country = 'USA';
> ```
> `Note : ` สามารถใช้ logic  _`AND`_,_`OR`_ ได้
> ## *`ORDER BY`*
> => เป็น command ที่เอาไว้เรียง data ตามเงื่อนไข
> ```
> SELECT * FROM customers
> WHERE Country = 'Canada'
> ORDER BY "ชื่อfieldที่ต้องการจะใช้เป็นเงื่อนไขในการเรียง";
>
> defalut น้อย => มาก
> SELECT * FROM customers
> WHERE Country = 'Canada'
> ORDER BY FirstName;
>
> มาก => น้อย
> SELECT * FROM customers
> WHERE Country = 'Canada'
> ORDER BY FirstName DESC;
> ```
> `Note : ` default ของ `ORDER BY` คือเรียงจากน้อยไปหามาก ถ้าต้องการเรียงจากมากไปหาน้อยให้ใช้ `DESC` (Descending) ต่อท้าย `ORDER BY`
> ## *`LIMIT`*
> => เป็น command ที่เอาไว้จำกัด data ที่จะเอามาแสดง
> ```
> SELECT * FROM customers
> WHERE Country = 'Canada'
> ORDER BY CustomerId DESC
> LIMIT 5;
> ```
> ## *`INSERT`*
> => เป็น command ที่เอาไว้เพิ่ม data เข้าไปใน Table ของ database
> 
> **Approach 1**
> ```
> INSERT INTO "ชื่อTable"
> VALUES("ใส่ค่าเรียงตามลำดับของ field ใน Table");
>
>INSERT INTO customers
>VALUES(60,'Jomphop','Saibuatong','2BSimple Co.',
>'171/281 Khonkaen','Khonkaen','KH','Thailand','40000',
>'0845167512',NULL,'Jomphop.Saibuatong@hotmail.com',3);
> ```
> `Note : ` บาง field ไม่สามารถเป็น `NULL` ทำให้ไม่สามารถ INSERT ได้ ควรระวัง
>
> **Approach 2**
> ```
> INSERT INTO "ชื่อTable" ("เฉพาะชื่อ field ที่เราต้องการจะใส่ Value เพื่อ INSERT")
> VALUES("ใส่ค่าเรียงตามลำดับของ field ที่กำหนดไว้ข้างบน");
>
> INSERT INTO customers (FirstName,LastName,Email)
> VALUES('Kant','Saibuatong','Kant@hotmail.com');
> ```
> ## *`UPDATE`*
> => เป็น command ที่เอาไว้ update ข้อมูลแต่ละ field ใน record ของ Table
> ```
> UPDATE "ชื่อ Table" 
>SET 
> "ชื่อ field ที่ต้องการจะ update" = value ใหม่ที่ต้องการจะ update,
> "ชื่อ field ที่ต้องการจะ update" = value ใหม่ที่ต้องการจะ update
> WHERE "เงื่อนไขของ record ที่ต้องการจะ update ข้อมูล";
>
> UPDATE customers 
>SET 
> FirstName = 'KantWhenUpdate',
> LastName = 'SaibuatongWhenUpdate'
> WHERE CustomerId = 61;
> ```
> `Note : ` ระวังทุกครั้งที่เรา `UPDATE` ถ้าไม่ใส่ `WHERE` มันจะ Update ให้ทุก record บน Table
> ## *`DELETE`*
> => เป็น command ที่เอาไว้ลบ data ออกจาก Table
> ```
> DELETE FROM "ชื่อ Table"
> WHERE "เงื่อนไขของ record ที่ต้องการจะลบ";
>
> DELETE FROM customers
> WHERE CustomerId = 61;
> ```
> `Note : ` `DELETE` ถ้าไม่ใส่ `WHERE` มันจะ delete ทุก record บน Table