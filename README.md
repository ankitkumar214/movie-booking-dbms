DBMS Mini Project – Online Movie Ticket Booking System

Queries and Solutions:
1. Write a query to create tables: customer, employee,registration,theatre, movie and screen, which have the necessary details. Set the primary keys for all tables. (DDL)

MariaDB [project]> create table employee (
    -> employee_id int not null primary key,
    -> employee_name varchar(30),
    -> role varchar(30),
    -> contact varchar(20));
Query OK, 0 rows affected (0.016 sec)

MariaDB [project]> desc employee;
+---------------+-------------+------+-----+---------+-------+
| Field         | Type        | Null | Key | Default | Extra |
+---------------+-------------+------+-----+---------+-------+
| employee_id   | int(11)     | NO   | PRI | NULL    |       |
| employee_name | varchar(30) | YES  |     | NULL    |       |
| role          | varchar(30) | YES  |     | NULL    |       |
| contact       | varchar(20) | YES  |     | NULL    |       |
+---------------+-------------+------+-----+---------+-------+
4 rows in set (0.039 sec)

MariaDB [project]> create table movie (
    -> movie_id int not null primary key,
    -> movie_name varchar(30),
    -> run_time int,
    -> language varchar(30),
    -> rating int);
Query OK, 0 rows affected (0.008 sec)

MariaDB [project]> desc movie;
+------------+-------------+------+-----+---------+-------+
| Field      | Type        | Null | Key | Default | Extra |
+------------+-------------+------+-----+---------+-------+
| movie_id   | int(11)     | NO   | PRI | NULL    |       |
| movie_name | varchar(30) | YES  |     | NULL    |       |
| run_time   | int(11)     | YES  |     | NULL    |       |
| language   | varchar(30) | YES  |     | NULL    |       |
| rating     | int(11)     | YES  |     | NULL    |       |
+------------+-------------+------+-----+---------+-------+
5 rows in set (0.024 sec)

MariaDB [project]> create table theatre (
    -> theatre_id int not null primary key,
    -> theatre_name varchar(30),
    -> city varchar(40));
Query OK, 0 rows affected (0.008 sec)

MariaDB [project]> desc theatre;
+--------------+-------------+------+-----+---------+-------+
| Field        | Type        | Null | Key | Default | Extra |
+--------------+-------------+------+-----+---------+-------+
| theatre_id   | int(11)     | NO   | PRI | NULL    |       |
| theatre_name | varchar(30) | YES  |     | NULL    |       |
| city         | varchar(40) | YES  |     | NULL    |       |
+--------------+-------------+------+-----+---------+-------+
3 rows in set (0.025 sec)

MariaDB [project]> create table screen(
    -> screen_no int,
    -> no_of_seats int);
Query OK, 0 rows affected (0.009 sec)

MariaDB [project]> desc screen;
+-------------+---------+------+-----+---------+-------+
| Field       | Type    | Null | Key | Default | Extra |
+-------------+---------+------+-----+---------+-------+
| screen_no   | int(11) | YES  |     | NULL    |       |
| no_of_seats | int(11) | YES  |     | NULL    |       |
+-------------+---------+------+-----+---------+-------+
2 rows in set (0.022 sec)

MariaDB [project]> create table reservation(
    -> res_id int not null primary key,
    -> show_time time,
    -> show_date date,
    ->seat_no varchar(30),
    -> classvarchar(10));

Query OK, 0 rows affected (0.009 sec)

MariaDB [project]> desc reservation;
+-----------+-------------+------+-----+---------+-------+
| Field     | Type    | Null | Key | Default | Extra |
+-----------+-------------+------+-----+---------+-------+
| res_id    | int(11) | NO   | PRI | NULL    |       |
| show_time | time    | YES  |     | NULL    |       |
| show_date | date| YES  |     | NULL    |       |
| show_date | varchar(30) | YES  |     | NULL    |       |
| show_date | varchar(10) | YES  |     | NULL    |       |
| seat_no| varchar(30) | YES  |     | NULL    |       |
| class     | varchar(10) | YES  |     | NULL    |       |
+-----------+-------------+------+-----+---------+-------+
7 rows in set (0.022 sec)

MariaDB [project]> create table customer (
    -> customer_id int not null primary key,
    -> customer_name varchar(30),
    -> contact varchar(30),
    -> payment_method varchar(30),
    -> amount float);
Query OK, 0 rows affected (0.006 sec)

MariaDB [project]> desc customer;
+----------------+-------------+------+-----+---------+-------+
| Field          | Type        | Null | Key | Default | Extra |
+----------------+-------------+------+-----+---------+-------+
| customer_id    | int(11)     | NO   | PRI | NULL    |       |
| customer_name  | varchar(30) | YES  |     | NULL    |       |
| contact        | varchar(30) | YES  |     | NULL    |       |
| payment_method | varchar(30) | YES  |     | NULL    |       |
| amount         | float       | YES  |     | NULL    |       |
+----------------+-------------+------+-----+---------+-------+
5 rows in set (0.023 sec)



MariaDB [project]> create table price (
    -> movie_id int,
    -> cost float);
Query OK, 0 rows affected (0.006 sec)

MariaDB [project]> desc price;
+----------------+-------------+------+-----+---------+-------+
| Field          | Type        | Null | Key | Default | Extra |
+----------------+-------------+------+-----+---------+-------+
| movie_id| int(11)     | YES  | | NULL    |       |
| amount         | float       | YES  |     | NULL    |       |
+----------------+-------------+------+-----+---------+-------+
2 rows in set (0.023 sec)

2.Make sure referential integrity is maintained. Insert values into the table and print all the entries of all tables once. (DML)

MariaDB [project]> alter table reservation add column movie_id int;
Query OK, 0 rows affected (0.010 sec)
Records: 0  Duplicates: 0  Warnings: 0

MariaDB [project]> alter table reservation add constraint res_mov foreign key (movie_id) references movie(movie_id);
Query OK, 0 rows affected (0.027 sec)
Records: 0  Duplicates: 0  Warnings: 0

MariaDB [project]> alter table reservation add column theatre_id int;
Query OK, 0 rows affected (0.009 sec)
Records: 0  Duplicates: 0  Warnings: 0

MariaDB [project]> alter table reservation add constraint res_the foreign key (theatre_id) references theatre(theatre_id);
Query OK, 0 rows affected (0.026 sec)
Records: 0  Duplicates: 0  Warnings: 0


MariaDB [project]> alter table reservation add column customer_idint;
Query OK, 0 rows affected (0.009 sec)
Records: 0  Duplicates: 0  Warnings: 0

MariaDB [project]> alter table reservation add constraint res_cust foreign key (customer_id) references customer(customer_id);
Query OK, 0 rows affected (0.031 sec)
Records: 0  Duplicates: 0  Warnings: 0

MariaDB [project]> desc reservation;
+-------------+-------------+------+-----+---------+-------+
| Field       | Type    | Null | Key | Default | Extra |
+-------------+-------------+------+-----+---------+-------+
| res_id      | int(11) | NO   | PRI | NULL    |       |
| show_time   | time    | YES  |     | NULL    |       |
| show_date   | date    | YES  |     | NULL    |       |
| seat_no| varchar(30) | YES  |     | NULL    |       |
| class    | varchar(10) | YES  |     | NULL    |       |
| movie_id    | int(11) | YES  | MUL | NULL    |       |
| theatre_id  | int(11) | YES  | MUL | NULL    |       |
| customer_id | int(11) | YES  | MUL | NULL    |       |
+-------------+-------------+------+-----+---------+-------+
8 rows in set (0.029 sec)

MariaDB [project]> alter table customer add column employee_id int;
Query OK, 0 rows affected (0.010 sec)
Records: 0  Duplicates: 0  Warnings: 0

MariaDB [project]> alter table customer add constraint cust_emp foreign key (employee_id) references employee(employee_id);
Query OK, 0 rows affected (0.029 sec)
Records: 0  Duplicates: 0  Warnings: 0

MariaDB [project]> desc customer;
+----------------+-------------+------+-----+---------+-------+
| Field          | Type        | Null | Key | Default | Extra |
+----------------+-------------+------+-----+---------+-------+
| customer_id    | int(11)     | NO   | PRI | NULL    |       |
| customer_name  | varchar(30) | YES  |     | NULL    |       |
| contact        | varchar(30) | YES  |     | NULL    |       |
| payment_method | varchar(30) | YES  |     | NULL    |       |
| amount         | float       | YES  |     | NULL    |       |
| employee_id    | int(11)     | YES  | MUL | NULL    |       |
+----------------+-------------+------+-----+---------+-------+
6 rows in set (0.022 sec)

MariaDB [project]> alter table screen add column theatre_id int;
Query OK, 0 rows affected (0.010 sec)
Records: 0  Duplicates: 0  Warnings: 0

MariaDB [project]> alter table screen add constraint scr_the foreign key (theatre_id) references theatre(theatre_id);
Query OK, 0 rows affected (0.028 sec)
Records: 0  Duplicates: 0  Warnings: 0

MariaDB [project]> alter table screen add column movie_id int;
Query OK, 0 rows affected (0.009 sec)
Records: 0  Duplicates: 0  Warnings: 0

MariaDB [project]> alter table screen add constraint scr_mov foreign key (movie_id) references movie(movie_id);
Query OK, 0 rows affected (0.024 sec)
Records: 0  Duplicates: 0  Warnings: 0

MariaDB [project]> desc screen;
+-------------+---------+------+-----+---------+-------+
| Field       | Type    | Null | Key | Default | Extra |
+-------------+---------+------+-----+---------+-------+
| screen_no   | int(11) | YES  |     | NULL    |       |
| no_of_seats | int(11) | YES  |     | NULL    |       |
| theatre_id  | int(11) | YES  | MUL | NULL    |       |
| movie_id    | int(11) | YES  | MUL | NULL    |       |
+-------------+---------+------+-----+---------+-------+
4 rows in set (0.023 sec)

MariaDB [project]> alter table price add constraintmov_pri foreign key (movie_id) references movie(movie_id);
Query OK, 0 rows affected (0.015 sec)
Records: 0  Duplicates: 0  Warnings: 0

MariaDB [project]> desc price;
+----------------+-------------+------+-----+---------+-------+
| Field          | Type        | Null | Key | Default | Extra |
+----------------+-------------+------+-----+---------+-------+
| movie_id| int(11)     |YES  | MUL | NULL    |       |
| amount         | float       | YES  |     | NULL    |       |
+----------------+-------------+------+-----+---------+-------+
2 rows in set (0.023 sec)

MariaDB [project]> insert into employee values
    -> (1001,"john doe","manager","713435178"),
    -> (1002,"bill chase","worker",812958412),
    -> (1003,"tony stark","worker","955690216"),
    -> (1004,"wanda maximoff","worker","741830460"),
    -> (1005,"walter heisenberg","manager",773195118),
    -> (1006,"clint barton","worker","924196865"),
    -> (1007,"rajesh patel","worker","669037198"),
    -> (1008,"nina williams","worker","878244310"),
    -> (1009,"bucky barnes","worker","951329304"),
    -> (1010,"steve rogers","manager","795853639"),
    -> (1011,"annie von holm","worker","833471617"),
    -> (1012,"susan socks","worker","897174317"),
    -> (1013,"sergei dragunov","manager","981129676"),
    -> (1014,"lei wulong","worker","878829834"),
    -> (1015,"alisa matic","worker","939119675"),
    -> (1016,"jack hummels","worker","742003538");
    -> (1017,"randy orton","manager","414325311");
    -> (1018,"sasha banks","worker","842033535");
    -> (1019,"deepika singh","worker","515426133");
    -> (1020,"rajveer singh","worker","762452145");

Query OK, 20 rows affected (0.040 sec)
Records: 20  Duplicates: 0  Warnings: 0

MariaDB [project]> select * from employee;
+-------------+-------------------+---------+-----------+
| employee_id | employee_name     | role    | contact   |
+-------------+-------------------+---------+-----------+
|        1001 | john doe          | manager | 713435178 |
|        1002 | bill chase        | worker  | 812958412 |
|        1003 | tony stark        | worker  | 955690216 |
|        1004 | wanda maximoff    | worker  | 741830460 |
|        1005 | walter heisenberg | manager | 773195118 |
|        1006 | clint barton      | worker  | 924196865 |
|        1007 | rajesh patel      | worker  | 669037198 |
|        1008 | nina williams     | worker  | 878244310 |
|        1009 | bucky barnes      | worker  | 951329304 |
|        1010 | steve rogers      | manager | 795853639 |
|        1011 | annie von holm    | worker  | 833471617 |
|        1012 | susan socks       | worker  | 897174317 |
|        1013 | sergei dragunov   | manager | 981129676 |
|        1014 | lei wulong        | worker  | 878829834 |
|        1015 | alisa matic       | worker  | 939119675 |
|        1016 | jack hummels      | worker  | 742003538 |
|        1017 | randy orton       | manager | 414325311|
|        1018 | sasha banks       | worker  | 842033535|
|        1019 | deepika singh     | worker  | 515426133|
|        1020 | rajveer singh     | worker  | 762452145|
+-------------+-------------------+---------+-----------+
20 rows in set (0.001 sec)

MariaDB [project]> alter table movie modify column movie_name varchar(100);
Query OK, 0 rows affected (0.055 sec)
Records: 0  Duplicates: 0  Warnings: 0

MariaDB [project]> insert into movie values
    -> (201, "uncharted", 116, "english", 7),
    -> (202, "the lost city", 112, "english", 7),
    -> (203, "moonfall", 120, "english", 6),
    -> (204, "the batman", 176, "english", 9),
    -> (205, "the adam project", 106, "english", 8),
    -> (206, "bachchan pandey", 149, "hindi", 7),
    -> (207, "heropanti 2", 150, "hindi", 5),
    -> (208, "jersey", 170, "hindi", 8),
    -> (209, "kgf chapter 2", 168, "hindi", 9),
    -> (210, "rrr", 187, "hindi", 8),
    -> (211, "beast", 155, "tamil", 6),
    -> (212, "kgf chapter 2", 168, "tamil", 9),
    -> (213, "rrr", 187, "tamil", 8),
    -> (214, "pushpa the rise", 179, "telugu", 8),
    -> (215, "rrr", 187, "telugu", 8),
    -> (216, "kgf chapter 2", 168, "telugu", 9),
    -> (217, "radhe shyam", 138, "telugu", 6),
    -> (218, "kgf chapter 2", 168, "kannada", 9);
    -> (219, "sita ram", 170, "hindi", 8);
    -> (220, "inception", 172, "english", 7);

Query OK, 20 rows affected (0.042 sec)
Records: 20  Duplicates: 0  Warnings: 0


















MariaDB [project]> select * from movie;
+----------+------------------+----------+----------+--------+
| movie_id | movie_name       | run_time | language | rating |
+----------+------------------+----------+----------+--------+
|      201 | uncharted        |      116 | english  |      7 |
|      202 | the lost city    |      112 | english  |      7 |
|      203 | moonfall         |      120 | english  |      6 |
|      204 | the batman       |      176 | english  |      9 |
|      205 | the adam project |      106 | english  |      8 |
|      206 | bachchan pandey  |      149 | hindi    |      7 |
|      207 | heropanti 2      |      150 | hindi    |      5 |
|      208 | jersey           |      170 | hindi    |      8 |
|      209 | kgf chapter 2    |      168 | hindi    |      9 |
|      210 | rrr              |      187 | hindi    |      8 |
|      211 | beast            |      155 | tamil    |      6 |
|      212 | kgf chapter 2    |      168 | tamil    |      9 |
|      213 | rrr              |      187 | tamil    |      8 |
|      214 | pushpa the rise  |      179 | telugu   |      8 |
|      215 | rrr              |      187 | telugu   |      8 |
|      216 | kgf chapter 2    |      168 | telugu   |      9 |
|      217 | radhe shyam      |      138 | telugu   |      6 |
|      218 | kgf chapter 2    |      168 | kannada  |      9 |
|      219 | sita ram     |      170 | hindi    |      8 |
|      220 | inception        |      172 | english  |      7 |
+----------+------------------+----------+----------+--------+
20 rows in set (0.101 sec)

MariaDB [project]> insert into theatre values
    -> (501, "pvr director's cut", "new delhi"),
    -> (502, "pvr select city walk", "new delhi"),
    -> (503, "prasad movies", "hyderabad"),
    -> (504, "pvr koramangala", "bengaluru"),
    -> (505, "urvashi theater", "bengaluru"),
    -> (506, "inox laserplex", "mumbai"),
    -> (507, "carnival cinemas", "mumbai"),
    -> (508, "regal cinema", "mumbai"),
    -> (509, "ariesplex sl cinemas", "thiruvananthapuram"),
    -> (510, "raj mandir cinema", "jaipur"),
    -> (511, "mayajaal multiplex", "chennai"),
    -> (512, "rdb cinemas", "kolkata"),
    -> (513, "jeeva rukmani cinemas", "puducherry"),
    -> (514, "cinepolis", "kolkata");

Query OK, 14 rows affected (0.041 sec)
Records: 14  Duplicates: 0  Warnings: 0


MariaDB [project]> select * from theatre;
+------------+-----------------------+--------------------+
| theatre_id | theatre_name          | city               |
+------------+-----------------------+--------------------+
|        501 | pvr director's cut    | new delhi          |
|        502 | pvr select city walk  | new delhi          |
|        503 | prasad movies         | hyderabad          |
|        504 | pvr koramangala       | bengaluru          |
|        505 | urvashi theater       | bengaluru          |
|        506 | inox laserplex        | mumbai             |
|        507 | carnival cinemas      | mumbai             |
|        508 | regal cinema          | mumbai             |
|        509 | ariesplex sl cinemas  | thiruvananthapuram |
|        510 | raj mandir cinema     | jaipur             |
|        511 | mayajaal multiplex    | chennai            |
|        512 | rdb cinemas           | kolkata            |
|        513 | jeeva rukmani cinemas | puducherry         |
|        514 | cinepolis             | kolkata            |

+------------+-----------------------+--------------------+
14 rows in set (0.001 sec)

MariaDB [project]> insert into customer values
    -> (2001, "arvind mahajan", "6346496800", "card", 1002, 250.0),
    -> (2002, "priyanka chaudhry", "7180283913", "card", 1004, 300.00),
    -> (2003, "somnath arya", "8878250806", "cash", 1006, 190.00),
    -> (2004, "clayton wilson", "9458499050", "cash", 1008, 210.00),
    -> (2005, "julia rollins", "9564690714", "card", 1012, 280.00),
    -> (2006, "maaya ishida", "8034604040", "cash", 1014, 220.00),
    -> (2007, "cameron clark", "9672887224", "cash", 1016, 310.00),
    -> (2008, "novikova fedosya", "8009978540", "card", 1002, 240.00),
    -> (2009, "zhu jingwen", "6942255772", "card", 1003, 187.00),
    -> (2010, "breanne kuhic", "7044533023", "card", 1004, 200.00);
    -> (2011, "alexander white", "4167101190", "cash", 1005, 243.00),
    -> (2012, "christine harrison", "4905239370", "cash", 1007, 400.00),
    -> (2013, "alfredo garcia", "8546005445", "card", 1009, 350.00),
    -> (2014, "rajesh patel", "669037198", "card", 1011, 254.00),
    -> (2015, "olaf van dijk", "2302815512", "card", 1015, 337.00),
    -> (2016, "bastien meunier", "5332333537", "card", 1003, 270.00),
    -> (2017, "owen murphy", "6718364853", "cash", 1004, 289.00),
    -> (2018, "aaryan sathasivam", "9717223547", "cash", 1002, 198.00),
    -> (2019, "hamed al-mahmoudi", "2829488295", "card", 1005, 204.00),
    -> (2020, "clint barton", "924196865", "card", 1008, 213.00),
    -> (2021, "aniruddh kapur", "5237922664", "cash", 1003, 421.00),
    -> (2022, "sam wilson", "9991112233", "card", 1003, 376.00),
    -> (2023, "emre can", "9050943250", "card", 1012, 281.00),
    -> (2024, "thunder carlbach", "5026820459", "cash", 1014, 188.00);
Query OK, 24 rows affected (0.002 sec)
Records: 24  Duplicates: 0  Warnings: 0



MariaDB [project]> insert into reservation values
    -> (3001, "09:00", "2022-05-18", 218, 514, 2010),
    -> (3002, "14:00", "2022-05-23", 216, 513, 2009),
    -> (3003, "18:00", "2022-05-18", 214, 512, 2008),
    -> (3004, "09:00", "2022-05-24", 212, 511, 2007),
    -> (3005, "18:00", "2022-05-31", 210, 510, 2006),
    -> (3006, "14:00", "2022-05-28", 208, 505, 2005),
    -> (3007, "14:00", "2022-05-30", 206, 506, 2004),
    -> (3008, "18:00", "2022-05-19", 204, 507, 2003),
    -> (3009, "22:00", "2022-05-21", 213, 508, 2002),
    -> (3010, "09:00", "2022-05-25", 201, 509, 2001),
    -> (3011, "09:00", "2022-05-26", 203, 504, 2010),
    -> (3012, "18:00", "2022-05-26", 205, 501, 2012),
    -> (3013, "14:00", "2022-05-26", 209, 503, 2013),
    -> (3014, "22:00", "2022-05-26", 209, 502, 2014),
    -> (3015, "14:00", "2022-06-03", 211, 502, 2015),
    -> (3016, "22:00", "2022-06-04", 213, 501, 2020),
    -> (3017, "18:00", "2022-06-06", 215, 506, 2019),
    -> (3018, "09:00", "2022-06-07", 217, 509, 2018),
    -> (3019, "22:00", "2022-06-09", 204, 511, 2017),
    -> (3020, "22:00", "2022-06-10", 204, 513, 2016),
    -> (3021, "14:00", "2022-06-11", 209, 507, 2021),
    -> (3022, "09:00", "2022-06-12", 213, 508, 2022),
    -> (3023, "18:00", "2022-06-12", 212, 510, 2024),
    -> (3024, "22:00", "2022-06-12", 213, 505, 2023);
Query OK, 24 rows affected (0.002 sec)
Records: 24  Duplicates: 0  Warnings: 0

MariaDB [project]> select * from reservation;
+--------+-----------+------------+----------+------------+-------------+
| res_id | show_time | show_date  | movie_id | theatre_id | customer_id |
+--------+-----------+------------+----------+------------+-------------+
|   3001 | 09:00:00  | 2022-05-18 |      218 |        514 |        2010 |
|   3002 | 14:00:00  | 2022-05-23 |      216 |        513 |        2009 |
|   3003 | 18:00:00  | 2022-05-18 |      214 |        512 |        2008 |
|   3004 | 09:00:00  | 2022-05-24 |      212 |        511 |        2007 |
|   3005 | 18:00:00  | 2022-05-31 |      210 |        510 |        2006 |
|   3006 | 14:00:00  | 2022-05-28 |      208 |        505 |        2005 |
|   3007 | 14:00:00  | 2022-05-30 |      206 |        506 |        2004 |
|   3008 | 18:00:00  | 2022-05-19 |      204 |        507 |        2003 |
|   3009 | 22:00:00  | 2022-05-21 |      213 |        508 |        2002 |
|   3010 | 09:00:00  | 2022-05-25 |      201 |        509 |        2001 |
|   3011 | 09:00:00  | 2022-05-26 |      203 |        504 |        2010 |
|   3012 | 18:00:00  | 2022-05-26 |      205 |        501 |        2012 |
|   3013 | 14:00:00  | 2022-05-26 |      209 |        503 |        2013 |
|   3014 | 22:00:00  | 2022-05-26 |      209 |        502 |        2014 |
|   3015 | 14:00:00  | 2022-06-03 |      211 |        502 |        2015 |
|   3016 | 22:00:00  | 2022-06-04 |      213 |        501 |        2020 |
|   3017 | 18:00:00  | 2022-06-06 |      215 |        506 |        2019 |
|   3018 | 09:00:00  | 2022-06-07 |      217 |        509 |        2018 |
|   3019 | 22:00:00  | 2022-06-09 |      204 |        511 |        2017 |
|   3020 | 22:00:00  | 2022-06-10 |      204 |        513 |        2016 |
|   3021 | 14:00:00  | 2022-06-11 |      209 |        507 |        2021 |
|   3022 | 09:00:00  | 2022-06-12 |      213 |        508 |        2022 |
|   3023 | 18:00:00  | 2022-06-12 |      212 |        510 |        2024 |
|   3024 | 22:00:00  | 2022-06-12 |      213 |        505 |        2023 |
+--------+-----------+------------+----------+------------+-------------+
24 rows in set (0.000 sec)
MariaDB [project]> insert into screen values
    -> (1, 600, 501, 205),
    -> (2, 550, 501, 213),
    -> (1, 550, 502, 209),
    -> (2, 600, 502, 211),
    -> (1, 600, 503, 209),
    -> (1, 500, 504, 203),
    -> (1, 450, 505, 208),
    -> (2, 300, 505, 213),
    -> (1, 440, 506, 206),
    -> (2, 420, 506, 215),
    -> (1, 350, 507, 204),
    -> (2, 450, 507, 209),
    -> (1, 450, 508, 213),
    -> (1, 500, 509, 201),
    -> (2, 600, 509, 217),
    -> (1, 500, 510, 212),
    -> (2, 400, 510, 210),
    -> (1, 460, 511, 204),
    -> (2, 450, 511, 212),
    -> (1, 350, 512, 214),
    -> (1, 300, 513, 216),
    -> (1, 400, 514, 218);
Query OK, 22 rows affected (0.002 sec)
Records: 22  Duplicates: 0  Warnings: 0






















MariaDB [project]> select * from screen;
+-----------+-------------+------------+----------+
| screen_no | no_of_seats | theatre_id | movie_id |
+-----------+-------------+------------+----------+
|         1 |         600 |        501 |      205 |
|         2 |         550 |        501 |      213 |
|         1 |         550 |        502 |      209 |
|         2 |         600 |        502 |      211 |
|         1 |         600 |        503 |      209 |
|         1 |         500 |        504 |      203 |
|         1 |         450 |        505 |      208 |
|         2 |         300 |        505 |      213 |
|         1 |         440 |        506 |      206 |
|         2 |         420 |        506 |      215 |
|         1 |         350 |        507 |      204 |
|         2 |         450 |        507 |      209 |
|         1 |         450 |        508 |      213 |
|         1 |         500 |        509 |      201 |
|         2 |         600 |        509 |      217 |
|         1 |         500 |        510 |      212 |
|         2 |         400 |        510 |      210 |
|         1 |         460 |        511 |      204 |
|         2 |         450 |        511 |      212 |
|         1 |         350 |        512 |      214 |
|         1 |         300 |        513 |      216 |
|         1 |         400 |        514 |      218 |
+-----------+-------------+------------+----------+
22 rows in set (0.000 sec)


3. Write a query to add a column in any of the above tables. (DDL)

MariaDB [project]> alter table customer add column city varchar(30);
Query OK, 0 rows affected (0.053 sec)
Records: 0  Duplicates: 0  Warnings: 0

 

4. Write a query to perform drop and rename column in any of the above tables. (DDL)
MariaDB [project]> alter table customer rename column city to address;
Query OK, 0 rows affected (0.051 sec)
Records: 0  Duplicates: 0  Warnings: 0
MariaDB [project]> alter table customer drop column address;
Query OK, 0 rows affected (0.050 sec)
Records: 0  Duplicates: 0  Warnings: 0

 



5. Write a query to delete any one unnecessary row. (DML)
MariaDB [project]> insert into customer values
    -> (2025, "john doe", "123456789", "card", 1008, 267.00);
Query OK, 1 row affected (0.041 sec)

 

MariaDB [project]> delete from customer where customer_id = 2025;
Query OK, 1 row affected (0.040 sec)


 
 











6. Write a query to get the role-wise number of employees from the employee table. (DML)
MariaDB [project]> select * from employee;
+-------------+-------------------+---------+---------------+
| employee_id | employee_name     | role    | contact       |
+-------------+-------------------+---------+---------------+
|        1001 | john doe          | manager | +91 713435178 |
|        1002 | bill chase        | worker  | +91 812958412 |
|        1003 | tony stark        | worker  | +91 955690216 |
|        1004 | wanda maximoff    | worker  | +91 741830460 |
|        1005 | walter heisenberg | manager | +91 773195118 |
|        1006 | clint barton      | worker  | +91 924196865 |
|        1007 | rajesh patel      | worker  | +91 669037198 |
|        1008 | nina williams     | worker  | +91 878244310 |
|        1009 | bucky barnes      | worker  | +91 951329304 |
|        1010 | steve rogers      | manager | +91 795853639 |
|        1011 | annie von holm    | worker  | +91 833471617 |
|        1012 | susan socks       | worker  | +91 897174317 |
|        1013 | sergei dragunov   | manager | +91 981129676 |
|        1014 | lei wulong        | worker  | +91 878829834 |
|        1015 | alisa matic       | worker  | +91 939119675 |
|        1016 | jack hummels      | worker  | +91 742003538 |
+-------------+-------------------+---------+---------------+
16 rows in set (0.063 sec)

MariaDB [project]> select role, count(*) as no_of_emps from employee group by role;
+---------+------------+
| role    | no_of_emps |
+---------+------------+
| manager |          4 |
| worker  |         12 |
+---------+------------+
2 rows in set (0.040 sec)





7. Write a query to print all the theatres that are showing the movie “Beast”, also find if any theatre in Chennai is doing the same.(joins)

MariaDB [project]> insert into screen values (3, 525, 511, 211);
Query OK, 1 row affected (0.066 sec)
Records: 1  Duplicates: 0  Warnings: 0

MariaDB [project]> select * from screen;
+-----------+-------------+------------+----------+
| screen_no | no_of_seats | theatre_id | movie_id |
+-----------+-------------+------------+----------+
|         1 |         600 |        501 |      205 |
|         2 |         550 |        501 |      213 |
|         1 |         550 |        502 |      209 |
|         2 |         600 |        502 |      211 |
|         1 |         600 |        503 |      209 |
|         1 |         500 |        504 |      203 |
|         1 |         450 |        505 |      208 |
|         2 |         300 |        505 |      213 |
|         1 |         440 |        506 |      206 |
|         2 |         420 |        506 |      215 |
|         1 |         350 |        507 |      204 |
|         2 |         450 |        507 |      209 |
|         1 |         450 |        508 |      213 |
|         1 |         500 |        509 |      201 |
|         2 |         600 |        509 |      217 |
|         1 |         500 |        510 |      212 |
|         2 |         400 |        510 |      210 |
|         1 |         460 |        511 |      204 |
|         2 |         450 |        511 |      212 |
|         1 |         350 |        512 |      214 |
|         1 |         300 |        513 |      216 |
|         1 |         400 |        514 |      218 |
+-----------+-------------+------------+----------+
22 rows in set (0.001 sec)

MariaDB [project]> create table screen_detailed as select * from screen natural join theatre natural join movie;
Query OK, 23 rows affected (0.064 sec)
Records: 23  Duplicates: 0  Warnings: 0






MariaDB [project]> select theatre_name, city, movie_name, language from screen_detailed where movie_name like "beast";
+----------------------+-----------+------------+----------+
| theatre_name         | city      | movie_name | language |
+----------------------+-----------+------------+----------+
| pvr select city walk | new delhi | beast      | tamil    |
| mayajaal multiplex   | chennai   | beast      | tamil    |
+----------------------+-----------+------------+----------+
2 rows in set (0.001 sec)

MariaDB [project]> select theatre_name, city, movie_name, language from screen_detailed where movie_name like "beast" and city like "chennai";
+--------------------+---------+------------+----------+
| theatre_name       | city    | movie_name | language |
+--------------------+---------+------------+----------+
| mayajaal multiplex | chennai | beast      | tamil    |
+--------------------+---------+------------+----------+
1 row in set (0.001 sec) 
8. Write a query to get the customer details who have booked shows between 06-06-2022 and12-06-2022, and the details of their reservation as well. (date manipulation, joins)

MariaDB [project]> create table cust_res as select c.*, r.* from customer c inner join reservation r on c.customer_id = r.customer_id;
Query OK, 24 rows affected (0.066 sec)
Records: 24  Duplicates: 0  Warnings: 0


MariaDB [project]> select customer_name, contact, payment_method, amount, show_time, show_date, movie_name, language, theatre_name, city from cust_res natural join movie natural join theatre where show_date between "2022-06-06" and "2022-06-12";
9. Write a query to print the screens of theatres which have the greatest number of seats in their respective cities. (joins, aggregate functions)

MariaDB [project]> create table screen_detailed as select * from screen natural join theatre natural join movie;
Query OK, 23 rows affected (0.064 sec)
Records: 23  Duplicates: 0  Warnings: 0



MariaDB [project]> select screen_no, max(no_of_seats) as maximum_seats,theatre_name, city from screen_detailed group by city order by maximum_seats desc;
+-----------+---------------+-----------------------+--------------------+
| screen_no | maximum_seats | theatre_name          | city               |
+-----------+---------------+-----------------------+--------------------+
|         1 |           600 | ariesplex sl cinemas  | thiruvananthapuram |
|         1 |           600 | prasad movies         | hyderabad          |
|         1 |           600 | pvr director's cut    | new delhi          |
|         1 |           525 | mayajaal multiplex    | chennai            |
|         1 |           500 | raj mandir cinema     | jaipur             |
|         1 |           500 | pvr koramangala       | bengaluru          |
|         1 |           450 | inox laserplex        | mumbai             |
|         1 |           400 | rdb cinemas           | kolkata            |
|         1 |           300 | jeeva rukmani cinemas | puducherry         |
+-----------+---------------+-----------------------+--------------------+
9 rows in set (0.001 sec) 
10. Write a query toprint all the movies which are rated above 7 and have a run time of more than 150 minutes. (DML)
MariaDB [project]> select * from movie;
+----------+------------------+----------+----------+--------+
| movie_id | movie_name       | run_time | language | rating |
+----------+------------------+----------+----------+--------+
|      201 | uncharted        |      116 | english  |      7 |
|      202 | the lost city    |      112 | english  |      7 |
|      203 | moonfall         |      120 | english  |      6 |
|      204 | the batman       |      176 | english  |      9 |
|      205 | the adam project |      106 | english  |      8 |
|      206 | bachchan pandey  |      149 | hindi    |      7 |
|      207 | heropanti 2      |      150 | hindi    |      5 |
|      208 | jersey           |      170 | hindi    |      8 |
|      209 | kgf chapter 2    |      168 | hindi    |      9 |
|      210 | rrr              |      187 | hindi    |      8 |
|      211 | beast            |      155 | tamil    |      6 |
|      212 | kgf chapter 2    |      168 | tamil    |      9 |
|      213 | rrr              |      187 | tamil    |      8 |
|      214 | pushpa the rise  |      179 | telugu   |      8 |
|      215 | rrr              |      187 | telugu   |      8 |
|      216 | kgf chapter 2    |      168 | telugu   |      9 |
|      217 | radhe shyam      |      138 | telugu   |      6 |
|      218 | kgf chapter 2    |      168 | kannada  |      9 |
+----------+------------------+----------+----------+--------+
18 rows in set (0.001 sec)

MariaDB [project]> select distinct movie_name, run_time, rating from movie where rating > 7 and run_time > 150;
+-----------------+----------+--------+
| movie_name      | run_time | rating |
+-----------------+----------+--------+
| the batman      |      176 |      9 |
| jersey          |      170 |      8 |
| kgf chapter 2   |      168 |      9 |
| rrr             |      187 |      8 |
| pushpa the rise |      179 |      8 |
+-----------------+----------+--------+
5 rows in set (0.000 sec)
11. Write a query toprint all those customer details who have booked for the show time between 6 pm and 12 am, in the city of Jaipur.(joins)

MariaDB [project]> create table cust_details as select cust_res.*, movie_name, language from cust_resnatural join movie;
Query OK, 24 rows affected (0.014 sec)
Records: 24  Duplicates: 0  Warnings: 0

MariaDB [project]> select * from cust_details;


 
12. Write a query to print the theatres which are screening the movie “KGF: Chapter 2” in but not in Hindi language.(strings, joins)

MariaDB [project]> create table screen_detailed as select * from screen natural join theatre natural join movie;
Query OK, 23 rows affected (0.064 sec)
Records: 23  Duplicates: 0  Warnings: 0

MariaDB [project]> select theatre_name, city, movie_name, language from screen_detailed where movie_name like "kgf chapter 2" and language not like "hindi";
+-----------------------+------------+---------------+----------+
| theatre_name          | city       | movie_name    | language |
+-----------------------+------------+---------------+----------+
| raj mandir cinema     | jaipur     | kgf chapter 2 | tamil    |
| mayajaal multiplex    | chennai    | kgf chapter 2 | tamil    |
| jeeva rukmani cinemas | puducherry | kgf chapter 2 | telugu   |
| cinepolis             | kolkata    | kgf chapter 2 | kannada  |
+-----------------------+------------+---------------+----------+
4 rows in set (0.000 sec)
 
13. Write a query to print all the English movies running incinemas located in the cities New Delhi, Mumbai, and Chennai. (joins)
MariaDB [project]> create table temp as select * from screen natural join movie where language = "english";
Query OK, 5 rows affected (0.015 sec)
Records: 5  Duplicates: 0  Warnings: 0

MariaDB [project]> select * from temp;
 


MariaDB [project]> select * from temp natural join theatre;


MariaDB [project]> select * from temp natural join theatre where city in ('new delhi', 'mumbai', 'chennai');


 
14.Write a query to print all employees who have also booked tickets to watch a movie.(nested queries)

MariaDB [project]> select customer_name, contact, payment_method, amount from customer where customer_name in (select employee_name from employee);
+---------------+---------------+----------------+--------+
| customer_name | contact       | payment_method | amount |
+---------------+---------------+----------------+--------+
| rajesh patel  | +91 669037198 | card           |    254 |
| clint barton  | +91 924196865 | upi            |    213 |
+---------------+---------------+----------------+--------+
2 rows in set (0.001 sec)

15. Find the ticket sales movie-wise and print the movie that has maximum overall amount. (views,nested queries, aggregate functions)

MariaDB [project]> create table cust_res as select c.amount, c.discount, r.show_time, r.show_date, m.movie_name from customer c, reservation r, movie m where c.customer_id = r.customer_id and r.movie_id = m.movie_id;
Query OK, 24 rows affected (0.014 sec)
Records: 24  Duplicates: 0  Warnings: 0

















MariaDB [project]> select * from cust_res;
+--------+----------+-----------+------------+------------------+
| amount | discount | show_time | show_date  | movie_name       |
+--------+----------+-----------+------------+------------------+
|    243 |    24.30 | 09:00:00  | 2022-05-18 | kgf chapter 2    |
|    187 |    18.70 | 14:00:00  | 2022-05-23 | kgf chapter 2    |
|    240 |    24.00 | 18:00:00  | 2022-05-18 | pushpa the rise  |
|    310 |     0.00 | 09:00:00  | 2022-05-24 | kgf chapter 2    |
|    220 |    22.00 | 18:00:00  | 2022-05-31 | rrr              |
|    280 |    14.00 | 14:00:00  | 2022-05-28 | jersey           |
|    210 |    21.00 | 14:00:00  | 2022-05-30 | bachchan pandey  |
|    190 |    19.00 | 18:00:00  | 2022-05-19 | the batman       |
|    300 |    15.00 | 22:00:00  | 2022-05-21 | rrr              |
|    250 |    25.00 | 09:00:00  | 2022-05-25 | uncharted        |
|    200 |    20.00 | 09:00:00  | 2022-05-26 | moonfall         |
|    400 |     0.00 | 18:00:00  | 2022-05-26 | the adam project |
|    350 |    17.50 | 14:00:00  | 2022-05-26 | kgf chapter 2    |
|    254 |    12.70 | 22:00:00  | 2022-05-26 | kgf chapter 2    |
|    337 |    16.85 | 14:00:00  | 2022-06-03 | beast            |
|    213 |    21.30 | 22:00:00  | 2022-06-04 | rrr              |
|    204 |    20.40 | 18:00:00  | 2022-06-06 | rrr              |
|    198 |    19.80 | 09:00:00  | 2022-06-07 | radhe shyam      |
|    289 |     0.00 | 22:00:00  | 2022-06-09 | the batman       |
|    270 |    13.50 | 22:00:00  | 2022-06-10 | the batman       |
|    421 |     0.00 | 14:00:00  | 2022-06-11 | kgf chapter 2    |
|    376 |    18.80 | 09:00:00  | 2022-06-12 | rrr              |
|    188 |    18.80 | 18:00:00  | 2022-06-12 | kgf chapter 2    |
|    281 |    14.05 | 22:00:00  | 2022-06-12 | rrr              |
+--------+----------+-----------+------------+------------------+
24 rows in set (0.000 sec)

MariaDB [project]> create view v as select movie_name, sum(amount - discount) as total_amount from cust_res group by movie_name;
Query OK, 0 rows affected (0.004 sec)









MariaDB [project]> select * from v;
+------------------+--------------+
| movie_name       | total_amount |
+------------------+--------------+
| bachchan pandey  |          189 |
| beast            |       320.15 |
| jersey           |          266 |
| kgf chapter 2    |         1861 |
| moonfall         |          180 |
| pushpa the rise  |          216 |
| radhe shyam      |        178.2 |
| rrr              |      1482.45 |
| the adam project |          400 |
| the batman       |        716.5 |
| uncharted        |          225 |
+------------------+--------------+
11 rows in set (0.000 sec)

MariaDB [project]> select * from v where total_amount = (select max(total_amount) from v);
+---------------+--------------+
| movie_name    | total_amount |
+---------------+--------------+
| kgf chapter 2 |         1861 |
+---------------+--------------+
1 row in set (0.001 sec)









16. Find the movies out of the movies table which have not been screened in any of the theatres. (nested queries)
MariaDB [project]> select * from movie where movie_id not in (select movie_id from screen);
+----------+---------------+----------+----------+--------+
| movie_id | movie_name    | run_time | language | rating |
+----------+---------------+----------+----------+--------+
|      202 | the lost city |      112 | english  |      7 |
|      207 | heropanti 2   |      150 | hindi    |      5 |
+----------+---------------+----------+----------+--------+
2 rows in set (0.001 sec)

17.Find the date wise amount which has been earned, and find the top 5 days in which the sales was maximum. (aggregate functions, joins)
MariaDB [project]> select show_date, sum(amount) as day_total from customer natural join reservation group by show_date;
+------------+-----------+
| show_date  | day_total |
+------------+-----------+
| 2022-05-18 |       483 |
| 2022-05-19 |       190 |
| 2022-05-21 |       300 |
| 2022-05-23 |       187 |
| 2022-05-24 |       310 |
| 2022-05-25 |       250 |
| 2022-05-26 |      1204 |
| 2022-05-28 |       280 |
| 2022-05-30 |       210 |
| 2022-05-31 |       220 |
| 2022-06-03 |       337 |
| 2022-06-04 |       213 |
| 2022-06-06 |       204 |
| 2022-06-07 |       198 |
| 2022-06-09 |       289 |
| 2022-06-10 |       270 |
| 2022-06-11 |       421 |
| 2022-06-12 |       845 |
+------------+-----------+
18 rows in set (0.001 sec)
MariaDB [project]> select show_date, sum(amount) as day_total from customer natural join reservation group by show_date order by day_total desc limit 5;
+------------+-----------+
| show_date  | day_total |
+------------+-----------+
| 2022-05-26 |      1204 |
| 2022-06-12 |       845 |
| 2022-05-18 |       483 |
| 2022-06-11 |       421 |
| 2022-06-03 |       337 |
+------------+-----------+
5 rows in set (0.000 sec)















18. Find the ASCII code of the first letter of customer names, using the in-built ASCII function in SQL. (string functions)
MariaDB [project]> select customer_name,ascii(customer_name) as ascii_code from customer;
+--------------------+------------+
| customer_name      | ascii_code |
+--------------------+------------+
| arvind mahajan     |         97 |
| priyanka chaudhry  |        112 |
| somnath arya       |        115 |
| clayton wilson     |         99 |
| julia rollins      |        106 |
| maaya ishida       |        109 |
| cameron clark      |         99 |
| novikova fedosya   |        110 |
| zhu jingwen        |        122 |
| breanne kuhic      |         98 |
| alexander white    |         97 |
| christine harrison |         99 |
| alfredo garcia     |         97 |
| rajesh patel       |        114 |
| olaf van dijk      |        111 |
| bastien meunier    |         98 |
| owen murphy        |        111 |
| aaryan sathasivam  |         97 |
| hamed al-mahmoudi  |        104 |
| clint barton       |         99 |
| aniruddh kapur     |         97 |
| sam wilson         |        115 |
| emre can           |        101 |
| thunder carlbach   |        116 |
+--------------------+------------+
24 rows in set (0.000 sec)

 
19. Find out the details of customers who have booked for the movie "RRR" and compare the prices that they have paid for the ticket of the same movie, and find out which theatre sold the ticket to this movie at a minimum and maximum price. (nested queries, strings)
MariaDB [project]> create table cust_res as select c.*, r.* from customer c inner join reservation r on c.customer_id = r.customer_id;
Query OK, 24 rows affected (0.066 sec)
Records: 24  Duplicates: 0  Warnings: 0

MariaDB [project]> select * from cust_res;

MariaDB [project]> create table cust_details as select cust_res.*, movie_name, language from cust_res natural join movie;
Query OK, 24 rows affected (0.014 sec)
Records: 24  Duplicates: 0  Warnings: 0










MariaDB [project]> select * from cust_details;

MariaDB [project]> select * from cust_details where movie_name like "rrr";
MariaDB [project]> select customer_id, customer_name, amount, theatre_name, city from cust_details natural join theatre where movie_name like "rrr" and amount = (select max(amount) from cust_details where movie_name like "rrr");
+-------------+---------------+--------+--------------+--------+
| customer_id | customer_name | amount | theatre_name | city   |
+-------------+---------------+--------+--------------+--------+
|        2022 | sam wilson    |    376 | regal cinema | mumbai |
+-------------+---------------+--------+--------------+--------+
1 row in set (0.001 sec)

MariaDB [project]> select customer_id, customer_name, amount, theatre_name, city from cust_details natural join theatre where movie_name like "rrr" and amount = (select min(amount) from cust_details where movie_name like "rrr");
+-------------+-------------------+--------+----------------+--------+
| customer_id | customer_name     | amount | theatre_name   | city   |
+-------------+-------------------+--------+----------------+--------+
|        2019 | hamed al-mahmoudi |    204 | inox laserplex | mumbai |
+-------------+-------------------+--------+----------------+--------+
1 row in set (0.000 sec) 
20. Create view to get customer details along with their reservtion table? (views)
MariaDB [project]>create view customer_details as selectc.customer_name,c.contact,c.amount,r.res_id,r.show_date,r.theatre_id,r.movie_id,r.show_time from customer c inner join reservation r on
c.res_id=r.res_id;
Query OK, 0 rows affected (0.004 sec)

MariaDB [project]> select * from customer_details;






21. Find the customers who had booked tickets in the past week?(time and date functions)
MariaDB [project]> select c.customer_name,c.customer_id,r.show_date from customer c innerjoin reservation r on c.customer_id = r.customer_id where timestampdiff(day,show_date,curdate())<7;
+-------------------+-------------+------------+
| customer_name     | customer_id | show_date  |
+-------------------+-------------+------------+
| aaryan sathasivam |        2018 | 2022-06-07 |
| owen murphy       |        2017 | 2022-06-09 |
| bastien meunier   |        2016 | 2022-06-10 |
| aniruddh kapur    |        2021 | 2022-06-11 |
| sam wilson        |        2022 | 2022-06-12 |
| thunder carlbach  |        2024 | 2022-06-12 |
| emre can          |        2023 | 2022-06-12 |
+-------------------+-------------+------------+
7 rows in set (0.001 sec)

22. Add a column named discount in the customer table, and update it according to the payment method:
a) If paid by cash, give no discount
b) If paid by card give 5% discount
c) If paid by upi give 10% discount
(DDL &DML)

MariaDB [project]> alter table customer add column discount decimal(10,2);
Query OK, 0 rows affected (0.014 sec)
Records: 0  Duplicates: 0  Warnings: 0

MariaDB [project]> update customer set discount = 0 where payment_method like "cash";
Query OK, 4 rows affected (0.006 sec)
Rows matched: 4  Changed: 4  Warnings: 0




MariaDB [project]> update customer set discount = 0.05 * amount where payment_method like "card";
Query OK, 8 rows affected, 1 warning (0.002 sec)
Rows matched: 8  Changed: 8  Warnings: 1

MariaDB [project]> update customer set discount = 0.1 * amount where payment_method like "upi";
Query OK, 12 rows affected, 1 warning (0.001 sec)
Rows matched: 12  Changed: 12  Warnings: 1

MariaDB [project]> select * from customer; 





23. Show the details of all theatres which have more than 1 screen.(joins, aggregate functions)

MariaDB [project]> create table screen_detailed as select * from screen natural join theatre natural join movie;
Query OK, 23 rows affected (0.064 sec)
Records: 23  Duplicates: 0  Warnings: 0

MariaDB [project]> select * from screen_detailed;


















MariaDB [project]> select count(screen_no) as no_of_screens, theatre_name, city from screen_detailed group by theatre_id;
+---------------+-----------------------+--------------------+
| no_of_screens | theatre_name          | city               |
+---------------+-----------------------+--------------------+
|             2 | pvr director's cut    | new delhi          |
|             2 | pvr select city walk  | new delhi          |
|             1 | prasad movies         | hyderabad          |
|             1 | pvr koramangala       | bengaluru          |
|             2 | urvashi theater       | bengaluru          |
|             2 | inox laserplex        | mumbai             |
|             2 | carnival cinemas      | mumbai             |
|             1 | regal cinema          | mumbai             |
|             2 | ariesplex sl cinemas  | thiruvananthapuram |
|             2 | raj mandir cinema     | jaipur             |
|             3 | mayajaal multiplex    | chennai            |
|             1 | rdb cinemas           | kolkata            |
|             1 | jeeva rukmani cinemas | puducherry         |
|             1 | cinepolis             | kolkata            |
+---------------+-----------------------+--------------------+
14 rows in set (0.001 sec)

MariaDB [project]> select count(screen_no) as no_of_screens, theatre_name, city from screen_detailed group by theatre_id having no_of_screens > 1;
+---------------+----------------------+--------------------+
| no_of_screens | theatre_name         | city               |
+---------------+----------------------+--------------------+
|             2 | pvr director's cut   | new delhi          |
|             2 | pvr select city walk | new delhi          |
|             2 | urvashi theater      | bengaluru          |
|             2 | inox laserplex       | mumbai             |
|             2 | carnival cinemas     | mumbai             |
|             2 | ariesplex sl cinemas | thiruvananthapuram |
|             2 | raj mandir cinema    | jaipur             |
|             3 | mayajaal multiplex   | chennai            |
+---------------+----------------------+--------------------+
8 rows in set (0.000 sec)

24. Implement left join on the customer and employee table, and find names of employees who have not been assigned to handle any customer. (joins)
MariaDB [project]> select e.*, c.* from employee e inner join customer c on c.employee_id = e.employee_id order by e.employee_id;


MariaDB [project]> select e.employee_id, e.employee_name from employee e left join customer c on c.employee_id = e.employee_id where c.customer_id is null;
+-------------+-----------------+
| employee_id | employee_name   |
+-------------+-----------------+
|        1001 | john doe        |
|        1010 | steve rogers    |
|        1013 | sergei dragunov |
+-------------+-----------------+
3 rows in set (0.000 sec) 
25. Write a query to display the count of various payment modes and the total money paid using that payment mode. (aggregate functions)

MariaDB [project]> update customer set payment_method = "upi" where amount between 180 and 250;
Query OK, 12 rows affected (0.001 sec)
Rows matched: 12  Changed: 12  Warnings: 0

MariaDB [project]> select * from customer;

MariaDB [project]> select payment_method, count(payment_method) as no_of_payments, sum(amount) as total_amount from customer group by payment_method;
+----------------+----------------+--------------+
| payment_method | no_of_payments | total_amount |
+----------------+----------------+--------------+
| card           |              8 |         2448 |
| cash           |              4 |         1420 |
| upi            |             12 |         2543 |
+----------------+----------------+--------------+
3 rows in set (0.000 sec) 
26. Write a query to display the names of customers which start with a vowel. (string functions)
MariaDB [project]> select customer_id, customer_name, amount from customer where left(customer_name,1) not in ('a','e','i','o','u');
+-------------+--------------------+--------+
| customer_id | customer_name      | amount |
+-------------+--------------------+--------+
|        2002 | priyanka chaudhry  |    300 |
|        2003 | somnath arya       |    190 |
|        2004 | clayton wilson     |    210 |
|        2005 | julia rollins      |    280 |
|        2006 | maaya ishida       |    220 |
|        2007 | cameron clark      |    310 |
|        2008 | novikova fedosya   |    240 |
|        2009 | zhu jingwen        |    187 |
|        2010 | breanne kuhic      |    200 |
|        2012 | christine harrison |    400 |
|        2014 | rajesh patel       |    254 |
|        2016 | bastien meunier    |    270 |
|        2019 | hamed al-mahmoudi  |    204 |
|        2020 | clint barton       |    213 |
|        2022 | sam wilson         |    376 |
|        2024 | thunder carlbach   |    188 |
+-------------+--------------------+--------+
16 rows in set (0.001 sec)

26. Write a query to add a prefix ‘+91’ to the phone numbers of customers and employees using CONCAT. (string functions)

MariaDB [project]> update customer set contact = concat("+91 ",contact);
Query OK, 24 rows affected (0.007 sec)
Rows matched: 24  Changed: 24  Warnings: 0

MariaDB [project]> select * from customer;
 

MariaDB [project]> update employee set contact = concat("+91 ",contact);
Query OK, 16 rows affected (0.001 sec)
Rows matched: 16  Changed: 16  Warnings: 0


















MariaDB [project]> select * from employee;
+-------------+-------------------+---------+---------------+
| employee_id | employee_name     | role    | contact       |
+-------------+-------------------+---------+---------------+
|        1001 | john doe          | manager | +91 713435178 |
|        1002 | bill chase        | worker  | +91 812958412 |
|        1003 | tony stark        | worker  | +91 955690216 |
|        1004 | wanda maximoff    | worker  | +91 741830460 |
|        1005 | walter heisenberg | manager | +91 773195118 |
|        1006 | clint barton      | worker  | +91 924196865 |
|        1007 | rajesh patel      | worker  | +91 669037198 |
|        1008 | nina williams     | worker  | +91 878244310 |
|        1009 | bucky barnes      | worker  | +91 951329304 |
|        1010 | steve rogers      | manager | +91 795853639 |
|        1011 | annie von holm    | worker  | +91 833471617 |
|        1012 | susan socks       | worker  | +91 897174317 |
|        1013 | sergei dragunov   | manager | +91 981129676 |
|        1014 | lei wulong        | worker  | +91 878829834 |
|        1015 | alisa matic       | worker  | +91 939119675 |
|        1016 | jack hummels      | worker  | +91 742003538 |
+-------------+-------------------+---------+---------------+
16 rows in set (0.000 sec)


27.Create a trigger that does not allow movie ticket to be less than 150? (trigger)

MariaDB [project]> delimiter //
MariaDB [project]> create trigger trig1 before insert on customer for each row
    -> begin
    -> if new.amount < 150 then
    -> signal sqlstate '20200' set message_text = 'movie ticket price is less than 150';
    -> end if;
    -> end;
    -> //
Query OK, 0 rows affected (0.008 sec)
MariaDB [project]> delimiter;
MariaDB [project]> insert into customer (customer_id, customer_name,amount) values (2025,"test guy",149);
ERROR 1644 (20200): movie ticket price is less than 150
28. Create a procedure that takes the movie name as an argument and prints in which theatres it is being screened. (procedure)

MariaDB [project]> create table screen_detailed as  select * from screen natural join theatre natural join movie;
Query OK, 22 rows affected (0.068 sec)
Records: 22  Duplicates: 0  Warnings: 0


MariaDB [project]> delimiter $$
MariaDB [project]> create procedure movie_details(movie varchar(30))
    -> begin
    -> select movie_name, language, theatre_name, city, run_time from screen_detailed where movie_name like movie;
    -> end;
    -> $$
Query OK, 0 rows affected (0.009 sec)

MariaDB [project]> delimiter ;


MariaDB [project]> select * from screen_detailed;





MariaDB [project]> call movie_details("kgf chapter 2");
+---------------+----------+-----------------------+------------+----------+
| movie_name    | language | theatre_name          | city       | run_time |
+---------------+----------+-----------------------+------------+----------+
| kgf chapter 2 | hindi    | pvr select city walk  | new delhi  |      168 |
| kgf chapter 2 | hindi    | prasad movies         | hyderabad  |      168 |
| kgf chapter 2 | hindi    | carnival cinemas      | mumbai     |      168 |
| kgf chapter 2 | tamil    | raj mandir cinema     | jaipur     |      168 |
| kgf chapter 2 | tamil    | mayajaal multiplex    | chennai    |      168 |
| kgf chapter 2 | telugu   | jeeva rukmani cinemas | puducherry |      168 |
| kgf chapter 2 | kannada  | cinepolis             | kolkata    |      168 |
+---------------+----------+-----------------------+------------+----------+
7 rows in set (0.027 sec)

Query OK, 0 rows affected (0.031 sec)

MariaDB [project]> call movie_details("rrr");
+------------+----------+--------------------+-----------+----------+
| movie_name | language | theatre_name       | city      | run_time |
+------------+----------+--------------------+-----------+----------+
| rrr        | tamil    | pvr director's cut | new delhi |      187 |
| rrr        | tamil    | urvashi theater    | bengaluru |      187 |
| rrr        | telugu   | inox laserplex     | mumbai    |      187 |
| rrr        | tamil    | regal cinema       | mumbai    |      187 |
| rrr        | hindi    | raj mandir cinema  | jaipur    |      187 |
+------------+----------+--------------------+-----------+----------+
5 rows in set (0.020 sec)

Query OK, 0 rows affected (0.026 sec)

29. Create view for finding all the movies that have movies playing  with movie_id,movie_title,theatre _id,show _date,show_time? (views)

MariaDB [project]> create view movie_ticket as
    -> select m.movie_id, m.movie_name, m.run_time, m.language,
    -> r.theatre_id, r.show_date, r.show_time
    -> from movie m inner join reservation r on m.movie_id = r.movie_id;
Query OK, 0 rows affected (0.006 sec)

MariaDB [project]> select * from movie_ticket;

30. Write a trigger to make sure you cannot insert an employee_id greater than the number 1030. (trigger, constraints)
MariaDB [project]> delimiter //
MariaDB [project]> create trigger trig before insert on employee for each row
    -> begin
    -> if new.employee_id > 1030 then
    -> signal sqlstate '20200' set message_text = 'employee_id is not allowed above 1030';
    -> end if;
    -> end;
    -> //
Query OK, 0 rows affected (0.010 sec)

MariaDB [project]> insert into employee values (1031,"test","worker",123456789);
ERROR 1644 (20200): employee_id is not allowed above 1030
31. Write a trigger to prevent a user for booking ticket at the same show time for two different movies, on the same date. (trigger)

MariaDB [project]> create table cust_res as select c.*, r.* from customer c inner join reservation r on c.customer_id = r.customer_id;
Query OK, 24 rows affected (0.066 sec)
Records: 24  Duplicates: 0  Warnings: 0

MariaDB [project]> select * from cust_res;

MariaDB [project]> delimiter $$
MariaDB [project]> create trigger user_trig before insert on reservation for each row
    -> begin
    -> declare is_true integer;
    -> set @is_true := 0;
    -> select count(customer_id) into @is_true from cust_res
    -> where show_time = new.show_time and show_date = new.show_date and customer_id = new.customer_id
    -> group by customer_id;
    -> if @is_true > 0 then
    -> signal sqlstate '20200' set message_text = 'cannot book for two movies at the same show date and time';
    -> end if;
    -> end
    -> $$
Query OK, 0 rows affected (0.010 sec)

MariaDB [project]> delimiter ;
MariaDB [project]> select * from reservation;
+--------+-----------+------------+----------+------------+-------------+
| res_id | show_time | show_date  | movie_id | theatre_id | customer_id |
+--------+-----------+------------+----------+------------+-------------+
|   3001 | 09:00:00  | 2022-05-18 |      218 |        514 |        2010 |
|   3002 | 14:00:00  | 2022-05-23 |      216 |        513 |        2009 |
|   3003 | 18:00:00  | 2022-05-18 |      214 |        512 |        2008 |
|   3004 | 09:00:00  | 2022-05-24 |      212 |        511 |        2007 |
|   3005 | 18:00:00  | 2022-05-31 |      210 |        510 |        2006 |
|   3006 | 14:00:00  | 2022-05-28 |      208 |        505 |        2005 |
|   3007 | 14:00:00  | 2022-05-30 |      206 |        506 |        2004 |
|   3008 | 18:00:00  | 2022-05-19 |      204 |        507 |        2003 |
|   3009 | 22:00:00  | 2022-05-21 |      213 |        508 |        2002 |
|   3010 | 09:00:00  | 2022-05-25 |      201 |        509 |        2001 |
|   3011 | 09:00:00  | 2022-05-26 |      203 |        504 |        2010 |
|   3012 | 18:00:00  | 2022-05-26 |      205 |        501 |        2012 |
|   3013 | 14:00:00  | 2022-05-26 |      209 |        503 |        2013 |
|   3014 | 22:00:00  | 2022-05-26 |      209 |        502 |        2014 |
|   3015 | 14:00:00  | 2022-06-03 |      211 |        502 |        2015 |
|   3016 | 22:00:00  | 2022-06-04 |      213 |        501 |        2020 |
|   3017 | 18:00:00  | 2022-06-06 |      215 |        506 |        2019 |
|   3018 | 09:00:00  | 2022-06-07 |      217 |        509 |        2018 |
|   3019 | 22:00:00  | 2022-06-09 |      204 |        511 |        2017 |
|   3020 | 22:00:00  | 2022-06-10 |      204 |        513 |        2016 |
|   3021 | 14:00:00  | 2022-06-11 |      209 |        507 |        2021 |
|   3022 | 09:00:00  | 2022-06-12 |      213 |        508 |        2022 |
|   3023 | 18:00:00  | 2022-06-12 |      212 |        510 |        2024 |
|   3024 | 22:00:00  | 2022-06-12 |      213 |        505 |        2023 |
+--------+-----------+------------+----------+------------+-------------+
24 rows in set (0.011 sec)
MariaDB [project]> insert into reservation values (3025, "09:00", "2022-06-12", 212, 510, 2022);
ERROR 1644 (20200): cannot book for two movies at the same show date and time



Conclusion:
Thus, we can say that using the online ticket booking system, we can provide the customers the benefit of booking tickets for movies.
