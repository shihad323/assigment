1 . Explain the Primary Key and Foreign Key concepts in PostgreSQL .
 
 Primary Key (প্রাইমারি কি): সবগুলো উপাদান ইউনিক থাকে, এর দ্বারা টেবিলের প্রত্যেকটি রো একটি থেকে আরেকটি আলাদা হয়ে থাকে।

 CREATE TABLE students (
    student_id SERIAL PRIMARY KEY,
    name TEXT,
    age INT
);

(এখানে student_id হল Primary Key)

 student_id  name    age 
 1           Rakib   20
 2           Meera   21
 3           Tanvir  22


Foreign Key (ফরেইন কি):ফরেন কি মূলত অন্য একটি টেবিলের প্রাইমারি কি কে রেফারেন্স হিসাবে ব্যবহার করে। এর দ্বারা দুইটি টেবিলের মধ্যে সম্পর্ক তৈরি হয়।

CREATE TABLE students (
    student_id SERIAL PRIMARY KEY,
    name TEXT,
    age INT
);

(এখানে student_id হল Primary Key)

student_id   name    age 
1            Rakib   20  
2            Meera   21  
3            Tanvir  22  

CREATE TABLE enrollments (
    enrollment_id SERIAL PRIMARY KEY,
    student_id INT REFERENCES students(student_id),
    course TEXT
);

 enrollment_id   student_id   course   
 101             1            Math     
 102             2            English  
 103             1            Computer 
 104             3            Physics

5 . Explain the purpose of the WHERE clause in a SELECT statement.

WHERE ক্লজটি SELECT স্টেটমেন্টে ব্যবহার করার কারণ হলো একটি নির্দিষ্ট শর্ত অনুযায়ী ডাটা গুলোকে ফিল্টার করা যায় সবগুলো ডাটা না দেখিয়ে, যেগুলো ফিল্টার করা হয় শুধুমাত্র সে ডাটা গুলোকে দেখানো যায়। এর মাধ্যমে ডাটা গুলো প্রোটেক্টেড থাকে।

in this question we use previous question data table:

SELECT * FROM students
WHERE age = 20;

 student_id   name    age 
 1            Rakib   20
 3            Nabila  20


8 . What is the significance of the JOIN operation, and how does it work in PostgreSQL?

JOIN  এর মাধ্যমে দুইটি টেবিল কে একসাথে যুক্ত করা যায়, এবং তথ্যগুলোকে একসাথে ব্যবহার করা যায়। JOIN  এ সাধারণত একটি টেবিলের Primary Key অন্য একটি টেবিলের Foreign Key হিসাবে ব্যবহৃত হয়।

Types of JOIN in PostgreSQL

1.Inner join
2.Left join
3.Right join

Students:

student_id	name
1	        Rakib
2	        Meera

enrollments

enrollment_id	student_id	course
101	            1	        Math
102	            1	        English

SELECT students.name, enrollments.course
FROM students
INNER JOIN enrollments
ON students.student_id = enrollments.student_id;


Output: 
name	course
Rakib	Math
Rakib	English

9.Explain the GROUP BY clause and its role in aggregation operations.

একই ধরনের ডাটা গুলোকে একসাথে করে একটি  নির্দিষ্ট অপারেশন করে থাকে। এর জন্য সাধারনত Aggregate ফাংশন ব্যবহার করা হয়ে থাকে

COUNT()	
SUM()	
AVG()	
MAX()	
MIN()	

orders:

order_id	customer_name	amount
1	        Rakib	        200
2	        Meera	        150
3	        Rakib	        300
4	        Meera	        100

SELECT customer_name, SUM(amount)
FROM orders
GROUP BY customer_name;

Output:

customer_name	sum
Rakib	        500
Meera	        250


10 . How can you calculate aggregate functions like COUNT(), SUM(), and AVG() in PostgreSQL?

একই ধরনের ডাটা গুলোকে একসাথে করে একটি  নির্দিষ্ট অপারেশন করে থাকে। এর জন্য সাধারনত Aggregate ফাংশন ব্যবহার করা হয়ে থাকে

1 . COUNT() : Count number of rows

SELECT COUNT(*) FROM orders;

2 . total of values

SELECT SUM(amount) FROM orders;


3 . AVG() – average value

SELECT AVG(amount) FROM orders;

 multiple aggregate can use in one query

 SELECT 
    COUNT(*) AS total_orders,
    SUM(amount) AS total_amount,
    AVG(amount) AS average_amount
FROM orders; 