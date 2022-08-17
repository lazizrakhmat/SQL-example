# SQL-Lessons
Ushbu repositoriyda SQL darslariga oid kodlar jamlangan.

Asosan 3 xil turda bo'g'lanish bo'ladi, DUPLICATE'larni olidini olish uchun.
Boshqacha bo'lishiham mumkin !

1) ONE TO MANY
2) ONE TO ONE
3) MANY TO MANY

Bu yerda asosiy DATABASE <contacts.csv>. Tog'ri dizayin bo'lishi uchun yo'riqnoma 

1. Professions TABLE <contacts> ga << One To Many >> FK relitionship bo'lib bog'langan.
   Sababi 1 ta PROFESSION ko'pgina CONTACT'ga tegishli bo'lishi mumkin . A lekin 1 ta CONTACT'ga 
   1 ta PROFESSION tegishli bo'ladi.
   

2. Salary esa <contacts> ga << One To One >> FK relitionship bo'lib bo'g'langan.
   Lekin SALARY xar 1 ta CONTACT'ga 1 ta tegishli bo'ladi.
   Har doimham bunday bo'ladi deyaolmaymiz ammo to'g'ri DESIGN uchun shu yo'l to'g'ri hisoblanadi.

3. Shunday ekan biz <contact_salary> TABLE yaratib oldik unga <contact_id> REFERENCE va UNIQUE (contact_id)
   berdik. Bu bizga bitta contact'ga 2 marta value berishdan saqlaydi. Bu esa to'g'ri DESIGN qilganimizni
   anglatadi. ( One to one )

4. ONE TO MANY nima ?
   
   Jadvalda ko'rishingiz mumkin bizda 1 ta contact'da 1 ta profession bor,
   A 1 ta profession'da ko'pgina contact bo'lishi mumkin. 

5. ONE TO ONE qachon ishlatiladi ?
   
   * Tezroq query yozish uchun 
   * Security tarafdan 
   * Asosiy jadval kattalashib ketganda 
   
   #ExampleCode 
    >>    CREATE TABLE contact_salary (
             id SERIAL PRIMARY KEY,
             amount NUMERIC NOT NULL,
             UNIQUE (contact_id)
        );
        
    >>    INSERT INTO contact_salary (amount, contact_id) VALUES (300, 1);
        

6. MANY TO MANY 
   
   Nima uchun Many To Many ?
      
      1 ta contact'da ko'pgina interest bo'lshi mumkin, 
      A 1 ta interest ko'pgina contact'ga bo'lshi mumkin.

   Bizda interests row bor edi uni jadvalimizdan DUPLICATE bo'lib qolshidan saqlash
   maqsadida alohida TABLE qilib oldik . Endi < interests > TABLE'mizni interest_id 
   si ni olib FK qilib yangi TABLE'ga < contact_interest > bo'glaymiz . 

   < contact_interest> ni ichida 
    FK * contact_id
    FK * interest_id 

    #ExampleCode
     >>   CREATE TABLE interests (
             id SERIAL PRIMARY KEY,
             name VARCHAR(50)
            );
        
     >>   INSERT INTO interest (name) VALUES ('technology');
       
     >>   CREATE TABLE contact_interests ( 
             id SERIAL PRIMARY KEY,
             contact_id INT REFERENCE contacts (id),
             interests_id INT REFERENCE interests (id)
            );


### Aslida biz nima qildik 1 ta TABLE 'ni 5 ta TABLE 'ga ajtratib oldik, sababi TRUE DESIGN qilganimiz bois
    https://app.diagrams.net/#G164HfPSOm9rrFMSgUE4StscDax5bImlVX
    ###
Bu link'da siz relitionship'larni qnday turda bog'langanini ko'rasiz,( goodreads )
saytini kichkina qismini DESIGN qilib ko'rdik.
 











   

