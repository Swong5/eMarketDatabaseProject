# eMarketDatabaseProject
#ER DIAGRAM for Mini World eMarket

![image](https://user-images.githubusercontent.com/83190617/116118402-439d9d80-a68b-11eb-971e-92c02d8ff50d.png)

CREATE DATABASE eMarket

#Table: User
CREATE table user (UID integer(30) not null, Type varchar(10) not null, Ufname varchar (30), Ulname varchar(30), Uemail varchar(30), UAddress varchar (30), PRIMARY KEY (UID));
#Data Values:
INSERT INTO user VALUES (001, 'Buyer', 'John', 'Smith', 'jsmith@email.org', '1001 23 St NY NY 11290');

INSERT INTO user VALUES (002, 'Seller', 'Zach', 'Porter', 'zporter', '200 Springfield Rd Elmhurst NY 11098');

INSERT INTO user VALUES (003, 'Buyer', 'Sydney', 'Quiseng', 'squiseng@email.org', '1721 Maine Rd Chicago IL 07290');

INSERT INTO user VALUES (004, 'Seller', 'Christina', 'Zinni', 'czinni@email.org', '72 Highland Way Tree Hill NC 21349');

INSERT INTO user VALUES (005, 'Buyer', 'James', 'Eubanks', 'jeubanks', '102 36 St Columbus OH 05670');

INSERT INTO user VALUES (006, 'Seller', 'David', 'Wright', 'dwright@email.org', '47 Seaver Way Flushing NY 11209');

![image](https://user-images.githubusercontent.com/83190617/116119357-595f9280-a68c-11eb-9761-f411f3a8ac86.png)


#Table: CreditCard

CREATE table creditcard (CID integer(30) not null, CUID integer(30) not null, CName varchar (30), CCompany varchar (30), Cexpdate varchar (30), PRIMARY KEY (CID, CUID), FOREIGN KEY (CUID) REFERENCES user (UID));

#Data Values:

INSERT INTO creditcard VALUES ('001', '001', 'John Smith', 'Visa', '01/2025');

INSERT INTO creditcard VALUES ('002', '002', 'Zach Porter', 'Mastercard', '02/2025');

INSERT INTO creditcard VALUES ('003', '003', 'Sydney Quiseng', 'Chase', '06/2025');

INSERT INTO creditcard VALUES ('004', '004', 'Christina Zinni', 'Visa', '01/2025');

INSERT INTO creditcard VALUES ('005', '005', 'James Eubanks', 'American Express', '05/2024');

INSERT INTO creditcard VALUES ('006', '006', 'David Wright', 'Visa', '09/2025');

![image](https://user-images.githubusercontent.com/83190617/116119378-5f557380-a68c-11eb-8da6-03e767f4a753.png)

#Table: Account

CREATE table account (ACID integer(30) not null, AUID integer(30), Acfname varchar(30), Aclname varchar(30), PRIMARY KEY (ACID, AUID), FOREIGN KEY (AUID) REFERENCES user (UID));

#Data Values:

INSERT INTO account VALUES ('001', '001', 'John', 'Smith');

INSERT INTO account VALUES ('002', '002', 'Zach', 'Porter');

INSERT INTO account VALUES ('003', '003', 'Syndey', 'Quiseng');

INSERT INTO account VALUES ('004', '004', 'Christina', 'Zinni');

INSERT INTO account VALUES ('005', '005', 'James', 'Eubanks');

INSERT INTO account VALUES ('006', '006', 'David', 'Wright');

![image](https://user-images.githubusercontent.com/83190617/116119405-68dedb80-a68c-11eb-9ddf-d730bec4a398.png)

#Table: Post

CREATE table post (PID integer(30) not null, ACID integer(30) not null, Pdate varchar(30), likesnum varchar(30), sharesnum varchar(30), PRIMARY KEY (PID, ACID), FOREIGN KEY (ACID) REFERENCES account (ACID));

#Data Values:

INSERT INTO post VALUES('001', '002', '05/23/2021', '17', '21');

INSERT INTO post VALUES('002', '004', '03/11/2021', '28', '36');

INSERT INTO post VALUES('003', '002', '05/32/2021', '42', '63');

INSERT INTO post VALUES('004', '006', '05/32/2021', '12', '19');

INSERT INTO post VALUES('005', '002', '05/32/2021', '43', '27');

INSERT INTO post VALUES('006', '006', '05/32/2021', '55', '77');

![image](https://user-images.githubusercontent.com/83190617/116119459-75fbca80-a68c-11eb-9e00-aaf93cb160e6.png)

#Table Advertisement

CREATE table advertisement (ADID integer(30) not null, PID integer(30) not null, ShareDate varchar(30), PRIMARY KEY (ADID, PID), FOREIGN KEY (PID) REFERENCES post (PID));

#Data Values:

INSERT INTO advertisement VALUES('001', '001', '05/23/2021');

INSERT INTO advertisement VALUES('002', '002', '03/11/2021');

INSERT INTO advertisement VALUES('003', '003', '04/07/2021');

INSERT INTO advertisement VALUES('004', '004', '03/22/2021');

INSERT INTO advertisement VALUES('005', '005', '01/14/2021');

INSERT INTO advertisement VALUES('006', '006', '02/11/2021');

![image](https://user-images.githubusercontent.com/83190617/116119500-80b65f80-a68c-11eb-8dd9-6a388f5ff7bb.png)

#Table: Product

CREATE table product (PDID integer(30) not null, Cost varchar(30), Available varchar(30), PDName varchar(50), PRIMARY KEY (PDID));
#Data Values:

INSERT INTO product VALUES ('101', '29.99', '4', 'Water Bottle');

INSERT INTO product VALUES ('102', '65.00', '2', 'Weighted Blanket');

INSERT INTO product VALUES ('103', '45.26', '1', 'Nike Sneakers(Pair)');

INSERT INTO product VALUES ('104', '10.50', '12', 'Ring');

INSERT INTO product VALUES ('105', '100.00', '10', 'Ostrich Pillow');

INSERT INTO product VALUES ('106', '75.00', '5', 'Picture Frame');

![image](https://user-images.githubusercontent.com/83190617/116119520-88760400-a68c-11eb-9fca-bfded2723723.png)

#Table: Sales

CREATE table sales (SID integer(30) not null, PDID integer(30) not null, SellerID integer(30) not null, BuyerID integer(30) not null, Revenue varchar(30), PRIMARY KEY (SID, PDID, SellerID, BuyerID), FOREIGN KEY (PDID) REFERENCES product (PDID), FOREIGN KEY (SellerID) REFERENCES user (UID), FOREIGN KEY (BuyerID) REFERENCES user (UID));

#Data Values:

INSERT INTO sales VALUES ('001', '101', '002', '001', '29.99');

INSERT INTO sales VALUES ('002', '102', '004', '003', '65.00');

INSERT INTO sales VALUES ('003', '101', '002', '001', '59.98');

INSERT INTO sales VALUES ('004', '104', '006', '001', '31.50');

INSERT INTO sales VALUES ('005', '105', '002', '005', '100.00');

INSERT INTO sales VALUES ('006', '105', '002', '005', '300.00');

![image](https://user-images.githubusercontent.com/83190617/116119564-92980280-a68c-11eb-9a2a-708186d31aae.png)

#QUESTION 3-INSERT/DELETE/UPDATE STATEMENTS

#Table: User

INSERT INTO user VALUES (007, 'Buyer', 'Sean', 'Wong', 'swong@email.org', '6522 83 Blvd Middle Village NY 11380');

UPDATE user SET UAddress = ’21 Main St Los Angeles CA 09210’ WHERE UID = 002

![image](https://user-images.githubusercontent.com/83190617/116119588-99bf1080-a68c-11eb-9568-2b0bb9e127eb.png)
 
#Table: CreditCard

INSERT INTO creditcard VALUES ('007', '007', 'Sean Wong', 'Chase', '11/2025');

UPDATE creditcard SET Cexpdate = '04/2023' WHERE CID = 002;

![image](https://user-images.githubusercontent.com/83190617/116119604-9fb4f180-a68c-11eb-915d-2b6f33fd2134.png)
 
#Table: Account

INSERT INTO account VALUES ('007', '007', 'Sean', 'Wong');

![image](https://user-images.githubusercontent.com/83190617/116119632-a5123c00-a68c-11eb-81db-34e33103d317.png)
 
#Table: Post

INSERT INTO post VALUES('007', '007', '3/21/2021', '13', '5');

![image](https://user-images.githubusercontent.com/83190617/116119656-ab081d00-a68c-11eb-8782-029fb7a261eb.png)
 
#Table: Advertisement

INSERT INTO advertisement VALUES('007', '007', '03/21/2021');

![image](https://user-images.githubusercontent.com/83190617/116119680-b0656780-a68c-11eb-82b6-d7fe9b3cd159.png)
 
#Table: Product

INSERT INTO product VALUES ('107', '154.00', '2', 'Autographed Baseball Card');

![image](https://user-images.githubusercontent.com/83190617/116119705-b6f3df00-a68c-11eb-9279-c8674f3b3e74.png)
 
#Table: Sales

INSERT INTO sales VALUES ('001', '107', '004', '007', '154'); (This was a mistake so I actually had to use a delete operation)

DELETE from sales where SID = 1 and PDID = 107;

INSERT INTO sales VALUES ('007', '107', '004', '007', '154');

![image](https://user-images.githubusercontent.com/83190617/116119787-cc690900-a68c-11eb-9729-88fd8d641c76.png)

 
#QUESTION 5-SQL QUERIES

#1. Find the name of the products that cost less than $100

SELECT PDNAME from eMarket.product as e where cost < 100;

![image](https://user-images.githubusercontent.com/83190617/116119804-d2f78080-a68c-11eb-9593-345c655b180e.png)
 

#2. Find the name of the person who sold an Autographed Baseball Card

SELECT ufname, ulname from eMarket.user as eu, eMarket.sales as es where es.SellerID = eu.UID and SellerID = 4 and PDID = 107;
 
![image](https://user-images.githubusercontent.com/83190617/116119901-ee628b80-a68c-11eb-8365-2577c4000efb.png)



